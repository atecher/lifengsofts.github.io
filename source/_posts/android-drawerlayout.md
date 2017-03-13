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

android:layout_gravity="start",一定要设置这个属性

# NavigationView

谷歌侧滑的View。一种规范，用来规范侧滑的样式

Design包中。使用NavigationView，依赖design，recycelerView,CardView。外层还是DrawerLayout，这是Activity布局

```xml
<?xml version="1.0" encoding="utf-8"?>
<android.support.v4.widget.DrawerLayout xmlns:android="http://schemas.android.com/apk/res/android"
  xmlns:app="http://schemas.android.com/apk/res-auto"
  xmlns:tools="http://schemas.android.com/tools"
  android:layout_width="match_parent"

  android:layout_height="match_parent"
  android:fitsSystemWindows="true"
  tools:context="cn.woblog.android.ls_md_drawerlayout.NavigationActivity">

  <!--内容-->
  <RelativeLayout
    android:layout_width="match_parent"
    android:layout_height="wrap_content"></RelativeLayout>

  <android.support.design.widget.NavigationView
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:layout_gravity="start"
    app:headerLayout="@layout/header_menu"
    app:menu="@menu/navigation_menu"></android.support.design.widget.NavigationView>

</android.support.v4.widget.DrawerLayout>

```

NavigationView引用了一个菜单和header_menu，header_menu就是一个常规布局用于显示到Item上方。

menu和普通的menu写法一样

```xml
<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android="http://schemas.android.com/apk/res/android">

  <item
    android:id="@+id/menu_1"
    android:icon="@android:drawable/ic_menu_add"
    android:orderInCategory="100"
    android:title="add" />

  <item
    android:id="@+id/menu_2"
    android:icon="@android:drawable/ic_menu_agenda"
    android:orderInCategory="100"
    android:title="agenda" />

  <item
    android:id="@+id/menu_3"
    android:icon="@android:drawable/ic_menu_call"
    android:orderInCategory="100"
    android:title="call" />
</menu>
```

还可以有子菜单

```xml
<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android="http://schemas.android.com/apk/res/android">

  <item
    android:id="@+id/menu_1"
    android:icon="@android:drawable/ic_menu_add"
    android:orderInCategory="100"
    android:title="add" />

  <item
    android:id="@+id/menu_2"
    android:icon="@android:drawable/ic_menu_agenda"
    android:orderInCategory="100"
    android:title="agenda" />

  <item
    android:id="@+id/menu_3"
    android:icon="@android:drawable/ic_menu_call"
    android:orderInCategory="100"
    android:title="call">
    <menu>
      <item
        android:id="@+id/menu_31"
        android:icon="@android:drawable/ic_menu_agenda"
        android:orderInCategory="100"
        android:title="agenda" />

    </menu>
  </item>
</menu>
```

# SnackBar

一个新的toast，和Dialog中间的产物。design中s

Toast:用户无法交互

Dialog:打断用户。

他结合了两种

基本使用

```java
Snackbar s=Snackbar.make(view,"打开GPS?",Snackbar.LENGTH_LONG);
//按钮，不能设置多个，后面的覆盖前面的
s.setAction("确定", new OnClickListener() {
  @Override
  public void onClick(View v) {
    showToast(null);
  }
});
//监听关闭，打开
s.addCallback(new Callback(){
  @Override
  public void onShown(Snackbar sb) {
    super.onShown(sb);
  }

  @Override
  public void onDismissed(Snackbar transientBottomBar, int event) {
    super.onDismissed(transientBottomBar, event);
  }
});

//按钮颜色
s.setActionTextColor(Color.RED);

s.show();
```



Android Resource Navigator：源码查看器

Android SDK Search:



如果想更改消息的颜色，可以通过更改项目的样式

```xml
<item name="android:textSize">@dimen/design_snackbar_text_size</item>
<item name="android:textColor">?android:textColorPrimary</item>
```

但是这样就更改了全局样式。

# TextInputLayout

带提示的信息的EditText

```xml
<android.support.design.widget.TextInputLayout
  android:layout_width="match_parent"
  app:hintAnimationEnabled="false"
  android:layout_height="wrap_content">
  <EditText
    android:layout_width="match_parent"
    android:hint="请输入密码"
    android:layout_height="wrap_content" />
</android.support.design.widget.TextInputLayout>
```

app:hintAnimationEnabled="false"：是否开启提示文字动画

app:errorEnabled="true":是否开启错误提示，但是你的自定义什么错误

 app:counterOverflowTextAppearance=""  超出字符数文字样式

app:counterTextAppearance=""
app:errorTextAppearance=""

计数

```java
til = (TextInputLayout) findViewById(R.id.til);
//    til.getEditText().addTextChangedListener();

    //计数
    til.setCounterEnabled(true);
    til.setCounterMaxLength(10);
```

```java
til.getEditText().addTextChangedListener(new MinLengthTextWatch(til,"长度应低于6"));

```

```java
//自定义错误
class MinLengthTextWatch implements TextWatcher{

    private final TextInputLayout textInputLayout;
    private final String message;

    public MinLengthTextWatch(TextInputLayout textInputLayout,String message) {
      this.textInputLayout=textInputLayout;
      this.message=message;
    }

    @Override
    public void beforeTextChanged(CharSequence s, int start, int count, int after) {

    }

    @Override
    public void onTextChanged(CharSequence s, int start, int before, int count) {

    }

    @Override
    public void afterTextChanged(Editable s) {
      if (textInputLayout.getEditText().getText().toString().length() <= 6) {
        textInputLayout.setErrorEnabled(false);
      } else {
        textInputLayout.setErrorEnabled(true);
        textInputLayout.setError(message);
      }
    }
}
```

# ToolBar

ActionBar:3.0,也就是兼容包,google规范了导航，但是不好用，扩展性不好。多数人用民间ActionBar，是SherlockActionBar,后面google重新定义了ToolBar,在MD中有AppBar

作用：导航-显示标题，导航back，会计操作，操蛋，toolbar不一定放在顶部，也可以底部



使用：

1.引入v7-appcompat

2.使用appcompatActivity

3.修改主题为Theme.AppCompat.Light.NoActionBar

4.然后在布局中添加Toolbar

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
  xmlns:tools="http://schemas.android.com/tools"
  xmlns:app="http://schemas.android.com/apk/res-auto"
  android:id="@+id/activity_main"
  android:layout_width="match_parent"
  android:layout_height="match_parent"
  tools:context="cn.woblog.android.l10_md_toolbar.MainActivity">

  <android.support.v7.widget.Toolbar
    android:id="@+id/tb"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:background="?attr/colorPrimary"
    app:logo="@mipmap/ic_launcher"
    app:navigationIcon="@android:drawable/ic_menu_upload"
    app:subtitle="副标题"
    app:title="这是标题">
    <!--<TextView-->
      <!--android:layout_width="wrap_content"-->
      <!--android:layout_height="wrap_content"-->
      <!--android:layout_gravity="center"-->
      <!--android:text="这是其他文本" />-->
  </android.support.v7.widget.Toolbar>

