---
title: 全方位动态调试Apk
date: 2016-08-19 11:20:54
categories: Android
tags: 
    - 调试APk
    -  debug
---

# 软件调试分类

## 源码调试

多用于软件开发阶段，我们可以拿到软件源码，可以通过集成开发环境(Eclipse,Android Studio)来跟踪软件的变量等

## 汇编级调试

他通常用在逆向工程，分析人员通常拿不到源码，所以只能跟踪栈，分析目标文件的汇编代码和查看寄存器的值，这种方式调试显然没有源码调试那个直观，但是动态调试通用能够跟踪软件的执行流程。通常用在静态分析很难取得突破时，就只能上动态调试了

# Android对动态调试的支持

我们都知道android调试分为java代码的调试和ndk编译的代码调试，java程序使用dalvik虚拟机提供的调试特性来调试，他在最初的版本就加入了对调试的支持并实现了JDWP(java debug wire protocol,java调试有线协议)，所以说我们可以直接使用支持JDWP协议的调试器来调试android程序，如：jdb,eclipse,intellJ,jswat等，但是他并不支持JVMTI(java virtual machine tool interface,java虚拟机接口工具)



dalvik虚拟机为JDWP实现加入了DDM(dalvik debug monitor,davlik调试监视器)特性。他的实现为DDMS(dalvik debug monitor server,dalvik调试监控服务)，他集成到了eclipse和android studio(当然也可以单独运行)



dalvik虚拟机中所有调试的实现在dalvik/vm/jdwp/目录下

dalvik与JDWP之间的通讯桥梁位于dalvik/vm/Debugger.c

这样将代码分开的好处是，多个项目可以复用JDWP的代码



每一个开启了调试的Dalvik虚拟机都会启动一个JDWP线程，一直处于等待状态，直到DDMS或其他调试器来连接它，他只负责接收发来的调试连接，调试的处理则有其他相应的线程发出(比如：虚拟机遇到断点要通知调试器时)

# 开启Dalvik调试功能

当启动一个虚拟机时如果系统属性ro.debuggable=1(可通adb shell getprop ro.debuggable命令查看)时所有的程序都会开启调试支持，如果为0则在判断清单文件debuggable="true"只开启当前程序的调试支持



原生程序则使用传统的Linux程序调试方法来调试，如：GUN调试调试服务器(gdb)。其中原生程序又分动态链接库和可执行程序。动态链接库需要先启动android程序以加载他，然后在以附件的方式来调试，可执行程序则可以直接使用远程方式调试








































