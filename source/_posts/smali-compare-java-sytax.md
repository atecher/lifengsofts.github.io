---
title: Smali语法与Java语法的对比
date: 2016-08-05 11:41:27
categories: Dalvik
tags: 
    - smali
---

# smali文件格式

反编译过来的smali文件会依次根据包名放在相应的目录里，普通类，抽象类，接口和内部类都是单独的smali文件

## 文件头

每个文件头前3行描述了当前类的一些信息

```
.class <权限修饰符> [修饰关键字] <类名> #classIdx
.super <父类名> #superclassIdx
.source <源文件名(没有路径)> #sourceFileIdx
```

```
.class public Lcom/example/testsmali/MainActivity;
.super Landroid/app/Activity;
.source "MainActivity.java"
```

如果没有父类，就没有.super这行，混淆后的apk .source有可能就没有值，其实这里面的信息就是Dex中DexClassDef结构中的

加有final修饰符的结构

```
.class public final Lcom/woblog/testsmali/smali/StaticFinalClass;
.super Ljava/lang/Object;
.source "StaticFinalClass.java"
```

## 字段

使用.field 声明

### 实例字段

.field <权限修饰符> [修饰关键字] <字段名>:<字段类型>

### 静态字段

.field <权限修饰符> static [修饰关键字] <字段名>:<字段类型>

可以看到静态的只是多了static修饰关键字

```
# static fields
.field private static name:Ljava/lang/String; = null

.field private static final password:Ljava/lang/String; = "123456"


# instance fields
.field private final age:I

.field private price:Ljava/lang/Integer;
```

`# instance fields`这是baksmali添加的注释

```
private static String name;
private static final String password = "123456";
private final int age = 25;
private Integer price = 888888;
```

## 方法

使用.method指令声明

```
# direct method
.method <权限修饰符> [修饰关键字] <方法原型>
	<.locals>
	[.param]
	[.prologue]
	[.line]

	<代码块>

.end method
```

`# direct methods`是baksmali添加的注释

locals:局部变量数

param：参数

prologue：代码开始

line：源代码行数，混淆了可能没有

```
.method public static append([III)[I
    .locals 4
    .param p0, "array"    # [I
    .param p1, "currentSize"    # I
    .param p2, "element"    # I

    .prologue
    const/4 v3, 0x0

    .line 57
    sget-boolean v1, Landroid/support/v7/content/res/GrowingArrayUtils;->$assertionsDisabled:Z

    if-nez v1, :cond_0

    array-length v1, p0

    if-le p1, v1, :cond_0

    new-instance v1, Ljava/lang/AssertionError;

    invoke-direct {v1}, Ljava/lang/AssertionError;-><init>()V

    throw v1

    .line 59
    :cond_0
    add-int/lit8 v1, p1, 0x1

    array-length v2, p0

    if-le v1, v2, :cond_1

    .line 60
    invoke-static {p1}, Landroid/support/v7/content/res/GrowingArrayUtils;->growSize(I)I

    move-result v1

    new-array v0, v1, [I

    .line 61
    .local v0, "newArray":[I
    invoke-static {p0, v3, v0, v3, p1}, Ljava/lang/System;->arraycopy(Ljava/lang/Object;ILjava/lang/Object;II)V

    .line 62
    move-object p0, v0

    .line 64
    .end local v0    # "newArray":[I
    :cond_1
    aput p2, p0, p1

    .line 65
    return-object p0
.end method
```

```java
public static int[] append(int[] array, int currentSize, int element) {
    assert currentSize <= array.length;

    if (currentSize + 1 > array.length) {
        int[] newArray = new int[growSize(currentSize)];
        System.arraycopy(array, 0, newArray, 0, currentSize);
        array = newArray;
    }
    array[currentSize] = element;
    return array;
}
```

direct methods：直接方法

virtual methods:虚方法

他们的区别是直接方法一般是private，虚方法一般是覆盖，重载，或者实现的接口，抽象类的方法

```
# direct methods
.method public constructor <init>()V
    .locals 1

    .prologue
    .line 3
    invoke-direct {p0}, Ljava/lang/Object;-><init>()V

    .line 6
    const/16 v0, 0x19

    iput v0, p0, Lcn/woblog/testsmali/smali/StaticFinalClass;->age:I

    .line 7
    const v0, 0xd9038

    invoke-static {v0}, Ljava/lang/Integer;->valueOf(I)Ljava/lang/Integer;

    move-result-object v0

    iput-object v0, p0, Lcn/woblog/testsmali/smali/StaticFinalClass;->price:Ljava/lang/Integer;

    return-void
.end method
```

