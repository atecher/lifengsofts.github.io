---
title: LinearLayoutCompat源码分析
date: 2017-03-04 20:15:58
categories: Android
tags: 
    - LinearLayoutCompat
    - View
---

# 简介

他可以实现快速为里面的内容前，中和后面添加分割线，使用方法也很简单。

其中有几个很重要的属性：

app:divider="@drawable/item_divider"：给他一个drawable,用来当做分割线

app:showDividers="beginning|middle|end"：显示分割线的位置



# 水平分割线

```xml
<?xml version="1.0" encoding="utf-8"?>
<HorizontalScrollView xmlns:android="http://schemas.android.com/apk/res/android"
  xmlns:app="http://schemas.android.com/apk/res-auto"
  xmlns:tools="http://schemas.android.com/tools"
  android:layout_width="match_parent"
  android:layout_height="match_parent">
  <android.support.v7.widget.LinearLayoutCompat
    android:id="@+id/ll_root_container"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="horizontal"
    app:divider="@drawable/item_divider"
    app:showDividers="beginning|middle|end"
    tools:context="cn.woblog.android.linealayoutcompat.MainActivity">

    <TextView
      android:layout_width="100dp"
      android:layout_height="30dp"
      android:gravity="center"
      android:text="1" />

    <TextView
      android:background="#f00"
      android:layout_width="100dp"
      android:layout_height="30dp"
      android:gravity="center"
      android:text="1" />
    <TextView
      android:layout_width="100dp"
      android:layout_height="30dp"
      android:gravity="center"
      android:text="1" />
    <TextView
      android:layout_width="100dp"
      android:layout_height="30dp"
      android:gravity="center"
      android:text="1" />
    <TextView
      android:layout_width="100dp"
      android:layout_height="30dp"
      android:gravity="center"
      android:text="1" />
  </android.support.v7.widget.LinearLayoutCompat>
</HorizontalScrollView>
```



# 垂直分割线

```xml
<?xml version="1.0" encoding="utf-8"?>
<ScrollView xmlns:android="http://schemas.android.com/apk/res/android"
  xmlns:app="http://schemas.android.com/apk/res-auto"
  xmlns:tools="http://schemas.android.com/tools"
  android:layout_width="match_parent"
  android:layout_height="match_parent">
  <android.support.v7.widget.LinearLayoutCompat
    android:id="@+id/ll_root_container"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    app:divider="@drawable/item_divider"
    app:showDividers="beginning|middle|end"
    tools:context="cn.woblog.android.linealayoutcompat.MainActivity">

    <TextView
      android:layout_width="100dp"
      android:layout_height="30dp"
      android:gravity="center"
      android:text="1" />

    <TextView
      android:background="#f00"
      android:layout_width="100dp"
      android:layout_height="30dp"
      android:gravity="center"
      android:text="1" />
    <TextView
      android:layout_width="100dp"
      android:layout_height="30dp"
      android:gravity="center"
      android:text="1" />
    <TextView
      android:layout_width="100dp"
      android:layout_height="30dp"
      android:gravity="center"
      android:text="1" />
    <TextView
      android:layout_width="100dp"
      android:layout_height="30dp"
      android:gravity="center"
      android:text="1" />
  </android.support.v7.widget.LinearLayoutCompat>
</ScrollView>
```

item_divider.xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<shape xmlns:android="http://schemas.android.com/apk/res/android" 
    android:shape="rectangle">
    <size android:width="10dp" android:height="10dp"/>
	<solid android:color="#ff0000"/>
</shape>
```