</LinearLayout>

```

5.替换默认的actionBar

```java
Toolbar tb= (Toolbar) findViewById(R.id.tb);
    setSupportActionBar(tb);
```

//text 默认覆盖了 toolbar的字

监听返回按钮

```java
tb.setNavigationOnClickListener(new OnClickListener() {
      @Override
      public void onClick(View v) {
        finish();
      }
    });
```

app:popupTheme="@style/ThemeOverlay.AppCompat.Dark":修改弹出窗体也就是右上角菜单的样式



# SearchView

可以实现在Toolbar上显示一个搜索框

```xml
<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android="http://schemas.android.com/apk/res/android"
  xmlns:app="http://schemas.android.com/apk/res-auto">


  <item
    android:id="@+id/menu_search"
    app:actionViewClass="android.support.v7.widget.SearchView"
    android:icon="@android:drawable/ic_menu_search"
    android:title="搜索"
    app:showAsAction="always" />
  <item
    android:id="@+id/menu_share"
    android:icon="@android:drawable/ic_menu_share"
    android:title="分享" />
  <item
    android:id="@+id/menu_more"
    android:icon="@android:drawable/ic_menu_more"
    android:title="更多"
    app:showAsAction="never" />
</menu>
```

然后在activity中添加，显示menu，还可以设置一些监听器

```java
package cn.woblog.android.l10_md_toolbar;

import android.graphics.Color;
import android.support.v4.view.MenuItemCompat;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.support.v7.widget.SearchView;
import android.support.v7.widget.SearchView.OnQueryTextListener;
import android.support.v7.widget.SearchView.SearchAutoComplete;
import android.support.v7.widget.Toolbar;
import android.view.Menu;
import android.view.MenuItem;
import android.view.View;
import android.view.View.OnClickListener;
import android.view.View.OnFocusChangeListener;
import android.widget.Toast;

public class MainActivity extends AppCompatActivity {

  @Override
  protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);

    Toolbar tb= (Toolbar) findViewById(R.id.tb);
    setSupportActionBar(tb);

    tb.setNavigationOnClickListener(new OnClickListener() {
      @Override
      public void onClick(View v) {
        finish();
      }
    });
  }

  @Override
  public boolean onCreateOptionsMenu(Menu menu) {
    getMenuInflater().inflate(R.menu.menu_main,menu);
    //SearchView在menu中
    MenuItem item = menu.findItem(R.id.menu_search);
    SearchView searchView = (SearchView) MenuItemCompat.getActionView(item);
    //进来就呈现搜索框
//    searchView.setIconified(false);
    //不能取消这个搜索框
//    searchView.setIconifiedByDefault(false);

    //自定义扩展,更改提示和颜色
    SearchView.SearchAutoComplete searchEditTextView = (SearchAutoComplete) searchView.findViewById(R.id.search_src_text);
    searchEditTextView.setHint("请输入商品名称");
    searchEditTextView.setHintTextColor(Color.WHITE);

  searchView.setSubmitButtonEnabled(true);

    //想AutoCompleteTextView提示
//    searchView.setSuggestionsAdapter();


    //进入查询
    searchView.setOnQueryTextFocusChangeListener(new OnFocusChangeListener() {
      @Override
      public void onFocusChange(View v, boolean hasFocus) {


      }

    });

    //关闭
//    searchView.setOnCloseListener();
    //搜索按钮
//    searchView.setOnSearchClickListener(/);

    //文本变化
    searchView.setOnQueryTextListener(new OnQueryTextListener() {
      @Override
      public boolean onQueryTextSubmit(String query) {
        //点击提交时
        return false;
      }

      @Override
      public boolean onQueryTextChange(String newText) {
        return false;
      }
    });

    return super.onCreateOptionsMenu(menu);
  }

  @Override
  public boolean onOptionsItemSelected(MenuItem item) {
    switch (item.getItemId()) {
      case R.id.menu_share:
        Toast.makeText(this, "share", Toast.LENGTH_SHORT).show();
        break;
    }
    return super.onOptionsItemSelected(item);
  }
}

```

# 滑动是状态栏变透明

重点：

```
android:paddingTop="?attr/actionBarSize" //padding
android:clipToPadding="false" //绘制范围是否在padding里面，
android:clipChildren="false" //子控件是否超出padding区域
```

布局

```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
  xmlns:tools="http://schemas.android.com/tools"
  xmlns:app="http://schemas.android.com/apk/res-auto"
  android:id="@+id/activity_main"
  android:layout_width="match_parent"
  android:layout_height="match_parent"
  tools:context="cn.woblog.android.l10_md_toolbar_translucent.MainActivity">

  <cn.woblog.android.l10_md_toolbar_translucent.MyScrollView
    android:layout_width="match_parent"
    android:id="@+id/sv"
    android:paddingTop="?attr/actionBarSize"
    android:clipToPadding="false"
    android:clipChildren="false"
    android:layout_height="match_parent">

    <android.support.v7.widget.LinearLayoutCompat
      android:layout_width="match_parent"
      android:layout_height="match_parent"

      android:orientation="vertical">
      <Button
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="button" />
      <Button
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="button" />
      <Button
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="button" />
      <Button
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="button" />
      <Button
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="button" />
      <Button
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="button" />
      <Button
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="button" />
      <Button
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="button" />
      <Button
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="button" />
      <Button
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="button" />
      <Button
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="button" />
      <Button
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="button" />

      <Button
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="button" />
      <Button
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="button" />
      <Button
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="button" />
      <Button
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="button" />
      <Button
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="button" />
      <Button
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="button" />
      <Button
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="button" />
      <Button
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="button" />
    </android.support.v7.widget.LinearLayoutCompat>
  </cn.woblog.android.l10_md_toolbar_translucent.MyScrollView>

  <android.support.v7.widget.Toolbar
    android:id="@+id/tb"
    android:layout_width="match_parent"
    android:background="?attr/colorPrimary"
    app:title="标题"
    android:layout_height="?attr/actionBarSize">

  </android.support.v7.widget.Toolbar>
</RelativeLayout>

```

自定义scrollView

```java
package cn.woblog.android.l10_md_toolbar_translucent;

import android.content.Context;
import android.util.AttributeSet;
import android.widget.ScrollView;

/**
 * Created by renpingqing on 2017/3/10.
 */

public class MyScrollView extends ScrollView {

  private  ScrollListener scrollListener;

  public void setScrollListener(ScrollListener scrollListener) {
    this.scrollListener = scrollListener;
  }

  public MyScrollView(Context context, AttributeSet attrs) {
    super(context, attrs);
  }

  @Override
  protected void onScrollChanged(int l, int t, int oldl, int oldt) {
    super.onScrollChanged(l, t, oldl, oldt);

    if (scrollListener != null) {

//      滑出去的高度/屏幕高度
      int scrollY=getScrollY();
      int height=getContext().getResources().getDisplayMetrics().heightPixels;

      double v = height * 1.0 / 3.0;
      if (scrollY<= v) {
        scrollListener.onScroll((float) (1- (scrollY*1.0/v))); //1~0
      }

    }
  }


}
```

使用

```java
package cn.woblog.android.l10_md_toolbar_translucent;