### 抛出异常

如果方法的声明中使用throws关键字抛出异常，就会生成Throws注解

```
# virtual methods
.method public throw1()V
    .locals 1
    .annotation system Ldalvik/annotation/Throws;
        value = {
            Ljava/lang/Exception;
        }
    .end annotation

    .prologue
    .line 5
    new-instance v0, Ljava/lang/Exception;

    invoke-direct {v0}, Ljava/lang/Exception;-><init>()V

    throw v0
.end method

.method public throw2()V
    .locals 1

    .prologue
    .line 9
    new-instance v0, Ljava/lang/RuntimeException;

    invoke-direct {v0}, Ljava/lang/RuntimeException;-><init>()V

    throw v0
.end method
```

```
public class ThrowClass {
    public void throw1() throws Exception {
        throw new Exception();
    }

    public void throw2() {
        throw new RuntimeException();
    }
}
```

## 类实现了接口

```
# interfcase
.implements <接口名>
```

```
# interfaces
.implements Lcn/woblog/testsmali/ICallback; #来着interfacesOff指定的结构体中的值
.implements Lcn/woblog/testsmali/ICallbackTwo;
```

```java
public class Callback implements ICallback,ICallbackTwo {
    @Override
    public void onSuccess() {

    }

    @Override
    public void success() {

    }
}
```

## 注解

注解可以作用到类，方法和字段，但他们的表现形式是不一样的

### 类

类的注解是直接添加到smali文件上面的

```
# annotations <注解属性> <注解类名>
	[注解字段=值]
.end annotation
```

```
# annotations
.annotation runtime Lcn/woblog/testsmali/smali/MyClassAnnotation;
    otherName = "otherName"
.end annotation

.annotation runtime Lcn/woblog/testsmali/smali/MyClassAnnotationTwo;
    value = "value"
.end annotation
```

```java
@MyClassAnnotation(otherName = "otherName")
@MyClassAnnotationTwo("value")
//@MyClassAnnotationTwo(value = "value")
public class Callback{
  
}
```

### 字段

如果注解在字段上，他会被包含在field里面

```
.field <权限修饰符> static [修饰关键字] <字段名>:<字段类型>
	# annotations <注解属性> <注解类名>
		[注解字段=值]
	.end annotation
..end field
```

```
# instance fields
.field private name:Ljava/lang/String;
    .annotation runtime Lcn/woblog/testsmali/smali/MyFiledAnnotation;
        report = false
        tag = "tag1"
    .end annotation
.end field

.field private password:Ljava/lang/String;
    .annotation runtime Lcn/woblog/testsmali/smali/MyFiledAnnotation;
        report = true
    .end annotation
.end field

.field private vip:Z
    .annotation runtime Lcn/woblog/testsmali/smali/MyFiledAnnotation;
        report = false
    .end annotation
.end field
```

```java
//字段注解
@MyFiledAnnotation(tag = "tag1",report = false)
private String name;

@MyFiledAnnotation(report = true)
private String password;

@MyFiledAnnotation(report = false)
private boolean vip;
```

## 类

```
.class public Lcn/woblog/testsmali/Callback;
.super Ljava/lang/Object;
.source "Callback.java"
```

```
package cn.woblog.testsmali.smali;

public final class StaticFinalClass {

}
```

## 内部类

内部类可分为，内部类，静态嵌套类，方法内部类，匿名内部类，他为每个内部类生成一个独立的文件，格式为：[外部类]$[内部类].smali

```
package cn.woblog.testsmali.smali;

import android.util.Log;

public class OuterClass {
    //内部类
    class Inner {
        class Inner1 {
            public void main() {
                Inner inner = new Inner();
                inner.run();
            }
        }

        public void run() {
            Log.d("TAG", "run");
        }
    }

    //静态内部类
    public static class InnerStatic {
        public void main() {
            new Thread() {
                @Override
                public void run() {
                    super.run();
                    Log.d("TAG", "static run");
                }
            }.start();
        }
    }


}
```

上述代码会生成下面这些smali文件

```shell
OuterClass$Inner$Inner1.smali
OuterClass$Inner.smali
OuterClass$InnerStatic$1.smali
OuterClass$InnerStatic.smali
OuterClass.smali
```

