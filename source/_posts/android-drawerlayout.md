---
title: DrawerLayout
date: 2017-03-06 21:23:04
categories: Android
tags: 
    - DrawerLayout
---

```
compile 'com.android.support:appcompat-v7:25.1.0'
```

布局

这种布局是，侧滑不盖住toolbar

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
  xmlns:tools="http://schemas.android.com/tools"

  android:layout_width="match_parent"
  android:layout_height="match_parent"
  android:orientation="vertical">
  <android.support.v7.widget.Toolbar
    android:id="@+id/tb"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:background="@color/colorPrimary"></android.support.v7.widget.Toolbar>
  <android.support.v4.widget.DrawerLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/dl"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context="cn.woblog.android.ls_md_drawerlayout.MainActivity">

    <!--内容-->
    <LinearLayout
      android:layout_width="match_parent"
      android:layout_height="match_parent"
      android:background="#0f0"
      android:orientation="vertical">

      <!--<android.support.v7.widget.Toolbar-->
      <!--android:layout_width="match_parent"-->
      <!--android:id="@+id/tb"-->
      <!--android:background="@color/colorPrimary"-->
      <!--android:layout_height="wrap_content"></android.support.v7.widget.Toolbar>-->
      <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="我是内容"
        android:textColor="#f00" />
    </LinearLayout>

    <!--我是侧滑-->
    <LinearLayout
      android:layout_width="match_parent"
      android:layout_height="match_parent"
      android:layout_gravity="start"
      android:background="#00f"
      android:orientation="vertical">
      <TextView
        android:layout_width="match_parent"
        android:layout_height="50dp"
        android:gravity="center"
        android:text="item1"
        android:textColor="#f00" />
      <TextView
        android:layout_width="match_parent"
        android:layout_height="50dp"
        android:gravity="center"
        android:text="item1"
        android:textColor="#f00" />
      <TextView
        android:layout_width="match_parent"
        android:layout_height="50dp"
        android:gravity="center"
        android:text="item1"
        android:textColor="#f00" />
    </LinearLayout>
  </android.support.v4.widget.DrawerLayout>
</LinearLayout>
```

盖住toolbar

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
  xmlns:tools="http://schemas.android.com/tools"

  android:layout_width="match_parent"
  android:layout_height="match_parent"
  android:orientation="vertical">

  <android.support.v4.widget.DrawerLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/dl"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context="cn.woblog.android.ls_md_drawerlayout.MainActivity">

    <!--内容-->
    <LinearLayout
      android:layout_width="match_parent"
      android:layout_height="match_parent"
      android:background="#0f0"
      android:orientation="vertical">

      <android.support.v7.widget.Toolbar
        android:id="@+id/tb"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:background="@color/colorPrimary"></android.support.v7.widget.Toolbar>
      <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="我是内容"
        android:textColor="#f00" />
    </LinearLayout>

    <!--我是侧滑-->
    <LinearLayout
      android:layout_width="match_parent"
      android:layout_height="match_parent"
      android:layout_gravity="start"
      android:background="#00f"
      android:orientation="vertical">
      <TextView
        android:layout_width="match_parent"
        android:layout_height="50dp"
        android:gravity="center"
        android:text="item1"
        android:textColor="#f00" />
      <TextView
        android:layout_width="match_parent"
        android:layout_height="50dp"
        android:gravity="center"
        android:text="item1"
        android:textColor="#f00" />
      <TextView
        android:layout_width="match_parent"
        android:layout_height="50dp"
        android:gravity="center"
        android:text="item1"
        android:textColor="#f00" />
    </LinearLayout>
  </android.support.v4.widget.DrawerLayout>
</LinearLayout>
```

现在就有侧滑效果了。

添加toolbar menu效果

在代码中找到，并设置为actionBar

```java
Toolbar tb = (Toolbar) findViewById(R.id.tb);
DrawerLayout dl = (DrawerLayout) findViewById(R.id.dl);

setSupportActionBar(tb);
ActionBarDrawerToggle actionBarDrawerToggle = new ActionBarDrawerToggle(this,dl,tb,R.string.drawer_open, R.string.drawer_close);

//同步状态
actionBarDrawerToggle.syncState();

dl.addDrawerListener(actionBarDrawerToggle);
```

