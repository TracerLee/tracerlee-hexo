---
title: 《七天学会NodeJS》笔记
date: 2016-05-07 23:35:26
tags: 笔记
---

Node.js是一个运行javascript的环境，NodeJS的作者创造NodeJS的目的是为了实现高性能Web服务器。

> Node.js® is a JavaScript runtime built on [Chrome's V8 JavaScript engine](https://developers.google.com/v8/). Node.js uses an event-driven, non-blocking I/O model that makes it lightweight and efficient. Node.js' package ecosystem, [npm](https://www.npmjs.com/), is the largest ecosystem of open source libraries in the world.
>
> —— [Node.js官网](https://nodejs.org/en/)



这篇文章主要摘录一些个人认为的重点，希望加深对Node.js的熟悉。



## Node.js基础

#### exports

`exports`对象是当前模块的导出对象，用于导出模块公有方法和属性。别的模块通过`require`函数使用当前模块时得到的就是当前模块的`exports`对象。以下例子中导出了一个公有方法。

<!-- more -->

```javascript
exports.hello = function () {
	console.log('Hello World!');
};
```
> `exports`默认是`{}`，是`module.exports`的一个引用。
>

#### 模块初始化

一个模块中的JS代码仅在模块<u>**第一次被使用时执行一次**</u>，并在执行过程中初始化模块的导出对象。之后，<u>**缓存起来**</u>的导出对象被重复利用。

#### 主模块

通过命令行参数传递给NodeJS以启动程序的模块被称为主模块。主模块负责调度组成整个程序的其它模块完成工作。例如通过以下命令启动程序时，`main.js`就是主模块。

```bash
$ node main.js
```
> 说明多次`require`不会导致执行多次模块内的程序内容。
>



- NodeJS是一个JS脚本解析器，任何操作系统下安装NodeJS本质上做的事情都是把NodeJS执行程序复制到一个目录，然后保证这个目录在系统PATH环境变量下，以便终端下可以使用`node`命令。
- 终端下直接输入`node`命令可进入命令交互模式，很适合用来测试一些JS代码片段，比如正则表达式。
- NodeJS使用[CMD](http://wiki.commonjs.org/)模块系统，主模块作为程序入口点，所有模块在执行过程中只初始化一次。
- 除非JS模块不能满足需求，否则不要轻易使用二进制模块，否则你的用户会叫苦连天。

> Node.js使用CMD规范，Sea.js也是遵循CMD规范。
>



## 代码的组织和部署

### 模块路径解析规则

1. 内置模块
2. node_modules目录
3. NODE_PATH环境变量



### 包（package）

当模块的文件名是`index.js`，加载模块时可以使用模块所在目录的路径代替模块文件路径，因此接着上例，以下两条语句等价。

```javascript
var cat = require('/home/user/lib/cat');
var cat = require('/home/user/lib/cat/index');
```

这样处理后，就只需要把包目录路径传递给`require`函数，感觉上整个目录被当作单个模块使用，更有整体感。

> 所以就是`require`一个文件夹就等同于`require`里面的`index.js`模块，这个很方便。
>



#### package.json

```json
{
"name": "node-echo",
"main": "./lib/echo.js",
"dependencies": {
"argv": "0.0.2"
}
}
```
> `name`是包名称，`main`是入口模块（主模块），`dependencies`是依赖模块。
>



#### 版本号

语义版本号分为`X.Y.Z`三位，分别代表主版本号、次版本号和补丁版本号。当代码变更时，版本号按以下原则更新。

```
如果只是修复bug，需要更新Z位。
如果是新增了功能，但是向下兼容，需要更新Y位。
如果有大变动，向下不兼容，需要更新X位。
```


#### NPM

- 使用`npm help `可查看某条命令的详细帮助，例如`npm help install`。
- 在`package.json`所在目录下使用`npm install . -g`可先在本地安装当前命令行程序，可用于发布前的本地测试。
- 使用`npm update `可以把当前目录下`node_modules`子目录里边的对应模块更新至最新版本。
- 使用`npm update -g`可以把全局安装的对应命令行程序更新至最新版。
- 使用`npm cache clear`可以清空NPM本地缓存，用于对付使用相同版本号发布新版本代码的人。



#### 使用NodeJS编写代码前需要做的准备工作

- 编写代码前先规划好目录结构，才能做到有条不紊。
- 稍大些的程序可以将代码拆分为多个模块管理，更大些的程序可以使用包来组织模块。
- 合理使用`node_modules`和`NODE_PATH`来解耦包的使用方式和物理路径。



## 文件操作

#### 小文件拷贝

*代码片段*

```javascript
fs.writeFileSync(dst, fs.readFileSync(src)); // dst:目标路径,src:源路径
```

#### 大文件拷贝

*代码片段*

```javascript
fs.createReadStream(src).pipe(fs.createWriteStream(dst));
```

以上程序使用`fs.createReadStream`创建了一个源文件的只读数据流，并使用`fs.createWriteStream`创建了一个目标文件的只写数据流，并且用`pipe`方法把两个数据流连接了起来。连接起来后发生的事情，说得抽象点的话，水顺着水管从一个桶流到了另一个桶。



`process`是一个全局变量，可通过`process.argv`获得命令行参数。

Node.js提供了基本的文件操作API，`require('fs')`即可使用。



#### Buffer（数据块）

*官方文档：*[http://nodejs.org/api/buffer.html](http://nodejs.org/api/buffer.html)

#### Stream（数据流）

*官方文档：*[http://nodejs.org/api/stream.html](http://nodejs.org/api/stream.html)



## 参考资料

* [七天学会NodeJS](http://nqdeng.github.io/7-days-nodejs/)
* [Node.js官网](https://nodejs.org/en/)
* [7-days-nodejs](https://papahot.gitbooks.io/7-days-nodejs/content/)