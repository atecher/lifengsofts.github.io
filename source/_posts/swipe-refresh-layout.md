---
title: Swipe Refresh Layout
date: 2017-03-01 22:38:40
categories: Android
tags: 
    - Refresh
---

# 简介

# 基本使用

用SwipeRefreshLayout包裹你要刷新的布局。然后在代码摄者一些参数

```java
srl = (SwipeRefreshLayout) findViewById(R.id.srl);
srl.setColorSchemeColors(Color.RED,Color.GREEN,Color.BLUE);
srl.setProgressBackgroundColorSchemeColor(Color.DKGRAY);

srl.setOnRefreshListener(new OnRefreshListener() {
  @Override
  public void onRefresh() {
    
  }
});
```

# ListPopupWindow

```java
ArrayAdapter<String> stringArrayAdapter = new ArrayAdapter<String>(this,android.R
.layout.simple_list_item_1,new String[]{"条目1","条目1","条目1","条目1"});
final ListPopupWindow listPopupWindow = new ListPopupWindow(this);
listPopupWindow.setAdapter(stringArrayAdapter);
listPopupWindow.setOnItemClickListener(new OnItemClickListener() {
  @Override
  public void onItemClick(AdapterView<?> adapterView, View view, int i, long l) {
    Toast.makeText(MainActivity.this, "click："+i, Toast.LENGTH_SHORT).show();
    listPopupWindow.dismiss();
  }
});
listPopupWindow.setAnchorView(view);
listPopupWindow.show();
```

# PopupMenu

```java
PopupMenu popupMenu = new PopupMenu(this, view);
popupMenu.getMenuInflater().inflate(R.menu.main,popupMenu.getMenu());
popupMenu.setOnMenuItemClickListener(new OnMenuItemClickListener() {
  @Override
  public boolean onMenuItemClick(MenuItem item) {
    Toast.makeText(MainActivity.this, item.getTitle(), Toast.LENGTH_SHORT).show();
    return true;
  }
});
popupMenu.show();
```

# LinearLayoutCompat

```xml
<android.support.v7.widget.LinearLayoutCompat xmlns:android="http://schemas.android.com/apk/res/android"
  xmlns:tools="http://schemas.android.com/tools"
  xmlns:app="http://schemas.android.com/apk/res-auto"
  android:id="@+id/activity_main"
  android:layout_width="match_parent"
  android:layout_height="match_parent"
  android:orientation="vertical"
  app:divider="@android:drawable/divider_horizontal_bright"
  app:showDividers="middle|end|beginning"
  tools:context="cn.woblog.android.androiddialog.MainActivity">
```

可以自动给每个条目前后添加分割线







