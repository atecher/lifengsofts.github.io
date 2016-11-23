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

# 常用API

## URL

### parse

将一个url解析为host等

```javascript
url.parse('http://i.woblog.cn:8080/post/list?a=b&c=d#abc')
```

输出：

```shell
Url {
  protocol: 'http:',
  slashes: true,
  auth: null,
  host: 'i.woblog.cn:8080',
  port: '8080',
  hostname: 'i.woblog.cn',
  hash: '#abc',
  search: '?a=b&c=d',
  query: 'a=b&c=d',
  pathname: '/post/list',
  path: '/post/list?a=b&c=d',
  href: 'http://i.woblog.cn:8080/post/list?a=b&c=d#abc' }
```

将query解析为对象，只需要传递第二个参数位true

```javascript
url.parse('http://i.woblog.cn:8080/post/list?a=b&c=d#abc',true)
```

```shell
Url {
  protocol: 'http:',
  slashes: true,
  auth: null,
  host: 'i.woblog.cn:8080',
  port: '8080',
  hostname: 'i.woblog.cn',
  hash: '#abc',
  search: '?a=b&c=d',
  query: { a: 'b', c: 'd' }, //这里已经是对象了
  pathname: '/post/list',
  path: '/post/list?a=b&c=d',
  href: 'http://i.woblog.cn:8080/post/list?a=b&c=d#abc' }
```

不知道url协议，也解析出host，不添加第三个参数，可以看到host为空

```javascript
url.parse('//i.woblog.cn:8080/post/list?a=b&c=d#abc',true)
```

```shell
Url {
  protocol: null,
  slashes: null,
  auth: null,
  host: null,
  port: null,
  hostname: null,
  hash: '#abc',
  search: '?a=b&c=d',
  query: { a: 'b', c: 'd' },
  pathname: '//i.woblog.cn:8080/post/list',
  path: '//i.woblog.cn:8080/post/list?a=b&c=d',
  href: '//i.woblog.cn:8080/post/list?a=b&c=d#abc' }
```

第三个参数为true

```javascript
url.parse('//i.woblog.cn:8080/post/list?a=b&c=d#abc',true,true)
```

```shell
Url {
  protocol: null,
  slashes: true,
  auth: null,
  host: 'i.woblog.cn:8080', //有值了
  port: '8080',
  hostname: 'i.woblog.cn',
  hash: '#abc',
  search: '?a=b&c=d',
  query: { a: 'b', c: 'd' },
  pathname: '/post/list',
  path: '/post/list?a=b&c=d',
  href: '//i.woblog.cn:8080/post/list?a=b&c=d#abc' }
```

## format

将一个对象转为一个url,可以是上面的parse对象

```javascript
url.format({
...   protocol: 'http:',
...   slashes: true,
...   auth: null,
...   host: 'i.woblog.cn:8080',
...   port: '8080',
...   hostname: 'i.woblog.cn',
...   hash: '#abc',
...   search: '?a=b&c=d',
...   query: 'a=b&c=d',
...   pathname: '/post/list',
...   path: '/post/list?a=b&c=d',
...   href: 'http://i.woblog.cn:8080/post/list?a=b&c=d#abc' })
```

```shell
http://i.woblog.cn:8080/post/list?a=b&c=d#abc
```

## resolve

```javascript
url.resolve('/one/two/three', 'four')         // '/one/two/four'
url.resolve('http://example.com/', '/one')    // 'http://example.com/one'
url.resolve('http://example.com/one', '/two') // 'http://example.com/two'
```

## queryString

### 将对象转为参数字符串

```javascript
querystring.stringify({name:'li',age:10,course:['b',1],other:''})
```

```shell
'name=li&age=10&course=b&course=1&other='
```

第二个参数表示多个参数间的连接符号，默认&

```javascript
querystring.stringify({name:'li',age:10,course:['b',1],other:''},',')
```

```shell
'name=li,age=10,course=b,course=1,other='
```

第三个参数表示key和value之间的分隔符，默认=

```javascript
querystring.stringify({name:'li',age:10,course:['b',1],other:''},',',':')
```

```shell
'name:li,age:10,course:b,course:1,other:'
```

### 将字符串解析为对象

```javascript
querystring.parse('name=li&age=10&course=b&course=1&other=')
```

```shell
{ name: 'li', age: '10', course: [ 'b', '1' ], other: '' }
```

通用也可以指定多个参数间的连接符号

```javascript
querystring.parse('name=li,age=10,course=b,course=1,other=',',')
```

```shell
{ name: 'li', age: '10', course: [ 'b', '1' ], other: '' }
```

指定key和value间的分隔符

```javascript
querystring.parse('name:li,age:10,course:b,course:1,other:',',',':')
```

```shell
{ name: 'li', age: '10', course: [ 'b', '1' ], other: '' }
```

### 字符转义

```javascript
querystring.escape('<呵 护>')
```

```shell
'%3C%E5%91%B5%20%E6%8A%A4%3E'
```

反转义

```javascript
querystring.unescape('%3C%E5%91%B5%20%E6%8A%A4%3E')
```









