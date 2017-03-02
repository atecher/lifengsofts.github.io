---
title: Android Dialog
date: 2017-03-01 21:49:11
categories: Android
tags: 
    - Dialog
---

# 简介

# 确定取消

```java
AlertDialog.Builder builder=new AlertDialog.Builder(this);
builder.setTitle("这是对话框标题");
builder.setMessage("消息");
builder.setPositiveButton("确定", new OnClickListener() {
  @Override
  public void onClick(DialogInterface dialogInterface, int i) {

  }
});
builder.setNegativeButton("取消", new OnClickListener() {
  @Override
  public void onClick(DialogInterface dialogInterface, int i) {

  }
});
builder.show();
```

如果导入android的包在19和23上效果很差，如果导入android.support.v7.app.AlertDialog效果相同。该类在appcompat-v7中。

该包还有其他的控件：AppCompatEditText，AppCompatButton