import android.os.Bundle;
import android.support.v7.app.AppCompatActivity;
import android.support.v7.widget.Toolbar;
import android.util.Log;

public class MainActivity extends AppCompatActivity implements ScrollListener {

  private Toolbar tb;

  @Override
  protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);

    tb = (Toolbar) findViewById(R.id.tb);

    setSupportActionBar(tb);

    MyScrollView sv= (MyScrollView) findViewById(R.id.sv);

    sv.setScrollListener(this);
  }

  @Override
  public void onScroll(float alpha) {
    Log.d("TAG","a:"+alpha);
    tb.setAlpha(alpha);
  }
}

```

# Palette

调色板，v7-palette，可以分析出一些色彩特性,主色调，鲜艳的颜色，柔和的颜色等。

```java
BitmapDrawable bitmapDrawable = (BitmapDrawable) iv.getDrawable();
    Bitmap bitmap = bitmapDrawable.getBitmap();
//    Palette palette = Palette.generate(bitmap); //不推荐
    Palette.from(bitmap).generate(new PaletteAsyncListener() {
      @Override
      public void onGenerated(Palette palette) {
        //暗，柔和
        int darkMutedColor = palette.getDarkMutedColor(Color.BLUE);
        //暗，鲜艳
        int darkVibrantColor = palette.getDarkVibrantColor(Color.BLUE);
        //亮，柔和
        int lightMutedColor = palette.getLightMutedColor(Color.BLUE);
        //亮，鲜艳
        int lightVibrantColor = palette.getLightVibrantColor(Color.BLUE);

        //鲜艳
        int vibrantColor = palette.getVibrantColor(Color.BLUE);
        //柔和
        int mutedColor = palette.getMutedColor(Color.BLUE);

        tv1.setBackgroundColor(darkMutedColor);
        tv2.setBackgroundColor(darkVibrantColor);
        tv3.setBackgroundColor(lightMutedColor);
        tv4.setBackgroundColor(lightVibrantColor);
        tv5.setBackgroundColor(vibrantColor);
        tv6.setBackgroundColor(mutedColor);

        //颜色样板，拿到亮，鲜艳的
        Swatch lightVibrantSwatch = palette.getLightVibrantSwatch();
        //推荐，标题颜色
        int titleTextColor = lightVibrantSwatch.getTitleTextColor();
        int bodyTextColor = lightVibrantSwatch.getBodyTextColor();
        //该颜色在图片中所占的比例
        int population = lightVibrantSwatch.getPopulation();
        //图片的整体颜色
        int rgb = lightVibrantSwatch.getRgb();

        tv_title.setBackgroundColor(getTranslucentColor(0.6,rgb));
        tv_body.setBackgroundColor(rgb);

        tv_title.setTextColor(titleTextColor);
        tv_body.setTextColor(bodyTextColor);
      }


    });
```

```java
private int getTranslucentColor(double v, int rgb) {
//    int blue=rgb&0xff;

    int blue=Color.blue(rgb); //还可以这样那

    int green=rgb>>8&0xff;
    int red=rgb>>16&0xff;
    int alpha=rgb>>>24; //无符号，高位补0
    alpha= (int) Math.round(alpha*v);
    return Color.argb(alpha,red,green,blue);
  }
```

# TabLayout

选项卡,design包

TabLayout+viewPager+fragment

布局

```java
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
  xmlns:tools="http://schemas.android.com/tools"
  xmlns:app="http://schemas.android.com/apk/res-auto"
  android:id="@+id/activity_main"
  android:layout_width="match_parent"
  android:orientation="vertical"
  android:layout_height="match_parent"
  tools:context="cn.woblog.android.l12_md_tablayout.MainActivity">

  <android.support.design.widget.TabLayout
    android:id="@+id/tl"
    app:tabIndicatorColor="@color/colorPrimary"
    app:tabTextColor="@color/colorPrimary"
    app:tabSelectedTextColor="#f00"
    app:tabMode="fixed"
    app:tabGravity="center"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"></android.support.design.widget.TabLayout>

  <android.support.v4.view.ViewPager
    android:id="@+id/vp"
    android:layout_width="match_parent"
    android:layout_height="match_parent"></android.support.v4.view.ViewPager>
</LinearLayout>

```

```java
package cn.woblog.android.l12_md_tablayout;

import android.support.design.widget.TabLayout;
import android.support.design.widget.TabLayout.OnTabSelectedListener;
import android.support.design.widget.TabLayout.Tab;
import android.support.design.widget.TabLayout.TabLayoutOnPageChangeListener;
import android.support.v4.app.Fragment;
import android.support.v4.app.FragmentManager;
import android.support.v4.app.FragmentPagerAdapter;
import android.support.v4.view.ViewPager;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;

public class MainActivity extends AppCompatActivity {

  private String[] titles={"新闻","体验"
//      ,"科学","汽车",
//  "科技","财经","美女","八卦"
  };

  @Override
  protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);

    final ViewPager vp= (ViewPager) findViewById(R.id.vp);
    TabLayout tl= (TabLayout) findViewById(R.id.tl);

    MyPagerAdapter myPagerAdapter = new MyPagerAdapter(getSupportFragmentManager());
    vp.setAdapter(myPagerAdapter);
    //title 来自PagerAdapter
  tl.setTabsFromPagerAdapter(myPagerAdapter);

  //1.tab和viewpager关联
    tl.addOnTabSelectedListener(new OnTabSelectedListener() {
      @Override
      public void onTabSelected(Tab tab) {
        //联动viewpager
        vp.setCurrentItem(tab.getPosition());
      }

      @Override
      public void onTabUnselected(Tab tab) {

      }

      @Override
      public void onTabReselected(Tab tab) {

      }
    });

//    2.viewpager关联tab
    vp.addOnPageChangeListener(new TabLayoutOnPageChangeListener(tl));
  }
  class  MyPagerAdapter extends FragmentPagerAdapter{

    public MyPagerAdapter(FragmentManager fm) {
      super(fm);
    }

    @Override
    public Fragment getItem(int position) {
      NewsFragment fragment = new NewsFragment();
      Bundle bundle = new Bundle();
      bundle.putString(NewsFragment.DATA,titles[position]);
      fragment.setArguments(bundle);
      return fragment;
    }

    @Override
    public int getCount() {
      return titles.length;
    }

    @Override
    public CharSequence getPageTitle(int position) {
      return titles[position];
    }
  }
}

