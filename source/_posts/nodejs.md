---
title: NodeJs
date: 2016-11-23 00:46:11
categories: NodeJs
tags: 
    - NodeJs
---

# 学习网站

官网：https://nodejs.org

npm:https://www.npmjs.com

github

stack overflow

# 安装nodeJS

## 版本

偶数为稳定版本:0.6.x,0.8.x,0.10.x

基数非稳定版本:0.7.x,0.9.x,0.11.x

## mac安装

升级mac系统到最新，安装最新的xcode

```javascript
xcode-select --install
```

## homebrew

安装方式可以去官网，用ruby命令安装。然后可以安装node js

```javascript
brew install nodejs
```

## 多版本安装

使用n模块来管理，先安装

```javascript
npm install -g n
```

然后就可以通过n来安装相应的版本

```javascript
n 0.10.2
```

安装完了以后，可以通过输入n来切换默认版本：

我们这里是v4.2.3

# 最简单的服务器

```javascript
var http = require('http');

var server = http.createServer(function(request, response) {
	// magic happens here!
	response.writeHead(200, {
		'Content-Type': 'text/html',
		'X-Powered-By': 'bacon'
	});

	response.write('<html>');
	response.write('<body>');
	response.write('<h1>Hello, World!</h1>');
	response.write('</body>');
	response.write('</html>');
	response.end();
});

server.listen(1337, '127.0.0.1')
```

打开浏览器访问http://127.0.0.1:1337,就能看到hello world

# 在命令行执行

我们可以将这段输入到chrome的console中

```javascript
var a=1;var b=2;var add=function(a,b){return a+b};console.log(add(a,b));
```

就可以看到结果为3

同样可以将上面的代码复制到nodejs的命令行，发现结果也是一样。但是他们的全局变量是不一样的，比如我们可以在chrome中输入window,document但是，node里面就不行。但是他有自己的全局变量，比如process,通用浏览器中也是拿不到了。

# 模块

## 模块的使用流程

创建模块：teacher.js

导出模块：exports.add=function(){}

加载模块：var teacher=require('./teacher.js')

使用模块：teacher.add('Li')







