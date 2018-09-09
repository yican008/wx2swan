## 搬家工具转换支持的Feature List
### 样式转换
1. `wxml`转换为`css`

### 视图转换
支持微信视图绝大部分语法的转换，具体如下：

#### 完美转换的功能
1. 插值语法: `{{variable}}`
2. `wx:if、wx:elif、wx:else`指令
3. `wx:for、wx:for-item、wx:for-index`指令
4. `wx:for-items`指令
5. `import、include`
6. `template`

#### 可能影响视图展现的转换（极少见）
1. 强制去除`input`标签的闭合标签
   - From： `<input>hello</input>`
   - To：`<input />hello`
2. 自定义组件名称强制修改为`dasherize`风格，搬家工具会自动修改json配置和视图代码中的自定义组件名称；名称转换通过[lodash.kebabCase](https://lodash.com/docs/4.17.10#kebabCase)实现。
3. 双引号包裹的标签属性值中出现转义的双引号时，强制转换为单引号:
   - From：`<view value="{{\"hello\"}}"></view>`
   - To：`<view value="{{'hello'}}"></view>`

#### 暂不支持的功能点
1. 暂不支持`<wxs></wxs>`的转换；

### API转换
由于百度智能小程序API与微信的API存在diff，针对不同的API及开发者的使用方法，有不同的转换逻辑，具体如下：

1. 百度小程序已支持的API：替换全局变量`wx`为`swan`;
2. 百度小程序不支持的API：
   - 逻辑表达式中使用API，转换规则如下：
     - From: `if (wx.unSupportedAPI && expression)`
     - To: `if (swan.unSupportedAPI != null && expression)`
   - 一元运算符中使用API，转换规则如下:
     - From: `!wx.unSupportedAPI` 或者`typeof wx.unSupportedAPI`
     - To: `!swan.unSupportedAPI` `typeof swan.unSupportedAPI`
   - 其他使用场景：尝试删除调用api的父级语句或表达式的代码，删除失败的话则保留原始代码。