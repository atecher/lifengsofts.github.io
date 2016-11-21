## Navigator

包含浏览器的信息，通常用于检测浏览器与操作系统的版本。

### 属性

| 属性名         | 解释                      |
| ----------- | ----------------------- |
| appCodeName | 浏览器代码名字符串表示             |
| appName     | 返回浏览器名字                 |
| appVersion  | 浏览器平台和版本信息              |
| platform    | 运行浏览器的操作系统平台            |
| userAgent   | 返回客户机发给服务器user-agent头的值 |

```javascript
document.write(navigator.appCodeName+'<br />');
document.write(navigator.appName+'<br />');
document.write(navigator.appVersion+'<br />');
document.write(navigator.platform+'<br />');
document.write(navigator.userAgent+'<br />');
```

输出：

```shell
Mozilla
Netscape
5.0 (Macintosh; Intel Mac OS X 10_11_0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/54.0.2840.98 Safari/537.36
MacIntel
Mozilla/5.0 (Macintosh; Intel Mac OS X 10_11_0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/54.0.2840.98 Safari/537.36
```

通过userAgent判断是什么浏览器：

```javascript
var u_agent = navigator.userAgent;
var B_name = "不是想用的主流浏览器!";
if(u_agent.indexOf("Firefox") > -1) {
	B_name = "Firefox";
} else if(u_agent.indexOf("Chrome") > -1) {
	B_name = "Chrome";
} else if(u_agent.indexOf("MSIE") > -1 && u_agent.indexOf("Trident") > -1) {
	B_name = "IE(8-10)";
} else if(u_agent.indexOf("Safari") > -1) {
	B_name = "Safari";
}
document.write("浏览器:" + B_name + "<br>");
document.write("u_agent:" + u_agent + "<br>");
```

输出：

```shell
浏览器:Chrome
u_agent:Mozilla/5.0 (Macintosh; Intel Mac OS X 10_11_0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/54.0.2840.98 Safari/537.36
```

## Screen

用于获取用户的屏幕信息。

### 属性

| 属性名         | 解释                        |
| ----------- | ------------------------- |
| availHeight | 窗口可用的屏幕高度,px, 减去界面特性,如任务栏 |
| availWidth  | 可用的屏幕宽度，px                |
| colorDepth  | 用户浏览器表示的颜色位数，通常为32位       |
| pixeDepth   | 同上，ie不支持                  |
| height      | 屏幕的高度，px                  |
| width       | 屏幕的宽度，px                  |

屏幕宽高：

```javascript
//macbook 13.3 retina
document.write(screen.width+'<br />'); //1280
document.write(screen.height+'<br />'); //800
```

屏幕可用宽高

```javascript
document.write("可用宽度：" + screen.availWidth); //1280
document.write("可用高度：" + screen.availHeight); //705
```

## DOM

DOM(Document Object Model)定义和处理HTML文档的标准方法，DOM将html呈现为元素，属性，文本的树结构，也叫节点树。

HTML文档可以说由节点构成的集合，DOM节点有:

1. 元素节点：上图中<html>、<body>、<p>等都是元素节点，即标签。
2. 文本节点:向用户展示的内容，如<li>...</li>中的JavaScript、DOM、CSS等文本。
3. 属性节点:元素属性，如<a>标签的链接属性href="http://bing.com"。

### 属性

| 属性名       | 解释       |
| --------- | -------- |
| nodeName  | 节点名称，字符串 |
| nodeType  | 节点类型，整型  |
| nodeValue | 节点值，字符串  |

```javascript
<body>
	<h1 id="h1">h1</h1>
	<ul>
		<li>l1</li>
		<li>l2</li>
		<li>l3</li>
		<li>l4</li>
		<li>l5</li>
	</ul>

	<script>
		var h1 = document.getElementById('h1');
		console.log(h1.nodeName); //H1
		console.log(h1.nodeType); //1
		console.log(h1.childNodes[0].nodeValue); //h1
	</script>
</body>
```

### 遍历节点方法

| 方法名             | 解释         |
| --------------- | ---------- |
| childNodes      | 元素子节点，数组   |
| firstChild      | 第一个子节点     |
| lastChild       | 最后一个子节点    |
| parentNode      | 父节点        |
| nextSibling     | 当前节点的下一个节点 |
| previousSibling | 当前节点的上一个节点 |

### 节点操作方法

| 方法名                  | 解释                |
| -------------------- | ----------------- |
| createElement(name)  | 创建一个新节点           |
| createTextNode(text) | 创建包含给定文本的文本节点     |
| appendChild()        | 指定节点的子节点最后位置添加新节点 |
| insertBefore()       |                   |
| removeChild()        | 从给定元素中删除一个子节点     |
| replaceChild()       | 替换一个节点            |

```javascript
<!DOCTYPE html>
<html>

	<head>
		<meta charset="UTF-8">
		<title></title>
	</head>

	<body>
		<h1 id="h1">h1</h1>
		<ul>
			<li>l1</li>
			<li>l2</li>
			<li id="ul_l3">l3</li>
			<li>l4</li>
			<li>l5</li>
		</ul>

		<script>
			var ul = document.getElementsByTagName('ul')[0];

			var ul_l3 = document.getElementById('ul_l3');

			var h2Node = document.createElement("h2");
			var textNode = document.createTextNode('这是text');

			var replaceextNode = document.createTextNode('这是替换进来的');

			ul.appendChild(h2Node);

			ul.insertBefore(textNode, ul_l3);

			ul.replaceChild(replaceextNode, ul_l3);

			ul.removeChild(replaceextNode);
		</script>
	</body>

</html>
```

节点类型

**元素类型    节点类型**
  元素          1
  属性          2
  文本          3
  注释          8
  文档          9





































