---
title: 常用alias
date: 2017-02-26 17:21:44
categories: Android
tags: 
    - Material Design
---

# 什么是Material Design

Android5.0引入的，是一种全新的设计语言，翻译为原材料设计，是Goole提倡的一种设计风格，理念，原则。是拟物设计和扁平设计的一种结合。

层次感：z轴

1.对于美工：遵循MD的界面设计，图标合集

2.对于产品：页面的跳转，动画效果，交互设计。

3.对于开发：参与原型，辅助美工原型设计。开发实现，界面，动画，专场

# 如何开发MD效果

使用appcompat包，自定义控件实现MD效果

v4:最低兼容到android1.6,ViewPager

v7:2.1,appcompat,cardview,gridlayout,mediarouter,palette,preference,recyclerview(3.0)，该包让开发人员统一开发标准，在任何系统版本保证统一，如：Theme,value，布局，新的特性，动画

现在一般兼容到4.0

# Theme

```xml
<style name="AppTheme" parent="Theme.AppCompat.Light.DarkActionBar">
  <!-- Customize your theme here. -->
  <item name="colorPrimary">#f00</item>
  <item name="colorPrimaryDark">#0f0</item>
  <item name="colorAccent">#00f</item>
  <item name="android:textColor">#080</item>
</style>
```

colorPrimary:主色调用于标题栏，Toolbar背景

colorPrimaryDark：次(深)主色调，用于状态栏，底部导航栏

colorAccent：每个控件的主色调，比如RatingBar的填充色

android:textColor：所有文本颜色











