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

# 查看工具

## file

基本信息我们可以用file命令查看

```
file hello 
```

```
hello: ELF 32-bit LSB executable, ARM, version 1 (SYSV), dynamically linked (uses shared libs), stripped
```

## readelf

### 显示头部信息

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
  Start of section headers:          12616 (bytes into file) //10进制,要转换为16进制查看所在内存地址
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

### 显示节(section)信息

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

动态文件

arm-linux-androideabi-readelf -S libhello.so

```
There are 22 section headers, starting at offset 0x3148:

Section Headers:
  [Nr] Name              Type            Addr     Off    Size   ES Flg Lk Inf Al
  [ 0]                   NULL            00000000 000000 000000 00      0   0  0
  [ 1] .interp           PROGBITS        00000134 000134 000013 00   A  0   0  1
  [ 2] .dynsym           DYNSYM          00000148 000148 0003d0 10   A  3   1  4
  [ 3] .dynstr           STRTAB          00000518 000518 0004b1 00   A  0   0  1
  [ 4] .hash             HASH            000009cc 0009cc 000190 04   A  2   0  4
  [ 5] .rel.dyn          REL             00000b5c 000b5c 000048 08   A  2   0  4
  [ 6] .rel.plt          REL             00000ba4 000ba4 000048 08  AI  2   7  4
  [ 7] .plt              PROGBITS        00000bec 000bec 000080 00  AX  0   0  4
  [ 8] .text             PROGBITS        00000c6c 000c6c 001664 00  AX  0   0  4
  [ 9] .ARM.extab        PROGBITS        000022d0 0022d0 00003c 00   A  0   0  4
  [10] .ARM.exidx        ARM_EXIDX       0000230c 00230c 000110 08  AL  8   0  4
  [11] .rodata           PROGBITS        00002420 002420 000028 01 AMS  0   0  8
  [12] .fini_array       FINI_ARRAY      00003eac 002eac 000008 00  WA  0   0  4
  [13] .init_array       INIT_ARRAY      00003eb4 002eb4 000004 00  WA  0   0  1
  [14] .dynamic          DYNAMIC         00003eb8 002eb8 0000f8 08  WA  3   0  4
  [15] .got              PROGBITS        00003fb0 002fb0 000050 00  WA  0   0  4
  [16] .data             PROGBITS        00004000 003000 000018 00  WA  0   0  4
  [17] .bss              NOBITS          00004018 003018 000000 00  WA  0   0  1
  [18] .comment          PROGBITS        00000000 003018 000026 01  MS  0   0  1
  [19] .note.gnu.gold-ve NOTE            00000000 003040 00001c 00      0   0  4
  [20] .ARM.attributes   ARM_ATTRIBUTES  00000000 00305c 00002b 00      0   0  1
  [21] .shstrtab         STRTAB          00000000 003087 0000c0 00      0   0  1
Key to Flags:
  W (write), A (alloc), X (execute), M (merge), S (strings)
  I (info), L (link order), G (group), T (TLS), E (exclude), x (unknown)
  O (extra OS processing required) o (OS specific), p (processor specific)
```

那什么是节呢，节是elf文件里用来装载内容数据的最小容器。其中每一个sections内部都装载了性质和属性差不多的内容如：

.text section：可以执行代码

.data section:初始化数据

.bss section:未初始时数据

等，一个文件到底有哪些section，是有这个elf中的section head table(sht)决定的。

# dex文件整体结构

## ELF Header

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
| e_flags     | 0x24 | 4    | //TODO                                   |
| e_ehsize    | 0x28 | 2    | elf头的大小,Size of this header就是这个字段        |
| e_phentsize | 0x2a | 2    | 程序头表(program header table)大小,Size of program headers |
| e_phnum     | 0x2c | 2    | 程序头表(program header table)个数, Number of program headers |
| e_shentsize | 0x2e | 2    | section头的大小(单个), Size of section headers |
| e_shnum     | 0x30 | 2    | section header table中的入口数目               |
| e_shstrndx  | 0x32 | 2    | 跟section名字字符表相关入口的section头表(section header table)索引,//TODO |

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

## Section Header

只有文件是链接格式才有效，Section Header是对每一个section进行了一些描述，包括名称，类型，大小，在整个文件的整体偏移位置，他的定义如下

```c++
struct Elf32_Shdr {
  Elf32_Word   sh_name;
  Elf32_Word   sh_type;
  Elf32_Word   sh_flags;
  Elf32_Addr   sh_addr;
  Elf32_Off    sh_offset;
  Elf32_Word   sh_size;
  Elf32_Word   sh_link;
  Elf32_Word   sh_info;
  Elf32_Word   sh_addralign;
  Elf32_Word   sh_entsize;
};
```

