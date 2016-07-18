---
title: Smali语法
date: 2016-07-17 11:23:12
categories: Dalvik
tags: 
    - Dalvik
    - Android
    - Smali
---

# 数据类型

Dalvik字节码只有两种格式：基本类型和引用类型。对象和数组属于引用类型

|   语法      |   含义                      |
|:---------:|:-------------------------:|
|   V       |   void，只用于返回值类型       |
|   Z       |   boolean                 |
|   B       |   byte                    |
|   S       |   short                   |
|   C       |   char                    |
|   I       |   int                     |
|   J       |   long                    |
|   F       |   flot                    |
|   D       |   double                  |
|   L       |   Java类 类型                |
|   [       |   数组类型                    |

Ljava/lang/String; 相当于java.lang.String
[I 相当于一维int数组，int[]
[[I 相当于int[][]

# 方法

它使用方法名，参数类型和返回值来描述一个方法
package/name/ObjectName;->methodName(III)Z

package/name/ObjectName:一个类
methodName：方法名
III：参数类型
Z：返回值

(III)Z：方法签名


BakSmali生成的方法代码以.method指令开始，以.end method指令结束，根据方法的类型不同，可以会在方法前加#表示方法类型

\# vitual methods:虚方法，如：

```smali
# virtual methods
.method public get(Ljava/lang/String;)Lcn/woblog/markdowndiary/domain/Note;
    .locals 2
    .param p1, "noteId"    # Ljava/lang/String;

    .prologue
    .line 50
    iget-object v0, p0, Lcn/woblog/markdowndiary/repository/LocalNoteRepository;->orm:Lcom/litesuits/orm/LiteOrm;

    const-class v1, Lcn/woblog/markdowndiary/domain/Note;

    invoke-virtual {v0, p1, v1}, Lcom/litesuits/orm/LiteOrm;->queryById(Ljava/lang/String;Ljava/lang/Class;)Ljava/lang/Object;

    move-result-object v0

    check-cast v0, Lcn/woblog/markdowndiary/domain/Note;

    return-object v0
.end method
```

\# direct methods:直接方法，如：

```smali
# direct methods
.method public constructor <init>(Landroid/content/Context;)V
    .locals 2
    .param p1, "context"    # Landroid/content/Context;

    .prologue
    .line 22
    invoke-direct {p0}, Ljava/lang/Object;-><init>()V

    .line 23
    iput-object p1, p0, Lcn/woblog/markdowndiary/repository/LocalNoteRepository;->context:Landroid/content/Context;

    .line 24
    const-string v0, "note.db"

    invoke-static {p1, v0}, Lcom/litesuits/orm/LiteOrm;->newSingleInstance(Landroid/content/Context;Ljava/lang/String;)Lcom/litesuits/orm/LiteOrm;

    move-result-object v0

    iput-object v0, p0, Lcn/woblog/markdowndiary/repository/LocalNoteRepository;->orm:Lcom/litesuits/orm/LiteOrm;

    .line 25
    iget-object v0, p0, Lcn/woblog/markdowndiary/repository/LocalNoteRepository;->orm:Lcom/litesuits/orm/LiteOrm;

    const/4 v1, 0x1

    invoke-virtual {v0, v1}, Lcom/litesuits/orm/LiteOrm;->setDebugged(Z)V

    .line 26
    return-void
.end method
```

有些方法没有这样的注释

```smali
.method public save(Lcn/woblog/markdowndiary/domain/Note;)V
    .locals 1
    .param p1, "note"    # Lcn/woblog/markdowndiary/domain/Note;

    .prologue
    .line 37
    iget-object v0, p0, Lcn/woblog/markdowndiary/repository/LocalNoteRepository;->orm:Lcom/litesuits/orm/LiteOrm;

    invoke-virtual {v0, p1}, Lcom/litesuits/orm/LiteOrm;->save(Ljava/lang/Object;)J

    .line 38
    return-void
.end method
```

静态方法：

```smali
.method public static formatTime(J)Ljava/lang/String;
    .locals 4
    .param p0, "date"    # J

    .prologue
    .line 11
    new-instance v0, Ljava/text/SimpleDateFormat;

    const-string v1, "yyyy\u5e74MM\u6708dd\u65e5 EEEE"

    sget-object v2, Ljava/util/Locale;->CHINESE:Ljava/util/Locale;

    invoke-direct {v0, v1, v2}, Ljava/text/SimpleDateFormat;-><init>(Ljava/lang/String;Ljava/util/Locale;)V

    .line 13
    .local v0, "simpleDateFormat":Ljava/text/SimpleDateFormat;
    invoke-static {p0, p1}, Ljava/lang/Long;->valueOf(J)Ljava/lang/Long;

    move-result-object v1

    invoke-virtual {v0, v1}, Ljava/text/SimpleDateFormat;->format(Ljava/lang/Object;)Ljava/lang/String;

    move-result-object v1

    return-object v1
.end method
```

# 字段

与方法表示很相似，只是字段没有方法签名和返回值，取而代之的是字段类型
Lpackage/name/ObjectName;->FiedlName:Ljava/lang/String;

其中字段名与字段类型用冒号“:”分割

```smali
# static fields
.field private static instance:Lcn/woblog/markdowndiary/repository/LocalNoteRepository;


# instance fields
.field private final context:Landroid/content/Context;
```

其中：
\# static fields：静态字段
\# instance fields：实例字段


# Dalvik指令集

他在调用格式上模仿了C语言的调用约定，[官方地址](https://source.android.com/devices/tech/dalvik/dalvik-bytecode.html),指令语法与助词有如下特点：

1. 采用采用从目标(destination)到源(source)的方法
2. 根据字节码的大小与类型不同，一些字节码添加了名称后缀已消除歧义
2.1 32位常规类型的字节码未添加任何后缀
2.2 64位常规类型的字节码添加 -wide后缀
3.3 特殊类型的字节码根据具体类型添加后缀，-boolean,-byte,-char,-short,-int,-long,-float,-double,-object,-string,-class,-void之一
3. 根据字节码的布局和选项不同，一些字节码添加了字节后缀消除歧义，后缀与字节码直接用/分割
4. 在指令集的描述中，宽度值中每个字母表示宽度为4位

如：
move-wide/from16 vAA, vBBBB
move-wide/from16 v18, v0

move:基础字节码(base opcode)，标示是基本操作
wide:标示指令操作的数据宽度为64位宽度
from16:字节码后缀(opcode suffix),标示源(vBBBB)为一个16的寄存器引用变量
vAA:目的寄存器，v0~v255
vBBBB:源寄存器，v0~v65535

# 方法调用

在方法调用者我们可以看到有：

```smali
invoke-super {p0, p1}, Lcom/woblog/testsmali/BaseActivity;->onCreate(Landroid/os/Bundle;)V

invoke-virtual {p0, v0}, Lcom/woblog/testsmali/MainActivity;->setContentView(I)V

invoke-direct {p0}, Lcom/woblog/testsmali/MainActivity;->initMove()V

invoke-static {}, Lcom/woblog/testsmali/TimeUtil;->getCurrentTime()J

invoke-interface {v0}, Lcom/woblog/testsmali/ICallback;->onSuccess()V
```

# 指令

## nop

空操作，被用来做对齐代码

## 数据操作指令

move destination, source
根据字节码大小和类型不同，后面回天津不同的后缀
move vA, vB：vB寄存器值赋值给vA寄存器，都为4位
move-object vA,vB
move-result vAA：将上一个invoke类型的指令操作的单字非对象结果负责vAA寄存器
move-result-object vAA：将上一个invoke类型指令操作的对象赋值给vAA
move-exception vAA:保存一个运行时发生的异常vAA寄存器，必须是异常发生时的异常处理的第一条指令


```java
private void testMove() {
    int a = 100;
    long b = 100000000000000000L;

    int c = a;
    long d = b;

    Log.d(TAG,c+"");
    Log.d(TAG,d+"");


    int e = getIntResult();
    Log.d(TAG,e+"");

    try {
        int f = e/c;
    } catch (ArithmeticException e1) {
        e1.printStackTrace();
    }catch (Exception e1) {
        e1.printStackTrace();
    }finally {

    }
}
```

```smali

//move-result-object
invoke-direct {v7}, Ljava/lang/StringBuilder;-><init>()V

invoke-virtual {v7, v1}, Ljava/lang/StringBuilder;->append(I)Ljava/lang/StringBuilder;

move-result-object v7

const-string v8, ""

invoke-virtual {v7, v8}, Ljava/lang/StringBuilder;->append(Ljava/lang/String;)Ljava/lang/StringBuilder;

move-result-object v7

//move-result
invoke-direct {p0}, Lcom/woblog/testsmali/MainActivity;->getIntResult()I

move-result v6

//move exception
.line 35
:try_start_0
div-int v8, v6, v1
:try_end_0
.catch Ljava/lang/ArithmeticException; {:try_start_0 .. :try_end_0} :catch_0
.catch Ljava/lang/Exception; {:try_start_0 .. :try_end_0} :catch_1
.catchall {:try_start_0 .. :try_end_0} :catchall_0

.line 43
:goto_0
return-void

.line 36
:catch_0
move-exception v7

.line 37
.local v7, "e1":Ljava/lang/ArithmeticException;
:try_start_1
invoke-virtual {v7}, Ljava/lang/ArithmeticException;->printStackTrace()V
:try_end_1
.catchall {:try_start_1 .. :try_end_1} :catchall_0

goto :goto_0

.line 40
.end local v7    # "e1":Ljava/lang/ArithmeticException;
:catchall_0
move-exception v8

throw v8

.line 38
:catch_1
move-exception v7

.line 39
.local v7, "e1":Ljava/lang/Exception;
:try_start_2
invoke-virtual {v7}, Ljava/lang/Exception;->printStackTrace()V
:try_end_2
.catchall {:try_start_2 .. :try_end_2} :catchall_0

goto :goto_0

```

## 返回指令
return-void :返回一个void
return vAA:返回一个32位非对象类型的值，返回寄存器为8位
return-wide vAA：返回一个64位非对象类型的值，返回寄存器为8位
return-object vAA:返回一个对象类型

```java
private String returnObject() {
    return new String("");
}

private float returnFloat() {
    return 12333334.00234345F;
}

private double returnDouble() {
    return 3425465767.9345865;
}

private long returnLong() {
    return 12445657999999L;
}

private int returnInt() {
    return 1024;
}

private void returnVoid() {
    int a = 3;
}
```

```smali
.method private returnDouble()D
    .locals 2

    .prologue
    .line 40
    const-wide v0, 0x41e9858eb4fde822L    # 3.4254657679345865E9

    return-wide v0
.end method

.method private returnFloat()F
    .locals 1

    .prologue
    .line 36
    const v0, 0x4b3c3116    # 1.2333334E7f

    return v0
.end method

.method private returnInt()I
    .locals 1

    .prologue
    .line 48
    const/16 v0, 0x400

    return v0
.end method

.method private returnLong()J
    .locals 2

    .prologue
    .line 44
    const-wide v0, 0xb51bb062a7fL

    return-wide v0
.end method

.method private returnObject()Ljava/lang/String;
    .locals 2

    .prologue
    .line 32
    new-instance v0, Ljava/lang/String;

    const-string v1, ""

    invoke-direct {v0, v1}, Ljava/lang/String;-><init>(Ljava/lang/String;)V

    return-object v0
.end method

.method private returnVoid()V
    .locals 1

    .prologue
    .line 52
    const/4 v0, 0x3

    .line 53
    .local v0, "a":I
    return-void
.end method
```

## 数据定义

用来定义程序中用到的常量，字符串，类等数据
const/4 vA, #+B :将数组扩展为32位后赋给寄存器vA
const/16 vAA, #+BBBB
const vAA, #+BBBBBBBB：将数组赋值给寄存器vAA
const-wide/16 vAA, #+BBBBB ：将数值扩展为64位后赋给寄存器vAA
const-string vAA, string@BBBB：将字符串索引构造一个字符串并赋给vAA
const-class vAA, type@BBBB:通过类型索引获取一个类的引用并赋给寄存器vAA


```java
private void testConst() {
    int a = 1;
    int b = 7;
    int c = 254;
    int d = 2345;
    int d1 = 65538;

    long e = 12435465657677L;
    float f = 123235409234.09097945F;
    double g = 111343333454999999999.912384375;
}
```

```smali
//小于255用4，大于255小于等于65535用16
const/4 v0, 0x1

.line 25
.local v0, "a":I
const/4 v1, 0x7

.line 26
.local v1, "b":I
const/16 v2, 0xfe

.line 27
.local v2, "c":I
const/16 v3, 0x929

.line 28
.local v3, "d":I
const v4, 0x10002 //65538，大于65535用const v4

//long用const-wide
.line 30
.local v4, "d1":I
const-wide v6, 0xb4f5b835d4dL

.line 31
.local v6, "e":J
const v5, 0x51e58b39

.line 32
.local v5, "f":F
const-wide v8, 0x441824cbef6b9491L    # 1.11343333455E20
```

## 锁指令

锁指令多用在多线程程序中对同一对象的操作
monitor-enter vAA 为指定的对象获取锁
monitor-exit vAA 释放指定的对象的锁

```java
private void callSynchronizeClassMethod() {
    synchronized (MainActivity.class) {
        Log.d("TAG","synchronized class");
    }
}

private void callSynchronizeMethod() {
    synchronized (this) {
        Log.d("TAG","synchronized this");
    }
}

private synchronized void callLockMethod() {
    Log.d("TAG","synchronized method");
}
```

```smali
.method private declared-synchronized callLockMethod()V
    .locals 2

    .prologue
    .line 43
    monitor-enter p0

    :try_start_0
    const-string v0, "TAG"

    const-string v1, "synchronized method"

    invoke-static {v0, v1}, Landroid/util/Log;->d(Ljava/lang/String;Ljava/lang/String;)I
    :try_end_0
    .catchall {:try_start_0 .. :try_end_0} :catchall_0

    .line 44
    monitor-exit p0

    return-void

    .line 43
    :catchall_0
    move-exception v0

    monitor-exit p0

    throw v0
.end method

.method private callSynchronizeClassMethod()V
    .locals 3

    .prologue
    .line 31
    const-class v1, Lcom/woblog/testsmali/MainActivity;

    monitor-enter v1

    .line 32
    :try_start_0
    const-string v0, "TAG"

    const-string v2, "synchronized class"

    invoke-static {v0, v2}, Landroid/util/Log;->d(Ljava/lang/String;Ljava/lang/String;)I

    .line 33
    monitor-exit v1

    .line 34
    return-void

    .line 33
    :catchall_0
    move-exception v0

    monitor-exit v1
    :try_end_0
    .catchall {:try_start_0 .. :try_end_0} :catchall_0

    throw v0
.end method

.method private callSynchronizeMethod()V
    .locals 2

    .prologue
    .line 37
    monitor-enter p0

    .line 38
    :try_start_0
    const-string v0, "TAG"

    const-string v1, "synchronized this"

    invoke-static {v0, v1}, Landroid/util/Log;->d(Ljava/lang/String;Ljava/lang/String;)I

    .line 39
    monitor-exit p0

    .line 40
    return-void

    .line 39
    :catchall_0
    move-exception v0

    monitor-exit p0
    :try_end_0
    .catchall {:try_start_0 .. :try_end_0} :catchall_0

    throw v0
.end method
```


















































