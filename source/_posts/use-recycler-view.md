---
title: RecyclerView的使用解析
date: 2016-07-28 14:10:19
categories: Android
tags: 
    - RecyclerView
---
# 常见错误

## item宽度一直是wrap_content

布局里面我们一直是写的match_parent，但是运行后却不是，最后发现是inflate时没有穿parent

```kotlin
//return ViewHolder(ViewGroup.inflate(parent.ctx, R.layout.item_weather, null),itemClick);
//return ViewHolder(View.inflate(parent.ctx, R.layout.item_weather, null),itemClick);
return ViewHolder(LayoutInflater.from(parent.context).inflate(R.layout.item_weather, parent,false),itemClick);
```

## ScrollView嵌套

对于这个问题，网上的解决办法五花八门，但都是重写layoutManager的onMeasure方法，这样会有各种问题，要么兼容性不好，要么有性能问题，好消息是在23.2.0后，google提供了官方解决方法，我们只需要

```kotlin
layoutManager.isAutoMeasureEnabled = true
```

这样就不会有问题了