左右都侧滑，只需要在原有的菜单下面在添加一个菜单布局，然后android:layout_gravity="end"

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
  xmlns:tools="http://schemas.android.com/tools"

  android:layout_width="match_parent"
  android:layout_height="match_parent"
  android:orientation="vertical">

  <android.support.v4.widget.DrawerLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/dl"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context="cn.woblog.android.ls_md_drawerlayout.MainActivity">

    <!--内容-->
    <LinearLayout
      android:layout_width="match_parent"
      android:layout_height="match_parent"
      android:background="#0f0"
      android:orientation="vertical">

      <android.support.v7.widget.Toolbar
        android:id="@+id/tb"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:background="@color/colorPrimary"></android.support.v7.widget.Toolbar>
      <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="我是内容"
        android:textColor="#f00" />
    </LinearLayout>

    <!--我是侧滑-->
    <LinearLayout
      android:layout_width="match_parent"
      android:layout_height="match_parent"
      android:layout_gravity="start"
      android:background="#00f"
      android:orientation="vertical">
      <TextView
        android:layout_width="match_parent"
        android:layout_height="50dp"
        android:gravity="center"
        android:text="item1"
        android:textColor="#f00" />
      <TextView
        android:layout_width="match_parent"
        android:layout_height="50dp"
        android:gravity="center"
        android:text="item1"
        android:textColor="#f00" />
      <TextView
        android:layout_width="match_parent"
        android:layout_height="50dp"
        android:gravity="center"
        android:text="item1"
        android:textColor="#f00" />
    </LinearLayout>

    <!--我是右边的侧滑-->
    <LinearLayout
      android:layout_width="match_parent"
      android:layout_height="match_parent"
      android:layout_gravity="end"
      android:background="#00f"
      android:orientation="vertical">
      <TextView
        android:layout_width="match_parent"
        android:layout_height="50dp"
        android:gravity="center"
        android:text="item20"
        android:textColor="#f00" />
      <TextView
        android:layout_width="match_parent"
        android:layout_height="50dp"
        android:gravity="center"
        android:text="item21"
        android:textColor="#f00" />
      <TextView
        android:layout_width="match_parent"
        android:layout_height="50dp"
        android:gravity="center"
        android:text="item22"
        android:textColor="#f00" />
    </LinearLayout>
  </android.support.v4.widget.DrawerLayout>
</LinearLayout>
```

实现大概qq的效果,起始就是menu从小放大，并移动，内容缩小，右边移动

```java
//实现类似qq旧版侧滑
dl.addDrawerListener(new DrawerListener() {
  @Override
  public void onDrawerSlide(View drawerView, float slideOffset) {
    //抽屉滑动的时候，调用，0~1

    float scale=1-slideOffset;  //1~0;

    float leftScale= (float) (1-scale*0.3); //scale*0.3,就将这个scale缩小到了0.3~0中，然后1-这个值，就是0.7~1
    ll_left_men_container.setScaleX(leftScale); //从小到大，0.7~1
    ll_left_men_container.setScaleY(leftScale); //从小到大，0.7~1

    float rightScale= (float) (0.7+scale*0.3);

    //内容布局，缩放，0.7~1
    ll_content_container.setScaleX(rightScale);
    ll_content_container.setScaleY(rightScale);

    // 右移动,0~width*0.3
    float translation= (float) (ll_content_container.getMeasuredWidth()*(slideOffset*0.3));
    ll_content_container.setTranslationX(translation);
  }

  @Override
  public void onDrawerOpened(View drawerView) {
    //完全打开
  }

  @Override
  public void onDrawerClosed(View drawerView) {
//完全关闭
  }

  @Override
  public void onDrawerStateChanged(int newState) {
//状态改变，比如现在是打开，然后关闭了
  }
});
```



```java
//    或者，内容右移动菜单的宽度
ll_content_container.setTranslationX(ll_left_men_container.getMeasuredWidth()*slideOffset);
```
















