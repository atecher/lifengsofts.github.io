---
title: Dex文件格式
date: 2016-07-23 09:21:53
categories: Dalvik
tags: 
    - Dex
---

# 什么是dex文件

他是Android系统的可执行文件，包含应用程序的全部操作指令以及运行时数据。

由于dalvik是一种针对嵌入式设备而特殊设计的java虚拟机，所以dex文件与标准的class文件在结构设计上有着本质的区别

当java程序编译成class后，还需要使用dx工具将所有的class文件整合到一个dex文件，目的是其中各个类能够共享数据，在一定程度上降低了冗余，同时也是文件结构更加经凑，实验表明，dex文件是传统jar文件大小的50%左右

![](http://i.stack.imgur.com/1kLrB.png)

可以看见：
dex将原来class每个文件都有的共有信息合成一体，这样减少了class的冗余

# 数据结构

|   类型  |   含义  |
|:------:|:-------:|
|   u1  |  unit8_t,1字节无符号数 |
|   u2  |  unit16_t,2字节无符号数    |
|   u4  |  unit32_t,4字节无符号数    |
|   u8  |  unit64_t,8字节无符号数    |
|sleb128|  有符号LEB128,可变长度1~5    |
|uleb128|  无符号LEB128,               |
|uleb128p1| 无符号LEB128值加1，          |

其中u1~u8很好理解,(不理解的可以参考这里)[http://blog.csdn.net/zklth/article/details/7978362]，表示1到8个字节的无符号数，后面三个是dex特有的数据类型，更详细的参考：[深入到源码解析leb128数据类型](http://i.woblog.cn/2016/07/23/leb128-format/)
























