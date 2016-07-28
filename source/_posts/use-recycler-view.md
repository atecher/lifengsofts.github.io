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