```

上面关联tabLayout和ViewPager可以这样关联

```java
tl.setupWithViewPager(vp);
```



# 当tab使用和自定义View

只需要将tabLyout放到底部，自定义item，但是Item要定义高度，但是选中的颜色需要特别处理。

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
  xmlns:tools="http://schemas.android.com/tools"
  xmlns:app="http://schemas.android.com/apk/res-auto"
  android:id="@+id/activity_main"
  android:layout_width="match_parent"
  android:orientation="vertical"
  android:layout_height="match_parent"
  tools:context="cn.woblog.android.l12_md_tablayout.MainActivity">

  <android.support.v4.view.ViewPager
    android:id="@+id/vp"
    android:layout_width="match_parent"
    android:layout_height="0dp" android:layout_weight="1"></android.support.v4.view.ViewPager>

  <android.support.design.widget.TabLayout
    android:id="@+id/tl"
    app:tabIndicatorHeight="0dp"
    app:tabIndicatorColor="@color/colorPrimary"
    app:tabTextColor="@color/colorPrimary"
    app:tabSelectedTextColor="#f00"
    app:tabMode="fixed"
    app:tabGravity="fill"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"></android.support.design.widget.TabLayout>
</LinearLayout>

```

代码

```java
package cn.woblog.android.l12_md_tablayout;

import android.os.Bundle;
import android.support.design.widget.TabLayout;
import android.support.design.widget.TabLayout.Tab;
import android.support.v4.app.Fragment;
import android.support.v4.app.FragmentManager;
import android.support.v4.app.FragmentPagerAdapter;
import android.support.v4.content.ContextCompat;
import android.support.v4.view.ViewPager;
import android.support.v7.app.AppCompatActivity;
import android.view.View;
import android.widget.LinearLayout;
import android.widget.TextView;

public class MainActivity extends AppCompatActivity {

  private String[] titles={"新闻","体验"
//      ,"科学","汽车",
//  "科技","财经","美女","八卦"
  };

  @Override
  protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);

    final ViewPager vp= (ViewPager) findViewById(R.id.vp);
    TabLayout tl= (TabLayout) findViewById(R.id.tl);

    MyPagerAdapter myPagerAdapter = new MyPagerAdapter(getSupportFragmentManager());
    vp.setAdapter(myPagerAdapter);
    //title 来自PagerAdapter
  tl.setTabsFromPagerAdapter(myPagerAdapter);

//  //1.tab和viewpager关联
//    tl.addOnTabSelectedListener(new OnTabSelectedListener() {
//      @Override
//      public void onTabSelected(Tab tab) {
//        //联动viewpager
//        vp.setCurrentItem(tab.getPosition());
//      }
//
//      @Override
//      public void onTabUnselected(Tab tab) {
//
//      }
//
//      @Override
//      public void onTabReselected(Tab tab) {
//
//      }
//    });
//
////    2.viewpager关联tab
//    vp.addOnPageChangeListener(new TabLayoutOnPageChangeListener(tl));

    //在setAdapter后调用
    tl.setupWithViewPager(vp);

    //自定义view
    for (int i = 0; i < tl.getTabCount(); i++) {
      Tab tab = tl.getTabAt(i);
      View view = View.inflate(this, R.layout.item_tab, null);
     TextView tv_tab_title= (TextView) view.findViewById(R.id.tv_tab_title);
      tv_tab_title.setText("标题："+i);
      tab.setCustomView(view);

      //分割线
      LinearLayout linearLayout = (LinearLayout) tl.getChildAt(0);
      linearLayout.setShowDividers(LinearLayout.SHOW_DIVIDER_MIDDLE);
      linearLayout.setDividerDrawable(ContextCompat.getDrawable(this,
          R.drawable.item_divider));
      linearLayout.setDividerPadding(40); //值越大，线越短


    }
  }
  class  MyPagerAdapter extends FragmentPagerAdapter{

    public MyPagerAdapter(FragmentManager fm) {
      super(fm);
    }

    @Override
    public Fragment getItem(int position) {
      NewsFragment fragment = new NewsFragment();
      Bundle bundle = new Bundle();
      bundle.putString(NewsFragment.DATA,titles[position]);
      fragment.setArguments(bundle);
      return fragment;
    }

    @Override
    public int getCount() {
      return titles.length;
    }

    @Override
    public CharSequence getPageTitle(int position) {
      return titles[position];
    }
  }
}

```

现在还需要处理，选中颜色，首先需要定义一个selector

```xml
<?xml version="1.0" encoding="utf-8"?>
<shape xmlns:android="http://schemas.android.com/apk/res/android">
  <solid android:color="#80c0c0c0"/>
  <size android:width="1dp"/>
</shape>
```

然后在item里面引用这个

```xml
<TextView
    android:textColor="@drawable/selector_tab_text"
    android:id="@+id/tv_tab_title"
    android:text="标题"
    android:layout_width="wrap_content"
    android:layout_height="0dp" android:layout_weight="1" />
  </LinearLayout>
```

选中处理

```java
//处理选中监听
    tl.addOnTabSelectedListener(new OnTabSelectedListener() {
      @Override
      public void onTabSelected(Tab tab) {
        tab.getCustomView().findViewById(R.id.tv_tab_title).setSelected(true);
      }

      @Override
      public void onTabUnselected(Tab tab) {
        tab.getCustomView().findViewById(R.id.tv_tab_title).setSelected(false);
      }

      @Override
      public void onTabReselected(Tab tab) {

      }
    });
```

# 澄清是

让整个app沉浸到整个屏幕，没有显示状态栏，美有导航栏。显示做的是，状态栏和导航和app一体的颜色，还有考虑兼容性。兼容到4.4

## 5.0

自定实现了，但是要用AppCompat主题

### 设置主题

值是colorPrimaryDark

### 样式属性

在values-v21及以上可以用这句话设置导航栏颜色

```
<item name="android:navigationBarColor">#0f0</item>
    <item name="android:statusBarColor">#0f0</item>
```

### 代码

```java
getWindow().setStatusBarColor(Color.YELLOW);
    getWindow().setNavigationBarColor(Color.RED);
```

## 4.4 19

只能使用特殊手段，特殊手段就是这个版本中可以设置状态栏为透明

### 样式

不推荐，只能设置19，而且写到主题的。

```
<item name="android:windowTranslucentStatus">true</item>
```

### 代码

```java
getWindow().addFlags(LayoutParams.FLAG_TRANSLUCENT_STATUS);
```

布局内部，的toolbar上

```
android:fitsSystemWindows="true"
```

在setCOntentView前，另外界面到了状态栏下面了，但现在有问题了，就是如果有EditText,只要弹出键盘，toolbar的颜色就会连接到键盘顶部（6.0,4.4没有）。还有就是toolbar标题在最地步了。去掉外层的scrollview就可以了

1.解决办法，推荐

