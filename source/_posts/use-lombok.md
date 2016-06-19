---
title: Java界的神器-使用Lombok来消除你的冗余代码量
date: 2016-06-19 11:20:08
categories: Java
tags: 
    - Android
    - Lombok
---

## 简介

他是一个通过注解方式来减少你的POJO类的getter和setter等方法的一个工具，我这里演示的在Android Studio中的使用方式，当然如果你使用的是idea那么这方法也通用，如果你用的是eclipse，那么[官网](https://projectlombok.org)也有视频教程，我这里就不演示了

## 安装依赖

众所周知在在Android Studio中添加依赖有直接下载jar包和使用cradle的dependencies方法，我们这里直接使用dependencies方法

### 添加gradle依赖

在你的项目的build.grade文件中添加

```groovy
provided 'org.projectlombok:lombok:1.12.6'
```

至于为什么是provided而不是compile，因为这个框架是在将java编译为class前处理代码了，意思是在生成的class文件中已经生成了getter和setter，所以这个依赖是我们在编译的时候使用，不需要打包到apk中

## 安装Lombok插件

虽然我们添加了依赖，但是Android Studio他知道怎么处理这个文件吗，肯定是不知道啦，所以我们的安装一个插件来告诉他怎么处理

Preferences > Plugins > Browse repositories

在输入框内输入combo，可看到已经搜索出来了这个插件，我们点击旁边的安装，安装完成后重启插件我们就安装完毕了，它的使用使用说明可以查看[插件主页](https://github.com/mplushnikov/lombok-intellij-plugin)

![](http://7qnc6h.com1.z0.glb.clouddn.com/lombok_plugins.png)

现在插件虽然安装完了，但是Android Studio他怎么知道什么时候来使用这个插件呢，他是不是有个开关什么的，没错！你猜对了

## 开启项目的Annotation process

首先我们打开项目的设置，要强调的是项目的，而不是工具全局的设置，如下图

![](http://7qnc6h.com1.z0.glb.clouddn.com/project_pre.png)

打开后按照下图勾选Enable annotation processing

![](http://7qnc6h.com1.z0.glb.clouddn.com/Snip20160619_2.png)

到这里为止，工具和基本环境我们基本配置完了，接下来我们需要创建一个项目来测试