可以看见内部类是以$符号分隔每个类的，匿名内部类会依次生成$1~这样的格式

OuterClass.smali

```
.class public Lcn/woblog/testsmali/smali/OuterClass;
.super Ljava/lang/Object;
.source "OuterClass.java"


# annotations
.annotation system Ldalvik/annotation/MemberClasses;
    value = {
        Lcn/woblog/testsmali/smali/OuterClass$InnerStatic;,
        Lcn/woblog/testsmali/smali/OuterClass$Inner;
    }
.end annotation


# direct methods
.method public constructor <init>()V
    .locals 0

    .prologue
    .line 5
    invoke-direct {p0}, Ljava/lang/Object;-><init>()V

    return-void
.end method
```

可以看见如果一个类中有定义内部类，那么会有MemberClasses的注解，他的value是一个列表，里面是每一个类名

OuterClass$Inner.smali

```
.class Lcn/woblog/testsmali/smali/OuterClass$Inner;
.super Ljava/lang/Object;
.source "OuterClass.java"


# annotations
.annotation system Ldalvik/annotation/EnclosingClass;
    value = Lcn/woblog/testsmali/smali/OuterClass;
.end annotation

.annotation system Ldalvik/annotation/InnerClass;
    accessFlags = 0x0
    name = "Inner"
.end annotation

.annotation system Ldalvik/annotation/MemberClasses;
    value = {
        Lcn/woblog/testsmali/smali/OuterClass$Inner$Inner1;
    }
.end annotation


# instance fields
.field final synthetic this$0:Lcn/woblog/testsmali/smali/OuterClass;


# direct methods
.method constructor <init>(Lcn/woblog/testsmali/smali/OuterClass;)V
    .locals 0
    .param p1, "this$0"    # Lcn/woblog/testsmali/smali/OuterClass;

    .prologue
    .line 7
    iput-object p1, p0, Lcn/woblog/testsmali/smali/OuterClass$Inner;->this$0:Lcn/woblog/testsmali/smali/OuterClass;

    invoke-direct {p0}, Ljava/lang/Object;-><init>()V

    return-void
.end method


# virtual methods
.method public run()V
    .locals 2

    .prologue
    .line 16
    const-string v0, "TAG"

    const-string v1, "run"

    invoke-static {v0, v1}, Landroid/util/Log;->d(Ljava/lang/String;Ljava/lang/String;)I

    .line 17
    return-void
.end method
```

如果是一个内部类，他有两个注解EnclosingClass，InnerClass

EnclosingClass：里面的值为父类类名

InnerClass：定义了内部类一些信息

​	accessFlags = 0x0：访问修饰符
  	name = "Inner"：内部类类名，如果是匿名内部类他为name = null

还有一个synthetic修饰的this$0实例字段，是外部类的引用，0表示引用层数

```
public class OuterClass { //this$0
    class Inner { //this$1
        class Inner1 {
            public void main() {
                Inner inner = new Inner();
                inner.run();
            }
        }
    }
}
```

synthetic表示合成的，表示不是我们自己写的，而是编译器生成的，下面我们来看看内部类的初始化过程

首先他的init方法有两个参数，第一个p0是this,p1是外部类的应用，传递进来赋值给this$0，然后在调用父类的初始化方法

OuterClass$Inner$Inner1.smali