将  android:fitsSystemWindows="true"，移动根布局，然后在设置一个背景(也可以设置android:windowBackground,默认主题里)，还得给内容设置白色。

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
  xmlns:app="http://schemas.android.com/apk/res-auto"
  xmlns:tools="http://schemas.android.com/tools"
  android:id="@+id/activity_main"
  android:layout_width="match_parent"
  android:layout_height="match_parent"
  android:background="?attr/colorPrimary"
  android:fitsSystemWindows="true"
  android:orientation="vertical"
  tools:context="cn.woblog.android.l13mdtranslucent.MainActivity">

  <android.support.v7.widget.Toolbar
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:background="@color/colorPrimary"
    app:title="这是toolbar标题"></android.support.v7.widget.Toolbar>

  <ScrollView
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="#fff">
    <LinearLayout
      android:layout_width="match_parent"
      android:layout_height="match_parent"
      android:orientation="vertical">
      <EditText
        android:layout_width="match_parent"
        android:layout_height="80dp"
        android:text="清输入名字" />
      <EditText
        android:layout_width="match_parent"
        android:layout_height="80dp"
        android:text="清输入名字" />
      <EditText
        android:layout_width="match_parent"
        android:layout_height="80dp"
        android:text="清输入名字" />
      <EditText
        android:layout_width="match_parent"
        android:layout_height="80dp"
        android:text="清输入名字" />
      <EditText
        android:layout_width="match_parent"
        android:layout_height="80dp"
        android:text="清输入名字" />
      <EditText
        android:layout_width="match_parent"
        android:layout_height="80dp"
        android:text="清输入名字" />
      <EditText
        android:layout_width="match_parent"
        android:layout_height="80dp"
        android:text="清输入名字" />
      <EditText
        android:layout_width="match_parent"
        android:layout_height="80dp"
        android:text="清输入名字" />
    </LinearLayout>
  </ScrollView>
</LinearLayout>

```

2.修改toolbal的高度

设置

```
android:fitsSystemWindows="true"
```

到Toolbar,然后修改toolbar高度

```
ViewGroup.LayoutParams layoutParams = toolbar.getLayoutParams();
layoutParams.height+=getStatusBarHeight();
toolbar.setLayoutParams(layoutParams);

//反射
private int getStatusBarHeight() {
    //反射android.R.dimen.status_bar_height
    try {
      Class<?> aClass = Class.forName("com.android.internal.R$dimen");
      Object o = aClass.newInstance();
      String status_bar_height = aClass.getField("status_bar_height").get(o).toString();
      int height = Integer.parseInt(status_bar_height); //id
      int dimensionPixelOffset = getResources().getDimensionPixelSize(height);
      return dimensionPixelOffset;
    } catch (Exception e) {
      e.printStackTrace();
    }
    return 0;
  }
```

3.修改toolbar的padding，比上面那种靠谱

# 虚拟导航NavigationBar沉浸

## 5.x

### 属性

navigationBarColor

values-v21下设置

```
<item name="android:navigationBarColor">#0f0</item>
```

### 代码

setNavigationBarColor

## 4.4

设置虚拟导航透明

跟scrollView设置一个marginBottom或者添加一个TextView,48dp，但是要在代码中动态判断，因为有些手机可以没有虚拟导航栏

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
  xmlns:app="http://schemas.android.com/apk/res-auto"
  xmlns:tools="http://schemas.android.com/tools"
  android:id="@+id/activity_main"
  android:layout_width="match_parent"
  android:layout_height="match_parent"
  android:orientation="vertical"
  android:background="@color/colorPrimary"
  tools:context="cn.woblog.android.l13mdtranslucent.MainActivity">

  <android.support.v7.widget.Toolbar
    android:id="@+id/tb"
    android:layout_width="match_parent"
    android:titleTextColor="#fff"
    android:fitsSystemWindows="true"
    android:layout_height="?attr/actionBarSize"
    android:background="@color/colorPrimary"
    app:title="这是toolbar标题"></android.support.v7.widget.Toolbar>

  <ScrollView
    android:layout_width="match_parent"
    android:layout_height="0dp"
    android:layout_weight="1"
    android:background="#fff">
    <LinearLayout
      android:layout_width="match_parent"
      android:layout_height="match_parent"
      android:orientation="vertical">
      <EditText
        android:layout_width="match_parent"
        android:layout_height="80dp"
        android:text="清输入名字" />
      <EditText
        android:layout_width="match_parent"
        android:layout_height="80dp"
        android:text="清输入名字" />
      <EditText
        android:layout_width="match_parent"
        android:layout_height="80dp"
        android:text="清输入名字" />
      <EditText
        android:layout_width="match_parent"
        android:layout_height="80dp"
        android:text="清输入名字" />
      <EditText
        android:layout_width="match_parent"
        android:layout_height="80dp"
        android:text="清输入名字" />
      <EditText
        android:layout_width="match_parent"
        android:layout_height="80dp"
        android:text="清输入名字" />
      <EditText
        android:layout_width="match_parent"
        android:layout_height="80dp"
        android:text="清输入名字" />
      <EditText
        android:layout_width="match_parent"
        android:layout_height="80dp"
        android:text="清输入名字" />
    </LinearLayout>
  </ScrollView>
  <TextView
    android:layout_width="match_parent"
    android:layout_height="1dp"
    android:id="@+id/tv_navigation_bar"/>
</LinearLayout>

```



```
//导航栏
ViewGroup.LayoutParams params = tv_navigation_bar.getLayoutParams();
params.height=getNavigationBarHeight();
tv_navigation_bar.setLayoutParams(params);
```

```
private int getNavigationBarHeight() {
  //反射android.R.dimen.status_bar_height
  try {
    Class<?> aClass = Class.forName("com.android.internal.R$dimen");
    Object o = aClass.newInstance();
    String status_bar_height = aClass.getField("navigation_bar_height").get(o).toString();
    int height = Integer.parseInt(status_bar_height); //id
    int dimensionPixelOffset = getResources().getDimensionPixelSize(height);
    return dimensionPixelOffset;
  } catch (Exception e) {
    e.printStackTrace();
  }
  return 0;
}
```



## 兼容性判断

1.sdk版本不一样

​	大于等于5.0，小于5.0大于等于4.4

2.有的没有虚拟导航

​	是否有（源码有方法）

3.有的虚拟导航可以隐藏

​	是否隐藏了

2，3可以一起解决，解决方法是navigationBarHeight高度=这个那个屏幕高度-内容部分view高度，如果大于0表示有

封装完成如下

