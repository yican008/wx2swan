# swan小程序搬家工具

## Introduction:
`这是个基于Abstract Syntax Tree微信小程序转换成swan的东东`
- 将微信小程序 搬家 到swan上；
- 工具只做了语法上的转换；
- swan框架、API和组件功能上的差异，框架层正在努力滴磨平~~；

## Quick Start

### 第一式


1. 	外网(稳定版)：
	```npm i -g wx2swan```

2. wx2swan 微信小程序的目录 (生成swan的目录)

	```javascript
		wx2swan ./test/demo ./test/swanDemo
	```

3. test目录下有个demo，这是微信小程序的目录，运行完上面命令后，会出现swanDemo目录，这个就是咱们swan小程序啦~
4.  **转换过程中的log都已经输出了，记得去看下转换log哟，会对你接下来的二次开发很有裨益的~~**
5. Enjoy IT ~~~


## Document

- [Tutorial FAQ](https://github.com/yican008/wx2swan/blob/master/docs/Tutorial.md)


## Feature
1. parse Abstract Syntax Tree;
2. traverse and repalce 、transform
3. generate code
4. cli console transform log
5. editor plugin

## Todo
- editor plugin

## ChangeLog
Please visit document [ChangeLog](https://github.com/yican008/wx2swan/blob/master/docs/ChangeLog.md)