```
.class Lcn/woblog/testsmali/smali/OuterClass$Inner$Inner1;
.super Ljava/lang/Object;
.source "OuterClass.java"


# annotations
.annotation system Ldalvik/annotation/EnclosingClass;
    value = Lcn/woblog/testsmali/smali/OuterClass$Inner;
.end annotation

.annotation system Ldalvik/annotation/InnerClass;
    accessFlags = 0x0
    name = "Inner1"
.end annotation


# instance fields
.field final synthetic this$1:Lcn/woblog/testsmali/smali/OuterClass$Inner;


# direct methods
.method constructor <init>(Lcn/woblog/testsmali/smali/OuterClass$Inner;)V
    .locals 0
    .param p1, "this$1"    # Lcn/woblog/testsmali/smali/OuterClass$Inner;

    .prologue
    .line 8
    iput-object p1, p0, Lcn/woblog/testsmali/smali/OuterClass$Inner$Inner1;->this$1:Lcn/woblog/testsmali/smali/OuterClass$Inner;

    invoke-direct {p0}, Ljava/lang/Object;-><init>()V

    return-void
.end method


# virtual methods
.method public main()V
    .locals 2

    .prologue
    .line 10
    new-instance v0, Lcn/woblog/testsmali/smali/OuterClass$Inner;

    iget-object v1, p0, Lcn/woblog/testsmali/smali/OuterClass$Inner$Inner1;->this$1:Lcn/woblog/testsmali/smali/OuterClass$Inner;

    iget-object v1, v1, Lcn/woblog/testsmali/smali/OuterClass$Inner;->this$0:Lcn/woblog/testsmali/smali/OuterClass;

    invoke-direct {v0, v1}, Lcn/woblog/testsmali/smali/OuterClass$Inner;-><init>(Lcn/woblog/testsmali/smali/OuterClass;)V

    .line 11
    .local v0, "inner":Lcn/woblog/testsmali/smali/OuterClass$Inner;
    invoke-virtual {v0}, Lcn/woblog/testsmali/smali/OuterClass$Inner;->run()V

    .line 12
    return-void
.end method
```

OuterClass$InnerStatic$1.smali

```
.class Lcn/woblog/testsmali/smali/OuterClass$InnerStatic$1;
.super Ljava/lang/Thread;
.source "OuterClass.java"


# annotations
.annotation system Ldalvik/annotation/EnclosingMethod;
    value = Lcn/woblog/testsmali/smali/OuterClass$InnerStatic;->main()V
.end annotation

.annotation system Ldalvik/annotation/InnerClass;
    accessFlags = 0x0
    name = null
.end annotation


# instance fields
.field final synthetic this$0:Lcn/woblog/testsmali/smali/OuterClass$InnerStatic;


# direct methods
.method constructor <init>(Lcn/woblog/testsmali/smali/OuterClass$InnerStatic;)V
    .locals 0
    .param p1, "this$0"    # Lcn/woblog/testsmali/smali/OuterClass$InnerStatic;

    .prologue
    .line 23
    iput-object p1, p0, Lcn/woblog/testsmali/smali/OuterClass$InnerStatic$1;->this$0:Lcn/woblog/testsmali/smali/OuterClass$InnerStatic;

    invoke-direct {p0}, Ljava/lang/Thread;-><init>()V

    return-void
.end method


# virtual methods
.method public run()V
    .locals 2

    .prologue
    .line 26
    invoke-super {p0}, Ljava/lang/Thread;->run()V

    .line 27
    const-string v0, "TAG"

    const-string v1, "static run"

    invoke-static {v0, v1}, Landroid/util/Log;->d(Ljava/lang/String;Ljava/lang/String;)I

    .line 28
    return-void
.end method
```

## 监听器

```
const v2, 0x7f0b0054

invoke-virtual {p0, v2}, Lcn/woblog/testsmali/MainActivity;->findViewById(I)Landroid/view/View;

move-result-object v0

check-cast v0, Landroid/widget/Button;

.line 37
.local v0, "bt1":Landroid/widget/Button;
new-instance v2, Lcn/woblog/testsmali/MainActivity$1; //创建匿名监听器对象

invoke-direct {v2, p0}, Lcn/woblog/testsmali/MainActivity$1;-><init>(Lcn/woblog/testsmali/MainActivity;)V

invoke-virtual {v0, v2}, Landroid/widget/Button;->setOnClickListener(Landroid/view/View$OnClickListener;)V //设置匿名监听器

.line 44
const v2, 0x7f0b0055

invoke-virtual {p0, v2}, Lcn/woblog/testsmali/MainActivity;->findViewById(I)Landroid/view/View;

move-result-object v1

check-cast v1, Landroid/widget/Button;

.line 45
.local v1, "bt2":Landroid/widget/Button;
invoke-virtual {v1, p0}, Landroid/widget/Button;->setOnClickListener(Landroid/view/View$OnClickListener;)V //设置类监听器
```

MainActivity$1.smali

匿名监听器

