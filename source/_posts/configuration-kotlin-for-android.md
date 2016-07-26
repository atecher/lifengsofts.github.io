---
title: 搭建使用Kotlin语言开发Android的环境
date: 2016-07-26 18:38:18
categories: Android
tags: 
    - Kotlin
---
# 简介

大家都知道Kotlin语言在Android界还是很火的，到底有多好呢，这篇文章暂不介绍，而这里主要讲解是搭建一个开发环境

# 首先创建一个Android项目

这一步不细讲

> 注意：是使用Android Studio创建不是eclipse

# 安装Kotlin插件

在plugins的仓库里搜索kotlin,安装完成并重启

# 配置build.gradle

这一步值让我们的项目支持kotlin语言

选择Android Studio菜单的Help-Find Action，输入：configure kotlin in project

安装回车，瞬间就配置完了

# 将现有代码转为Kotlin文件

选择Android Studio菜单的Code-conver java file to kotlin file,转换完后，可以看见我们的MainActivity变成这样了：

```kotlin
package cn.woblog.weatherapp

import android.os.Bundle
import android.support.v7.app.AppCompatActivity

class MainActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

    }

}
```

然后运行，如果不出意外，就可以看见主界面了