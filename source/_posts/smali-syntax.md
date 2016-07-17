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

|	语法		|	含义						|
|:---------:|:-------------------------:|
|	V		|	void，只用于返回值类型		|
|	Z		|	boolean					|
|	B 		|	byte					|
|	S 		|	short					|
|	C 		|	char					|
|	I 		|	int						|
|	J		|	long					|
|	F 		| 	flot					|
|	D 		|	double					|
|	L 		|	Java类 类型				|
|	[		|	数组类型					|

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

# vitual methods:虚方法，如：

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

# direct methods:直接方法，如：

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



