```java
package cn.woblog.android.l13mdtranslucent;

import android.os.Build.VERSION;
import android.os.Build.VERSION_CODES;
import android.os.Bundle;
import android.support.v7.app.AppCompatActivity;
import android.support.v7.widget.Toolbar;
import android.view.View;
import android.view.ViewGroup;
import android.view.WindowManager.LayoutParams;

/**
 * Created by renpingqing on 2017/3/12.
 */

public class BaseTranslucentActivity extends AppCompatActivity {

  @Override
  public void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);

    //版本大于等于4.4，小于5.0就设置状态栏，导航栏透明
    if (VERSION.SDK_INT>= VERSION_CODES.KITKAT &&VERSION.SDK_INT<VERSION_CODES.LOLLIPOP ) {
      getWindow().addFlags(LayoutParams.FLAG_TRANSLUCENT_STATUS);
      getWindow().addFlags(LayoutParams.FLAG_TRANSLUCENT_NAVIGATION);
    }
  }

  public void setOrChangeTranslucentColor( Toolbar toolbar,View bottomNavigationBar,int primaryColor){
    //版本大于等于4.4，小于5.0就设置状态栏，导航栏透明
    if (VERSION.SDK_INT >= VERSION_CODES.KITKAT && VERSION.SDK_INT < VERSION_CODES.LOLLIPOP) {
      if (toolbar != null) {
        //1.设置toolbar高度
        ViewGroup.LayoutParams layoutParams = toolbar.getLayoutParams();
        layoutParams.height+=getStatusBarHeight();
        toolbar.setLayoutParams(layoutParams);

        //2.然后在设置顶部的padding,这样就不会有控件跑到状态栏下面了
        toolbar.setPadding(
            toolbar.getPaddingLeft(),
            toolbar.getPaddingTop()+getStatusBarHeight(),
            toolbar.getPaddingRight(),
            toolbar.getPaddingBottom()
        );

        toolbar.setBackgroundColor(primaryColor);
      }

      //导航栏
      if (bottomNavigationBar != null) {
        //导航栏
        ViewGroup.LayoutParams params = bottomNavigationBar.getLayoutParams();
        params.height=getNavigationBarHeight();
        bottomNavigationBar.setLayoutParams(params);

        //设置导航栏颜色
        bottomNavigationBar.setBackgroundColor(primaryColor);
      }
    } else if (VERSION.SDK_INT >= VERSION_CODES.LOLLIPOP) {
      //大于等于5.0
      getWindow().setStatusBarColor(primaryColor);
    getWindow().setNavigationBarColor(primaryColor);

    } else {
      //小于4.4,不处理
    }
  }

  private int getNavigationBarHeight() {
    //反射android.R.dimen.status_bar_height
    try {
      Class<?> aClass = Class.forName("com.android.internal.R$dimen");
      Object o = aClass.newInstance();
      String status_bar_height = aClass.getField("navigation_bar_height").get(o).toString();
      int height = Integer.parseInt(status_bar_height); //id
      int dimensionPixelOffset = getResources().getDimensionPixelSize(height);
      return dimensionPixelOffset;
    } catch (Exception e) {
      e.printStackTrace();
    }
    return 0;
  }

  private int getStatusBarHeight() {
    //反射android.R.dimen.status_bar_height
    try {
      Class<?> aClass = Class.forName("com.android.internal.R$dimen");
      Object o = aClass.newInstance();
      String status_bar_height = aClass.getField("status_bar_height").get(o).toString();
      int height = Integer.parseInt(status_bar_height); //id
      int dimensionPixelOffset = getResources().getDimensionPixelSize(height);
      return dimensionPixelOffset;
    } catch (Exception e) {
      e.printStackTrace();
    }
    return 0;
  }
}

```

然后在activity里这么使用

```
super.onCreate(savedInstanceState);
setContentView(R.layout.activity_main);
Toolbar toolbar= (Toolbar) findViewById(R.id.tb);
    TextView tv_navigation_bar= (TextView) findViewById(R.id.tv_navigation_bar);

    setOrChangeTranslucentColor(toolbar,tv_navigation_bar,getResources().getColor(R.color.colorPrimary));
```

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
  xmlns:app="http://schemas.android.com/apk/res-auto"
  xmlns:tools="http://schemas.android.com/tools"
  android:id="@+id/activity_main"
  android:layout_width="match_parent"
  android:layout_height="match_parent"
  android:orientation="vertical"
  android:background="@color/colorPrimary"
  tools:context="cn.woblog.android.l13mdtranslucent.MainActivity">

  <android.support.v7.widget.Toolbar
    android:id="@+id/tb"
    android:layout_width="match_parent"
    android:titleTextColor="#fff"
    android:fitsSystemWindows="true"
    android:layout_height="?attr/actionBarSize"
    android:background="@color/colorPrimary"
    app:title="这是toolbar标题"></android.support.v7.widget.Toolbar>

  <ScrollView
    android:layout_width="match_parent"
    android:layout_height="0dp"
    android:layout_weight="1"
    android:background="#fff">
    <LinearLayout
      android:layout_width="match_parent"
      android:layout_height="match_parent"
      android:orientation="vertical">
      <EditText
        android:layout_width="match_parent"
        android:layout_height="80dp"
        android:text="清输入名字" />
      <EditText
        android:layout_width="match_parent"
        android:layout_height="80dp"
        android:text="清输入名字" />
      <EditText
        android:layout_width="match_parent"
        android:layout_height="80dp"
        android:text="清输入名字" />
      <EditText
        android:layout_width="match_parent"
        android:layout_height="80dp"
        android:text="清输入名字" />
      <EditText
        android:layout_width="match_parent"
        android:layout_height="80dp"
        android:text="清输入名字" />
      <EditText
        android:layout_width="match_parent"
        android:layout_height="80dp"
        android:text="清输入名字" />
      <EditText
        android:layout_width="match_parent"
        android:layout_height="80dp"
        android:text="清输入名字" />
      <EditText
        android:layout_width="match_parent"
        android:layout_height="80dp"
        android:text="清输入名字" />
    </LinearLayout>
  </ScrollView>
  <TextView
    android:layout_width="match_parent"
    android:layout_height="1dp"
    android:id="@+id/tv_navigation_bar"/>
</LinearLayout>

```

# FloatingActionButton

design包，悬浮动作按钮，可以设置着色阴影

特性：阴影，反馈（按下去，elevation）



兼容性：

需要些两个layout

layout-v21这里添加layoutMargin,16dp

低版本要将margin改为0dp



app:backgroundTint:背景着色

elevation：水波颜色

rippleColor:点击后的效果颜色，还要设置clickable，不然没效果

pressedTranslationZ:点击z轴变小多少高度，



点击弹出菜单：

多个按钮上下排列

```xml
<android.support.design.widget.FloatingActionButton
    android:layout_width="wrap_content"
    android:src="@android:drawable/ic_input_add"
    app:backgroundTint="@color/colorPrimary"
    android:elevation="10dp"
    android:onClick="rotate"
    android:layout_margin="16dp"
    app:pressedTranslationZ="10dp"
    android:layout_alignParentBottom="true"
    android:layout_alignParentRight="true"
    app:rippleColor="#f00"
    android:clickable="true"
    android:layout_height="wrap_content" />
```

```java
public void rotate(View view) {
    float toDegree =reverse?-90.0F:90.0F;
    ObjectAnimator anim=ObjectAnimator
        .ofFloat(view,"rotation",0.0f,toDegree)
        ;
    anim
        .setDuration(200)
        .start();

        reverse=!reverse;
  }
