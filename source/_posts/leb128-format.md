---
title: 深入到源码解析leb128数据类型
date: 2016-07-23 11:53:44
categories: Dalvik
tags: 
    - leb128
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

其中u1~u8很好理解，表示1到8个字节的无符号数

后面三个是dex特有的数据类型，每个LEB128由1~5字节组成，所有的字节组合在一起表示一个32位的数据 


<table class="leb128Bits">
<thead>
<tr><th colspan="16">Bitwise diagram of a two-byte LEB128 value</th></tr>
<tr>
  <th colspan="8">First byte
  </th><th colspan="8">Second byte
</th></tr>
</thead>
<tbody>
<tr>
  <td class="start1"><code>1</code></td>
  <td>bit<sub>6</sub></td>
  <td>bit<sub>5</sub></td>
  <td>bit<sub>4</sub></td>
  <td>bit<sub>3</sub></td>
  <td>bit<sub>2</sub></td>
  <td>bit<sub>1</sub></td>
  <td>bit<sub>0</sub></td>
  <td class="start2"><code>0</code></td>
  <td>bit<sub>13</sub></td>
  <td>bit<sub>12</sub></td>
  <td>bit<sub>11</sub></td>
  <td>bit<sub>10</sub></td>
  <td>bit<sub>9</sub></td>
  <td>bit<sub>8</sub></td>
  <td class="end2">bit<sub>7</sub></td>
</tr>
</tbody>
</table>

从上图我们可以看到：
第一个的最高位为1，表示他还需要第二个字节，但是我们看第二个字节的最高位发现他是0，所以他不需要第三个字节了

更详细的参考：[深入源码解析leb128数据类型]()
























