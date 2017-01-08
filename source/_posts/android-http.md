---
title: AndroidHttp
date: 2017-01-07 21:21:29
categories: Android
tags: 
    - Android
---

# 常用网络框架介绍

# Volley

### 优点

默认2.3及上以上基于HttpUrlConnection，2.3以下基于HttpClient

符合http缓存语义的缓存机制（提供了默认的磁盘缓存和内存缓存）

请求队列的优先级排序

提供多样的取消机制

提供简单的图片加载工具（一般使用它就是为了他有图片加载功能，很轻量）

### 缺点

不能下载文件

## Android-async-http

### 优点

在匿名回调中处理请求结构

在子线程中处理Http请求

文件的端点上传

智能重试功能

默认开启gzip亚索

支持解析json数据

可以将Cookies保存到SharedPreferences

### 缺点

可以说是基本上没有缺点，但是就是作者好像没维护了

## Afinal

### 优点

该框架提供了很多功能

数据库：使用了线程池操作sqlite

注解模块：ioc框架，使用注解方法绑定UI和事件，不需要findViewById和setOnClickListener

网络模块：通过httpclient请求数据，支持ajax方法，支持文件下载，上传功能

图片缓存模块：通过FinalBitmap,使得加载Bitmap无序考虑是否有OOM异常

## XUtils

和Afinal差不多

## Okhttp

支持Http/2协议

使用连接池减少网络延迟

支持gzip

请求的缓存

## retrofit

在okhttp上的一层封装

## 优点

支持okhttp

注解处理，简化代码

支持上传和下载文件

支持自定义解析数据格式

支持多种http库

# 如何选择一个框架

学习成本

文档是否完善

github star数量

现在是否有人在维护

流行程度

代码的设计是否有可借鉴性

代码的体积

# Okhttp

## 加入引用

```groovy
compile 'com.squareup.okhttp3:okhttp:3.5.0'
```

## 基本使用

```java
OkHttpClient okHttpClient = new OkHttpClient();

Request request = new Request.Builder().url("http://www.baidu.com").build();
try {
    Response response = okHttpClient.newCall(request).execute();
    if (response.isSuccessful()) {
        System.out.println(response.body().string());
    }
} catch (IOException e) {
    e.printStackTrace();
}
```






