---
title: 全面讲解Android App Widgets之基本使用(一)
date: 2016-5-12 10:05:05
categories: Android
tags: 
    - App Widgets
    - 桌面小插件
---
## 简介

App Widgets他是一个迷你的Application Views他能嵌入到其他应用程序里(例如：桌面)并且它还能接受一个周期性的更新，所有称她为桌面小部件

![](http://7qnc6h.com1.z0.glb.clouddn.com/ez5v229r5wi88141r1przegjpp.png)

可以看到这是一个天气的桌面插件，他上面可以显示时间，日期，天气，同时还有背景，是不是很方便呢，这种部件对新闻类应用，代办事项等这类软件很有帮助，因为我们不需要打开客户端就能获取到信息，同时对于用户是没有时间消耗的，因为他解锁屏幕就看见了，不经意间的~

## 创建一个App Widgets的一般步骤

### AppWidgetProviderInfo

来描述一些Widget的元数据，比如：更新周期，布局，所对应的class灯，是一个xml文件

### AppWidgetProvider

我实现它提供一些的接口，比如：Widget的创建，第一次添加，删除等状态，[他是一个类参考这里](http://developer.android.com/reference/android/appwidget/AppWidgetProvider.html)

### View Layout

这很容易理解啦，就是要显示的布局，你不告诉他，他怎么知道要显示TextView还是ImageView，对吧

### 清单文件配置状态广播

因为AppWidgetProvider实际上是一个receiver，你说要不要配置

可选配置：

我们可以设置一个App Widget的配置Activity，他可以在你启动App Widget时提供一些配置

下面我们来创建一个简单的App Widget

## 布局

这里有个问题就是这里不支持一些输入控件，比如：EditText，它支持的布局有：

FrameLayout
LinearLayout
RelativeLayout
GridLayout

支持的控件有：

AnalogClock
Button
Chronometer
ImageButton
ImageView
ProgressBar
TextView
ViewFlipper
ListView
GridView
StackView
AdapterViewFlipper

同时也支持[ViewStub](http://developer.android.com/reference/android/view/ViewStub.html)

### 添加Widget的margin

通过情况下我们Widget的内容不应该太靠近屏幕的边缘了，所有要设置一个margin，在Android 4.0上他会自动的加上的margin，基于这样的需求，所有我们需要采用如果方法适配这个margin

#### 设置targetSdkVersion为14或者更高

#### 创建一个布局

```xml
<?xml version="1.0" encoding="utf-8"?>
<FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"
             android:layout_width="match_parent"
             android:layout_height="match_parent"
             android:padding="@dimen/widget_margin">

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:background="#f00"
        android:orientation="horizontal">
        <TextView android:layout_width="wrap_content" android:layout_height="wrap_content"
                  android:text="我是一个最基本的Widget"/>
    </LinearLayout>

</FrameLayout>
```

#### 创建尺寸资源

res/values/dimens.xml:
```xml
<dimen name="widget_margin">8dp</dimen>
```

res/values-v14/dimens.xml:
```xml
<dimen name="widget_margin">0dp</dimen>
```

## 使用AppWidgetProvider

这个和使用Activity差不多，如果你要有Activity的一些特性，你既要继承他，这样也是一样的

AppWidgetProvider是一个继承了BroadcastReceiver的类，他用来接受Widget的一些事件，比如：Widget的更新，删除，启用和禁用并回调相应的事件方法

### onUpdate()

这个方法是第一次创建Widget(如果设置配置activity他不调用)和到达我们配置的updatePeriodMillis时间时调用，所以在这我们执行一些基本设置，事件处理，或者创建一个临时的Service

## 创建Widget配置文件

res/xml/basic_widget.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<appwidget-provider xmlns:android="http://schemas.android.com/apk/res/android"
                    android:minWidth="40dp"
                    android:minHeight="40dp"
                    android:updatePeriodMillis="86400000"
                    android:previewImage="@drawable/ic_launcher"
                    android:initialLayout="@layout/layout_basic_widget"
                    android:widgetCategory="home_screen">
</appwidget-provider>
···

其中我们指定了更新的间隔时间，初始化布局，以及预览图片

## 配置BasicWidget

因为它本身是一个BroadcastReceiver，所以和使用普通的BroadcastReceiver没有什么两样，同样需要配置

```xml
<receiver android:name=".BasicWidget" >
    <intent-filter>
        <action android:name="android.appwidget.action.APPWIDGET_UPDATE" />
    </intent-filter>
    <meta-data android:name="android.appwidget.provider"
               android:resource="@xml/basic_widget" />
</receiver>
```

其中android:resource就是我们上面创建的的Widget配置文件

到这时候，我们的Widget基本已经完成了，运行代码到手机，就可以在控件列表找到我们只做的控件，添加到桌面上的效果如下：

![](http://7qnc6h.com1.z0.glb.clouddn.com/82oolrm84vzbmxrsfipyhxzdun.png)

点击其中的按钮是可以打开我们应用主界面的


## Widget尺寸

我们可以在桌面看到很多控件，他们有大小有高有矮，有的甚至还可以在添加的时候动态调整尺寸，那么下面我们就来看看，怎么实现这些功能吧

我看到上面的描述文件里指定了android:minWidth和android:minHeight，必须指定这两个属性，他的最小尺寸是一个格子[更新信息参考这里](http://developer.android.com/guide/practices/ui_guidelines/widget_design.html#anatomy_determining_size)也就是40dp，如果小于这值，他默认就是40dp，其中尺寸的计算公式是70 × n − 30，其中n是暂几格

比如：我要3格，那个尺寸应该为：180dp

minResizeWidth：最小可调整到的尺寸，比如：我最小尺寸是110dp，也就是两格，但是如果设置android:minResizeWidth="40dp"，可以调整最小为一格，用户添加的时候默认是2格，这个用意的设计就是推荐2格的空间，但是要是桌面有点挤，缩成1格也是可以的。如果大于minResizeWidth将忽略

这一篇就到这里，下一篇我们会讲解Widget的高级使用，以及一个使用实例

参考：http://blog.csdn.net/jjwwmlp456/article/details/38466969
http://www.cnblogs.com/devinzhang/archive/2012/01/26/2329790.html
http://developer.android.com/guide/topics/appwidgets/index.html
很详细和官方文档差不多：http://blog.csdn.net/dyllove98/article/details/9199195