```

# RV+FAB+TB

实现的效果就是滚动RV，然后分别隐藏FAB和TB

```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
  xmlns:tools="http://schemas.android.com/tools"
  android:id="@+id/activity_main"
  android:layout_width="match_parent"
  android:layout_height="match_parent"
  tools:context="cn.woblog.android.l16mdfabanimation.MainActivity">

  <android.support.v7.widget.RecyclerView
    android:layout_width="match_parent"
    android:id="@+id/rv"
    android:clipToPadding="false"
    android:clipChildren="false"
    android:paddingTop="?attr/actionBarSize"
    android:layout_height="match_parent"></android.support.v7.widget.RecyclerView>

  <android.support.v7.widget.Toolbar
    android:id="@+id/tb"
    android:background="@color/colorPrimary"
    android:layout_width="match_parent"
    android:layout_height="?attr/actionBarSize"></android.support.v7.widget.Toolbar>

  <ImageView
    android:id="@+id/fab"
    android:layout_width="58dp"
    android:layout_alignParentBottom="true"
    android:layout_alignParentRight="true"
    android:layout_height="58dp"
    android:layout_margin="16dp"
    android:background="@drawable/fab_bg"
    android:src="@android:drawable/ic_input_add" />
</RelativeLayout>

```

```java
package cn.woblog.android.l16mdfabanimation;

import android.os.Bundle;
import android.support.v7.app.AppCompatActivity;
import android.support.v7.widget.LinearLayoutManager;
import android.support.v7.widget.RecyclerView;
import android.support.v7.widget.RecyclerView.OnScrollListener;
import android.support.v7.widget.RecyclerView.ViewHolder;
import android.support.v7.widget.Toolbar;
import android.util.Log;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.view.animation.AccelerateInterpolator;
import android.view.animation.DecelerateInterpolator;
import android.widget.ImageView;
import android.widget.RelativeLayout;
import android.widget.TextView;
import java.util.ArrayList;

public class MainActivity extends AppCompatActivity {
  private static final int THRESHOLD = 20;

  private Toolbar tb;
  private ImageView fab;
  private RecyclerView rv;
  private boolean isVisiable=true;
  private int distance;

  @Override
  protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);

    rv = (RecyclerView) findViewById(R.id.rv);
    tb = (Toolbar) findViewById(R.id.tb);
    fab = (ImageView) findViewById(R.id.fab);

    setSupportActionBar(tb);

    rv.addOnScrollListener(new OnScrollListener() {
      @Override
      public void onScrolled(RecyclerView recyclerView, int dx,int dy) {
        super.onScrolled(recyclerView, dx, dy);
        Log.d("TAG","dy:"+dy);
        //dy 垂直方向的，滚动值正，向上滚动，要隐藏
        if (distance > THRESHOLD && isVisiable) {
          //dy为正，表示
          isVisiable = false;
          hide();
          distance = 0;
        } else if (distance<-THRESHOLD&&!isVisiable) {
        //如果值，小于，并且没有显示，那就显示
          isVisiable=true;
          show();
          distance = 0;
        }

        //累加滚动距离distance
        if ((isVisiable&& dy>0)||(!isVisiable&&dy<0)) {
        distance+=dy;
        }
      }
    });

    rv.setLayoutManager(new LinearLayoutManager(this));

    ArrayList<String> strings = new ArrayList<>();
    for (int i = 0; i < 50; i++) {
      strings.add("item:"+i);
    }
    MyAdapter myAdapter = new MyAdapter(strings);

    rv.setAdapter(myAdapter);
  }

  private void show() {
  //和hide逻辑相反
    tb.animate().translationY(0).setInterpolator(new AccelerateInterpolator(3));

    RelativeLayout.LayoutParams layoutParams= (RelativeLayout.LayoutParams) fab.getLayoutParams();
    fab.animate().translationY(0).setInterpolator(new DecelerateInterpolator(3));
  }

  private void hide() {
    //toolbar，向上移动，自己的高度
    tb.animate().translationY(-tb.getHeight()).setInterpolator(new AccelerateInterpolator(3));

    //fab向下移动，自己的高度和底部的高度
    RelativeLayout.LayoutParams layoutParams = (RelativeLayout.LayoutParams) fab.getLayoutParams();
    fab.animate().translationY(fab.getHeight()+layoutParams.bottomMargin).setInterpolator(new AccelerateInterpolator(3));
  }

  private class MyAdapter extends RecyclerView.Adapter<RecyclerView.ViewHolder>{

    private final ArrayList<String> strings;

    public MyAdapter(ArrayList<String> strings) {
      this.strings=strings;
    }

    @Override
    public ViewHolder onCreateViewHolder(ViewGroup parent, int viewType) {
      return new MyViewHolder(LayoutInflater.from(parent.getContext()).inflate(android.R.layout.simple_list_item_1,parent,false));
    }

    @Override
    public void onBindViewHolder(ViewHolder holder, int position) {

      String s = strings.get(position);
      MyViewHolder holder1= (MyViewHolder) holder;
      holder1.tv.setText(s);
    }

    @Override
    public int getItemCount() {
      return strings.size();
    }

    private class MyViewHolder extends ViewHolder {

      public TextView tv;

      public MyViewHolder(View inflate) {
        super(inflate);
        tv = (TextView) itemView.findViewById(android.R.id.text1);
      }
    }
  }
}

```



# CoordinatorLayout

上面那种实现方法我们还得写监听器，继承ViewGroup,协调并掉拥堵子控件，产生一些效果。

通过设置View的Behavior来设置触摸动画的调度。

## Behavior

他是监听和被监听的桥梁，被监听通知Behavior，我们在Behavior里更改监听控件，这里是监听RV,更改FAB

```xml
<?xml version="1.0" encoding="utf-8"?>
<android.support.design.widget.CoordinatorLayout
  xmlns:android="http://schemas.android.com/apk/res/android"
  xmlns:app="http://schemas.android.com/apk/res-auto"
  xmlns:tools="http://schemas.android.com/tools"
  android:id="@+id/activity_main"
  android:layout_width="match_parent"
  android:layout_height="match_parent"
  tools:context="cn.woblog.android.l16mdfabanimation.MainActivity">

  <android.support.v7.widget.Toolbar
    android:id="@+id/tb"
    android:background="@color/colorPrimary"
    android:layout_width="match_parent"
    android:layout_height="?attr/actionBarSize"></android.support.v7.widget.Toolbar>

  <android.support.design.widget.FloatingActionButton
    android:id="@+id/fab"
    android:layout_width="58dp"
    app:layout_behavior="cn.woblog.android.l16mdfabanimation.FabBehavior"
    android:layout_height="58dp"
    android:layout_margin="16dp"
    android:background="@drawable/fab_bg"
    android:layout_gravity="bottom|end"
    android:src="@android:drawable/ic_input_add" />

  <android.support.v7.widget.RecyclerView
    android:layout_width="match_parent"
    android:id="@+id/rv"

    android:clipToPadding="false"
    android:clipChildren="false"
    android:paddingTop="?attr/actionBarSize"
    android:layout_height="match_parent"></android.support.v7.widget.RecyclerView>

</android.support.design.widget.CoordinatorLayout>

```

```java
package cn.woblog.android.l16mdfabanimation;

