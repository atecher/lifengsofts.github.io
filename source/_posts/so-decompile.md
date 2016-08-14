---
title: Android so文件反编译
date: 2016-08-14 21:57:33
categories: NDK
tags: 
    - objdump
    - ida pro
---

# objdump

他是ndk中提供的一个工具

```
arm-linux-androideabi-objdump -S libhello-jni.so
```

```
libhello-jni.so:     file format elf32-littlearm


Disassembly of section .plt:

00000c60 <__cxa_atexit@plt-0x14>:
 c60:	e52de004 	push	{lr}		; (str lr, [sp, #-4]!)
 c64:	e59fe004 	ldr	lr, [pc, #4]	; c70 <__cxa_atexit@plt-0x4>
 c68:	e08fe00e 	add	lr, pc, lr
 c6c:	e5bef008 	ldr	pc, [lr, #8]!
 c70:	00003368 	andeq	r3, r0, r8, ror #6

00000c74 <__cxa_atexit@plt>:
 c74:	e28fc600 	add	ip, pc, #0, 12
 c78:	e28cca03 	add	ip, ip, #12288	; 0x3000
 c7c:	e5bcf368 	ldr	pc, [ip, #872]!	; 0x368

00000c80 <__cxa_finalize@plt>:
 c80:	e28fc600 	add	ip, pc, #0, 12
 c84:	e28cca03 	add	ip, ip, #12288	; 0x3000
 c88:	e5bcf360 	ldr	pc, [ip, #864]!	; 0x360

00000c8c <__gnu_Unwind_Find_exidx@plt>:
 c8c:	e28fc600 	add	ip, pc, #0, 12
 c90:	e28cca03 	add	ip, ip, #12288	; 0x3000
 c94:	e5bcf358 	ldr	pc, [ip, #856]!	; 0x358

00000c98 <abort@plt>:
 c98:	e28fc600 	add	ip, pc, #0, 12
 c9c:	e28cca03 	add	ip, ip, #12288	; 0x3000
 ca0:	e5bcf350 	ldr	pc, [ip, #848]!	; 0x350

00000ca4 <memcpy@plt>:
 ca4:	e28fc600 	add	ip, pc, #0, 12
 ca8:	e28cca03 	add	ip, ip, #12288	; 0x3000
 cac:	e5bcf348 	ldr	pc, [ip, #840]!	; 0x348

00000cb0 <__cxa_begin_cleanup@plt>:
 cb0:	e28fc600 	add	ip, pc, #0, 12
 cb4:	e28cca03 	add	ip, ip, #12288	; 0x3000
 cb8:	e5bcf340 	ldr	pc, [ip, #832]!	; 0x340

00000cbc <__cxa_type_match@plt>:
 cbc:	e28fc600 	add	ip, pc, #0, 12
 cc0:	e28cca03 	add	ip, ip, #12288	; 0x3000
 cc4:	e5bcf338 	ldr	pc, [ip, #824]!	; 0x338

Disassembly of section .text:

00000cc8 <Java_com_example_hellojni_HelloJni_stringFromJNI-0x3c>:
     cc8:	e59f0004 	ldr	r0, [pc, #4]	; cd4 <__cxa_type_match@plt+0x18>
     ccc:	e08f0000 	add	r0, pc, r0
     cd0:	eaffffea 	b	c80 <__cxa_finalize@plt>
     cd4:	0000332c 	andeq	r3, r0, ip, lsr #6
     cd8:	e3500000 	cmp	r0, #0
     cdc:	012fff1e 	bxeq	lr
     ce0:	e12fff10 	bx	r0
     ce4:	e1a01000 	mov	r1, r0
     ce8:	e59f200c 	ldr	r2, [pc, #12]	; cfc <__cxa_type_match@plt+0x40>
     cec:	e59f000c 	ldr	r0, [pc, #12]	; d00 <__cxa_type_match@plt+0x44>
     cf0:	e08f2002 	add	r2, pc, r2
     cf4:	e08f0000 	add	r0, pc, r0
     cf8:	eaffffdd 	b	c74 <__cxa_atexit@plt>
     cfc:	00003308 	andeq	r3, r0, r8, lsl #6
     d00:	ffffffdc 			; <UNDEFINED> instruction: 0xffffffdc

00000d04 <Java_com_example_hellojni_HelloJni_stringFromJNI>:
     d04:	e92d4800 	push	{fp, lr}
     d08:	e28db004 	add	fp, sp, #4
     d0c:	e24dd008 	sub	sp, sp, #8
     d10:	e50b0008 	str	r0, [fp, #-8]
     d14:	e50b100c 	str	r1, [fp, #-12]
     d18:	e51b3008 	ldr	r3, [fp, #-8]
     d1c:	e5933000 	ldr	r3, [r3]
     d20:	e593329c 	ldr	r3, [r3, #668]	; 0x29c
     d24:	e51b0008 	ldr	r0, [fp, #-8]
     d28:	e59f201c 	ldr	r2, [pc, #28]	; d4c <Java_com_example_hellojni_HelloJni_stringFromJNI+0x48>
     d2c:	e08f2002 	add	r2, pc, r2
     d30:	e1a01002 	mov	r1, r2
     d34:	e12fff33 	blx	r3
     d38:	e1a03000 	mov	r3, r0
     d3c:	e1a00000 	nop			; (mov r0, r0)
     d40:	e1a00003 	mov	r0, r3
     d44:	e24bd004 	sub	sp, fp, #4
     d48:	e8bd8800 	pop	{fp, pc}
     d4c:	0000153c 	andeq	r1, r0, ip, lsr r5
     d50:	e5903000 	ldr	r3, [r0]
     d54:	e3130101 	tst	r3, #1073741824	; 0x40000000
     d58:	13833102 	orrne	r3, r3, #-2147483648	; 0x80000000
     d5c:	03c33102 	biceq	r3, r3, #-2147483648	; 0x80000000
     d60:	e0800003 	add	r0, r0, r3
     d64:	e12fff1e 	bx	lr
     d68:	e92d4ff7 	push	{r0, r1, r2, r4, r5, r6, r7, r8, r9, sl, fp, lr}
     d6c:	e3510000 	cmp	r1, #0
     d70:	e1a05001 	mov	r5, r1
     d74:	0a000021 	beq	e00 <Java_com_example_hellojni_HelloJni_stringFromJNI+0xfc>
     d78:	e2418001 	sub	r8, r1, #1
     d7c:	e1a06002 	mov	r6, r2
     d80:	e1a07000 	mov	r7, r0
     d84:	e1a09008 	mov	r9, r8
     d88:	e3a0b000 	mov	fp, #0
     d8c:	e08b4009 	add	r4, fp, r9
     d90:	e0844fa4 	add	r4, r4, r4, lsr #31
     d94:	e1a040c4 	asr	r4, r4, #1
     d98:	e1a0a184 	lsl	sl, r4, #3
     d9c:	e087500a 	add	r5, r7, sl
     da0:	e1a00005 	mov	r0, r5
     da4:	ebffffe9 	bl	d50 <Java_com_example_hellojni_HelloJni_stringFromJNI+0x4c>
     da8:	e1540008 	cmp	r4, r8
     dac:	0a000011 	beq	df8 <Java_com_example_hellojni_HelloJni_stringFromJNI+0xf4>
     db0:	e58d0004 	str	r0, [sp, #4]
     db4:	e28a0008 	add	r0, sl, #8
     db8:	e0870000 	add	r0, r7, r0
     dbc:	ebffffe3 	bl	d50 <Java_com_example_hellojni_HelloJni_stringFromJNI+0x4c>
     dc0:	e59d3004 	ldr	r3, [sp, #4]
     dc4:	e1560003 	cmp	r6, r3
     dc8:	2a000003 	bcs	ddc <Java_com_example_hellojni_HelloJni_stringFromJNI+0xd8>
     dcc:	e154000b 	cmp	r4, fp
     dd0:	0a000006 	beq	df0 <Java_com_example_hellojni_HelloJni_stringFromJNI+0xec>
     dd4:	e2449001 	sub	r9, r4, #1
     dd8:	eaffffeb 	b	d8c <Java_com_example_hellojni_HelloJni_stringFromJNI+0x88>
     ddc:	e2400001 	sub	r0, r0, #1
     de0:	e1560000 	cmp	r6, r0
     de4:	9a000005 	bls	e00 <Java_com_example_hellojni_HelloJni_stringFromJNI+0xfc>
     de8:	e284b001 	add	fp, r4, #1
     dec:	eaffffe6 	b	d8c <Java_com_example_hellojni_HelloJni_stringFromJNI+0x88>
     df0:	e3a05000 	mov	r5, #0
     df4:	ea000001 	b	e00 <Java_com_example_hellojni_HelloJni_stringFromJNI+0xfc>
     df8:	e1560000 	cmp	r6, r0
     dfc:	3afffff2 	bcc	dcc <Java_com_example_hellojni_HelloJni_stringFromJNI+0xc8>
     e00:	e1a00005 	mov	r0, r5
     e04:	e28dd00c 	add	sp, sp, #12
     e08:	e8bd8ff0 	pop	{r4, r5, r6, r7, r8, r9, sl, fp, pc}
     e0c:	e3500001 	cmp	r0, #1
     e10:	0a000006 	beq	e30 <Java_com_example_hellojni_HelloJni_stringFromJNI+0x12c>
     e14:	e3500002 	cmp	r0, #2
     e18:	0a000007 	beq	e3c <Java_com_example_hellojni_HelloJni_stringFromJNI+0x138>
     e1c:	e3500000 	cmp	r0, #0
     e20:	1a000008 	bne	e48 <Java_com_example_hellojni_HelloJni_stringFromJNI+0x144>
     e24:	e59f0024 	ldr	r0, [pc, #36]	; e50 <Java_com_example_hellojni_HelloJni_stringFromJNI+0x14c>
     e28:	e79f0000 	ldr	r0, [pc, r0]
     e2c:	e12fff1e 	bx	lr
     e30:	e59f001c 	ldr	r0, [pc, #28]	; e54 <Java_com_example_hellojni_HelloJni_stringFromJNI+0x150>
     e34:	e79f0000 	ldr	r0, [pc, r0]
     e38:	e12fff1e 	bx	lr
     e3c:	e59f0014 	ldr	r0, [pc, #20]	; e58 <Java_com_example_hellojni_HelloJni_stringFromJNI+0x154>
     e40:	e79f0000 	ldr	r0, [pc, r0]
     e44:	e12fff1e 	bx	lr
     e48:	e3a00000 	mov	r0, #0
     e4c:	e12fff1e 	bx	lr
     e50:	0000318c 	andeq	r3, r0, ip, lsl #3
     e54:	00003184 	andeq	r3, r0, r4, lsl #3
     e58:	0000317c 	andeq	r3, r0, ip, ror r1
     e5c:	e59f30f0 	ldr	r3, [pc, #240]	; f54 <Java_com_example_hellojni_HelloJni_stringFromJNI+0x250>
     e60:	e92d4037 	push	{r0, r1, r2, r4, r5, lr}
     e64:	e79f3003 	ldr	r3, [pc, r3]
     e68:	e1a04000 	mov	r4, r0
     e6c:	e3530000 	cmp	r3, #0
     e70:	e2415002 	sub	r5, r1, #2
     e74:	0a000008 	beq	e9c <Java_com_example_hellojni_HelloJni_stringFromJNI+0x198>
     e78:	e1a00005 	mov	r0, r5
     e7c:	e28d1004 	add	r1, sp, #4
     e80:	ebffff81 	bl	c8c <__gnu_Unwind_Find_exidx@plt>
     e84:	e3500000 	cmp	r0, #0
     e88:	1a00000a 	bne	eb8 <Java_com_example_hellojni_HelloJni_stringFromJNI+0x1b4>
     e8c:	e3a03000 	mov	r3, #0
     e90:	e5843010 	str	r3, [r4, #16]
     e94:	e3a00009 	mov	r0, #9
     e98:	ea00002b 	b	f4c <Java_com_example_hellojni_HelloJni_stringFromJNI+0x248>
     e9c:	e59f30b4 	ldr	r3, [pc, #180]	; f58 <Java_com_example_hellojni_HelloJni_stringFromJNI+0x254>
     ea0:	e59f00b4 	ldr	r0, [pc, #180]	; f5c <Java_com_example_hellojni_HelloJni_stringFromJNI+0x258>
     ea4:	e79f3003 	ldr	r3, [pc, r3]
     ea8:	e79f0000 	ldr	r0, [pc, r0]
     eac:	e0603003 	rsb	r3, r0, r3
     eb0:	e1a031c3 	asr	r3, r3, #3
     eb4:	e58d3004 	str	r3, [sp, #4]
     eb8:	e1a02005 	mov	r2, r5
     ebc:	e59d1004 	ldr	r1, [sp, #4]
     ec0:	ebffffa8 	bl	d68 <Java_com_example_hellojni_HelloJni_stringFromJNI+0x64>
     ec4:	e2505000 	subs	r5, r0, #0
     ec8:	0affffef 	beq	e8c <Java_com_example_hellojni_HelloJni_stringFromJNI+0x188>
     ecc:	ebffff9f 	bl	d50 <Java_com_example_hellojni_HelloJni_stringFromJNI+0x4c>
     ed0:	e5953004 	ldr	r3, [r5, #4]
     ed4:	e3530001 	cmp	r3, #1
     ed8:	03a03000 	moveq	r3, #0
     edc:	05843010 	streq	r3, [r4, #16]
     ee0:	e5840048 	str	r0, [r4, #72]	; 0x48
     ee4:	03a00005 	moveq	r0, #5
     ee8:	0a000017 	beq	f4c <Java_com_example_hellojni_HelloJni_stringFromJNI+0x248>
     eec:	e3530000 	cmp	r3, #0
     ef0:	e2850004 	add	r0, r5, #4
     ef4:	b584004c 	strlt	r0, [r4, #76]	; 0x4c
     ef8:	b3a03001 	movlt	r3, #1
     efc:	ba000002 	blt	f0c <Java_com_example_hellojni_HelloJni_stringFromJNI+0x208>
     f00:	ebffff92 	bl	d50 <Java_com_example_hellojni_HelloJni_stringFromJNI+0x4c>
     f04:	e3a03000 	mov	r3, #0
     f08:	e584004c 	str	r0, [r4, #76]	; 0x4c
     f0c:	e594004c 	ldr	r0, [r4, #76]	; 0x4c
     f10:	e5843050 	str	r3, [r4, #80]	; 0x50
     f14:	e5903000 	ldr	r3, [r0]
     f18:	e3530000 	cmp	r3, #0
     f1c:	aa000007 	bge	f40 <Java_com_example_hellojni_HelloJni_stringFromJNI+0x23c>
     f20:	e1a00c23 	lsr	r0, r3, #24
     f24:	e200000f 	and	r0, r0, #15
     f28:	ebffffb7 	bl	e0c <Java_com_example_hellojni_HelloJni_stringFromJNI+0x108>
     f2c:	e3500000 	cmp	r0, #0
     f30:	e5840010 	str	r0, [r4, #16]
     f34:	03a00009 	moveq	r0, #9
     f38:	13a00000 	movne	r0, #0
     f3c:	ea000002 	b	f4c <Java_com_example_hellojni_HelloJni_stringFromJNI+0x248>
     f40:	ebffff82 	bl	d50 <Java_com_example_hellojni_HelloJni_stringFromJNI+0x4c>
     f44:	e5840010 	str	r0, [r4, #16]
     f48:	e3a00000 	mov	r0, #0
     f4c:	e28dd00c 	add	sp, sp, #12
     f50:	e8bd8030 	pop	{r4, r5, pc}
     f54:	0000315c 	andeq	r3, r0, ip, asr r1
     f58:	00003120 	andeq	r3, r0, r0, lsr #2
     f5c:	00003120 	andeq	r3, r0, r0, lsr #2
     f60:	e5903000 	ldr	r3, [r0]
     f64:	e92d4010 	push	{r4, lr}
     f68:	e3130001 	tst	r3, #1
     f6c:	e1a04000 	mov	r4, r0
     f70:	1a000005 	bne	f8c <Java_com_example_hellojni_HelloJni_stringFromJNI+0x288>
     f74:	e3130002 	tst	r3, #2
     f78:	e2800048 	add	r0, r0, #72	; 0x48
     f7c:	0a000001 	beq	f88 <Java_com_example_hellojni_HelloJni_stringFromJNI+0x284>
     f80:	eb000335 	bl	1c5c <__gnu_Unwind_Restore_VFP_D>
     f84:	ea000000 	b	f8c <Java_com_example_hellojni_HelloJni_stringFromJNI+0x288>
     f88:	eb00032f 	bl	1c4c <__gnu_Unwind_Restore_VFP>
     f8c:	e5943000 	ldr	r3, [r4]
     f90:	e3130004 	tst	r3, #4
     f94:	1a000001 	bne	fa0 <Java_com_example_hellojni_HelloJni_stringFromJNI+0x29c>
     f98:	e28400d0 	add	r0, r4, #208	; 0xd0
     f9c:	eb000332 	bl	1c6c <__gnu_Unwind_Restore_VFP_D_16_to_31>
     fa0:	e5943000 	ldr	r3, [r4]
     fa4:	e3130008 	tst	r3, #8
     fa8:	1a000001 	bne	fb4 <Java_com_example_hellojni_HelloJni_stringFromJNI+0x2b0>
     fac:	e2840e15 	add	r0, r4, #336	; 0x150
     fb0:	eb000331 	bl	1c7c <__gnu_Unwind_Restore_WMMXD>
     fb4:	e5943000 	ldr	r3, [r4]
     fb8:	e3130010 	tst	r3, #16
     fbc:	18bd8010 	popne	{r4, pc}
     fc0:	e2840e1d 	add	r0, r4, #464	; 0x1d0
     fc4:	e8bd4010 	pop	{r4, lr}
     fc8:	ea00034d 	b	1d04 <__gnu_Unwind_Restore_WMMXC>
     fcc:	e5903000 	ldr	r3, [r0]
     fd0:	e3530000 	cmp	r3, #0
     fd4:	17930000 	ldrne	r0, [r3, r0]
     fd8:	01a00003 	moveq	r0, r3
     fdc:	e12fff1e 	bx	lr
     fe0:	e3a00009 	mov	r0, #9
     fe4:	e12fff1e 	bx	lr
     fe8:	e12fff1e 	bx	lr
     fec:	e92d4070 	push	{r4, r5, r6, lr}
     ff0:	e1a05000 	mov	r5, r0
     ff4:	e1a04001 	mov	r4, r1
     ff8:	e1a00005 	mov	r0, r5
     ffc:	e5941040 	ldr	r1, [r4, #64]	; 0x40
    1000:	ebffff95 	bl	e5c <Java_com_example_hellojni_HelloJni_stringFromJNI+0x158>
    1004:	e2506000 	subs	r6, r0, #0
    1008:	0a000000 	beq	1010 <Java_com_example_hellojni_HelloJni_stringFromJNI+0x30c>
    100c:	ebffff21 	bl	c98 <abort@plt>
    1010:	e5943040 	ldr	r3, [r4, #64]	; 0x40
    1014:	e5853014 	str	r3, [r5, #20]
    1018:	e3a00001 	mov	r0, #1
    101c:	e5953010 	ldr	r3, [r5, #16]
    1020:	e1a01005 	mov	r1, r5
    1024:	e1a02004 	mov	r2, r4
    1028:	e12fff33 	blx	r3
    102c:	e3500008 	cmp	r0, #8
    1030:	0afffff0 	beq	ff8 <Java_com_example_hellojni_HelloJni_stringFromJNI+0x2f4>
    1034:	e3500007 	cmp	r0, #7
    1038:	1afffff3 	bne	100c <Java_com_example_hellojni_HelloJni_stringFromJNI+0x308>
    103c:	e1a00006 	mov	r0, r6
    1040:	e5941040 	ldr	r1, [r4, #64]	; 0x40
    1044:	ebffffe7 	bl	fe8 <Java_com_example_hellojni_HelloJni_stringFromJNI+0x2e4>
    1048:	e2840004 	add	r0, r4, #4
    104c:	eb0002f9 	bl	1c38 <__restore_core_regs>
    1050:	e92d4ff0 	push	{r4, r5, r6, r7, r8, r9, sl, fp, lr}
    1054:	e281e004 	add	lr, r1, #4
    1058:	e590800c 	ldr	r8, [r0, #12]
    105c:	e5909018 	ldr	r9, [r0, #24]
    1060:	e1a04000 	mov	r4, r0
    1064:	e1a06002 	mov	r6, r2
    1068:	e8be000f 	ldm	lr!, {r0, r1, r2, r3}
    106c:	e24ddff3 	sub	sp, sp, #972	; 0x3cc
    1070:	e28dc00c 	add	ip, sp, #12
    1074:	e8ac000f 	stmia	ip!, {r0, r1, r2, r3}
    1078:	e8be000f 	ldm	lr!, {r0, r1, r2, r3}
    107c:	e8ac000f 	stmia	ip!, {r0, r1, r2, r3}
    1080:	e8be000f 	ldm	lr!, {r0, r1, r2, r3}
    1084:	e8ac000f 	stmia	ip!, {r0, r1, r2, r3}
    1088:	e89e000f 	ldm	lr, {r0, r1, r2, r3}
    108c:	e3a07000 	mov	r7, #0
    1090:	e28db008 	add	fp, sp, #8
    1094:	e28daf7a 	add	sl, sp, #488	; 0x1e8
    1098:	e88c000f 	stm	ip, {r0, r1, r2, r3}
    109c:	e58d7008 	str	r7, [sp, #8]
    10a0:	e1a00004 	mov	r0, r4
    10a4:	e59d1048 	ldr	r1, [sp, #72]	; 0x48
    10a8:	ebffff6b 	bl	e5c <Java_com_example_hellojni_HelloJni_stringFromJNI+0x158>
    10ac:	e3560000 	cmp	r6, #0
    10b0:	13a0600a 	movne	r6, #10
    10b4:	03a06009 	moveq	r6, #9
    10b8:	e2505000 	subs	r5, r0, #0
    10bc:	13866010 	orrne	r6, r6, #16
    10c0:	159d3040 	ldrne	r3, [sp, #64]	; 0x40
    10c4:	1a00000c 	bne	10fc <Java_com_example_hellojni_HelloJni_stringFromJNI+0x3f8>
    10c8:	e59d3048 	ldr	r3, [sp, #72]	; 0x48
    10cc:	e5843014 	str	r3, [r4, #20]
    10d0:	e1a0100b 	mov	r1, fp
    10d4:	e3a02e1e 	mov	r2, #480	; 0x1e0
    10d8:	e1a0000a 	mov	r0, sl
    10dc:	ebfffef0 	bl	ca4 <memcpy@plt>
    10e0:	e5943010 	ldr	r3, [r4, #16]
    10e4:	e1a00006 	mov	r0, r6
    10e8:	e1a01004 	mov	r1, r4
    10ec:	e1a0200a 	mov	r2, sl
    10f0:	e12fff33 	blx	r3
    10f4:	e59d3220 	ldr	r3, [sp, #544]	; 0x220
    10f8:	e1a07000 	mov	r7, r0
    10fc:	e58d304c 	str	r3, [sp, #76]	; 0x4c
    1100:	e58db000 	str	fp, [sp]
    1104:	e58d9004 	str	r9, [sp, #4]
    1108:	e3a00001 	mov	r0, #1
    110c:	e1a01006 	mov	r1, r6
    1110:	e1a02004 	mov	r2, r4
    1114:	e1a03004 	mov	r3, r4
    1118:	e12fff38 	blx	r8
    111c:	e3500000 	cmp	r0, #0
    1120:	1a00000f 	bne	1164 <Java_com_example_hellojni_HelloJni_stringFromJNI+0x460>
    1124:	e3550000 	cmp	r5, #0
    1128:	1a00000f 	bne	116c <Java_com_example_hellojni_HelloJni_stringFromJNI+0x468>
    112c:	e1a0000b 	mov	r0, fp
    1130:	e1a0100a 	mov	r1, sl
    1134:	e3a02e1e 	mov	r2, #480	; 0x1e0
    1138:	ebfffed9 	bl	ca4 <memcpy@plt>
    113c:	e3570008 	cmp	r7, #8
    1140:	e1a06005 	mov	r6, r5
    1144:	0affffd5 	beq	10a0 <Java_com_example_hellojni_HelloJni_stringFromJNI+0x39c>
    1148:	e3570007 	cmp	r7, #7
    114c:	1a000004 	bne	1164 <Java_com_example_hellojni_HelloJni_stringFromJNI+0x460>
    1150:	e1a00005 	mov	r0, r5
    1154:	e59d1048 	ldr	r1, [sp, #72]	; 0x48
    1158:	ebffffa2 	bl	fe8 <Java_com_example_hellojni_HelloJni_stringFromJNI+0x2e4>
    115c:	e28d000c 	add	r0, sp, #12
    1160:	eb0002b4 	bl	1c38 <__restore_core_regs>
    1164:	e3a00009 	mov	r0, #9
    1168:	ea000000 	b	1170 <Java_com_example_hellojni_HelloJni_stringFromJNI+0x46c>
    116c:	e1a00005 	mov	r0, r5
    1170:	e28ddff3 	add	sp, sp, #972	; 0x3cc
    1174:	e8bd8ff0 	pop	{r4, r5, r6, r7, r8, r9, sl, fp, pc}

00001178 <_Unwind_GetCFA>:
    1178:	e5900044 	ldr	r0, [r0, #68]	; 0x44
    117c:	e12fff1e 	bx	lr

00001180 <__gnu_Unwind_RaiseException>:
    1180:	e92d40f0 	push	{r4, r5, r6, r7, lr}
    1184:	e591303c 	ldr	r3, [r1, #60]	; 0x3c
    1188:	e281e004 	add	lr, r1, #4
    118c:	e5813040 	str	r3, [r1, #64]	; 0x40
    1190:	e1a05000 	mov	r5, r0
    1194:	e1a04001 	mov	r4, r1
    1198:	e8be000f 	ldm	lr!, {r0, r1, r2, r3}
    119c:	e24ddf79 	sub	sp, sp, #484	; 0x1e4
    11a0:	e28dc004 	add	ip, sp, #4
    11a4:	e8ac000f 	stmia	ip!, {r0, r1, r2, r3}
    11a8:	e8be000f 	ldm	lr!, {r0, r1, r2, r3}
    11ac:	e8ac000f 	stmia	ip!, {r0, r1, r2, r3}
    11b0:	e8be000f 	ldm	lr!, {r0, r1, r2, r3}
    11b4:	e8ac000f 	stmia	ip!, {r0, r1, r2, r3}
    11b8:	e89e000f 	ldm	lr, {r0, r1, r2, r3}
    11bc:	e28d6e1e 	add	r6, sp, #480	; 0x1e0
    11c0:	e88c000f 	stm	ip, {r0, r1, r2, r3}
    11c4:	e3e03000 	mvn	r3, #0
    11c8:	e52631e0 	str	r3, [r6, #-480]!	; 0xfffffe20
    11cc:	e1a00005 	mov	r0, r5
    11d0:	e59d1040 	ldr	r1, [sp, #64]	; 0x40
    11d4:	ebffff20 	bl	e5c <Java_com_example_hellojni_HelloJni_stringFromJNI+0x158>
    11d8:	e3500000 	cmp	r0, #0
    11dc:	1a00000d 	bne	1218 <__gnu_Unwind_RaiseException+0x98>
    11e0:	e5953010 	ldr	r3, [r5, #16]
    11e4:	e1a01005 	mov	r1, r5
    11e8:	e1a02006 	mov	r2, r6
    11ec:	e12fff33 	blx	r3
    11f0:	e3500008 	cmp	r0, #8
    11f4:	e1a07000 	mov	r7, r0
    11f8:	0afffff3 	beq	11cc <__gnu_Unwind_RaiseException+0x4c>
    11fc:	e1a00006 	mov	r0, r6
    1200:	ebffff56 	bl	f60 <Java_com_example_hellojni_HelloJni_stringFromJNI+0x25c>
    1204:	e3570006 	cmp	r7, #6
    1208:	1a000002 	bne	1218 <__gnu_Unwind_RaiseException+0x98>
    120c:	e1a00005 	mov	r0, r5
    1210:	e1a01004 	mov	r1, r4
    1214:	ebffff74 	bl	fec <Java_com_example_hellojni_HelloJni_stringFromJNI+0x2e8>
    1218:	e3a00009 	mov	r0, #9
    121c:	e28ddf79 	add	sp, sp, #484	; 0x1e4
    1220:	e8bd80f0 	pop	{r4, r5, r6, r7, pc}

00001224 <__gnu_Unwind_ForcedUnwind>:
    1224:	e5802018 	str	r2, [r0, #24]
    1228:	e593203c 	ldr	r2, [r3, #60]	; 0x3c
    122c:	e580100c 	str	r1, [r0, #12]
    1230:	e5832040 	str	r2, [r3, #64]	; 0x40
    1234:	e1a01003 	mov	r1, r3
    1238:	e3a02000 	mov	r2, #0
    123c:	eaffff83 	b	1050 <Java_com_example_hellojni_HelloJni_stringFromJNI+0x34c>

00001240 <__gnu_Unwind_Resume>:
    1240:	e92d4070 	push	{r4, r5, r6, lr}
    1244:	e590600c 	ldr	r6, [r0, #12]
    1248:	e5903014 	ldr	r3, [r0, #20]
    124c:	e3560000 	cmp	r6, #0
    1250:	e1a05000 	mov	r5, r0
    1254:	e1a04001 	mov	r4, r1
    1258:	e5813040 	str	r3, [r1, #64]	; 0x40
    125c:	0a000002 	beq	126c <__gnu_Unwind_Resume+0x2c>
    1260:	e3a02001 	mov	r2, #1
    1264:	ebffff79 	bl	1050 <Java_com_example_hellojni_HelloJni_stringFromJNI+0x34c>
    1268:	ea000010 	b	12b0 <__gnu_Unwind_Resume+0x70>
    126c:	e5903010 	ldr	r3, [r0, #16]
    1270:	e1a01005 	mov	r1, r5
    1274:	e3a00002 	mov	r0, #2
    1278:	e1a02004 	mov	r2, r4
    127c:	e12fff33 	blx	r3
    1280:	e3500007 	cmp	r0, #7
    1284:	0a000004 	beq	129c <__gnu_Unwind_Resume+0x5c>
    1288:	e3500008 	cmp	r0, #8
    128c:	1a000007 	bne	12b0 <__gnu_Unwind_Resume+0x70>
    1290:	e1a00005 	mov	r0, r5
    1294:	e1a01004 	mov	r1, r4
    1298:	ebffff53 	bl	fec <Java_com_example_hellojni_HelloJni_stringFromJNI+0x2e8>
    129c:	e1a00006 	mov	r0, r6
    12a0:	e5941040 	ldr	r1, [r4, #64]	; 0x40
    12a4:	ebffff4f 	bl	fe8 <Java_com_example_hellojni_HelloJni_stringFromJNI+0x2e4>
    12a8:	e2840004 	add	r0, r4, #4
    12ac:	eb000261 	bl	1c38 <__restore_core_regs>
    12b0:	ebfffe78 	bl	c98 <abort@plt>

000012b4 <__gnu_Unwind_Resume_or_Rethrow>:
    12b4:	e590200c 	ldr	r2, [r0, #12]
    12b8:	e3520000 	cmp	r2, #0
    12bc:	1a000000 	bne	12c4 <__gnu_Unwind_Resume_or_Rethrow+0x10>
    12c0:	eaffffae 	b	1180 <__gnu_Unwind_RaiseException>
    12c4:	e591203c 	ldr	r2, [r1, #60]	; 0x3c
    12c8:	e5812040 	str	r2, [r1, #64]	; 0x40
    12cc:	e3a02000 	mov	r2, #0
    12d0:	eaffff5e 	b	1050 <Java_com_example_hellojni_HelloJni_stringFromJNI+0x34c>

000012d4 <_Unwind_Complete>:
    12d4:	e12fff1e 	bx	lr

000012d8 <_Unwind_DeleteException>:
    12d8:	e5903008 	ldr	r3, [r0, #8]
    12dc:	e1a01000 	mov	r1, r0
    12e0:	e3530000 	cmp	r3, #0
    12e4:	012fff1e 	bxeq	lr
    12e8:	e3a00001 	mov	r0, #1
    12ec:	e12fff13 	bx	r3

000012f0 <_Unwind_VRS_Get>:
    12f0:	e3510004 	cmp	r1, #4
    12f4:	908ff101 	addls	pc, pc, r1, lsl #2
    12f8:	ea000011 	b	1344 <_Unwind_VRS_Get+0x54>
    12fc:	ea000003 	b	1310 <_Unwind_VRS_Get+0x20>
    1300:	ea00000d 	b	133c <_Unwind_VRS_Get+0x4c>
    1304:	ea00000e 	b	1344 <_Unwind_VRS_Get+0x54>
    1308:	ea00000b 	b	133c <_Unwind_VRS_Get+0x4c>
    130c:	ea00000a 	b	133c <_Unwind_VRS_Get+0x4c>
    1310:	e352000f 	cmp	r2, #15
    1314:	93530000 	cmpls	r3, #0
    1318:	13a03001 	movne	r3, #1
    131c:	03a03000 	moveq	r3, #0
    1320:	1a000007 	bne	1344 <_Unwind_VRS_Get+0x54>
    1324:	e0800102 	add	r0, r0, r2, lsl #2
    1328:	e59d2000 	ldr	r2, [sp]
    132c:	e5901004 	ldr	r1, [r0, #4]
    1330:	e5821000 	str	r1, [r2]
    1334:	e1a00003 	mov	r0, r3
    1338:	e12fff1e 	bx	lr
    133c:	e3a00001 	mov	r0, #1
    1340:	e12fff1e 	bx	lr
    1344:	e3a00002 	mov	r0, #2
    1348:	e12fff1e 	bx	lr
    134c:	e92d401f 	push	{r0, r1, r2, r3, r4, lr}
    1350:	e1a02001 	mov	r2, r1
    1354:	e28d300c 	add	r3, sp, #12
    1358:	e3a01000 	mov	r1, #0
    135c:	e58d3000 	str	r3, [sp]
    1360:	e1a03001 	mov	r3, r1
    1364:	ebffffe1 	bl	12f0 <_Unwind_VRS_Get>
    1368:	e59d000c 	ldr	r0, [sp, #12]
    136c:	e28dd014 	add	sp, sp, #20
    1370:	e49df004 	pop	{pc}		; (ldr pc, [sp], #4)

00001374 <_Unwind_VRS_Set>:
    1374:	e3510004 	cmp	r1, #4
    1378:	908ff101 	addls	pc, pc, r1, lsl #2
    137c:	ea000011 	b	13c8 <_Unwind_VRS_Set+0x54>
    1380:	ea000003 	b	1394 <_Unwind_VRS_Set+0x20>
    1384:	ea00000d 	b	13c0 <_Unwind_VRS_Set+0x4c>
    1388:	ea00000e 	b	13c8 <_Unwind_VRS_Set+0x54>
    138c:	ea00000b 	b	13c0 <_Unwind_VRS_Set+0x4c>
    1390:	ea00000a 	b	13c0 <_Unwind_VRS_Set+0x4c>
    1394:	e352000f 	cmp	r2, #15
    1398:	93530000 	cmpls	r3, #0
    139c:	13a03001 	movne	r3, #1
    13a0:	03a03000 	moveq	r3, #0
    13a4:	1a000007 	bne	13c8 <_Unwind_VRS_Set+0x54>
    13a8:	e59d1000 	ldr	r1, [sp]
    13ac:	e0800102 	add	r0, r0, r2, lsl #2
    13b0:	e5911000 	ldr	r1, [r1]
    13b4:	e5801004 	str	r1, [r0, #4]
    13b8:	e1a00003 	mov	r0, r3
    13bc:	e12fff1e 	bx	lr
    13c0:	e3a00001 	mov	r0, #1
    13c4:	e12fff1e 	bx	lr
    13c8:	e3a00002 	mov	r0, #2
    13cc:	e12fff1e 	bx	lr
    13d0:	e92d401f 	push	{r0, r1, r2, r3, r4, lr}
    13d4:	e1a0c001 	mov	ip, r1
    13d8:	e28d3010 	add	r3, sp, #16
    13dc:	e3a01000 	mov	r1, #0
    13e0:	e5232004 	str	r2, [r3, #-4]!
    13e4:	e1a0200c 	mov	r2, ip
    13e8:	e58d3000 	str	r3, [sp]
    13ec:	e1a03001 	mov	r3, r1
    13f0:	ebffffdf 	bl	1374 <_Unwind_VRS_Set>
    13f4:	e28dd014 	add	sp, sp, #20
    13f8:	e49df004 	pop	{pc}		; (ldr pc, [sp], #4)

000013fc <__gnu_Unwind_Backtrace>:
    13fc:	e592303c 	ldr	r3, [r2, #60]	; 0x3c
    1400:	e282c004 	add	ip, r2, #4
    1404:	e92d41f0 	push	{r4, r5, r6, r7, r8, lr}
    1408:	e5823040 	str	r3, [r2, #64]	; 0x40
    140c:	e1a07000 	mov	r7, r0
    1410:	e1a08001 	mov	r8, r1
    1414:	e8bc000f 	ldm	ip!, {r0, r1, r2, r3}
    1418:	e24ddf8e 	sub	sp, sp, #568	; 0x238
    141c:	e28de05c 	add	lr, sp, #92	; 0x5c
    1420:	e8ae000f 	stmia	lr!, {r0, r1, r2, r3}
    1424:	e8bc000f 	ldm	ip!, {r0, r1, r2, r3}
    1428:	e8ae000f 	stmia	lr!, {r0, r1, r2, r3}
    142c:	e8bc000f 	ldm	ip!, {r0, r1, r2, r3}
    1430:	e8ae000f 	stmia	lr!, {r0, r1, r2, r3}
    1434:	e89c000f 	ldm	ip, {r0, r1, r2, r3}
    1438:	e1a0600d 	mov	r6, sp
    143c:	e88e000f 	stm	lr, {r0, r1, r2, r3}
    1440:	e28d4058 	add	r4, sp, #88	; 0x58
    1444:	e3e03000 	mvn	r3, #0
    1448:	e58d3058 	str	r3, [sp, #88]	; 0x58
    144c:	e1a00006 	mov	r0, r6
    1450:	e59d1098 	ldr	r1, [sp, #152]	; 0x98
    1454:	ebfffe80 	bl	e5c <Java_com_example_hellojni_HelloJni_stringFromJNI+0x158>
    1458:	e3500000 	cmp	r0, #0
    145c:	0a000001 	beq	1468 <__gnu_Unwind_Backtrace+0x6c>
    1460:	e3a05009 	mov	r5, #9
    1464:	ea000011 	b	14b0 <__gnu_Unwind_Backtrace+0xb4>
    1468:	e1a00004 	mov	r0, r4
    146c:	e3a0100c 	mov	r1, #12
    1470:	e1a02006 	mov	r2, r6
    1474:	ebffffd5 	bl	13d0 <_Unwind_VRS_Set+0x5c>
    1478:	e1a00004 	mov	r0, r4
    147c:	e1a01008 	mov	r1, r8
    1480:	e12fff37 	blx	r7
    1484:	e3500000 	cmp	r0, #0
    1488:	1afffff4 	bne	1460 <__gnu_Unwind_Backtrace+0x64>
    148c:	e59d3010 	ldr	r3, [sp, #16]
    1490:	e3a00008 	mov	r0, #8
    1494:	e1a01006 	mov	r1, r6
    1498:	e1a02004 	mov	r2, r4
    149c:	e12fff33 	blx	r3
    14a0:	e2403005 	sub	r3, r0, #5
    14a4:	e3d33004 	bics	r3, r3, #4
    14a8:	e1a05000 	mov	r5, r0
    14ac:	1affffe6 	bne	144c <__gnu_Unwind_Backtrace+0x50>
    14b0:	e1a00004 	mov	r0, r4
    14b4:	ebfffea9 	bl	f60 <Java_com_example_hellojni_HelloJni_stringFromJNI+0x25c>
    14b8:	e1a00005 	mov	r0, r5
    14bc:	e28ddf8e 	add	sp, sp, #568	; 0x238
    14c0:	e8bd81f0 	pop	{r4, r5, r6, r7, r8, pc}
    14c4:	e92d4ff0 	push	{r4, r5, r6, r7, r8, r9, sl, fp, lr}
    14c8:	e1a07002 	mov	r7, r2
    14cc:	e591204c 	ldr	r2, [r1, #76]	; 0x4c
    14d0:	e24dd024 	sub	sp, sp, #36	; 0x24
    14d4:	e5924000 	ldr	r4, [r2]
    14d8:	e282c004 	add	ip, r2, #4
    14dc:	e2539000 	subs	r9, r3, #0
    14e0:	e1a05001 	mov	r5, r1
    14e4:	e2008003 	and	r8, r0, #3
    14e8:	e58d4014 	str	r4, [sp, #20]
    14ec:	e58dc018 	str	ip, [sp, #24]
    14f0:	1a000005 	bne	150c <__gnu_Unwind_Backtrace+0x110>
    14f4:	e1a04404 	lsl	r4, r4, #8
    14f8:	e3a03003 	mov	r3, #3
    14fc:	e58d4014 	str	r4, [sp, #20]
    1500:	e5cd901d 	strb	r9, [sp, #29]
    1504:	e5cd301c 	strb	r3, [sp, #28]
    1508:	ea000009 	b	1534 <__gnu_Unwind_Backtrace+0x138>
    150c:	e3590002 	cmp	r9, #2
    1510:	ca000007 	bgt	1534 <__gnu_Unwind_Backtrace+0x138>
    1514:	e1a03824 	lsr	r3, r4, #16
    1518:	e5cd301d 	strb	r3, [sp, #29]
    151c:	e20330ff 	and	r3, r3, #255	; 0xff
    1520:	e1a04804 	lsl	r4, r4, #16
    1524:	e3a02002 	mov	r2, #2
    1528:	e08cc103 	add	ip, ip, r3, lsl #2
    152c:	e58d4014 	str	r4, [sp, #20]
    1530:	e5cd201c 	strb	r2, [sp, #28]
    1534:	e5953050 	ldr	r3, [r5, #80]	; 0x50
    1538:	e3580002 	cmp	r8, #2
    153c:	0595c038 	ldreq	ip, [r5, #56]	; 0x38
    1540:	e2133001 	ands	r3, r3, #1
    1544:	1a0000b0 	bne	180c <__gnu_Unwind_Backtrace+0x410>
    1548:	e1a001a0 	lsr	r0, r0, #3
    154c:	e2200001 	eor	r0, r0, #1
    1550:	e58d3004 	str	r3, [sp, #4]
    1554:	e2003001 	and	r3, r0, #1
    1558:	e58d3008 	str	r3, [sp, #8]
    155c:	e59c4000 	ldr	r4, [ip]
    1560:	e3540000 	cmp	r4, #0
    1564:	0a0000aa 	beq	1814 <__gnu_Unwind_Backtrace+0x418>
    1568:	e3590002 	cmp	r9, #2
    156c:	059ca004 	ldreq	sl, [ip, #4]
    1570:	11dca0b2 	ldrhne	sl, [ip, #2]
    1574:	e5953048 	ldr	r3, [r5, #72]	; 0x48
    1578:	e3cab001 	bic	fp, sl, #1
    157c:	e1a00007 	mov	r0, r7
    1580:	e3a0100f 	mov	r1, #15
    1584:	028c6008 	addeq	r6, ip, #8
    1588:	11dc40b0 	ldrhne	r4, [ip]
    158c:	128c6004 	addne	r6, ip, #4
    1590:	e08bb003 	add	fp, fp, r3
    1594:	ebffff6c 	bl	134c <_Unwind_VRS_Get+0x5c>
    1598:	e15b0000 	cmp	fp, r0
    159c:	83a0c000 	movhi	ip, #0
    15a0:	8a000004 	bhi	15b8 <__gnu_Unwind_Backtrace+0x1bc>
    15a4:	e3c43001 	bic	r3, r4, #1
    15a8:	e08bb003 	add	fp, fp, r3
    15ac:	e150000b 	cmp	r0, fp
    15b0:	23a0c000 	movcs	ip, #0
    15b4:	33a0c001 	movcc	ip, #1
    15b8:	e20aa001 	and	sl, sl, #1
    15bc:	e2044001 	and	r4, r4, #1
    15c0:	e184408a 	orr	r4, r4, sl, lsl #1
    15c4:	e3540001 	cmp	r4, #1
    15c8:	0a000017 	beq	162c <__gnu_Unwind_Backtrace+0x230>
    15cc:	3a000002 	bcc	15dc <__gnu_Unwind_Backtrace+0x1e0>
    15d0:	e3540002 	cmp	r4, #2
    15d4:	0a000048 	beq	16fc <__gnu_Unwind_Backtrace+0x300>
    15d8:	ea0000a8 	b	1880 <__gnu_Unwind_Backtrace+0x484>
    15dc:	e3580000 	cmp	r8, #0
    15e0:	03a0c000 	moveq	ip, #0
    15e4:	120cc001 	andne	ip, ip, #1
    15e8:	e35c0000 	cmp	ip, #0
    15ec:	e286a004 	add	sl, r6, #4
    15f0:	0a00000b 	beq	1624 <__gnu_Unwind_Backtrace+0x228>
    15f4:	e1a00006 	mov	r0, r6
    15f8:	ebfffdd4 	bl	d50 <Java_com_example_hellojni_HelloJni_stringFromJNI+0x4c>
    15fc:	e585a038 	str	sl, [r5, #56]	; 0x38
    1600:	e1a04000 	mov	r4, r0
    1604:	e1a00005 	mov	r0, r5
    1608:	ebfffda8 	bl	cb0 <__cxa_begin_cleanup@plt>
    160c:	e3500000 	cmp	r0, #0
    1610:	0a00009a 	beq	1880 <__gnu_Unwind_Backtrace+0x484>
    1614:	e1a00007 	mov	r0, r7
    1618:	e3a0100f 	mov	r1, #15
    161c:	e1a02004 	mov	r2, r4
    1620:	ea000093 	b	1874 <__gnu_Unwind_Backtrace+0x478>
    1624:	e1a0c00a 	mov	ip, sl
    1628:	eaffffcb 	b	155c <__gnu_Unwind_Backtrace+0x160>
    162c:	e3580000 	cmp	r8, #0
    1630:	1a00001d 	bne	16ac <__gnu_Unwind_Backtrace+0x2b0>
    1634:	e35c0000 	cmp	ip, #0
    1638:	0a00002d 	beq	16f4 <__gnu_Unwind_Backtrace+0x2f8>
    163c:	e5963004 	ldr	r3, [r6, #4]
    1640:	e596a000 	ldr	sl, [r6]
    1644:	e3730002 	cmn	r3, #2
    1648:	e1a0afaa 	lsr	sl, sl, #31
    164c:	0a00008b 	beq	1880 <__gnu_Unwind_Backtrace+0x484>
    1650:	e2852058 	add	r2, r5, #88	; 0x58
    1654:	e3730001 	cmn	r3, #1
    1658:	e58d2010 	str	r2, [sp, #16]
    165c:	0a000008 	beq	1684 <__gnu_Unwind_Backtrace+0x288>
    1660:	e2860004 	add	r0, r6, #4
    1664:	ebfffe58 	bl	fcc <Java_com_example_hellojni_HelloJni_stringFromJNI+0x2c8>
    1668:	e1a0200a 	mov	r2, sl
    166c:	e28d3010 	add	r3, sp, #16
    1670:	e1a01000 	mov	r1, r0
    1674:	e1a00005 	mov	r0, r5
    1678:	ebfffd8f 	bl	cbc <__cxa_type_match@plt>
    167c:	e2504000 	subs	r4, r0, #0
    1680:	0a00001b 	beq	16f4 <__gnu_Unwind_Backtrace+0x2f8>
    1684:	e1a00007 	mov	r0, r7
    1688:	e3a0100d 	mov	r1, #13
    168c:	ebffff2e 	bl	134c <_Unwind_VRS_Get+0x5c>
    1690:	e3540002 	cmp	r4, #2
    1694:	e59d2010 	ldr	r2, [sp, #16]
    1698:	01a03005 	moveq	r3, r5
    169c:	11a03002 	movne	r3, r2
    16a0:	e5850020 	str	r0, [r5, #32]
    16a4:	05a3202c 	streq	r2, [r3, #44]!	; 0x2c
    16a8:	ea00007b 	b	189c <__gnu_Unwind_Backtrace+0x4a0>
    16ac:	e1a00007 	mov	r0, r7
    16b0:	e3a0100d 	mov	r1, #13
    16b4:	e5954020 	ldr	r4, [r5, #32]
    16b8:	ebffff23 	bl	134c <_Unwind_VRS_Get+0x5c>
    16bc:	e1540000 	cmp	r4, r0
    16c0:	1a00000b 	bne	16f4 <__gnu_Unwind_Backtrace+0x2f8>
    16c4:	e5953028 	ldr	r3, [r5, #40]	; 0x28
    16c8:	e1560003 	cmp	r6, r3
    16cc:	1a000008 	bne	16f4 <__gnu_Unwind_Backtrace+0x2f8>
    16d0:	e1a00006 	mov	r0, r6
    16d4:	ebfffd9d 	bl	d50 <Java_com_example_hellojni_HelloJni_stringFromJNI+0x4c>
    16d8:	e3a0100f 	mov	r1, #15
    16dc:	e1a02000 	mov	r2, r0
    16e0:	e1a00007 	mov	r0, r7
    16e4:	ebffff39 	bl	13d0 <_Unwind_VRS_Set+0x5c>
    16e8:	e1a00007 	mov	r0, r7
    16ec:	e3a01000 	mov	r1, #0
    16f0:	ea00003b 	b	17e4 <__gnu_Unwind_Backtrace+0x3e8>
    16f4:	e286c008 	add	ip, r6, #8
    16f8:	eaffff97 	b	155c <__gnu_Unwind_Backtrace+0x160>
    16fc:	e5964000 	ldr	r4, [r6]
    1700:	e3580000 	cmp	r8, #0
    1704:	e3c44102 	bic	r4, r4, #-2147483648	; 0x80000000
    1708:	1a000019 	bne	1774 <__gnu_Unwind_Backtrace+0x378>
    170c:	e35c0000 	cmp	ip, #0
    1710:	0a000037 	beq	17f4 <__gnu_Unwind_Backtrace+0x3f8>
    1714:	e59d3008 	ldr	r3, [sp, #8]
    1718:	e3540000 	cmp	r4, #0
    171c:	03833001 	orreq	r3, r3, #1
    1720:	e3530000 	cmp	r3, #0
    1724:	0a000032 	beq	17f4 <__gnu_Unwind_Backtrace+0x3f8>
    1728:	e1a0a008 	mov	sl, r8
    172c:	e285c058 	add	ip, r5, #88	; 0x58
    1730:	e28db010 	add	fp, sp, #16
    1734:	e15a0004 	cmp	sl, r4
    1738:	0a000052 	beq	1888 <__gnu_Unwind_Backtrace+0x48c>
    173c:	e28aa001 	add	sl, sl, #1
    1740:	e086010a 	add	r0, r6, sl, lsl #2
    1744:	e58dc010 	str	ip, [sp, #16]
    1748:	e58dc00c 	str	ip, [sp, #12]
    174c:	ebfffe1e 	bl	fcc <Java_com_example_hellojni_HelloJni_stringFromJNI+0x2c8>
    1750:	e3a02000 	mov	r2, #0
    1754:	e1a0300b 	mov	r3, fp
    1758:	e1a01000 	mov	r1, r0
    175c:	e1a00005 	mov	r0, r5
    1760:	ebfffd55 	bl	cbc <__cxa_type_match@plt>
    1764:	e59dc00c 	ldr	ip, [sp, #12]
    1768:	e3500000 	cmp	r0, #0
    176c:	0afffff0 	beq	1734 <__gnu_Unwind_Backtrace+0x338>
    1770:	ea00001f 	b	17f4 <__gnu_Unwind_Backtrace+0x3f8>
    1774:	e1a00007 	mov	r0, r7
    1778:	e3a0100d 	mov	r1, #13
    177c:	e595a020 	ldr	sl, [r5, #32]
    1780:	ebfffef1 	bl	134c <_Unwind_VRS_Get+0x5c>
    1784:	e15a0000 	cmp	sl, r0
    1788:	1a000019 	bne	17f4 <__gnu_Unwind_Backtrace+0x3f8>
    178c:	e5953028 	ldr	r3, [r5, #40]	; 0x28
    1790:	e1560003 	cmp	r6, r3
    1794:	1a000016 	bne	17f4 <__gnu_Unwind_Backtrace+0x3f8>
    1798:	e3a03004 	mov	r3, #4
    179c:	e3a0a000 	mov	sl, #0
    17a0:	e5853030 	str	r3, [r5, #48]	; 0x30
    17a4:	e0863003 	add	r3, r6, r3
    17a8:	e5854028 	str	r4, [r5, #40]	; 0x28
    17ac:	e585a02c 	str	sl, [r5, #44]	; 0x2c
    17b0:	e5853034 	str	r3, [r5, #52]	; 0x34
    17b4:	e5963000 	ldr	r3, [r6]
    17b8:	e153000a 	cmp	r3, sl
    17bc:	aa00000a 	bge	17ec <__gnu_Unwind_Backtrace+0x3f0>
    17c0:	e2840001 	add	r0, r4, #1
    17c4:	e0860100 	add	r0, r6, r0, lsl #2
    17c8:	ebfffd60 	bl	d50 <Java_com_example_hellojni_HelloJni_stringFromJNI+0x4c>
    17cc:	e3a0100f 	mov	r1, #15
    17d0:	e1a02000 	mov	r2, r0
    17d4:	e1a00007 	mov	r0, r7
    17d8:	ebfffefc 	bl	13d0 <_Unwind_VRS_Set+0x5c>
    17dc:	e1a00007 	mov	r0, r7
    17e0:	e1a0100a 	mov	r1, sl
    17e4:	e1a02005 	mov	r2, r5
    17e8:	ea000021 	b	1874 <__gnu_Unwind_Backtrace+0x478>
    17ec:	e3a03001 	mov	r3, #1
    17f0:	e58d3004 	str	r3, [sp, #4]
    17f4:	e5963000 	ldr	r3, [r6]
    17f8:	e284c001 	add	ip, r4, #1
    17fc:	e3530000 	cmp	r3, #0
    1800:	b2866004 	addlt	r6, r6, #4
    1804:	e086c10c 	add	ip, r6, ip, lsl #2
    1808:	eaffff53 	b	155c <__gnu_Unwind_Backtrace+0x160>
    180c:	e3a03000 	mov	r3, #0
    1810:	e58d3004 	str	r3, [sp, #4]
    1814:	e3590002 	cmp	r9, #2
    1818:	da000001 	ble	1824 <__gnu_Unwind_Backtrace+0x428>
    181c:	ebfffdef 	bl	fe0 <Java_com_example_hellojni_HelloJni_stringFromJNI+0x2dc>
    1820:	ea000002 	b	1830 <__gnu_Unwind_Backtrace+0x434>
    1824:	e1a00007 	mov	r0, r7
    1828:	e28d1014 	add	r1, sp, #20
    182c:	eb00018e 	bl	1e6c <__gnu_unwind_execute>
    1830:	e3500000 	cmp	r0, #0
    1834:	1a000011 	bne	1880 <__gnu_Unwind_Backtrace+0x484>
    1838:	e59d3004 	ldr	r3, [sp, #4]
    183c:	e3530000 	cmp	r3, #0
    1840:	03a00008 	moveq	r0, #8
    1844:	0a000017 	beq	18a8 <__gnu_Unwind_Backtrace+0x4ac>
    1848:	e3a0100f 	mov	r1, #15
    184c:	e1a00007 	mov	r0, r7
    1850:	ebfffebd 	bl	134c <_Unwind_VRS_Get+0x5c>
    1854:	e3a0100e 	mov	r1, #14
    1858:	e1a02000 	mov	r2, r0
    185c:	e1a00007 	mov	r0, r7
    1860:	ebfffeda 	bl	13d0 <_Unwind_VRS_Set+0x5c>
    1864:	e59f2044 	ldr	r2, [pc, #68]	; 18b0 <__gnu_Unwind_Backtrace+0x4b4>
    1868:	e1a00007 	mov	r0, r7
    186c:	e79f2002 	ldr	r2, [pc, r2]
    1870:	e3a0100f 	mov	r1, #15
    1874:	ebfffed5 	bl	13d0 <_Unwind_VRS_Set+0x5c>
    1878:	e3a00007 	mov	r0, #7
    187c:	ea000009 	b	18a8 <__gnu_Unwind_Backtrace+0x4ac>
    1880:	e3a00009 	mov	r0, #9
    1884:	ea000007 	b	18a8 <__gnu_Unwind_Backtrace+0x4ac>
    1888:	e1a00007 	mov	r0, r7
    188c:	e3a0100d 	mov	r1, #13
    1890:	ebfffead 	bl	134c <_Unwind_VRS_Get+0x5c>
    1894:	e59d3010 	ldr	r3, [sp, #16]
    1898:	e5850020 	str	r0, [r5, #32]
    189c:	e3a00006 	mov	r0, #6
    18a0:	e5853024 	str	r3, [r5, #36]	; 0x24
    18a4:	e5856028 	str	r6, [r5, #40]	; 0x28
    18a8:	e28dd024 	add	sp, sp, #36	; 0x24
    18ac:	e8bd8ff0 	pop	{r4, r5, r6, r7, r8, r9, sl, fp, pc}
    18b0:	00002760 	andeq	r2, r0, r0, ror #14

000018b4 <__aeabi_unwind_cpp_pr0>:
    18b4:	e3a03000 	mov	r3, #0
    18b8:	eaffff01 	b	14c4 <__gnu_Unwind_Backtrace+0xc8>

000018bc <__aeabi_unwind_cpp_pr1>:
    18bc:	e3a03001 	mov	r3, #1
    18c0:	eafffeff 	b	14c4 <__gnu_Unwind_Backtrace+0xc8>

000018c4 <__aeabi_unwind_cpp_pr2>:
    18c4:	e3a03002 	mov	r3, #2
    18c8:	eafffefd 	b	14c4 <__gnu_Unwind_Backtrace+0xc8>

000018cc <_Unwind_VRS_Pop>:
    18cc:	e92d43f0 	push	{r4, r5, r6, r7, r8, r9, lr}
    18d0:	e1a05000 	mov	r5, r0
    18d4:	e24ddf43 	sub	sp, sp, #268	; 0x10c
    18d8:	e1a04002 	mov	r4, r2
    18dc:	e3510004 	cmp	r1, #4
    18e0:	908ff101 	addls	pc, pc, r1, lsl #2
    18e4:	ea0000bc 	b	1bdc <_Unwind_VRS_Pop+0x310>
    18e8:	ea000003 	b	18fc <_Unwind_VRS_Pop+0x30>
    18ec:	ea000015 	b	1948 <_Unwind_VRS_Pop+0x7c>
    18f0:	ea0000b9 	b	1bdc <_Unwind_VRS_Pop+0x310>
    18f4:	ea000081 	b	1b00 <_Unwind_VRS_Pop+0x234>
    18f8:	ea00009d 	b	1b74 <_Unwind_VRS_Pop+0x2a8>
    18fc:	e3530000 	cmp	r3, #0
    1900:	1a0000b5 	bne	1bdc <_Unwind_VRS_Pop+0x310>
    1904:	e1a01802 	lsl	r1, r2, #16
    1908:	e3a03001 	mov	r3, #1
    190c:	e5902038 	ldr	r2, [r0, #56]	; 0x38
    1910:	e1a01821 	lsr	r1, r1, #16
    1914:	e1a00003 	mov	r0, r3
    1918:	e243c001 	sub	ip, r3, #1
    191c:	e011cc10 	ands	ip, r1, r0, lsl ip
    1920:	1592c000 	ldrne	ip, [r2]
    1924:	1785c103 	strne	ip, [r5, r3, lsl #2]
    1928:	e2833001 	add	r3, r3, #1
    192c:	12822004 	addne	r2, r2, #4
    1930:	e3530011 	cmp	r3, #17
    1934:	1afffff7 	bne	1918 <_Unwind_VRS_Pop+0x4c>
    1938:	e2140a02 	ands	r0, r4, #8192	; 0x2000
    193c:	05852038 	streq	r2, [r5, #56]	; 0x38
    1940:	0a0000ba 	beq	1c30 <_Unwind_VRS_Pop+0x364>
    1944:	ea0000a6 	b	1be4 <_Unwind_VRS_Pop+0x318>
    1948:	e3c32004 	bic	r2, r3, #4
    194c:	e3520001 	cmp	r2, #1
    1950:	1a0000a1 	bne	1bdc <_Unwind_VRS_Pop+0x310>
    1954:	e1a07824 	lsr	r7, r4, #16
    1958:	e1a04804 	lsl	r4, r4, #16
    195c:	e1a04824 	lsr	r4, r4, #16
    1960:	e3530001 	cmp	r3, #1
    1964:	e0846007 	add	r6, r4, r7
    1968:	1a000006 	bne	1988 <_Unwind_VRS_Pop+0xbc>
    196c:	e3560010 	cmp	r6, #16
    1970:	8a000099 	bhi	1bdc <_Unwind_VRS_Pop+0x310>
    1974:	e357000f 	cmp	r7, #15
    1978:	91a08003 	movls	r8, r3
    197c:	93a06000 	movls	r6, #0
    1980:	8a000095 	bhi	1bdc <_Unwind_VRS_Pop+0x310>
    1984:	ea000005 	b	19a0 <_Unwind_VRS_Pop+0xd4>
    1988:	e3560020 	cmp	r6, #32
    198c:	8a000092 	bhi	1bdc <_Unwind_VRS_Pop+0x310>
    1990:	e357000f 	cmp	r7, #15
    1994:	9a000094 	bls	1bec <_Unwind_VRS_Pop+0x320>
    1998:	e1a06004 	mov	r6, r4
    199c:	e3a08000 	mov	r8, #0
    19a0:	e2969000 	adds	r9, r6, #0
    19a4:	13a09001 	movne	r9, #1
    19a8:	e3530005 	cmp	r3, #5
    19ac:	13560000 	cmpne	r6, #0
    19b0:	1a000089 	bne	1bdc <_Unwind_VRS_Pop+0x310>
    19b4:	e357000f 	cmp	r7, #15
    19b8:	8a000012 	bhi	1a08 <_Unwind_VRS_Pop+0x13c>
    19bc:	e5952000 	ldr	r2, [r5]
    19c0:	e3120001 	tst	r2, #1
    19c4:	0a00000f 	beq	1a08 <_Unwind_VRS_Pop+0x13c>
    19c8:	e3c21001 	bic	r1, r2, #1
    19cc:	e1a00005 	mov	r0, r5
    19d0:	e3530005 	cmp	r3, #5
    19d4:	e4801048 	str	r1, [r0], #72	; 0x48
    19d8:	1a000007 	bne	19fc <_Unwind_VRS_Pop+0x130>
    19dc:	e3811002 	orr	r1, r1, #2
    19e0:	e5851000 	str	r1, [r5]
    19e4:	eb00009e 	bl	1c64 <__gnu_Unwind_Save_VFP_D>
    19e8:	e3590000 	cmp	r9, #0
    19ec:	1a000007 	bne	1a10 <_Unwind_VRS_Pop+0x144>
    19f0:	e28d0080 	add	r0, sp, #128	; 0x80
    19f4:	eb00009a 	bl	1c64 <__gnu_Unwind_Save_VFP_D>
    19f8:	ea00000f 	b	1a3c <_Unwind_VRS_Pop+0x170>
    19fc:	e3c22003 	bic	r2, r2, #3
    1a00:	e5852000 	str	r2, [r5]
    1a04:	eb000092 	bl	1c54 <__gnu_Unwind_Save_VFP>
    1a08:	e3590000 	cmp	r9, #0
    1a0c:	0a00007c 	beq	1c04 <_Unwind_VRS_Pop+0x338>
    1a10:	e5953000 	ldr	r3, [r5]
    1a14:	e3130004 	tst	r3, #4
    1a18:	0a000003 	beq	1a2c <_Unwind_VRS_Pop+0x160>
    1a1c:	e3c33004 	bic	r3, r3, #4
    1a20:	e1a00005 	mov	r0, r5
    1a24:	e48030d0 	str	r3, [r0], #208	; 0xd0
    1a28:	eb000091 	bl	1c74 <__gnu_Unwind_Save_VFP_D_16_to_31>
    1a2c:	e3580000 	cmp	r8, #0
    1a30:	1a000078 	bne	1c18 <_Unwind_VRS_Pop+0x34c>
    1a34:	e357000f 	cmp	r7, #15
    1a38:	9affffec 	bls	19f0 <_Unwind_VRS_Pop+0x124>
    1a3c:	e3590000 	cmp	r9, #0
    1a40:	0a000002 	beq	1a50 <_Unwind_VRS_Pop+0x184>
    1a44:	e1a0000d 	mov	r0, sp
    1a48:	eb000089 	bl	1c74 <__gnu_Unwind_Save_VFP_D_16_to_31>
    1a4c:	e2674010 	rsb	r4, r7, #16
    1a50:	e5952038 	ldr	r2, [r5, #56]	; 0x38
    1a54:	e3540000 	cmp	r4, #0
    1a58:	e1a03002 	mov	r3, r2
    1a5c:	da000009 	ble	1a88 <_Unwind_VRS_Pop+0x1bc>
    1a60:	e28d1080 	add	r1, sp, #128	; 0x80
    1a64:	e0811187 	add	r1, r1, r7, lsl #3
    1a68:	e1a04084 	lsl	r4, r4, #1
    1a6c:	e3a03000 	mov	r3, #0
    1a70:	e1530004 	cmp	r3, r4
    1a74:	17920103 	ldrne	r0, [r2, r3, lsl #2]
    1a78:	17810103 	strne	r0, [r1, r3, lsl #2]
    1a7c:	12833001 	addne	r3, r3, #1
    1a80:	1afffffa 	bne	1a70 <_Unwind_VRS_Pop+0x1a4>
    1a84:	e0823103 	add	r3, r2, r3, lsl #2
    1a88:	e3590000 	cmp	r9, #0
    1a8c:	0a00000a 	beq	1abc <_Unwind_VRS_Pop+0x1f0>
    1a90:	e3570010 	cmp	r7, #16
    1a94:	21a04007 	movcs	r4, r7
    1a98:	33a04010 	movcc	r4, #16
    1a9c:	e28d2f42 	add	r2, sp, #264	; 0x108
    1aa0:	e0824184 	add	r4, r2, r4, lsl #3
    1aa4:	e2444f63 	sub	r4, r4, #396	; 0x18c
    1aa8:	e0836186 	add	r6, r3, r6, lsl #3
    1aac:	e1530006 	cmp	r3, r6
    1ab0:	14932004 	ldrne	r2, [r3], #4
    1ab4:	15a42004 	strne	r2, [r4, #4]!
    1ab8:	1afffffb 	bne	1aac <_Unwind_VRS_Pop+0x1e0>
    1abc:	e3580000 	cmp	r8, #0
    1ac0:	12833004 	addne	r3, r3, #4
    1ac4:	e3580000 	cmp	r8, #0
    1ac8:	e5853038 	str	r3, [r5, #56]	; 0x38
    1acc:	0a000002 	beq	1adc <_Unwind_VRS_Pop+0x210>
    1ad0:	e28d0080 	add	r0, sp, #128	; 0x80
    1ad4:	eb00005c 	bl	1c4c <__gnu_Unwind_Restore_VFP>
    1ad8:	ea000041 	b	1be4 <_Unwind_VRS_Pop+0x318>
    1adc:	e357000f 	cmp	r7, #15
    1ae0:	8a000001 	bhi	1aec <_Unwind_VRS_Pop+0x220>
    1ae4:	e28d0080 	add	r0, sp, #128	; 0x80
    1ae8:	eb00005b 	bl	1c5c <__gnu_Unwind_Restore_VFP_D>
    1aec:	e3590000 	cmp	r9, #0
    1af0:	0a00003b 	beq	1be4 <_Unwind_VRS_Pop+0x318>
    1af4:	e1a0000d 	mov	r0, sp
    1af8:	eb00005b 	bl	1c6c <__gnu_Unwind_Restore_VFP_D_16_to_31>
    1afc:	ea000038 	b	1be4 <_Unwind_VRS_Pop+0x318>
    1b00:	e3530003 	cmp	r3, #3
    1b04:	1a000034 	bne	1bdc <_Unwind_VRS_Pop+0x310>
    1b08:	e1a07802 	lsl	r7, r2, #16
    1b0c:	e1a06822 	lsr	r6, r2, #16
    1b10:	e1a07827 	lsr	r7, r7, #16
    1b14:	e0873006 	add	r3, r7, r6
    1b18:	e3530010 	cmp	r3, #16
    1b1c:	8a00002e 	bhi	1bdc <_Unwind_VRS_Pop+0x310>
    1b20:	e5903000 	ldr	r3, [r0]
    1b24:	e3130008 	tst	r3, #8
    1b28:	0a000002 	beq	1b38 <_Unwind_VRS_Pop+0x26c>
    1b2c:	e3c33008 	bic	r3, r3, #8
    1b30:	e4803150 	str	r3, [r0], #336	; 0x150
    1b34:	eb000061 	bl	1cc0 <__gnu_Unwind_Save_WMMXD>
    1b38:	e28d8080 	add	r8, sp, #128	; 0x80
    1b3c:	e1a00008 	mov	r0, r8
    1b40:	eb00005e 	bl	1cc0 <__gnu_Unwind_Save_WMMXD>
    1b44:	e5954038 	ldr	r4, [r5, #56]	; 0x38
    1b48:	e0886186 	add	r6, r8, r6, lsl #3
    1b4c:	e2466004 	sub	r6, r6, #4
    1b50:	e0847187 	add	r7, r4, r7, lsl #3
    1b54:	e1540007 	cmp	r4, r7
    1b58:	14943004 	ldrne	r3, [r4], #4
    1b5c:	15a63004 	strne	r3, [r6, #4]!
    1b60:	1afffffb 	bne	1b54 <_Unwind_VRS_Pop+0x288>
    1b64:	e5854038 	str	r4, [r5, #56]	; 0x38
    1b68:	e1a00008 	mov	r0, r8
    1b6c:	eb000042 	bl	1c7c <__gnu_Unwind_Restore_WMMXD>
    1b70:	ea00001b 	b	1be4 <_Unwind_VRS_Pop+0x318>
    1b74:	e3520010 	cmp	r2, #16
    1b78:	93530000 	cmpls	r3, #0
    1b7c:	1a000016 	bne	1bdc <_Unwind_VRS_Pop+0x310>
    1b80:	e5903000 	ldr	r3, [r0]
    1b84:	e3130010 	tst	r3, #16
    1b88:	0a000002 	beq	1b98 <_Unwind_VRS_Pop+0x2cc>
    1b8c:	e3c33010 	bic	r3, r3, #16
    1b90:	e48031d0 	str	r3, [r0], #464	; 0x1d0
    1b94:	eb00005f 	bl	1d18 <__gnu_Unwind_Save_WMMXC>
    1b98:	e28d6080 	add	r6, sp, #128	; 0x80
    1b9c:	e1a00006 	mov	r0, r6
    1ba0:	eb00005c 	bl	1d18 <__gnu_Unwind_Save_WMMXC>
    1ba4:	e5952038 	ldr	r2, [r5, #56]	; 0x38
    1ba8:	e3a03000 	mov	r3, #0
    1bac:	e3a01001 	mov	r1, #1
    1bb0:	e0140311 	ands	r0, r4, r1, lsl r3
    1bb4:	15920000 	ldrne	r0, [r2]
    1bb8:	17860103 	strne	r0, [r6, r3, lsl #2]
    1bbc:	e2833001 	add	r3, r3, #1
    1bc0:	12822004 	addne	r2, r2, #4
    1bc4:	e3530004 	cmp	r3, #4
    1bc8:	1afffff8 	bne	1bb0 <_Unwind_VRS_Pop+0x2e4>
    1bcc:	e5852038 	str	r2, [r5, #56]	; 0x38
    1bd0:	e1a00006 	mov	r0, r6
    1bd4:	eb00004a 	bl	1d04 <__gnu_Unwind_Restore_WMMXC>
    1bd8:	ea000001 	b	1be4 <_Unwind_VRS_Pop+0x318>
    1bdc:	e3a00002 	mov	r0, #2
    1be0:	ea000012 	b	1c30 <_Unwind_VRS_Pop+0x364>
    1be4:	e3a00000 	mov	r0, #0
    1be8:	ea000010 	b	1c30 <_Unwind_VRS_Pop+0x364>
    1bec:	e3560010 	cmp	r6, #16
    1bf0:	93a08000 	movls	r8, #0
    1bf4:	91a06008 	movls	r6, r8
    1bf8:	9affff68 	bls	19a0 <_Unwind_VRS_Pop+0xd4>
    1bfc:	e2466010 	sub	r6, r6, #16
    1c00:	eaffff65 	b	199c <_Unwind_VRS_Pop+0xd0>
    1c04:	e3580000 	cmp	r8, #0
    1c08:	0a000005 	beq	1c24 <_Unwind_VRS_Pop+0x358>
    1c0c:	e28d0080 	add	r0, sp, #128	; 0x80
    1c10:	eb00000f 	bl	1c54 <__gnu_Unwind_Save_VFP>
    1c14:	eaffff8d 	b	1a50 <_Unwind_VRS_Pop+0x184>
    1c18:	e28d0080 	add	r0, sp, #128	; 0x80
    1c1c:	eb00000c 	bl	1c54 <__gnu_Unwind_Save_VFP>
    1c20:	eaffff89 	b	1a4c <_Unwind_VRS_Pop+0x180>
    1c24:	e357000f 	cmp	r7, #15
    1c28:	8affff88 	bhi	1a50 <_Unwind_VRS_Pop+0x184>
    1c2c:	eaffff6f 	b	19f0 <_Unwind_VRS_Pop+0x124>
    1c30:	e28ddf43 	add	sp, sp, #268	; 0x10c
    1c34:	e8bd83f0 	pop	{r4, r5, r6, r7, r8, r9, pc}

00001c38 <__restore_core_regs>:
    1c38:	e2801034 	add	r1, r0, #52	; 0x34
    1c3c:	e8910038 	ldm	r1, {r3, r4, r5}
    1c40:	e92d0038 	push	{r3, r4, r5}
    1c44:	e8900fff 	ldm	r0, {r0, r1, r2, r3, r4, r5, r6, r7, r8, r9, sl, fp}
    1c48:	e89de000 	ldm	sp, {sp, lr, pc}

00001c4c <__gnu_Unwind_Restore_VFP>:
    1c4c:	ec900b21 	fldmiax	r0, {d0-d15}	;@ Deprecated
    1c50:	e12fff1e 	bx	lr

00001c54 <__gnu_Unwind_Save_VFP>:
    1c54:	ec800b21 	fstmiax	r0, {d0-d15}	;@ Deprecated
    1c58:	e12fff1e 	bx	lr

00001c5c <__gnu_Unwind_Restore_VFP_D>:
    1c5c:	ec900b20 	vldmia	r0, {d0-d15}
    1c60:	e12fff1e 	bx	lr

00001c64 <__gnu_Unwind_Save_VFP_D>:
    1c64:	ec800b20 	vstmia	r0, {d0-d15}
    1c68:	e12fff1e 	bx	lr

00001c6c <__gnu_Unwind_Restore_VFP_D_16_to_31>:
    1c6c:	ecd00b20 	vldmia	r0, {d16-d31}
    1c70:	e12fff1e 	bx	lr

00001c74 <__gnu_Unwind_Save_VFP_D_16_to_31>:
    1c74:	ecc00b20 	vstmia	r0, {d16-d31}
    1c78:	e12fff1e 	bx	lr

00001c7c <__gnu_Unwind_Restore_WMMXD>:
    1c7c:	ecf00102 	ldfe	f0, [r0], #8
    1c80:	ecf01102 	ldfe	f1, [r0], #8
    1c84:	ecf02102 	ldfe	f2, [r0], #8
    1c88:	ecf03102 	ldfe	f3, [r0], #8
    1c8c:	ecf04102 	ldfe	f4, [r0], #8
    1c90:	ecf05102 	ldfe	f5, [r0], #8
    1c94:	ecf06102 	ldfe	f6, [r0], #8
    1c98:	ecf07102 	ldfe	f7, [r0], #8
    1c9c:	ecf08102 	ldfp	f0, [r0], #8
    1ca0:	ecf09102 	ldfp	f1, [r0], #8
    1ca4:	ecf0a102 	ldfp	f2, [r0], #8
    1ca8:	ecf0b102 	ldfp	f3, [r0], #8
    1cac:	ecf0c102 	ldfp	f4, [r0], #8
    1cb0:	ecf0d102 	ldfp	f5, [r0], #8
    1cb4:	ecf0e102 	ldfp	f6, [r0], #8
    1cb8:	ecf0f102 	ldfp	f7, [r0], #8
    1cbc:	e12fff1e 	bx	lr

00001cc0 <__gnu_Unwind_Save_WMMXD>:
    1cc0:	ece00102 	stfe	f0, [r0], #8
    1cc4:	ece01102 	stfe	f1, [r0], #8
    1cc8:	ece02102 	stfe	f2, [r0], #8
    1ccc:	ece03102 	stfe	f3, [r0], #8
    1cd0:	ece04102 	stfe	f4, [r0], #8
    1cd4:	ece05102 	stfe	f5, [r0], #8
    1cd8:	ece06102 	stfe	f6, [r0], #8
    1cdc:	ece07102 	stfe	f7, [r0], #8
    1ce0:	ece08102 	stfp	f0, [r0], #8
    1ce4:	ece09102 	stfp	f1, [r0], #8
    1ce8:	ece0a102 	stfp	f2, [r0], #8
    1cec:	ece0b102 	stfp	f3, [r0], #8
    1cf0:	ece0c102 	stfp	f4, [r0], #8
    1cf4:	ece0d102 	stfp	f5, [r0], #8
    1cf8:	ece0e102 	stfp	f6, [r0], #8
    1cfc:	ece0f102 	stfp	f7, [r0], #8
    1d00:	e12fff1e 	bx	lr

00001d04 <__gnu_Unwind_Restore_WMMXC>:
    1d04:	fcb08101 	ldc2	1, cr8, [r0], #4
    1d08:	fcb09101 	ldc2	1, cr9, [r0], #4
    1d0c:	fcb0a101 	ldc2	1, cr10, [r0], #4
    1d10:	fcb0b101 	ldc2	1, cr11, [r0], #4
    1d14:	e12fff1e 	bx	lr

00001d18 <__gnu_Unwind_Save_WMMXC>:
    1d18:	fca08101 	stc2	1, cr8, [r0], #4
    1d1c:	fca09101 	stc2	1, cr9, [r0], #4
    1d20:	fca0a101 	stc2	1, cr10, [r0], #4
    1d24:	fca0b101 	stc2	1, cr11, [r0], #4
    1d28:	e12fff1e 	bx	lr

00001d2c <_Unwind_RaiseException>:
    1d2c:	e92de000 	push	{sp, lr, pc}
    1d30:	e92d1fff 	push	{r0, r1, r2, r3, r4, r5, r6, r7, r8, r9, sl, fp, ip}
    1d34:	e3a03000 	mov	r3, #0
    1d38:	e92d000c 	push	{r2, r3}
    1d3c:	e28d1004 	add	r1, sp, #4
    1d40:	ebfffd0e 	bl	1180 <__gnu_Unwind_RaiseException>
    1d44:	e59de040 	ldr	lr, [sp, #64]	; 0x40
    1d48:	e28dd048 	add	sp, sp, #72	; 0x48
    1d4c:	e12fff1e 	bx	lr

00001d50 <_Unwind_Resume>:
    1d50:	e92de000 	push	{sp, lr, pc}
    1d54:	e92d1fff 	push	{r0, r1, r2, r3, r4, r5, r6, r7, r8, r9, sl, fp, ip}
    1d58:	e3a03000 	mov	r3, #0
    1d5c:	e92d000c 	push	{r2, r3}
    1d60:	e28d1004 	add	r1, sp, #4
    1d64:	ebfffd35 	bl	1240 <__gnu_Unwind_Resume>
    1d68:	e59de040 	ldr	lr, [sp, #64]	; 0x40
    1d6c:	e28dd048 	add	sp, sp, #72	; 0x48
    1d70:	e12fff1e 	bx	lr

00001d74 <_Unwind_Resume_or_Rethrow>:
    1d74:	e92de000 	push	{sp, lr, pc}
    1d78:	e92d1fff 	push	{r0, r1, r2, r3, r4, r5, r6, r7, r8, r9, sl, fp, ip}
    1d7c:	e3a03000 	mov	r3, #0
    1d80:	e92d000c 	push	{r2, r3}
    1d84:	e28d1004 	add	r1, sp, #4
    1d88:	ebfffd49 	bl	12b4 <__gnu_Unwind_Resume_or_Rethrow>
    1d8c:	e59de040 	ldr	lr, [sp, #64]	; 0x40
    1d90:	e28dd048 	add	sp, sp, #72	; 0x48
    1d94:	e12fff1e 	bx	lr

00001d98 <_Unwind_ForcedUnwind>:
    1d98:	e92de000 	push	{sp, lr, pc}
    1d9c:	e92d1fff 	push	{r0, r1, r2, r3, r4, r5, r6, r7, r8, r9, sl, fp, ip}
    1da0:	e3a03000 	mov	r3, #0
    1da4:	e92d000c 	push	{r2, r3}
    1da8:	e28d3004 	add	r3, sp, #4
    1dac:	ebfffd1c 	bl	1224 <__gnu_Unwind_ForcedUnwind>
    1db0:	e59de040 	ldr	lr, [sp, #64]	; 0x40
    1db4:	e28dd048 	add	sp, sp, #72	; 0x48
    1db8:	e12fff1e 	bx	lr

00001dbc <_Unwind_Backtrace>:
    1dbc:	e92de000 	push	{sp, lr, pc}
    1dc0:	e92d1fff 	push	{r0, r1, r2, r3, r4, r5, r6, r7, r8, r9, sl, fp, ip}
    1dc4:	e3a03000 	mov	r3, #0
    1dc8:	e92d000c 	push	{r2, r3}
    1dcc:	e28d2004 	add	r2, sp, #4
    1dd0:	ebfffd89 	bl	13fc <__gnu_Unwind_Backtrace>
    1dd4:	e59de040 	ldr	lr, [sp, #64]	; 0x40
    1dd8:	e28dd048 	add	sp, sp, #72	; 0x48
    1ddc:	e12fff1e 	bx	lr
    1de0:	e5d03008 	ldrb	r3, [r0, #8]
    1de4:	e3530000 	cmp	r3, #0
    1de8:	1a00000b 	bne	1e1c <_Unwind_Backtrace+0x60>
    1dec:	e5d03009 	ldrb	r3, [r0, #9]
    1df0:	e3530000 	cmp	r3, #0
    1df4:	0a00000f 	beq	1e38 <_Unwind_Backtrace+0x7c>
    1df8:	e2433001 	sub	r3, r3, #1
    1dfc:	e5c03009 	strb	r3, [r0, #9]
    1e00:	e5903004 	ldr	r3, [r0, #4]
    1e04:	e2832004 	add	r2, r3, #4
    1e08:	e5933000 	ldr	r3, [r3]
    1e0c:	e5803000 	str	r3, [r0]
    1e10:	e5802004 	str	r2, [r0, #4]
    1e14:	e3a03003 	mov	r3, #3
    1e18:	ea000000 	b	1e20 <_Unwind_Backtrace+0x64>
    1e1c:	e2433001 	sub	r3, r3, #1
    1e20:	e5c03008 	strb	r3, [r0, #8]
    1e24:	e5903000 	ldr	r3, [r0]
    1e28:	e1a02403 	lsl	r2, r3, #8
    1e2c:	e5802000 	str	r2, [r0]
    1e30:	e1a00c23 	lsr	r0, r3, #24
    1e34:	e12fff1e 	bx	lr
    1e38:	e3a000b0 	mov	r0, #176	; 0xb0
    1e3c:	e12fff1e 	bx	lr
    1e40:	e92d401f 	push	{r0, r1, r2, r3, r4, lr}
    1e44:	e3a01000 	mov	r1, #0
    1e48:	e28d300c 	add	r3, sp, #12
    1e4c:	e58d3000 	str	r3, [sp]
    1e50:	e3a0200c 	mov	r2, #12
    1e54:	e1a03001 	mov	r3, r1
    1e58:	ebfffd24 	bl	12f0 <_Unwind_VRS_Get>
    1e5c:	e59d000c 	ldr	r0, [sp, #12]
    1e60:	e28dd014 	add	sp, sp, #20
    1e64:	e49df004 	pop	{pc}		; (ldr pc, [sp], #4)
    1e68:	eafffff4 	b	1e40 <_Unwind_Backtrace+0x84>

00001e6c <__gnu_unwind_execute>:
    1e6c:	e92d47ff 	push	{r0, r1, r2, r3, r4, r5, r6, r7, r8, r9, sl, lr}
    1e70:	e1a05000 	mov	r5, r0
    1e74:	e1a07001 	mov	r7, r1
    1e78:	e3a06000 	mov	r6, #0
    1e7c:	e28d800c 	add	r8, sp, #12
    1e80:	e3a09eff 	mov	r9, #4080	; 0xff0
    1e84:	e1a00007 	mov	r0, r7
    1e88:	ebffffd4 	bl	1de0 <_Unwind_Backtrace+0x24>
    1e8c:	e35000b0 	cmp	r0, #176	; 0xb0
    1e90:	e1a04000 	mov	r4, r0
    1e94:	1a00000f 	bne	1ed8 <__gnu_unwind_execute+0x6c>
    1e98:	e3560000 	cmp	r6, #0
    1e9c:	1a0000d1 	bne	21e8 <__gnu_unwind_execute+0x37c>
    1ea0:	e28d400c 	add	r4, sp, #12
    1ea4:	e1a01006 	mov	r1, r6
    1ea8:	e1a03006 	mov	r3, r6
    1eac:	e58d4000 	str	r4, [sp]
    1eb0:	e1a00005 	mov	r0, r5
    1eb4:	e3a0200e 	mov	r2, #14
    1eb8:	ebfffd0c 	bl	12f0 <_Unwind_VRS_Get>
    1ebc:	e58d4000 	str	r4, [sp]
    1ec0:	e1a00005 	mov	r0, r5
    1ec4:	e1a01006 	mov	r1, r6
    1ec8:	e3a0200f 	mov	r2, #15
    1ecc:	e1a03006 	mov	r3, r6
    1ed0:	ebfffd27 	bl	1374 <_Unwind_VRS_Set>
    1ed4:	ea0000c3 	b	21e8 <__gnu_unwind_execute+0x37c>
    1ed8:	e2101080 	ands	r1, r0, #128	; 0x80
    1edc:	1a00000d 	bne	1f18 <__gnu_unwind_execute+0xac>
    1ee0:	e1a0a100 	lsl	sl, r0, #2
    1ee4:	e1a03001 	mov	r3, r1
    1ee8:	e58d8000 	str	r8, [sp]
    1eec:	e1a00005 	mov	r0, r5
    1ef0:	e3a0200d 	mov	r2, #13
    1ef4:	ebfffcfd 	bl	12f0 <_Unwind_VRS_Get>
    1ef8:	e20aa0ff 	and	sl, sl, #255	; 0xff
    1efc:	e59d300c 	ldr	r3, [sp, #12]
    1f00:	e28aa004 	add	sl, sl, #4
    1f04:	e3140040 	tst	r4, #64	; 0x40
    1f08:	106aa003 	rsbne	sl, sl, r3
    1f0c:	008aa003 	addeq	sl, sl, r3
    1f10:	e58da00c 	str	sl, [sp, #12]
    1f14:	ea000021 	b	1fa0 <__gnu_unwind_execute+0x134>
    1f18:	e20030f0 	and	r3, r0, #240	; 0xf0
    1f1c:	e3530080 	cmp	r3, #128	; 0x80
    1f20:	1a000013 	bne	1f74 <__gnu_unwind_execute+0x108>
    1f24:	e1a04400 	lsl	r4, r0, #8
    1f28:	e1a00007 	mov	r0, r7
    1f2c:	ebffffab 	bl	1de0 <_Unwind_Backtrace+0x24>
    1f30:	e1800004 	orr	r0, r0, r4
    1f34:	e3500902 	cmp	r0, #32768	; 0x8000
    1f38:	1a000001 	bne	1f44 <__gnu_unwind_execute+0xd8>
    1f3c:	e3a00009 	mov	r0, #9
    1f40:	ea0000a9 	b	21ec <__gnu_unwind_execute+0x380>
    1f44:	e1a02a00 	lsl	r2, r0, #20
    1f48:	e3a01000 	mov	r1, #0
    1f4c:	e1a04200 	lsl	r4, r0, #4
    1f50:	e1a02822 	lsr	r2, r2, #16
    1f54:	e1a00005 	mov	r0, r5
    1f58:	e1a03001 	mov	r3, r1
    1f5c:	ebfffe5a 	bl	18cc <_Unwind_VRS_Pop>
    1f60:	e3500000 	cmp	r0, #0
    1f64:	1afffff4 	bne	1f3c <__gnu_unwind_execute+0xd0>
    1f68:	e3140902 	tst	r4, #32768	; 0x8000
    1f6c:	13a06001 	movne	r6, #1
    1f70:	eaffffc3 	b	1e84 <__gnu_unwind_execute+0x18>
    1f74:	e3530090 	cmp	r3, #144	; 0x90
    1f78:	1a00000f 	bne	1fbc <__gnu_unwind_execute+0x150>
    1f7c:	e200300d 	and	r3, r0, #13
    1f80:	e353000d 	cmp	r3, #13
    1f84:	0affffec 	beq	1f3c <__gnu_unwind_execute+0xd0>
    1f88:	e3a01000 	mov	r1, #0
    1f8c:	e58d8000 	str	r8, [sp]
    1f90:	e1a00005 	mov	r0, r5
    1f94:	e204200f 	and	r2, r4, #15
    1f98:	e1a03001 	mov	r3, r1
    1f9c:	ebfffcd3 	bl	12f0 <_Unwind_VRS_Get>
    1fa0:	e1a00005 	mov	r0, r5
    1fa4:	e3a01000 	mov	r1, #0
    1fa8:	e58d8000 	str	r8, [sp]
    1fac:	e3a0200d 	mov	r2, #13
    1fb0:	e1a03001 	mov	r3, r1
    1fb4:	ebfffcee 	bl	1374 <_Unwind_VRS_Set>
    1fb8:	eaffffb1 	b	1e84 <__gnu_unwind_execute+0x18>
    1fbc:	e35300a0 	cmp	r3, #160	; 0xa0
    1fc0:	1a000008 	bne	1fe8 <__gnu_unwind_execute+0x17c>
    1fc4:	e1e02000 	mvn	r2, r0
    1fc8:	e2022007 	and	r2, r2, #7
    1fcc:	e1a02259 	asr	r2, r9, r2
    1fd0:	e3100008 	tst	r0, #8
    1fd4:	e2022eff 	and	r2, r2, #4080	; 0xff0
    1fd8:	13822901 	orrne	r2, r2, #16384	; 0x4000
    1fdc:	e1a00005 	mov	r0, r5
    1fe0:	e3a01000 	mov	r1, #0
    1fe4:	ea00000a 	b	2014 <__gnu_unwind_execute+0x1a8>
    1fe8:	e35300b0 	cmp	r3, #176	; 0xb0
    1fec:	1a000038 	bne	20d4 <__gnu_unwind_execute+0x268>
    1ff0:	e35000b1 	cmp	r0, #177	; 0xb1
    1ff4:	1a000008 	bne	201c <__gnu_unwind_execute+0x1b0>
    1ff8:	e1a00007 	mov	r0, r7
    1ffc:	ebffff77 	bl	1de0 <_Unwind_Backtrace+0x24>
    2000:	e2502000 	subs	r2, r0, #0
    2004:	0affffcc 	beq	1f3c <__gnu_unwind_execute+0xd0>
    2008:	e21210f0 	ands	r1, r2, #240	; 0xf0
    200c:	1affffca 	bne	1f3c <__gnu_unwind_execute+0xd0>
    2010:	e1a00005 	mov	r0, r5
    2014:	e1a03001 	mov	r3, r1
    2018:	ea00006e 	b	21d8 <__gnu_unwind_execute+0x36c>
    201c:	e35000b2 	cmp	r0, #178	; 0xb2
    2020:	1a000018 	bne	2088 <__gnu_unwind_execute+0x21c>
    2024:	e3a01000 	mov	r1, #0
    2028:	e3a0200d 	mov	r2, #13
    202c:	e1a03001 	mov	r3, r1
    2030:	e58d8000 	str	r8, [sp]
    2034:	e1a00005 	mov	r0, r5
    2038:	ebfffcac 	bl	12f0 <_Unwind_VRS_Get>
    203c:	e1a00007 	mov	r0, r7
    2040:	ebffff66 	bl	1de0 <_Unwind_Backtrace+0x24>
    2044:	e3a04002 	mov	r4, #2
    2048:	e2101080 	ands	r1, r0, #128	; 0x80
    204c:	e59d300c 	ldr	r3, [sp, #12]
    2050:	e200007f 	and	r0, r0, #127	; 0x7f
    2054:	0a000005 	beq	2070 <__gnu_unwind_execute+0x204>
    2058:	e0833410 	add	r3, r3, r0, lsl r4
    205c:	e1a00007 	mov	r0, r7
    2060:	e58d300c 	str	r3, [sp, #12]
    2064:	e2844007 	add	r4, r4, #7
    2068:	ebffff5c 	bl	1de0 <_Unwind_Backtrace+0x24>
    206c:	eafffff5 	b	2048 <__gnu_unwind_execute+0x1dc>
    2070:	e2833f81 	add	r3, r3, #516	; 0x204
    2074:	e0833410 	add	r3, r3, r0, lsl r4
    2078:	e58d8000 	str	r8, [sp]
    207c:	e58d300c 	str	r3, [sp, #12]
    2080:	e1a00005 	mov	r0, r5
    2084:	eaffffc8 	b	1fac <__gnu_unwind_execute+0x140>
    2088:	e35000b3 	cmp	r0, #179	; 0xb3
    208c:	1a000007 	bne	20b0 <__gnu_unwind_execute+0x244>
    2090:	e1a00007 	mov	r0, r7
    2094:	ebffff51 	bl	1de0 <_Unwind_Backtrace+0x24>
    2098:	e3a01001 	mov	r1, #1
    209c:	e200200f 	and	r2, r0, #15
    20a0:	e20030f0 	and	r3, r0, #240	; 0xf0
    20a4:	e2822001 	add	r2, r2, #1
    20a8:	e1a00005 	mov	r0, r5
    20ac:	ea000013 	b	2100 <__gnu_unwind_execute+0x294>
    20b0:	e20030fc 	and	r3, r0, #252	; 0xfc
    20b4:	e35300b4 	cmp	r3, #180	; 0xb4
    20b8:	0affff9f 	beq	1f3c <__gnu_unwind_execute+0xd0>
    20bc:	e2002007 	and	r2, r0, #7
    20c0:	e2822001 	add	r2, r2, #1
    20c4:	e1a00005 	mov	r0, r5
    20c8:	e3a01001 	mov	r1, #1
    20cc:	e3822702 	orr	r2, r2, #524288	; 0x80000
    20d0:	eaffffcf 	b	2014 <__gnu_unwind_execute+0x1a8>
    20d4:	e35300c0 	cmp	r3, #192	; 0xc0
    20d8:	1a000035 	bne	21b4 <__gnu_unwind_execute+0x348>
    20dc:	e35000c6 	cmp	r0, #198	; 0xc6
    20e0:	1a000008 	bne	2108 <__gnu_unwind_execute+0x29c>
    20e4:	e1a00007 	mov	r0, r7
    20e8:	ebffff3c 	bl	1de0 <_Unwind_Backtrace+0x24>
    20ec:	e3a01003 	mov	r1, #3
    20f0:	e200200f 	and	r2, r0, #15
    20f4:	e20030f0 	and	r3, r0, #240	; 0xf0
    20f8:	e2822001 	add	r2, r2, #1
    20fc:	e1a00005 	mov	r0, r5
    2100:	e1822603 	orr	r2, r2, r3, lsl #12
    2104:	eaffffc2 	b	2014 <__gnu_unwind_execute+0x1a8>
    2108:	e35000c7 	cmp	r0, #199	; 0xc7
    210c:	1a000008 	bne	2134 <__gnu_unwind_execute+0x2c8>
    2110:	e1a00007 	mov	r0, r7
    2114:	ebffff31 	bl	1de0 <_Unwind_Backtrace+0x24>
    2118:	e2502000 	subs	r2, r0, #0
    211c:	0affff86 	beq	1f3c <__gnu_unwind_execute+0xd0>
    2120:	e21230f0 	ands	r3, r2, #240	; 0xf0
    2124:	1affff84 	bne	1f3c <__gnu_unwind_execute+0xd0>
    2128:	e1a00005 	mov	r0, r5
    212c:	e3a01004 	mov	r1, #4
    2130:	ea000028 	b	21d8 <__gnu_unwind_execute+0x36c>
    2134:	e20030f8 	and	r3, r0, #248	; 0xf8
    2138:	e35300c0 	cmp	r3, #192	; 0xc0
    213c:	1a000005 	bne	2158 <__gnu_unwind_execute+0x2ec>
    2140:	e200200f 	and	r2, r0, #15
    2144:	e2822001 	add	r2, r2, #1
    2148:	e1a00005 	mov	r0, r5
    214c:	e3a01003 	mov	r1, #3
    2150:	e382280a 	orr	r2, r2, #655360	; 0xa0000
    2154:	eaffffae 	b	2014 <__gnu_unwind_execute+0x1a8>
    2158:	e35000c8 	cmp	r0, #200	; 0xc8
    215c:	1a000009 	bne	2188 <__gnu_unwind_execute+0x31c>
    2160:	e1a00007 	mov	r0, r7
    2164:	ebffff1d 	bl	1de0 <_Unwind_Backtrace+0x24>
    2168:	e3a01001 	mov	r1, #1
    216c:	e20020f0 	and	r2, r0, #240	; 0xf0
    2170:	e200000f 	and	r0, r0, #15
    2174:	e2803001 	add	r3, r0, #1
    2178:	e2822010 	add	r2, r2, #16
    217c:	e1a00005 	mov	r0, r5
    2180:	e1832602 	orr	r2, r3, r2, lsl #12
    2184:	ea000012 	b	21d4 <__gnu_unwind_execute+0x368>
    2188:	e35000c9 	cmp	r0, #201	; 0xc9
    218c:	1affff6a 	bne	1f3c <__gnu_unwind_execute+0xd0>
    2190:	e1a00007 	mov	r0, r7
    2194:	ebffff11 	bl	1de0 <_Unwind_Backtrace+0x24>
    2198:	e3a01001 	mov	r1, #1
    219c:	e200200f 	and	r2, r0, #15
    21a0:	e20030f0 	and	r3, r0, #240	; 0xf0
    21a4:	e2822001 	add	r2, r2, #1
    21a8:	e1a00005 	mov	r0, r5
    21ac:	e1822603 	orr	r2, r2, r3, lsl #12
    21b0:	ea000007 	b	21d4 <__gnu_unwind_execute+0x368>
    21b4:	e20030f8 	and	r3, r0, #248	; 0xf8
    21b8:	e35300d0 	cmp	r3, #208	; 0xd0
    21bc:	1affff5e 	bne	1f3c <__gnu_unwind_execute+0xd0>
    21c0:	e2002007 	and	r2, r0, #7
    21c4:	e2822001 	add	r2, r2, #1
    21c8:	e1a00005 	mov	r0, r5
    21cc:	e3a01001 	mov	r1, #1
    21d0:	e3822702 	orr	r2, r2, #524288	; 0x80000
    21d4:	e3a03005 	mov	r3, #5
    21d8:	ebfffdbb 	bl	18cc <_Unwind_VRS_Pop>
    21dc:	e3500000 	cmp	r0, #0
    21e0:	1affff55 	bne	1f3c <__gnu_unwind_execute+0xd0>
    21e4:	eaffff26 	b	1e84 <__gnu_unwind_execute+0x18>
    21e8:	e3a00000 	mov	r0, #0
    21ec:	e28dd010 	add	sp, sp, #16
    21f0:	e8bd87f0 	pop	{r4, r5, r6, r7, r8, r9, sl, pc}

000021f4 <__gnu_unwind_frame>:
    21f4:	e92d401f 	push	{r0, r1, r2, r3, r4, lr}
    21f8:	e590304c 	ldr	r3, [r0, #76]	; 0x4c
    21fc:	e1a00001 	mov	r0, r1
    2200:	e5932004 	ldr	r2, [r3, #4]
    2204:	e28d1004 	add	r1, sp, #4
    2208:	e1a02402 	lsl	r2, r2, #8
    220c:	e58d2004 	str	r2, [sp, #4]
    2210:	e2832008 	add	r2, r3, #8
    2214:	e58d2008 	str	r2, [sp, #8]
    2218:	e3a02003 	mov	r2, #3
    221c:	e5cd200c 	strb	r2, [sp, #12]
    2220:	e5d33007 	ldrb	r3, [r3, #7]
    2224:	e5cd300d 	strb	r3, [sp, #13]
    2228:	ebffff0f 	bl	1e6c <__gnu_unwind_execute>
    222c:	e28dd014 	add	sp, sp, #20
    2230:	e49df004 	pop	{pc}		; (ldr pc, [sp], #4)

00002234 <_Unwind_GetRegionStart>:
    2234:	e92d4008 	push	{r3, lr}
    2238:	ebffff0a 	bl	1e68 <_Unwind_Backtrace+0xac>
    223c:	e5900048 	ldr	r0, [r0, #72]	; 0x48
    2240:	e8bd8008 	pop	{r3, pc}

00002244 <_Unwind_GetLanguageSpecificData>:
    2244:	e92d4008 	push	{r3, lr}
    2248:	ebffff06 	bl	1e68 <_Unwind_Backtrace+0xac>
    224c:	e590304c 	ldr	r3, [r0, #76]	; 0x4c
    2250:	e5d30007 	ldrb	r0, [r3, #7]
    2254:	e0830100 	add	r0, r3, r0, lsl #2
    2258:	e2800008 	add	r0, r0, #8
    225c:	e8bd8008 	pop	{r3, pc}

00002260 <_Unwind_GetDataRelBase>:
    2260:	e92d4008 	push	{r3, lr}
    2264:	ebfffa8b 	bl	c98 <abort@plt>

00002268 <_Unwind_GetTextRelBase>:
    2268:	e92d4008 	push	{r3, lr}
    226c:	ebfffa89 	bl	c98 <abort@plt>
```

我们可以从上面看到他用汇编显示了这个文件的内容

plt:主要用于函数重定位

text:程序代码段

# ida pro

可以说是最强大的反汇编器，具体使用方法时将so拖入ida创建















