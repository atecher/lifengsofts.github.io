---
title: React Native
date: 2016-11-14 23:07:23
categories: React Native
tags: 
    - React Native
    - React
---

# 搭建React Native开发环境

## 安装xcode

可以从app Store下载或者在苹果开发者中心下载。

## 安装Command Line Tools

里面包括git这样的命令

```shell
xcode-select --install
```

## 安装homebrew

mac上的一个软件包管理器，和linux上的yum,apt-get差不多

```she
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

## 安装watchman

facebook的一个开源项目，用来监视文件并且记录文件改动情况的一个库。

## 安装flow

JavaScript的静态类检查器，用于找出JavaScript代码中的类型错误。

当然推荐是安装完在nodejs开发中常见的依赖：

```shell
brew install flow git gcc pkg-config cairo libpng jpeg mongodb
```

注意：安装mongodb前先要安装pkg-config，makedepend。如果报错：

```shell
Error: You must `brew link pkg-config makedepend` before mongodb can be installed
```

就要链接：

```shell
brew link makedepend
brew link pkg-config
```

## 安装nodejs

建议使用nvm，因为他可以管理多个版本

官方仓库：https://github.com/creationix/nvm

```shell
sudo curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.32.1/install.sh | bash
```

安装完成后就可以执行nvm命令了。

安装nodejs

```shell
nvm install v4.2.3
nvm alias default v4.2.3
```

当前版本为：

➜  ~ node -v
v4.2.3


➜  ~ npm -v
2.14.7

由于国内有时npm仓库有点慢，所以切换淘宝源：

```shell
npm install cnpm -g
```

## 安装react native

安装脚手架

```shell
cnpm install -g react-native-cli@0.1.10 -g
react-native -v
```

## 创建第一个项目

```shell
react-native init firstApp
```

创建完成后会有如下信息:

```
To run your app on iOS:
   cd /Users/renpingqing/Documents/work/react/fistApp
   react-native run-ios
   - or -
   Open /Users/renpingqing/Documents/work/react/fistApp/ios/fistApp.xcodeproj in Xcode
   Hit the Run button
To run your app on Android:
   Have an Android emulator running (quickest way to get started), or a device connected
   cd /Users/renpingqing/Documents/work/react/fistApp
   react-native run-android
```

现在就可以运行试试看。

运行完后，我可以尝试修改一些代码，来看看效果，但是如果每次修改都刷新模拟器(command+r)这很痛苦的，我们可以通过(command+d)，开启live reload，就可以实现每次保存源代码就自动刷新的功能了。

## 配置subline

首选安装package control(https://packagecontrol.io),这是一个专门管理sb的包网站。安装方法

点击网页的install now，左边会显示安装代码，只需要将这些复制到sb，按control+~贴入代码，安装完成后可以通过command+shift+p呼出package control的窗口。

输入install，然后输入要安装的包，回车就可以安装了。这里安装babel,sublimelinter-jsxhint(安装了就不会提示)。

安装完成后就可以通过sb的view-syntax-open all*-babel-javaScript(babel)，就能将当前语法识别为jsx。

还可以安装gitgutter，sublimelinter,sublimelinter-contrib-eslint。

## 安装全局exhint检查

```java
npm install -g eslint babel-eslint --registry=http://registry.npm.taobao.org
```

# react-native项目结构

可以看做是一个node js项目因为根目录有一个package.json文件，对应一个node_modules的文件夹是该项目的依赖。他下面有个react-native下面又有local-cli和packager(终端打开启动的package就是他)，同时还有一个node_modules，他就是react-native框架所依赖的库。

在最外层可以看到有ios和android目录分别对应相应平台的代码。

.flowconfig：js语法检查规则

.gitignore:版本控制忽略文件

.watchmanconfig：watchman配置文件



index.ios.js结构：

```javascript
import React, { Component } from 'react';
import {
  AppRegistry,
  StyleSheet,
  Text,
  View
} from 'react-native';
```

导入要用到的模块语法，结构赋值es6语法。表示从react-native导出了Text，View等。有点像python的导入。

```javascript
export default class fistApp extends Component {
  render() {
    return (
      <View style={styles.container}>
        <Text style={styles.welcome}>
          Welcome to React a!
        </Text>
        <Text style={styles.instructions}>
          To get started, edit index.ios.js
        </Text>
        <Text style={styles.instructions}>
          Press Cmd+R to reload,{'\n'}
          Cmd+D or shake for dev menu
        </Text>
      </View>
    );
  }
}
```

继承Component实现一个类，并实现render方法，返回一些jsx语法的内容。

```javascript
const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#F5FCFF',
  },
  welcome: {
    fontSize: 20,
    textAlign: 'center',
    margin: 10,
  },
  instructions: {
    textAlign: 'center',
    color: '#333333',
    marginBottom: 5,
  },
});
```

样式代码

```javascript
AppRegistry.registerComponent('fistApp', () => fistApp);
```

注册RN的入口代码。




