import android.os.Bundle;
import android.support.design.widget.FloatingActionButton;
import android.support.v7.app.AppCompatActivity;
import android.support.v7.widget.LinearLayoutManager;
import android.support.v7.widget.RecyclerView;
import android.support.v7.widget.RecyclerView.ViewHolder;
import android.support.v7.widget.Toolbar;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.view.animation.AccelerateInterpolator;
import android.view.animation.DecelerateInterpolator;
import android.widget.RelativeLayout;
import android.widget.TextView;
import java.util.ArrayList;

public class MainActivity extends AppCompatActivity {
  private static final int THRESHOLD = 20;

  private Toolbar tb;
  private FloatingActionButton fab;
  private RecyclerView rv;
  private boolean isVisiable=true;
  private int distance;

  @Override
  protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);

    rv = (RecyclerView) findViewById(R.id.rv);
    tb = (Toolbar) findViewById(R.id.tb);
    fab = (FloatingActionButton) findViewById(R.id.fab);

    setSupportActionBar(tb);

//    rv.addOnScrollListener(new OnScrollListener() {
//      @Override
//      public void onScrolled(RecyclerView recyclerView, int dx,int dy) {
//        super.onScrolled(recyclerView, dx, dy);
//        Log.d("TAG","dy:"+dy);
//        //dy 垂直方向的，滚动值正，向上滚动，要隐藏
//        if (distance > THRESHOLD && isVisiable) {
//          //dy为正，表示
//          isVisiable = false;
//          hide();
//          distance = 0;
//        } else if (distance<-THRESHOLD&&!isVisiable) {
//        //如果值，小于，并且没有显示，那就显示
//          isVisiable=true;
//          show();
//          distance = 0;
//        }
//
//        //累加滚动距离distance
//        if ((isVisiable&& dy>0)||(!isVisiable&&dy<0)) {
//        distance+=dy;
//        }
//      }
//    });

    rv.setLayoutManager(new LinearLayoutManager(this));

    ArrayList<String> strings = new ArrayList<>();
    for (int i = 0; i < 50; i++) {
      strings.add("item:"+i);
    }
    MyAdapter myAdapter = new MyAdapter(strings);

    rv.setAdapter(myAdapter);
  }

  private void show() {
  //和hide逻辑相反
    tb.animate().translationY(0).setInterpolator(new AccelerateInterpolator(3));

    RelativeLayout.LayoutParams layoutParams= (RelativeLayout.LayoutParams) fab.getLayoutParams();
    fab.animate().translationY(0).setInterpolator(new DecelerateInterpolator(3));
  }

  private void hide() {
    //toolbar，向上移动，自己的高度
    tb.animate().translationY(-tb.getHeight()).setInterpolator(new AccelerateInterpolator(3));

    //fab向下移动，自己的高度和底部的高度
    RelativeLayout.LayoutParams layoutParams = (RelativeLayout.LayoutParams) fab.getLayoutParams();
    fab.animate().translationY(fab.getHeight()+layoutParams.bottomMargin).setInterpolator(new AccelerateInterpolator(3));
  }

  private class MyAdapter extends RecyclerView.Adapter<RecyclerView.ViewHolder>{

    private final ArrayList<String> strings;

    public MyAdapter(ArrayList<String> strings) {
      this.strings=strings;
    }

    @Override
    public ViewHolder onCreateViewHolder(ViewGroup parent, int viewType) {
      return new MyViewHolder(LayoutInflater.from(parent.getContext()).inflate(android.R.layout.simple_list_item_1,parent,false));
    }

    @Override
    public void onBindViewHolder(ViewHolder holder, int position) {

      String s = strings.get(position);
      MyViewHolder holder1= (MyViewHolder) holder;
      holder1.tv.setText(s);
    }

    @Override
    public int getItemCount() {
      return strings.size();
    }

    private class MyViewHolder extends ViewHolder {

      public TextView tv;

      public MyViewHolder(View inflate) {
        super(inflate);
        tv = (TextView) itemView.findViewById(android.R.id.text1);
      }
    }
  }
}

```

```java
package cn.woblog.android.l16mdfabanimation;

import android.content.Context;
import android.support.design.widget.CoordinatorLayout;
import android.support.design.widget.FloatingActionButton;
import android.support.v4.view.ViewCompat;
import android.util.AttributeSet;
import android.view.View;
import android.view.animation.AccelerateInterpolator;
import android.view.animation.DecelerateInterpolator;

/**
 * Created by renpingqing on 2017/3/14.
 */

public class FabBehavior extends FloatingActionButton.Behavior {
  private boolean isVisiable=true;
//  @Override
//  public boolean layoutDependsOn(CoordinatorLayout parent, FloatingActionButton child,
//      View dependency) {
//    return super.layoutDependsOn(parent, child, dependency);
//  }
//
//  @Override
//  public boolean onDependentViewChanged(CoordinatorLayout parent, FloatingActionButton child,
//      View dependency) {
//    return super.onDependentViewChanged(parent, child, dependency);
//  }


  //要重写这两个构造方法，不然崩溃
  public FabBehavior() {
  }

  public FabBehavior(Context context, AttributeSet attrs) {
    super(context, attrs);
  }

  @Override
  public boolean onStartNestedScroll(CoordinatorLayout coordinatorLayout,
      FloatingActionButton child, View directTargetChild, View target, int nestedScrollAxes) {
    //当观察的view滑动的时候，开始滑动，这是RV
    //nestedScrollAxes:滑动关联轴，这里只关心，垂直

    return nestedScrollAxes== ViewCompat.SCROLL_AXIS_VERTICAL || super
        .onStartNestedScroll(coordinatorLayout, child, directTargetChild, target, nestedScrollAxes);
  }

  @Override
  public void onNestedScroll(CoordinatorLayout coordinatorLayout, FloatingActionButton child,
      View target, int dxConsumed, int dyConsumed, int dxUnconsumed, int dyUnconsumed) {
    //滑动的时候
    super.onNestedScroll(coordinatorLayout, child, target, dxConsumed, dyConsumed, dxUnconsumed,
        dyUnconsumed);

    //根据情况执行动画
    if (dyConsumed>0 && isVisiable) {
    //hide
      onHide(child);
      isVisiable=false;
    } else if (dyConsumed<0 && !isVisiable) {

      onShow(child);
      isVisiable=true;
    }
  }

  private void onHide(FloatingActionButton fab) {
    //fab向下移动，自己的高度和底部的高度
    CoordinatorLayout.LayoutParams layoutParams = (CoordinatorLayout.LayoutParams) fab.getLayoutParams();
    fab.animate().translationY(fab.getHeight()+layoutParams.bottomMargin).setInterpolator(new AccelerateInterpolator(3));

//    ViewCompat.animate(fab).scaleX(0f).scaleY(0f).start();;
  }

  private void onShow(FloatingActionButton fab) {
    CoordinatorLayout.LayoutParams layoutParams= (CoordinatorLayout.LayoutParams) fab.getLayoutParams();
    fab.animate().translationY(0).setInterpolator(new DecelerateInterpolator(3));

//    ViewCompat.animate(fab).scaleX(1f).scaleY(1f).start();;
  }
}

```

