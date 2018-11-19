# swan小程序搬家工具

## Introduction:
> **工具帮你迁移80%的代码，可能只节省你50%的工作量。**
> 这是个基于`Abstract Syntax Tree`微信小程序转换成百度小程序的工具。

- 工具只做了静态语法上的转换，根据一些规则去转换代码，抹平微信小程序语法和百度小程序语法上的差异，避免大家踩坑；
- 搬家工具是离线的，没有运行时框架，所以有些没法抹平的`运行时diff`，需要二次开发调整。
- 使用中的任何问题，都可以提[Issues](https://github.com/yican008/wx2swan/issues)或者加微信小助手：`wx2swan-helper`;
![wx2swan-helper](./img/wx.jpg)

## Quick Start
1. 	外网(稳定版)：
	```npm i -g wx2swan```
	
2. wx2swan   微信小程序的目录   (可选: 生成swan的目录，默认为entryDir_swan)   (可选: 生成日志的目录, 默认为outputDir)

	```javascript
		wx2swan ./test/entryDir
	```

	```javascript
		wx2swan ./test/entryDir ./test/outputDir
	```
	
3. 新增支持单文件入口转换：

	wx2swan   微信小程序的文件  (可选: 生成swan的目录或文件路径，默认为entryDir_swan/entryFile)   (可选: 生成日志的目录, 默认为outputDir)
	
	**注意：如果指定生成swan的文件路径，需要指定正确的文件扩展名，否则将只复制文件不进行处理**
	
	
	```javascript
		wx2swan ./test/entryFile
	```
	
	```javascript
		wx2swan ./test/entryFile ./test/outputDir
	```
	
	```javascript
		wx2swan ./test/entryFile ./test/outputFile
	```
3.  **转换过程中的log都已经输出了，记得去看下转换log哟，会对你接下来的二次开发很有裨益的~~**


4. Enjoy IT ~~~

## Document

- [Tutorial FAQ](https://github.com/yican008/wx2swan/blob/master/docs/Tutorial.md)
- [做了哪些事儿](https://github.com/yican008/wx2swan/blob/master/docs/FeatureList.md)
- [ChangeLog](https://github.com/yican008/wx2swan/blob/master/docs/ChangeLog.md)

## Feature
1. parse Abstract Syntax Tree;
2. traverse and repalce 、transform
3. generate code
4. cli console transform log
5. editor plugin


## ChangeLog
Please visit document [ChangeLog](https://github.com/yican008/wx2swan/blob/master/docs/ChangeLog.md)

[更多项目征集](https://github.com/yican008/wx2swan/issues/19)