我们从上面的信息显示这个文件有22个section，他的其使用位置可以从header中查看为12616转为16进制为0x3148，所以section header的开始位置就是这里，每个字段的解释如下：

| 字段名称         | 长度   | 说明                                       |
| ------------ | ---- | ---------------------------------------- |
| sh_name      | 4    | section的名字，值是String Table中的索引            |
| sh_type      | 4    | 把sections按内容和意义分类，见sh_type表              |
| sh_flags     | 4    | sections支持位的标记，用来描述多个属性,见sh_flags表       |
| sh_addr      | 4    | 如果该section加载到内存为内存地址，否则为0                |
| sh_offset    | 4    | 该section的真实偏移位置，SHT_NOBITS类的section不暂用空间 |
| sh_size      | 4    | section的字节大小，如果类型为SHT_NOBITS为0           |
| sh_link      | 4    | section报头表的索引连接,具体的还得依据他的类型来解释这个值        |
| sh_info      | 4    | 额外的信息，解释依靠该section的类型                    |
| sh_addralign | 4    | 地址对齐的约束,假如一个section保存着双字，系统就必须确定整个section是否双字对齐。所以sh_addr的值以sh_addralign的值 |
| sh_entsize   | 4    | 保存着一张固定大小入口的表，就象符号表。对于这样一个               |

sh_name：section的名字值是section报头字符表section的索引。[看以下的“String Table”], 以NULL空字符结束

off:该section从开始位置的偏移

size:表示section的大小

flg:表示当前section的标志，如：text只有可执行

根据上面的信息我们总结出21个section

| sh_name | sh_type  | sh_flags | sh_addr | sh_offset | sh_size | sh_link | sh_info | sh_addralign | sh_entsize |
| ------- | -------- | -------- | ------- | --------- | ------- | ------- | ------- | ------------ | ---------- |
| 0       | 0        | 0        | 0       | 0         | 0       | 0       | 0       | 0            | 0          |
| 0xb     | 0x1      | 0x2      | 0x134   | 0x134     | 0x13    | 0x0     | 0x0     | 0x1          | 0x0        |
| 0x13    | 0xb      | 0x2      | 148     | 148       | 3d0     | 3       | 1       | 4            | 10         |
| 1b      | 3        | 2        | 518     | 518       | 4b1     | 0       | 0       | 1            | 0          |
| 23      | 5        | 2        | 9cc     | 9cc       | 190     | 2       | 0       | 4            | 4          |
| 29      | 9        | 2        | b5c     | b5c       | 48      | 2       | 0       | 4            | 8          |
| 32      | 9        | 42       | ba4     | ba4       | 48      | 2       | 7       | 4            | 8          |
| 36      | 1        | 6        | bec     | bec       | 80      | 0       | 0       | 4            | 0          |
| 3b      | 1        | 6        | c6c     | c6c       | 1664    | 0       | 0       | 4            | 0          |
| 41      | 1        | 2        | 22d0    | 22d0      | 3c      | 0       | 0       | 4            | 0          |
| 4c      | 70000001 | 82       | 23c0    | 23c0      | 110     | 8       | 0       | 4            | 8          |
| 57      | 1        | 32       | 2420    | 2420      | 28      | 0       | 0       | 8            | 1          |
| 5f      | f        | 3        | 3eac    | 2eac      | 8       | 0       | 0       | 4            | 0          |
| 6b      | e        | e        | 3eb4    | 2eb4      | 4       | 0       | 0       | 1            | 0          |
| 77      | 6        | 3        | 3eb8    | 2eb8      | f8      | 3       | 0       | 4            | 8          |
| 80      | 1        | 3        | 3fb0    | 2fb0      | 50      | 0       | 0       | 4            | 0          |
| 85      | 1        | 3        | 4000    | 3000      | 18      | 0       | 0       | 4            | 0          |
| 8b      | 8        | 3        | 4018    | 3018      | 0       | 0       | 0       | 1            | 0          |
| 90      | 1        | 30       | 0       | 3018      | 26      | 0       | 0       | 1            | 1          |
| 99      | 7        | 0        | 0       | 3040      | 1c      | 0       | 0       | 4            | 0          |
| b0      | 70000003 | 0        | 0       | 305c      | 2b      | 0       | 0       | 1            | 0          |
| 1       | 3        | 0        | 0       | 3087      | c0      | 0       | 0       | 1            | 0          |



