```
.class Lcn/woblog/testsmali/MainActivity$1;
.super Ljava/lang/Object;
.source "MainActivity.java"

# interfaces
.implements Landroid/view/View$OnClickListener;


# annotations
.annotation system Ldalvik/annotation/EnclosingMethod;
    value = Lcn/woblog/testsmali/MainActivity;->testListener()V
.end annotation

.annotation system Ldalvik/annotation/InnerClass;
    accessFlags = 0x0
    name = null
.end annotation


# instance fields
.field final synthetic this$0:Lcn/woblog/testsmali/MainActivity;


# direct methods
.method constructor <init>(Lcn/woblog/testsmali/MainActivity;)V
    .locals 0
    .param p1, "this$0"    # Lcn/woblog/testsmali/MainActivity;

    .prologue
    .line 37
    iput-object p1, p0, Lcn/woblog/testsmali/MainActivity$1;->this$0:Lcn/woblog/testsmali/MainActivity;

    invoke-direct {p0}, Ljava/lang/Object;-><init>()V

    return-void
.end method


# virtual methods
.method public onClick(Landroid/view/View;)V
    .locals 2
    .param p1, "view"    # Landroid/view/View;

    .prologue
    .line 40
    const-string v0, "TAG"

    const-string v1, "onClick"

    invoke-static {v0, v1}, Landroid/util/Log;->d(Ljava/lang/String;Ljava/lang/String;)I

    .line 41
    return-void
.end method

```

类监听器

首先类要实现接口

```
# interfaces
.implements Landroid/view/View$OnClickListener;
```

并实现OnClickListener的方法

```
.method public onClick(Landroid/view/View;)V
    .locals 2
    .param p1, "view"    # Landroid/view/View;

    .prologue
    .line 383
    const-string v0, "TAG"

    const-string v1, "onClick1"

    invoke-static {v0, v1}, Landroid/util/Log;->d(Ljava/lang/String;Ljava/lang/String;)I

    .line 384
    return-void
.end method
```

```
Button bt1 = (Button) findViewById(R.id.bt1);
bt1.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View view) {
        Log.d("TAG", "onClick");
    }
});

Button bt2 = (Button) findViewById(R.id.bt2);
bt2.setOnClickListener(this);
```

## for

```
Iterator<对象> <对象名> = <方法返回一个对象列表>;
for (<对象> <对象名>:<对象列表>) {
	[code]
}
```

```
Iterator<对象> <对象名> = <方法返回一个对象列表>;
while(<对象名>.hasNext()) {
	<对象> <对象名> = <对象名>.next();
	[code]
}
```

```
public class Loop {

    public void for1(){
        ArrayList<String> strings = new ArrayList<>();
        strings.add("a");
        strings.add("b");
        strings.add("c");
        strings.add("d");

        for (String s:strings) {
            Log.d("TAG",s);
        }
    }
    
    public void for2(){
        ArrayList<String> strings = new ArrayList<>();
        strings.add("a");
        strings.add("b");
        strings.add("c");
        strings.add("d");

        for (int i = 0; i < strings.size(); i++) {
            Log.d("TAG",strings.get(i));
        }
    }

    public void while1(){
        ArrayList<String> strings = new ArrayList<>();
        strings.add("a");
        strings.add("b");
        strings.add("c");
        strings.add("d");


        Iterator<String> iterator = strings.iterator();
        while (iterator.hasNext()) {
            Log.d("TAG",iterator.next());
        }
    }
}
```

