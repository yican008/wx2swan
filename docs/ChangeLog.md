# ChangeLog

## 1.2.0 2018-11-07
- 【Feature】新增支持单一文件入口转换

	支持：

	`wx2swan entryFilePath outputFilePath`
    
	`wx2swan entryFilePath outputDirPath`
	
	注意: 指定outputFilePath时文件扩展名需为正确的文件类型，否则不会进行转换。

## 1.1.18 2018-11-06
- 【BugFix】修复`__route__` --> route转换的问题。
	- `arr[arr.length - 1].__route__`
		- 输出:  `arr[arr.length - 1].route`

## 1.1.17 2018-10-23
- 【Feature】获取页面路径的属性`__route__`转换为route
	- `currentPage.__route__`
		- 输出:  `currentPage.route`
- 【Feature】include、import添加.swan默认扩展名
	- `<include src="./test"/>
<import src="./test"/>`
		- 输出:  `<include src="./test.swan" />
<import src="./test.swan" />`

## 1.1.16 2018-10-22
- 【BugFix】修复on --> bind转换的问题。

## 1.1.15 2018-10-19
- 【Feature】使用on进行的数据绑定转换为bind绑定
	- `<button ontap="ontap">点击</button>`
		- 输出:  `<button bindtap="ontap">点击</button>`
- 【Feature】wx标识符全部转换为swan
	- `const wx = {};
for (const key in wx) {
    console.log(`wx${key}:`, wx[key]);
}`
		- 输出:  `const swan = {};
for (const key in swan) {
    console.log(`wx${key}:`, swan[key]);
}`

## 1.1.14 2018-10-15
- 【Feature】转换工具源码加入es6转码，解决在低版本node环境中报错的问题。

## 1.1.9 2018-10-10
- 【Feature】转换日志被分为三级 info、warning、error，保存在`/log`目录下。
	
	waring和error日志会被打印到控制台，开发者需要根据日志信息解决转换工具无法解决的问题。
	![图片](https://i.loli.net/2018/10/10/5bbde80e8dee6.png) 
    

## 1.1.8 2018-09-29
- 【Feature】部分组件数据绑定转换为双向绑定语法
    - `	<input value="{{1}}"></input>`
        - 输出：`<input value="{=1=}" />` 
    - `	<textarea value="{{1}}"></textarea>`
        - 输出：`<textarea value="{=1=}"></textarea>` 
    - `<scroll-view scroll-top="{{0}}" scroll-left="{{0}}" scroll-into-view="{{test}}"></scroll-view>`
        - 输出：`<scroll-view scroll-top="{=0=}" scroll-left="{=0=}" scroll-into-view="{=test=}"></scroll-view>`
    - `	<movable-view x="{{1}}" y="{{1}}"></movable-view>`
        - 输出：`<movable-view x="{=1=}" y="{=1=}"></movable-view>` 

## 1.1.7 2018-09-25
- 【Feature】空wx:前缀转码优化
    - `	<view wx:></view>`
        - 输出：`<view>test</view>` 
    - `<view wx:='test'>test</view>`
        - 输出：`<view>test</view>`
    - `<view wx:="test">test</view>`
        - 输出：`<view>test</view>`
- 【Feature】无请求协议的css静态资源转码优化(默认添加https协议头)
    - `	<view class="test" style="background: url(//www.test.com/test.jpg)"></view>`
        - 输出：`<view class="test" style="background: url(https://www.test.com/test.jpg)"></view>` 
    - `.backgroundImage1{background-image: url(//www.test.com/test.jpg);}`
        - 输出：`.backgroundImage1{background-image: url(https://www.test.com/test.jpg);}`       

## 1.1.5 2018-08-29
- 【Fix】增加`input`标签强制自闭合
- 【Fix】增加不规范的**自定义组件名**修正功能
- 【Refact】重构视图转换逻辑

## 1.1.4 2018-08-20
### 功能点
#### wxml to swan
- 【Feature】wx-for标签转码优化
    - `<view wx:for="{{list}}" wx:for-item="namedItem" wx:for-index="idx"></view>`
        - 输出：`<view s-for="namedItem, idx in list"></view>`
- 【Feature】保留包裹属性值的原始的引号
    - `<view class='title {{'first'}}'></view>`
        - 输出：`<view class='title {{'first'}}'></view>`
- 【Feature】支持wxml中奇怪的写法
    - `<view wx:if= class="time" />`转换为`<view s-if="" class="time" />`
    - `<view style="{{\"top: 0\"}}" />`转换为`<view style="{{'top: 0'}}" />`

#### js转码
- 【FIX】新增两个百度智能小程序不支持的api转码规则
    - `typeof`表达式
        - 输入：`if (typeof wx.unSupportedAPI === 'function') {}`
        - 输出：`if (typeof swan.unSupportedAPI === 'function') {}`
    - `!`表达式
        - 输入：`if (!wx.unSupportedAPI) {}`
        - 输出：`if (!swan.unSupportedAPI) {}`

### 其他
1. 将定制的htmlparser2和domhandler抽出独立的模块
    - [stricter-htmlparser2](https://www.npmjs.com/package/stricter-htmlparser2)
    - [x-domhandler](https://www.npmjs.com/package/x-domhandler)

## 1.1.3
- 【Fix】修复template组件data属性转换问题: {{item}} => {{{item}}}
- 【Fix】修复wx:if wx:for同时出现在一个标签时的转换问题
- 【Fix】修复js中逻辑表达式有api是否存在判断时，迁移工具意外退出问题
- 【Fix】`wx.navigateToMiniProgram`转为`swan.navigateToSmartProgram`
- 【Fix】`wx.chooseInvoiceTitle`转为`swan.chooseInvoiceTitle`
- 【Fix】修复function call传参中出现`wx`未被转换问题
- 【Fix】log.js更名为log.json

## 1.1.2
- 【Feature】增加对象字面量的转换，微信和swan标签语法的差异，{{}} ===> {{{}}}

## 1.1.1
- 【Feature】增加对swan小程序不支持if和for同级的处理，根据上下文将其重建标签错开

## 1.1.0
- 【Feature】重构了标签的AST处理逻辑，支持标志self-closing Tag;

## 1.0.10
- 【Feature】增加cli命令行的help和version操作;

## 1.0.8
- 【Fix bug】修复wx[key]转义成swan.key，expected：swan[key];

## 1.0.5
- 【Fix bug】增加self-closing标签转成带有endTag的，如微信支持`<navigator />和<navigator></navigator>`，而swan只支持`<navigator></navigator>`

## 1.0.4
- 【Fix bug】增加self-closing标签转成带有endTag的，如微信支持`<image />和<image></image>`，而swan只支持`<image></image>`

## 1.0.3
- 【Fix bug】include标签自闭合处理;

## 1.0.2
- 【Feature】增加cli命令行进度的支持；
- 【Fix bug】修复标签嵌套错乱的问题；
- 【Fix bug】修复self-closing标签的问题；
- 【Fix bug】修复模板语法，条件语句差异的diff，MustCache语法；
- 【Fix bug】修复s-else默认会加上空值的问题；
- 【Fix bug】修复Boolean Attributes的问题;

## 1.0.1
- 【Feature】增加输出log，给开发者二次开发提供辅助；
- 【Fix bug】js二级API，通过log给出tips提示;
