# ChangeLog

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