```
.class public Lcn/woblog/testsmali/smali/Loop;
.super Ljava/lang/Object;
.source "Loop.java"


# direct methods
.method public constructor <init>()V
    .locals 0

    .prologue
    .line 8
    invoke-direct {p0}, Ljava/lang/Object;-><init>()V

    return-void
.end method


# virtual methods
.method public for1()V
    .locals 4

    .prologue
    .line 11
    new-instance v1, Ljava/util/ArrayList;

    invoke-direct {v1}, Ljava/util/ArrayList;-><init>()V

    .line 12
    .local v1, "strings":Ljava/util/ArrayList;, "Ljava/util/ArrayList<Ljava/lang/String;>;"
    const-string v2, "a"

    invoke-virtual {v1, v2}, Ljava/util/ArrayList;->add(Ljava/lang/Object;)Z

    .line 13
    const-string v2, "b"

    invoke-virtual {v1, v2}, Ljava/util/ArrayList;->add(Ljava/lang/Object;)Z

    .line 14
    const-string v2, "c"

    invoke-virtual {v1, v2}, Ljava/util/ArrayList;->add(Ljava/lang/Object;)Z

    .line 15
    const-string v2, "d"

    invoke-virtual {v1, v2}, Ljava/util/ArrayList;->add(Ljava/lang/Object;)Z

    .line 17
    invoke-virtual {v1}, Ljava/util/ArrayList;->iterator()Ljava/util/Iterator;

    move-result-object v2

    :goto_0
    invoke-interface {v2}, Ljava/util/Iterator;->hasNext()Z

    move-result v3

    if-eqz v3, :cond_0

    invoke-interface {v2}, Ljava/util/Iterator;->next()Ljava/lang/Object;

    move-result-object v0

    check-cast v0, Ljava/lang/String;

    .line 18
    .local v0, "s":Ljava/lang/String;
    const-string v3, "TAG"

    invoke-static {v3, v0}, Landroid/util/Log;->d(Ljava/lang/String;Ljava/lang/String;)I

    goto :goto_0

    .line 20
    .end local v0    # "s":Ljava/lang/String;
    :cond_0
    return-void
.end method

.method public for2()V
    .locals 4

    .prologue
    .line 23
    new-instance v1, Ljava/util/ArrayList;

    invoke-direct {v1}, Ljava/util/ArrayList;-><init>()V

    .line 24
    .local v1, "strings":Ljava/util/ArrayList;, "Ljava/util/ArrayList<Ljava/lang/String;>;"
    const-string v2, "a"

    invoke-virtual {v1, v2}, Ljava/util/ArrayList;->add(Ljava/lang/Object;)Z

    .line 25
    const-string v2, "b"

    invoke-virtual {v1, v2}, Ljava/util/ArrayList;->add(Ljava/lang/Object;)Z

    .line 26
    const-string v2, "c"

    invoke-virtual {v1, v2}, Ljava/util/ArrayList;->add(Ljava/lang/Object;)Z

    .line 27
    const-string v2, "d"

    invoke-virtual {v1, v2}, Ljava/util/ArrayList;->add(Ljava/lang/Object;)Z

    .line 29
    const/4 v0, 0x0

    .local v0, "i":I
    :goto_0
    invoke-virtual {v1}, Ljava/util/ArrayList;->size()I

    move-result v2

    if-ge v0, v2, :cond_0

    .line 30
    const-string v3, "TAG"

    invoke-virtual {v1, v0}, Ljava/util/ArrayList;->get(I)Ljava/lang/Object;

    move-result-object v2

    check-cast v2, Ljava/lang/String;

    invoke-static {v3, v2}, Landroid/util/Log;->d(Ljava/lang/String;Ljava/lang/String;)I

    .line 29
    add-int/lit8 v0, v0, 0x1

    goto :goto_0

    .line 32
    :cond_0
    return-void
.end method

.method public while1()V
    .locals 4

    .prologue
    .line 35
    new-instance v1, Ljava/util/ArrayList;

    invoke-direct {v1}, Ljava/util/ArrayList;-><init>()V

    .line 36
    .local v1, "strings":Ljava/util/ArrayList;, "Ljava/util/ArrayList<Ljava/lang/String;>;"
    const-string v2, "a"

    invoke-virtual {v1, v2}, Ljava/util/ArrayList;->add(Ljava/lang/Object;)Z

    .line 37
    const-string v2, "b"

    invoke-virtual {v1, v2}, Ljava/util/ArrayList;->add(Ljava/lang/Object;)Z

    .line 38
    const-string v2, "c"

    invoke-virtual {v1, v2}, Ljava/util/ArrayList;->add(Ljava/lang/Object;)Z

    .line 39
    const-string v2, "d"

    invoke-virtual {v1, v2}, Ljava/util/ArrayList;->add(Ljava/lang/Object;)Z

    .line 42
    invoke-virtual {v1}, Ljava/util/ArrayList;->iterator()Ljava/util/Iterator;

    move-result-object v0

    .line 43
    .local v0, "iterator":Ljava/util/Iterator;, "Ljava/util/Iterator<Ljava/lang/String;>;"
    :goto_0
    invoke-interface {v0}, Ljava/util/Iterator;->hasNext()Z

    move-result v2

    if-eqz v2, :cond_0

    .line 44
    const-string v3, "TAG"

    invoke-interface {v0}, Ljava/util/Iterator;->next()Ljava/lang/Object;

    move-result-object v2

    check-cast v2, Ljava/lang/String;

    invoke-static {v3, v2}, Landroid/util/Log;->d(Ljava/lang/String;Ljava/lang/String;)I

    goto :goto_0

    .line 46
    :cond_0
    return-void
.end method

```















