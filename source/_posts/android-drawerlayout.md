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

