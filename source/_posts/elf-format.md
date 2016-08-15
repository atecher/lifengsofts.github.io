---
title: elf文件格式
date: 2016-08-14 21:47:34
categories: elf
tags: 
    - elf
---

# 简介

在计算机科学中，是一种用于二进制文件、可执行文件、目标代码、共享库和核心转储的标准文件格式。
是UNIX系统实验室（USL）作为应用程序二进制接口（Application Binary Interface，ABI）而开发和发布的，也是Linux的主要可执行文件格式。在android中同样也是该格式，但是有部分不太一样可以在[官网查看ARM ELF File Format](https://developer.android.com/ndk/guides/abis.html?hl=is)他会跳到[arm官方格式定义文档](http://infocenter.arm.com/help/topic/com.arm.doc.dui0101a/DUI0101A_Elf.pdf)

# 类型

elf文件分三种类型

relocatable file：可重定位文件，一般有汇编器生成的.o文件还未进行链接，链接后生成可执行的对象文件和可共享的对象文件。也可以使用ar工具将多个.o文件归档成.a静态库文件
executable file：可执行文件
shared object file：即.so文件

我们从上面的文档中发现，可执行文件和链接文件他们的结构不太一样

Linking View

| ELF Header                      |
| ------------------------------- |
| Program Header Table (Optional) |
| Section 1                       |
| ...                             |
| Section Header Table            |

Execution View

| ELF Header                      |
| ------------------------------- |
| Program Header Table            |
| Segment 1                       |
| ...                             |
| Section Header Table (Optional) |

# 数据类型

elf格式中会有很多自定义数据类型

| 类型            | 大小   | 对齐   | 解释      |
| ------------- | ---- | ---- | ------- |
| Elf32_Addr    | 4    | 4    | 无符号程序地址 |
| Elf32_Half    | 2    | 2    | 无符号短整数  |
| Elf32_Off     | 4    | 4    | 无符号文件偏移 |
| Elf32_Sword   | 4    | 4    | 有符号大整数  |
| Elf32_Word    | 4    | 4    | 无符号大整数  |
| unsigned char | 1    | 1    | 无符号小整数  |

他的定义可以在types_elf.h中查看

```
typedef uint32 Elf32_Addr;  // Unsigned program address
typedef uint16 Elf32_Half;  // Unsigned medium integer
typedef uint32 Elf32_Off;  // Unsigned file offset
typedef int32 Elf32_Sword;  // Signed large integer
typedef uint32 Elf32_Word;  // Unsigned large integer
```

# file

基本信息我们可以用file命令查看

```
file hello 
```

```
hello: ELF 32-bit LSB executable, ARM, version 1 (SYSV), dynamically linked (uses shared libs), stripped
```

# readelf

## 显示头部信息

arm-linux-androideabi-readelf -h hello

```
ELF Header:
  Magic:   7f 45 4c 46 01 01 01 00 00 00 00 00 00 00 00 00 
  Class:                             ELF32
  Data:                              2's complement, little endian
  Version:                           1 (current)
  OS/ABI:                            UNIX - System V
  ABI Version:                       0
  Type:                              EXEC (Executable file)
  Machine:                           ARM
  Version:                           0x1
  Entry point address:               0x8478
  Start of program headers:          52 (bytes into file)
  Start of section headers:          8552 (bytes into file)
  Flags:                             0x5000200, Version5 EABI, soft-float ABI
  Size of this header:               52 (bytes)
  Size of program headers:           32 (bytes)
  Number of program headers:         8
  Size of section headers:           40 (bytes)
  Number of section headers:         24
  Section header string table index: 23
```

上面看的是可执行文件，下面我们看看，共享文件

```
ELF Header:
  Magic:   7f 45 4c 46 01 01 01 00 00 00 00 00 00 00 00 00 
  Class:                             ELF32
  Data:                              2's complement, little endian
  Version:                           1 (current)
  OS/ABI:                            UNIX - System V
  ABI Version:                       0
  Type:                              DYN (Shared object file)
  Machine:                           ARM
  Version:                           0x1
  Entry point address:               0x0
  Start of program headers:          52 (bytes into file)
  Start of section headers:          12616 (bytes into file)
  Flags:                             0x5000200, Version5 EABI, soft-float ABI
  Size of this header:               52 (bytes)
  Size of program headers:           32 (bytes)
  Number of program headers:         8
  Size of section headers:           40 (bytes)
  Number of section headers:         22
  Section header string table index: 21
```

我们可以从type区分出他们的类型。

Entry point address:程序的入口地址，共享文件没有入口点

Start of program headers：

头部定义android-ndk-r11c/platforms/android-24/arch-arm/usr/include/linux/elf.h

```c++
#define EI_NIDENT 16
typedef struct elf32_hdr{
	/* WARNING: DO NOT EDIT, AUTO-GENERATED CODE - SEE TOP FOR INSTRUCTIONS */
	 unsigned char e_ident[EI_NIDENT]; //固定值7f 45 4c 46 01 01 01 00  00 00 00 00 00 00 00 00, ELF
	 Elf32_Half e_type;
	 Elf32_Half e_machine;
	 Elf32_Word e_version;
	/* WARNING: DO NOT EDIT, AUTO-GENERATED CODE - SEE TOP FOR INSTRUCTIONS */
	 Elf32_Addr e_entry;
	 Elf32_Off e_phoff; //程序头(Program Header)内容在整个文件的偏移值
	 Elf32_Off e_shoff; //段头(Section Header)内容在这个文件的偏移值
	 Elf32_Word e_flags; 
	/* WARNING: DO NOT EDIT, AUTO-GENERATED CODE - SEE TOP FOR INSTRUCTIONS */
	 Elf32_Half e_ehsize;
	 Elf32_Half e_phentsize;
	 Elf32_Half e_phnum; //程序头的个数
	 Elf32_Half e_shentsize;
	/* WARNING: DO NOT EDIT, AUTO-GENERATED CODE - SEE TOP FOR INSTRUCTIONS */
	 Elf32_Half e_shnum; //段头的个数
	 Elf32_Half e_shstrndx; //String段在整个段列表中的索引值
} Elf32_Ehdr;
```
当然定义也可以在/external/chromium_org/courgette/types_elf.h看到上面的定义

每个字段的解释如下：

| 字段名称        | 偏移值  | 长度   | 说明                                       |
| ----------- | ---- | ---- | ---------------------------------------- |
| e_ident     | 0x0  | 16   | elf文件幻数                                  |
| e_type      | 0x10 | 2    | 该文件的类型,见e_type表                          |
| e_machine   | 0x12 | 2    | 程序运行的体系结构,见e_machine表                    |
| e_version   | 0x14 | 4    | 文件版本,1表示当前版本                             |
| e_entry     | 0x18 | 4    | 程序入口点,动态链接文件没有入口，为0                      |
| e_phoff     | 0x1c | 4    | 程序头表(program header table)偏移量,如果没有为0     |
| e_shoff     | 0x20 | 4    | section头表(section header table)偏移,如果没有为0 |
| e_flags     | 0x24 | 4    |                                          |
| e_ehsize    | 0x28 | 2    | elf头的大小,Size of this header就是这个字段        |
| e_phentsize | 0x2a | 2    | 程序头表(program header table)大小,Size of program headers |
| e_phnum     | 0x2c |      |                                          |
|             |      |      |                                          |
|             |      |      |                                          |
|             |      |      |                                          |


e_type表
| 名称        | 值      | 解释                 |
| --------- | ------ | ------------------ |
| ET_NONE   | 0      | No file type       |
| ET_REL    | 1      | Relocatable file   |
| ET_EXEC   | 2      | Executable file    |
| ET_DYN    | 3      | Shared object file |
| ET_CORE   | 4      | Core file          |
| ET_LOPROC | 0xff00 | Processor-specific |
| ET_HIPROC | 0xffff | Processor-specific |

其中CORE的文件内容未被指明，他是保留的

ET_LOPROC-ET_HIPROC是为特殊处理器保留的

e_machine表

| 名称       | 值    | 解释             |
| -------- | ---- | -------------- |
| EM_NONE  | 0    | No machine     |
| EM_M32   | 1    | AT&T WE 32100  |
| EM_SPARC | 2    | SPARC          |
| EM_386   | 3    | Intel 80386    |
| EM_68K   | 4    | Motorola 68000 |
| EM_88K   | 5    | Motorola 88000 |
| EM_860   | 7    | Intel 80860    |
| EM_MIPS  | 8    | MIPS RS3000    |
|          | 28   | ARM            |

## 显示节(section)信息

arm-linux-androideabi-readelf -S hello

```
There are 24 section headers, starting at offset 0x2168:

Section Headers:
  [Nr] Name              Type            Addr     Off    Size   ES Flg Lk Inf Al
  [ 0]                   NULL            00000000 000000 000000 00      0   0  0
  [ 1] .interp           PROGBITS        00008134 000134 000013 00   A  0   0  1
  [ 2] .dynsym           DYNSYM          00008148 000148 0000e0 10   A  3   1  4
  [ 3] .dynstr           STRTAB          00008228 000228 0000c4 00   A  0   0  1
  [ 4] .hash             HASH            000082ec 0002ec 00004c 04   A  2   0  4
  [ 5] .rel.dyn          REL             00008338 000338 000010 08   A  2   0  4
  [ 6] .rel.plt          REL             00008348 000348 000048 08  AI  2   7  4
  [ 7] .plt              PROGBITS        00008390 000390 000080 00  AX  0   0  4
  [ 8] .text             PROGBITS        00008410 000410 0016d0 00  AX  0   0  4
  [ 9] .note.android.ide PROGBITS        00009ae0 001ae0 000018 00   A  0   0  4
  [10] .ARM.exidx        ARM_EXIDX       00009af8 001af8 000110 08  AL  8   0  4
  [11] .ARM.extab        PROGBITS        00009c08 001c08 00003c 00   A  0   0  4
  [12] .rodata           PROGBITS        00009c48 001c48 000028 01 AMS  0   0  8
  [13] .fini_array       FINI_ARRAY      0000ae84 001e84 000008 00  WA  0   0  4
  [14] .init_array       INIT_ARRAY      0000ae8c 001e8c 000010 00  WA  0   0  4
  [15] .preinit_array    PREINIT_ARRAY   0000ae9c 001e9c 000008 00  WA  0   0  4
  [16] .dynamic          DYNAMIC         0000aea4 001ea4 0000f8 08  WA  3   0  4
  [17] .got              PROGBITS        0000af9c 001f9c 000064 00  WA  0   0  4
  [18] .data             PROGBITS        0000b000 002000 000014 00  WA  0   0  4
  [19] .bss              NOBITS          0000b014 002014 000004 00  WA  0   0  4
  [20] .comment          PROGBITS        00000000 002014 000026 01  MS  0   0  1
  [21] .note.gnu.gold-ve NOTE            00000000 00203c 00001c 00      0   0  4
  [22] .ARM.attributes   ARM_ATTRIBUTES  00000000 002058 00002b 00      0   0  1
  [23] .shstrtab         STRTAB          00000000 002083 0000e3 00      0   0  1
Key to Flags:
  W (write), A (alloc), X (execute), M (merge), S (strings)
  I (info), L (link order), G (group), T (TLS), E (exclude), x (unknown)
  O (extra OS processing required) o (OS specific), p (processor specific)
➜  armeabi arm-linux-androideabi-readelf -S libhello.so 
```

那什么是节呢，节是elf文件里用来装载内容数据的最小容器。其中每一个sections内部都装载了性质和属性差不多的内容如：

.text section：可以执行代码

.data section:初始化数据

.bss section:未初始时数据

等，一个文件到底有哪些section，是有这个elf中的section head table(sht)决定的，其中对每一个section进行了一些描述，包括名称，类型，大小，在整个文件的整体偏移位置，他的定义如下

```c++
typedef struct elf32_shdr {
	 Elf32_Word sh_name;
	/* WARNING: DO NOT EDIT, AUTO-GENERATED CODE - SEE TOP FOR INSTRUCTIONS */
	 Elf32_Word sh_type;
	 Elf32_Word sh_flags;
	 Elf32_Addr sh_addr;
	 Elf32_Off sh_offset;
	/* WARNING: DO NOT EDIT, AUTO-GENERATED CODE - SEE TOP FOR INSTRUCTIONS */
	 Elf32_Word sh_size;
	 Elf32_Word sh_link;
	 Elf32_Word sh_info;
	 Elf32_Word sh_addralign;
	/* WARNING: DO NOT EDIT, AUTO-GENERATED CODE - SEE TOP FOR INSTRUCTIONS */
	 Elf32_Word sh_entsize;
} Elf32_Shdr;
```

我们从上面的信息显示这个文件有24个section

off:该section从开始位置的偏移

size:表示section的大小

flg:表示当前section的标志，如：text只有可执行















