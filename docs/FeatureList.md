## 搬家工具转换支持的Feature List
### 样式转换
1. `wxml`转换为`css`
2. 无请求协议的css静态资源转码优化(默认添加https协议头)
    - `.backgroundImage1{background-image: url(//www.test.com/test.jpg);}`
        - 输出：`.backgroundImage1{background-image: url(https://www.test.com/test.jpg);}` 

### 视图转换
支持微信视图绝大部分语法的转换，具体如下：

#### 完美转换的功能
1. 插值语法: `{{variable}}`
2. `wx:if、wx:elif、wx:else`指令: 语法的规则不一致，进行了转换(去掉了双大括号)
3. `wx:for、wx:for-item、wx:for-index`指令
4. `wx:for-items`指令
5. `import、include`
6. `template`
7. `wx:if`和`wx:for`同级：
  微信支持if和for同级，SWAN不支持，这里用空节点block进行拆分；
8. 空wx:前缀转码优化
    - `	<view wx:></view>`
        - 输出：`<view>test</view>` 
9. 无请求协议的css静态资源转码优化(默认添加https协议头)
    - `	<view class="test" style="background: url(//www.test.com/test.jpg)"></view>`
        - 输出：`<view class="test" style="background: url(https://www.test.com/test.jpg)"></view>` 
10. 部分组件数据绑定转换为双向绑定语法
    - `	<input value="{{1}}"></input>`
        - 输出：`<input value="{=1=}" />` 
    - `	<textarea value="{{1}}"></textarea>`
        - 输出：`<textarea value="{=1=}"></textarea>` 
11. template组件data属性转换: {{item}} => {{{item}}}
12. 使用on进行的数据绑定转换为bind绑定
	- `<button ontap="ontap">点击</button>`
		- 输出:  `<button bindtap="ontap">点击</button>`
13. include、import添加.swan默认扩展名
	- `<include src="./test"/>
<import src="./test"/>`
		- 输出:  `<include src="./test.swan" />
<import src="./test.swan" />`

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
2. 自定义组件的实现机制问题，`SWAN`自定义组件是微信的子集，需要二次开发；
3. 登录流程需要授权和server换code等等操作，和微信流程上存在diff，可能需要二次开发；
4. 支付流程，`SWAN`支付是用的聚合收银台的机制，和微信小程序存在整体的diff，需要二次开发；

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
3. 获取页面路径的属性`__route__`转换为route
	- `currentPage.__route__`
		- 输出:  `currentPage.route`
4. getExtConfigSync函数转换
    - `data = wx.getExtConfigSync().ext;`
        - 输出：`data = swan.getExtConfigSync().extConfig.ext;` 
5. 自定义组件内置behaviors映射关系。

        Component({
            behaviors: ['wx://form-field', 'wx://component-export']
        });
        
        // 输出: 
        Component({
            behaviors: ["swan://form-field", "swan://component-export"]
        });