---
title: JavaScript语法总结
date: 2016-11-17 11:58:02
categories: JavaScript
tags: 
    - JavaScript
---

# 概述

## 有什么优势

1. 他可以制作交互性极强的网页效果
2. 全世界大部分网页基本上都是用它
3. 所有的主流浏览器基本都支持

# Hello JS

js有很强的易学性，只需要一个文本编辑器就可以编写了，并且js是是解释性的，不需要想c++，java语言需要编译。我们演示一个最简单的例子，就是动态向文档里输出一句话并且动态改变一个标签的字体演示。

```javascript
<!DOCTYPE html>
<html>

	<head>
		<meta charset="utf-8" />
		<title></title>
	</head>

	<body>
		<div id="d1">第一段文字</div>
		<div id="d2">第二段文字</div>

		<script>
			document.write('hello js');
			document.getElementById('d1').style.color = 'red';
		</script>
	</body>

</html>
```

可以看到我们通过document.write方法可以向body标签中添加内容，还可以通过document.getElementById方法通过id选择器找到一个标签动态的将字体的颜色改为了红色。

# 如何在网页里引入js

## head标签

如果将js插入到head标签中，需要用script标签包裹住js代码：

```java
<head>
	<meta charset="utf-8" />
	<title></title>
	
	<script>
		alert('hi')
	</script>
</head>
```

## 引入js文件

js代码不一定非要嵌入到网页里，可以单独写到一个文件，然后引入这文件就好了

common.js

```javascript
alert('我来自一个外部文件')
```

然后在index.html中引入

```html
<script src="js/common.js">

</script>
```

当然也可以在body标签中引入

```javascript
<body>
	<script src="js/common.js">
	</script>

</body>
```

注意：js是一本脚本语言并且可以放到页面的任何位置，但是html是按照从前到后先后顺序执行的，一般放到body的最后面。

# 语句

js语句用分好或换行符隔开。

```javascript
document.write('我是一行语句')
document.write('我是也是一行语句');document.write('我是也是一行语句')
```

其实这是三行语句。

# 注释

注释是写给程序员开的，用以提高代码可读性的。

## 单行注释

用//表示

```javascript
//我是一个单行注释
```

## 多行注释

用`/*开始到*/`结束中间的内容都是注释。

```javascript
/*我是一个多行注释
我可以写多行*/
```

# 变量

简单来讲就是存储可变的量，比如我们我们的天气，每天都不一样。js中变量可以不声明直接使用，但这不符合规范，所有还是先声明，然后在使用，声明变量的语法是：

```javascript
//变量
var weather;
weather='晴天';
alert(weather)

weather='雷阵雨'
alert(weather)

weather=10;
alert(weather)
```

变量可以赋值为不同的类型。

注意：变量名区分大小写。

## 变量名命名规则

1. 字母，下划线，美元符开始
2. 后面接任意多个字母，数字，下划线，美元符
3. 不能使用js的保留关键字

# 流程控制

## if

if else语句可以判断条件是否成立，然后分别执行对应的代码。

```javascript
var age=17;
if (age>=18) {
	alert("你成年了")
} else{
	alert("你还没用成年")
}
```

# 函数

函数式用来完成某个特定功能的一组语句，用来提高代码的复用性。定义函数的语法是：

```javascript
function 函数名称 () {
	函数代码
}
```

1. 其中function是定义函数的关键字
2. 函数名就是为函数去一个名字，下次用只需要知道函数名称就行了，不需要知道这个函数具体怎么实现额。

例如我们可以编写一个计算两数之和的方法:

```javascript
//定义函数
function add (a,b) {
	return a+b;
}

alert(add(10,20)) //调用函数
```

函数是不能自动执行的，需要我们手动调用。当然我们也可以定义一个button，点击后才执行一个函数。

```javascript
<!DOCTYPE html>
<html>

	<head>
		<meta charset="utf-8" />
		<title></title>
		<script type="text/javascript">

			function clickMe() {
				alert('你再点一下试试！')
			}
		</script>
	</head>

	<body>
		<input type="button" onclick="clickMe()" value="你敢点击吗"></input>
	</body>

</html>
```

# 互动操作

这部分我们将讲解如何输出内容，警告，确认，提问对户口，以及打开新窗口，关闭窗口等操作。

## 输出内容

可以直接用document.write方法。

```javascript
//输出内容
document.write('输出内容')

//可以使用+号连接字符串
document.write('拼接字符串'+"<br/>")
```

## 警告信息

有时候在网页想给用户一个提示框，则可以使用alert对话框。

```javascript
alert('打印一个变量')
var name = '名字'
alert(name)
```

## 确认对话框

该对话框显示一个确定取消对话框，可以和用户交互。

```javascript
function showLoveJS () {
	var loveJS=confirm('你喜欢JS吗？')
	if (loveJS==true) {
		alert('好的，继续加油')
	} else{
		alert('不喜欢也得学呀')
	}
}
```

```html
<input type="button" onclick="showLoveJS()" value="你喜欢js吗">
```







































