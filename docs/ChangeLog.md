# ChangeLog

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
