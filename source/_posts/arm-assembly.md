---
title: ARM汇编
date: 2016-08-10 17:18:12
categories: ARM
tags: 
    - ARM汇编
---

# ARM汇编程序结构

Android中使用的ARM汇编是GUN ARM汇编，用到的编译器是GAS(GUN assembler)他有一套自己的语法，具体的可以参考[https://sourceware.org/binutils/docs/as/index.html](https://sourceware.org/binutils/docs/as/index.html)

# 解析ARM汇编

```assembly
	.arch armv5te @处理器架构
	.fpu softvfp @协处理类型
	.eabi_attribute 20, 1 @接口属性
	.eabi_attribute 21, 1
	.eabi_attribute 23, 3
	.eabi_attribute 24, 1
	.eabi_attribute 25, 1
	.eabi_attribute 26, 2
	.eabi_attribute 30, 6
	.eabi_attribute 34, 0
	.eabi_attribute 18, 4
	.file	"hello.c" @源文件名
	.global	nums @全局符号nums
	.data
	.align	2 @对齐方式2^2=4字节=32位
	.type	nums, %object @类型为对象
	.size	nums, 20 @20个字节，5个int值
nums:
	.word	1
	.word	2
	.word	3
	.word	4
	.word	5
	.text
	.align	2
	.global	for0
	.type	for0, %function
for0:
	@ args = 0, pretend = 0, frame = 16
	@ frame_needed = 1, uses_anonymous_args = 0
	@ link register save eliminated.
	str	fp, [sp, #-4]!
	add	fp, sp, #0
	sub	sp, sp, #20
	str	r0, [fp, #-16]
	mov	r3, #0
	str	r3, [fp, #-8]
	mov	r3, #0
	str	r3, [fp, #-12]
	mov	r3, #0
	str	r3, [fp, #-8]
	b	.L2
.L3:
	ldr	r2, [fp, #-12]
	ldr	r3, [fp, #-8]
	add	r3, r2, r3
	str	r3, [fp, #-12]
	ldr	r3, [fp, #-8]
	add	r3, r3, #1
	str	r3, [fp, #-8]
.L2:
	ldr	r2, [fp, #-8]
	ldr	r3, [fp, #-16]
	cmp	r2, r3
	blt	.L3
	ldr	r3, [fp, #-12]
	mov	r0, r3
	sub	sp, fp, #0
	@ sp needed
	ldr	fp, [sp], #4
	bx	lr
	.size	for0, .-for0
	.align	2
	.global	for1
	.type	for1, %function
for1:
	@ args = 0, pretend = 0, frame = 16
	@ frame_needed = 1, uses_anonymous_args = 0
	@ link register save eliminated.
	str	fp, [sp, #-4]!
	add	fp, sp, #0
	sub	sp, sp, #20
	str	r0, [fp, #-16]
	mov	r3, #0
	str	r3, [fp, #-8]
	mov	r3, #0
	str	r3, [fp, #-12]
	mov	r3, #0
	str	r3, [fp, #-8]
	b	.L6
.L7:
	ldr	r3, [fp, #-8]
	mov	r3, r3, asl #1
	ldr	r2, [fp, #-12]
	add	r3, r2, r3
	str	r3, [fp, #-12]
	ldr	r3, [fp, #-8]
	add	r3, r3, #1
	str	r3, [fp, #-8]
.L6:
	ldr	r2, [fp, #-8]
	ldr	r3, [fp, #-16]
	cmp	r2, r3
	blt	.L7
	ldr	r3, [fp, #-12]
	mov	r0, r3
	sub	sp, fp, #0
	@ sp needed
	ldr	fp, [sp], #4
	bx	lr
	.size	for1, .-for1
	.align	2
	.global	for2
	.type	for2, %function
for2:
	@ args = 0, pretend = 0, frame = 16
	@ frame_needed = 1, uses_anonymous_args = 0
	@ link register save eliminated.
	str	fp, [sp, #-4]!
	add	fp, sp, #0
	sub	sp, sp, #20
	str	r0, [fp, #-16]
	ldr	r1, .L13
.LPIC0:
	add	r1, pc, r1
	mov	r3, #0
	str	r3, [fp, #-8]
	mov	r3, #0
	str	r3, [fp, #-12]
	mov	r3, #0
	str	r3, [fp, #-8]
	b	.L10
.L11:
	ldr	r3, [fp, #-8]
	ldr	r2, [fp, #-8]
	mul	r2, r3, r2
	ldr	r3, [fp, #-16]
	sub	r0, r3, #1
	ldr	r3, .L13+4
	ldr	r3, [r1, r3]
	ldr	r3, [r3, r0, asl #2]
	add	r3, r2, r3
	ldr	r2, [fp, #-12]
	add	r3, r2, r3
	str	r3, [fp, #-12]
	ldr	r3, [fp, #-8]
	add	r3, r3, #1
	str	r3, [fp, #-8]
.L10:
	ldr	r2, [fp, #-8]
	ldr	r3, [fp, #-16]
	cmp	r2, r3
	blt	.L11
	ldr	r3, [fp, #-12]
	mov	r0, r3
	sub	sp, fp, #0
	@ sp needed
	ldr	fp, [sp], #4
	bx	lr
.L14:
	.align	2
.L13:
	.word	_GLOBAL_OFFSET_TABLE_-(.LPIC0+8)
	.word	nums(GOT)
	.size	for2, .-for2
	.section	.rodata @声明只读数据段
	.align	2
.LC0: @标号LC0
	.ascii	"hello ARM!\000" @声明字符串
	.align	2
.LC1:
	.ascii	"for0%d\012\000"
	.align	2
.LC2:
	.ascii	"for1%d\012\000"
	.align	2
.LC3:
	.ascii	"for2%d\012\000"
	.text @代码段
	.align	2
	.global	main @全局符号，main
	.type	main, %function @main符号的类型为函数
main:
	@ args = 0, pretend = 0, frame = 8
	@ frame_needed = 1, uses_anonymous_args = 0
	stmfd	sp!, {fp, lr} @将fp,lr寄存器入栈
	add	fp, sp, #4 @初始化fp寄存器，设置栈帧
	sub	sp, sp, #8 @开辟栈控件
	str	r0, [fp, #-8] @保存第一个参数
	str	r1, [fp, #-12] @保存第二个参数
	ldr	r3, .L17 @取标号L17处的内容，即“hello ARM!\n”
.LPIC1: @标号.LPIC1
	add	r3, pc, r3 @计算“hello ARM!\n”字符串的内存地址
	mov	r0, r3 @设置参数1
	bl	puts(PLT) @调用puts函数
	mov	r0, #5 @程序返回结果为0
	bl	for0(PLT) @调用函数for0
	mov	r2, r0 @for0的返回结果
	ldr	r3, .L17+4
.LPIC2:
	add	r3, pc, r3
	mov	r0, r3
	mov	r1, r2
	bl	printf(PLT)
	mov	r0, #5
	bl	for1(PLT)
	mov	r2, r0
	ldr	r3, .L17+8
.LPIC3:
	add	r3, pc, r3
	mov	r0, r3
	mov	r1, r2
	bl	printf(PLT)
	mov	r0, #5
	bl	for2(PLT)
	mov	r2, r0
	ldr	r3, .L17+12
.LPIC4:
	add	r3, pc, r3
	mov	r0, r3
	mov	r1, r2
	bl	printf(PLT)
	mov	r3, #0
	mov	r0, r3
	sub	sp, fp, #4
	@ sp needed
	ldmfd	sp!, {fp, pc} @回复，fp的值，并将lr寄存器的值赋值给pc寄存器
.L18:
	.align	2
.L17:
	.word	.LC0-(.LPIC1+8)
	.word	.LC1-(.LPIC2+8)
	.word	.LC2-(.LPIC3+8)
	.word	.LC3-(.LPIC4+8)
	.size	main, .-main
	.ident	"GCC: (GNU) 4.9 20150123 (prerelease)"
	.section	.note.GNU-stack,"",%progbits

```

## 处理器架构定义

```
.arch armv5te @处理器架构
.fpu softvfp @协处理类型
.eabi_attribute 20, 1 @接口属性
.eabi_attribute 21, 1
.eabi_attribute 23, 3
.eabi_attribute 24, 1
.eabi_attribute 25, 1
.eabi_attribute 26, 2
.eabi_attribute 30, 6
.eabi_attribute 34, 0
.eabi_attribute 18, 4
```

这些指令定义了程序使用的处理器架构，协处理器类型，接口属性

armv5te:表示本程序的代码可以在armv5te及以上的架构处理器上运行，包括armv6,armv7-a

fpt:

​	softvfp:表示使用浮点运算库来模拟协处理运算。取值vfpv2,vfpv3

eabi_attribute：指定了接口属性(Embedded application binary interface,嵌入式应用二进制接口)是arm制订的一套接口规范，Android实现了这套规范

## 段定义

段都是很多年前的术语了，现在的高级语言基本上没有直接使用，而是由编译器字节生成的。

使用.section指令来定义

```
.section name [, "flags" [,%type [,flag_specifice_arguments]]]
```

name:段名

flags:段属性，读，写，可执行

type:段的类型，如：progbits表示段中包含数据，note表示包含的数据非程序本身使用

flag_specifice_arguments：指定平台相关的参数



我们上面定义三个段

.section	.rodata:定义只读段，属性采用默认值

.text:代码段

.section .note.GUN-stack,"",%progbits：定义了.note.GUN-stack段，他的作用是禁止生产可以执行堆栈，用来保护代码安全

## 注释

/* 多行注释 */

@单行注释

## 标号

在汇编中标号十分常见，当程序跳转时就是使用标号作为跳转目的地，汇编器在编译时会将标号转为地址，标号申明格式为：

```
<标号名>:
	代码...
```

```
for1:
	@ args = 0, pretend = 0, frame = 16
	@ frame_needed = 1, uses_anonymous_args = 0
	@ link register save eliminated.
	str	fp, [sp, #-4]!
	add	fp, sp, #0
	sub	sp, sp, #20
	str	r0, [fp, #-16]
	mov	r3, #0
	str	r3, [fp, #-8]
	mov	r3, #0
	str	r3, [fp, #-12]
	mov	r3, #0
	str	r3, [fp, #-8]
	b	.L6
```

## 汇编指令

程序中所有以“.”开头的指令都是汇编指令，他不属于ARM指令集。在GAS的文档[Assembler Directives](https://sourceware.org/binutils/docs/as/Pseudo-Ops.html#Pseudo-Ops)列出了所以得汇编指令

在上面的示例中我们使用到的汇编指令有：

.file:源文件名

.align:代码定制方式，后面的数值为2^次数放

.ascii:声明字符串

.global:声明全局符号。全局符号是指在本程序外可以访问的符号

.type：指定符号的类型。

​	.type	for0, %function表示for0是一个函数

.word：用来存放地址值

​	.word	.LC0-(.LPIC1+8)表示存放一个与地址无关的偏移量

.size:设置指定符号的大小

​	.size	for2, .-for2表示当前地址减去for2符号的地址即为整个for2函数的大小

.ident:编译器表示，没有实际用途，生成可执行程序后值被放到.comment段中

## 子程序间参数传递

自程序一般用来完成一个独立的功能，汇编中的函数声明如下：

```
.global 函数名
.type 函数,%function
函数名:
	<函数体>
```

```
.global myAdd
.type myAdd,%function
myAdd:
	add r0, r0, r1 @两个参数相加
	mov pc, lr @函数返回
```

在ARM汇编中参数传递规则:用R0-R3传递1-4个参数，如果超出用堆栈来传递，R0返回时并保存函数的返回值



























