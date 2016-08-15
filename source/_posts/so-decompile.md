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
arm-linux-androideabi-objdump -S hello
```

```
hello:     file format elf32-littlearm


Disassembly of section .plt:

00008370 <__libc_init@plt-0x14>:
    8370:	e52de004 	push	{lr}		; (str lr, [sp, #-4]!)
    8374:	e59fe004 	ldr	lr, [pc, #4]	; 8380 <__libc_init@plt-0x4>
    8378:	e08fe00e 	add	lr, pc, lr
    837c:	e5bef008 	ldr	pc, [lr, #8]!
    8380:	00002c54 	andeq	r2, r0, r4, asr ip

00008384 <__libc_init@plt>:
    8384:	e28fc600 	add	ip, pc, #0, 12
    8388:	e28cca02 	add	ip, ip, #8192	; 0x2000
    838c:	e5bcfc54 	ldr	pc, [ip, #3156]!	; 0xc54

00008390 <__cxa_atexit@plt>:
    8390:	e28fc600 	add	ip, pc, #0, 12
    8394:	e28cca02 	add	ip, ip, #8192	; 0x2000
    8398:	e5bcfc4c 	ldr	pc, [ip, #3148]!	; 0xc4c

0000839c <puts@plt>:
    839c:	e28fc600 	add	ip, pc, #0, 12
    83a0:	e28cca02 	add	ip, ip, #8192	; 0x2000
    83a4:	e5bcfc44 	ldr	pc, [ip, #3140]!	; 0xc44

000083a8 <__gnu_Unwind_Find_exidx@plt>:
    83a8:	e28fc600 	add	ip, pc, #0, 12
    83ac:	e28cca02 	add	ip, ip, #8192	; 0x2000
    83b0:	e5bcfc3c 	ldr	pc, [ip, #3132]!	; 0xc3c

000083b4 <abort@plt>:
    83b4:	e28fc600 	add	ip, pc, #0, 12
    83b8:	e28cca02 	add	ip, ip, #8192	; 0x2000
    83bc:	e5bcfc34 	ldr	pc, [ip, #3124]!	; 0xc34

000083c0 <memcpy@plt>:
    83c0:	e28fc600 	add	ip, pc, #0, 12
    83c4:	e28cca02 	add	ip, ip, #8192	; 0x2000
    83c8:	e5bcfc2c 	ldr	pc, [ip, #3116]!	; 0xc2c

000083cc <__cxa_begin_cleanup@plt>:
    83cc:	e28fc600 	add	ip, pc, #0, 12
    83d0:	e28cca02 	add	ip, ip, #8192	; 0x2000
    83d4:	e5bcfc24 	ldr	pc, [ip, #3108]!	; 0xc24

000083d8 <__cxa_type_match@plt>:
    83d8:	e28fc600 	add	ip, pc, #0, 12
    83dc:	e28cca02 	add	ip, ip, #8192	; 0x2000
    83e0:	e5bcfc1c 	ldr	pc, [ip, #3100]!	; 0xc1c

Disassembly of section .text:

000083e4 <.text>:
    83e4:	4803b508 	stmdami	r3, {r3, r8, sl, ip, sp, pc}
    83e8:	f0004478 			; <UNDEFINED> instruction: 0xf0004478
    83ec:	2000ff97 	mulcs	r0, r7, pc	; <UNPREDICTABLE>
    83f0:	46c0bd08 	strbmi	fp, [r0], r8, lsl #26
    83f4:	00001190 	muleq	r0, r0, r1
    83f8:	e3500000 	cmp	r0, #0
    83fc:	012fff1e 	bxeq	lr
    8400:	e12fff10 	bx	r0
    8404:	e59fc05c 	ldr	ip, [pc, #92]	; 8468 <__cxa_type_match@plt+0x90>
    8408:	e59f205c 	ldr	r2, [pc, #92]	; 846c <__cxa_type_match@plt+0x94>
    840c:	e92d4800 	push	{fp, lr}
    8410:	e08fc00c 	add	ip, pc, ip
    8414:	e28db004 	add	fp, sp, #4
    8418:	e59f3050 	ldr	r3, [pc, #80]	; 8470 <__cxa_type_match@plt+0x98>
    841c:	e24dd010 	sub	sp, sp, #16
    8420:	e59f104c 	ldr	r1, [pc, #76]	; 8474 <__cxa_type_match@plt+0x9c>
    8424:	e79c2002 	ldr	r2, [ip, r2]
    8428:	e50b2014 	str	r2, [fp, #-20]	; 0xffffffec
    842c:	e59f2044 	ldr	r2, [pc, #68]	; 8478 <__cxa_type_match@plt+0xa0>
    8430:	e79c3003 	ldr	r3, [ip, r3]
    8434:	e50b3010 	str	r3, [fp, #-16]
    8438:	e59f303c 	ldr	r3, [pc, #60]	; 847c <__cxa_type_match@plt+0xa4>
    843c:	e79c1001 	ldr	r1, [ip, r1]
    8440:	e50b100c 	str	r1, [fp, #-12]
    8444:	e79c2002 	ldr	r2, [ip, r2]
    8448:	e50b2008 	str	r2, [fp, #-8]
    844c:	e28b0004 	add	r0, fp, #4
    8450:	e79c2003 	ldr	r2, [ip, r3]
    8454:	e3a01000 	mov	r1, #0
    8458:	e24b3014 	sub	r3, fp, #20
    845c:	ebffffc8 	bl	8384 <__libc_init@plt>
    8460:	e24bd004 	sub	sp, fp, #4
    8464:	e8bd8800 	pop	{fp, pc}
    8468:	00002bbc 			; <UNDEFINED> instruction: 0x00002bbc
    846c:	ffffffd0 			; <UNDEFINED> instruction: 0xffffffd0
    8470:	ffffffd4 			; <UNDEFINED> instruction: 0xffffffd4
    8474:	ffffffd8 			; <UNDEFINED> instruction: 0xffffffd8
    8478:	ffffffdc 			; <UNDEFINED> instruction: 0xffffffdc
    847c:	ffffffe0 			; <UNDEFINED> instruction: 0xffffffe0
    8480:	e1a01000 	mov	r1, r0
    8484:	e59f200c 	ldr	r2, [pc, #12]	; 8498 <__cxa_type_match@plt+0xc0>
    8488:	e59f000c 	ldr	r0, [pc, #12]	; 849c <__cxa_type_match@plt+0xc4>
    848c:	e08f2002 	add	r2, pc, r2
    8490:	e08f0000 	add	r0, pc, r0
    8494:	eaffffbd 	b	8390 <__cxa_atexit@plt>
    8498:	00002b6c 	andeq	r2, r0, ip, ror #22
    849c:	ffffff60 			; <UNDEFINED> instruction: 0xffffff60
    84a0:	005a6803 	subseq	r6, sl, r3, lsl #16
    84a4:	2280d503 	addcs	sp, r0, #12582912	; 0xc00000
    84a8:	43130612 	tstmi	r3, #18874368	; 0x1200000
    84ac:	005be001 	subseq	lr, fp, r1
    84b0:	18c0085b 	stmiane	r0, {r0, r1, r3, r4, r6, fp}^
    84b4:	b5f04770 	ldrblt	r4, [r0, #1904]!	; 0x770
    84b8:	b0871c0e 	addlt	r1, r7, lr, lsl #24
    84bc:	d02e2900 	eorle	r2, lr, r0, lsl #18
    84c0:	27001e4b 	strcs	r1, [r0, -fp, asr #28]
    84c4:	90059201 	andls	r9, r5, r1, lsl #4
    84c8:	93029303 	movwls	r9, #8963	; 0x2303
    84cc:	18fb9b02 	ldmne	fp!, {r1, r8, r9, fp, ip, pc}^
    84d0:	18e40fdc 	stmiane	r4!, {r2, r3, r4, r6, r7, r8, r9, sl, fp}^
    84d4:	9b051064 	blls	14c66c <_end+0x141668>
    84d8:	195e00e5 	ldmdbne	lr, {r0, r2, r5, r6, r7}^
    84dc:	f7ff1c30 			; <UNDEFINED> instruction: 0xf7ff1c30
    84e0:	9b03ffdf 	blls	108464 <_end+0xfd460>
    84e4:	429c9004 	addsmi	r9, ip, #4
    84e8:	9b05d015 	blls	17c544 <_end+0x171540>
    84ec:	19583508 	ldmdbne	r8, {r3, r8, sl, ip, sp}^
    84f0:	ffd6f7ff 			; <UNDEFINED> instruction: 0xffd6f7ff
    84f4:	9a049b01 	bls	12f100 <_end+0x1240fc>
    84f8:	d2044293 	andle	r4, r4, #805306377	; 0x30000009
    84fc:	d00842bc 			; <UNDEFINED> instruction: 0xd00842bc
    8500:	93021e63 	movwls	r1, #11875	; 0x2e63
    8504:	9b01e7e2 	blls	82494 <_end+0x77490>
    8508:	42833801 	addmi	r3, r3, #65536	; 0x10000
    850c:	1c67d907 	stclne	9, cr13, [r7], #-28	; 0xffffffe4
    8510:	2600e7dc 			; <UNDEFINED> instruction: 0x2600e7dc
    8514:	9b01e003 	blls	80528 <_end+0x75524>
    8518:	42939a04 	addsmi	r9, r3, #4, 20	; 0x4000
    851c:	1c30d3ee 	ldcne	3, cr13, [r0], #-952	; 0xfffffc48
    8520:	bdf0b007 	ldcllt	0, cr11, [r0, #28]!
    8524:	d0062801 	andle	r2, r6, r1, lsl #16
    8528:	d0072802 	andle	r2, r7, r2, lsl #16
    852c:	d1092800 	tstle	r9, r0, lsl #16
    8530:	44784805 	ldrbtmi	r4, [r8], #-2053	; 0xfffff7fb
    8534:	4805e004 	stmdami	r5, {r2, sp, lr, pc}
    8538:	e0014478 	and	r4, r1, r8, ror r4
    853c:	44784804 	ldrbtmi	r4, [r8], #-2052	; 0xfffff7fc
    8540:	e0006800 	and	r6, r0, r0, lsl #16
    8544:	47702000 	ldrbmi	r2, [r0, -r0]!
    8548:	00002a82 	andeq	r2, r0, r2, lsl #21
    854c:	00002a80 	andeq	r2, r0, r0, lsl #21
    8550:	00002a7e 	andeq	r2, r0, lr, ror sl
    8554:	b5374b25 	ldrlt	r4, [r7, #-2853]!	; 0xfffff4db
    8558:	681b447b 	ldmdavs	fp, {r0, r1, r3, r4, r5, r6, sl, lr}
    855c:	1e8d1c04 	cdpne	12, 8, cr1, cr13, cr4, {0}
    8560:	d0092b00 	andle	r2, r9, r0, lsl #22
    8564:	a9011c28 	stmdbge	r1, {r3, r5, sl, fp, ip}
    8568:	fedcf000 	cdp2	0, 13, cr15, cr12, cr0, {0}
    856c:	d10c2800 	tstle	ip, r0, lsl #16
    8570:	61232300 	teqvs	r3, r0, lsl #6
    8574:	e0362409 	eors	r2, r6, r9, lsl #8
    8578:	481e4b1d 	ldmdami	lr, {r0, r2, r3, r4, r8, r9, fp, lr}
    857c:	4478447b 	ldrbtmi	r4, [r8], #-1147	; 0xfffffb85
    8580:	6800681b 	stmdavs	r0, {r0, r1, r3, r4, fp, sp, lr}
    8584:	10db1a1b 	sbcsne	r1, fp, fp, lsl sl
    8588:	1c2a9301 	stcne	3, cr9, [sl], #-4
    858c:	f7ff9901 			; <UNDEFINED> instruction: 0xf7ff9901
    8590:	1e05ff92 	mcrne	15, 0, pc, cr5, cr2, {4}	; <UNPREDICTABLE>
    8594:	f7ffd0ec 			; <UNDEFINED> instruction: 0xf7ffd0ec
    8598:	686bff83 	stmdavs	fp!, {r0, r1, r7, r8, r9, sl, fp, ip, sp, lr, pc}^
    859c:	2b0164a0 	blcs	61824 <_end+0x56820>
    85a0:	2300d103 	movwcs	sp, #259	; 0x103
    85a4:	24056123 	strcs	r6, [r5], #-291	; 0xfffffedd
    85a8:	1d28e01d 	stcne	0, cr14, [r8, #-116]!	; 0xffffff8c
    85ac:	da022b00 	ble	931b4 <_end+0x881b0>
    85b0:	230164e0 	movwcs	r6, #5344	; 0x14e0
    85b4:	f7ffe003 			; <UNDEFINED> instruction: 0xf7ffe003
    85b8:	2300ff73 	movwcs	pc, #3955	; 0xf73	; <UNPREDICTABLE>
    85bc:	6ce064e0 	cfstrdvs	mvd6, [r0], #896	; 0x380
    85c0:	68036523 	stmdavs	r3, {r0, r1, r5, r8, sl, sp, lr}
    85c4:	da0a2b00 	ble	2931cc <_end+0x2881c8>
    85c8:	0f000118 	svceq	0x00000118
    85cc:	ffaaf7ff 			; <UNDEFINED> instruction: 0xffaaf7ff
    85d0:	42436120 	submi	r6, r3, #32, 2
    85d4:	24094158 	strcs	r4, [r9], #-344	; 0xfffffea8
    85d8:	40044240 	andmi	r4, r4, r0, asr #4
    85dc:	f7ffe003 			; <UNDEFINED> instruction: 0xf7ffe003
    85e0:	6120ff5f 	msrvs	LR_irq, pc
    85e4:	1c202400 	cfstrsne	mvf2, [r0], #-0
    85e8:	46c0bd3e 			; <UNDEFINED> instruction: 0x46c0bd3e
    85ec:	00002a68 	andeq	r2, r0, r8, ror #20
    85f0:	00002a48 	andeq	r2, r0, r8, asr #20
    85f4:	00002a4a 	andeq	r2, r0, sl, asr #20
    85f8:	b5106803 	ldrlt	r6, [r0, #-2051]	; 0xfffff7fd
    85fc:	07da1c04 	ldrbeq	r1, [sl, r4, lsl #24]
    8600:	3048d407 	subcc	sp, r8, r7, lsl #8
    8604:	d502079b 	strle	r0, [r2, #-1947]	; 0xfffff865
    8608:	fe90f000 	cdp2	0, 9, cr15, cr0, cr0, {0}
    860c:	f000e001 			; <UNDEFINED> instruction: 0xf000e001
    8610:	6823fe91 	stmdavs	r3!, {r0, r4, r7, r9, sl, fp, ip, sp, lr, pc}
    8614:	d403075b 	strle	r0, [r3], #-1883	; 0xfffff8a5
    8618:	30d01c20 	sbcscc	r1, r0, r0, lsr #24
    861c:	fe8ef000 	cdp2	0, 8, cr15, cr14, cr0, {0}
    8620:	071b6823 	ldreq	r6, [fp, -r3, lsr #16]
    8624:	1c20d404 	cfstrsne	mvf13, [r0], #-16
    8628:	30ff3051 	rscscc	r3, pc, r1, asr r0	; <UNPREDICTABLE>
    862c:	fe8af000 	cdp2	0, 8, cr15, cr10, cr0, {0}
    8630:	06db6823 	ldrbeq	r6, [fp], r3, lsr #16
    8634:	1c20d404 	cfstrsne	mvf13, [r0], #-16
    8638:	30ff30d1 	ldrsbtcc	r3, [pc], #1
    863c:	fe86f000 	cdp2	0, 8, cr15, cr6, cr0, {0}
    8640:	6802bd10 	stmdavs	r2, {r4, r8, sl, fp, ip, sp, pc}
    8644:	429a2300 	addsmi	r2, sl, #0, 6
    8648:	5813d000 	ldmdapl	r3, {ip, lr, pc}
    864c:	47701c18 			; <UNDEFINED> instruction: 0x47701c18
    8650:	47702009 	ldrbmi	r2, [r0, -r9]!
    8654:	b5704770 	ldrblt	r4, [r0, #-1904]!	; 0xfffff890
    8658:	1c0c1c05 	stcne	12, cr1, [ip], {5}
    865c:	6c211c28 	stcvs	12, cr1, [r1], #-160	; 0xffffff60
    8660:	ff78f7ff 			; <UNDEFINED> instruction: 0xff78f7ff
    8664:	d0011e06 	andle	r1, r1, r6, lsl #28
    8668:	fe74f000 	cdp2	0, 7, cr15, cr4, cr0, {0}
    866c:	616b6c23 	cmnvs	fp, r3, lsr #24
    8670:	1c292001 	stcne	0, cr2, [r9], #-4
    8674:	692b1c22 	stmdbvs	fp!, {r1, r5, sl, fp, ip}
    8678:	28084798 	stmdacs	r8, {r3, r4, r7, r8, r9, sl, lr}
    867c:	2807d0ee 	stmdacs	r7, {r1, r2, r3, r5, r6, r7, ip, lr, pc}
    8680:	1c30d1f2 	ldfned	f5, [r0], #-968	; 0xfffffc38
    8684:	f7ff6c21 			; <UNDEFINED> instruction: 0xf7ff6c21
    8688:	1d20ffe5 	stcne	15, cr15, [r0, #-916]!	; 0xfffffc6c
    868c:	fe66f000 	cdp2	0, 6, cr15, cr6, cr0, {0}
    8690:	4c2db5f0 	cfstr32mi	mvfx11, [sp], #-960	; 0xfffffc40
    8694:	44a568c3 	strtmi	r6, [r5], #2243	; 0x8c3
    8698:	25009304 	strcs	r9, [r0, #-772]	; 0xfffffcfc
    869c:	1c046983 	stcne	9, cr6, [r4], {131}	; 0x83
    86a0:	31041c17 	tstcc	r4, r7, lsl ip
    86a4:	2240a807 	subcs	sl, r0, #458752	; 0x70000
    86a8:	f0009305 			; <UNDEFINED> instruction: 0xf0009305
    86ac:	9506fe5b 	strls	pc, [r6, #-3675]	; 0xfffff1a5
    86b0:	ae069503 	cfsh32ge	mvfx9, mvfx6, #3
    86b4:	6c311c20 	ldcvs	12, cr1, [r1], #-128	; 0xffffff80
    86b8:	ff4cf7ff 			; <UNDEFINED> instruction: 0xff4cf7ff
    86bc:	417b427b 	cmnmi	fp, fp, ror r2
    86c0:	1ad3220a 	bne	ff4d0ef0 <_end+0xff4c5eec>
    86c4:	1e059302 	cdpne	3, 0, cr9, cr5, cr2, {0}
    86c8:	6c33d110 	ldfvsd	f5, [r3], #-64	; 0xffffffc0
    86cc:	22f0af7e 	rscscs	sl, r0, #504	; 0x1f8
    86d0:	1c316163 	ldfnes	f6, [r1], #-396	; 0xfffffe74
    86d4:	1c380052 	ldcne	0, cr0, [r8], #-328	; 0xfffffeb8
    86d8:	fe44f000 	cdp2	0, 4, cr15, cr4, cr0, {0}
    86dc:	98026923 	stmdals	r2, {r0, r1, r5, r8, fp, sp, lr}
    86e0:	1c3a1c21 	ldcne	12, cr1, [sl], #-132	; 0xffffff7c
    86e4:	6bbb4798 	blvs	feeda54c <_end+0xfeecf548>
    86e8:	e0049003 	and	r9, r4, r3
    86ec:	23109a02 	tstcs	r0, #8192	; 0x2000
    86f0:	6bb3431a 	blvs	fecd9360 <_end+0xfecce35c>
    86f4:	64739202 	ldrbtvs	r9, [r3], #-514	; 0xfffffdfe
    86f8:	ae069b05 	vmlage.f64	d9, d6, d5
    86fc:	96009301 	strls	r9, [r0], -r1, lsl #6
    8700:	99022001 	stmdbls	r2, {r0, sp}
    8704:	1c231c22 	stcne	12, cr1, [r3], #-136	; 0xffffff78
    8708:	47b89f04 	ldrmi	r9, [r8, r4, lsl #30]!
    870c:	d1142800 	tstle	r4, r0, lsl #16
    8710:	d1142d00 	tstle	r4, r0, lsl #26
    8714:	1c3022f0 	lfmne	f2, 4, [r0], #-960	; 0xfffffc40
    8718:	0052a97e 	subseq	sl, r2, lr, ror r9
    871c:	fe22f000 	cdp2	0, 2, cr15, cr2, cr0, {0}
    8720:	1c2f9b03 	stcne	11, cr9, [pc], #-12	; 871c <__cxa_type_match@plt+0x344>
    8724:	d0c42b08 	sbcle	r2, r4, r8, lsl #22
    8728:	d1062b07 	tstle	r6, r7, lsl #22
    872c:	6c311c28 	ldcvs	12, cr1, [r1], #-160	; 0xffffff60
    8730:	ff90f7ff 			; <UNDEFINED> instruction: 0xff90f7ff
    8734:	f000a807 			; <UNDEFINED> instruction: 0xf000a807
    8738:	2009fe11 	andcs	pc, r9, r1, lsl lr	; <UNPREDICTABLE>
    873c:	1c28e000 	stcne	0, cr14, [r8], #-0
    8740:	009b23f7 			; <UNDEFINED> instruction: 0x009b23f7
    8744:	bdf0449d 	cfldrdlt	mvd4, [r0, #628]!	; 0x274
    8748:	fffffc24 			; <UNDEFINED> instruction: 0xfffffc24
    874c:	47706c40 	ldrbmi	r6, [r0, -r0, asr #24]!
    8750:	6bcbb5f0 	blvs	ff2f5f18 <_end+0xff2eaf14>
    8754:	640bb0f9 	strvs	fp, [fp], #-249	; 0xffffff07
    8758:	1c0c1c05 	stcne	12, cr1, [ip], {5}
    875c:	3104a801 	tstcc	r4, r1, lsl #16
    8760:	f0002240 			; <UNDEFINED> instruction: 0xf0002240
    8764:	2301fdff 	movwcs	pc, #7679	; 0x1dff	; <UNPREDICTABLE>
    8768:	9300425b 	movwls	r4, #603	; 0x25b
    876c:	99101c28 	ldmdbls	r0, {r3, r5, sl, fp, ip}
    8770:	fef0f7ff 	mrc2	7, 7, pc, cr0, cr15, {7}
    8774:	d10f2800 	tstle	pc, r0, lsl #16
    8778:	466a1c29 	strbtmi	r1, [sl], -r9, lsr #24
    877c:	4798692b 	ldrmi	r6, [r8, fp, lsr #18]
    8780:	2f081e07 	svccs	0x00081e07
    8784:	4668d0f2 			; <UNDEFINED> instruction: 0x4668d0f2
    8788:	ff36f7ff 			; <UNDEFINED> instruction: 0xff36f7ff
    878c:	d1032f06 	tstle	r3, r6, lsl #30
    8790:	1c211c28 	stcne	12, cr1, [r1], #-160	; 0xffffff60
    8794:	ff5ff7ff 			; <UNDEFINED> instruction: 0xff5ff7ff
    8798:	b0792009 	rsbslt	r2, r9, r9
    879c:	b508bdf0 	strlt	fp, [r8, #-3568]	; 0xfffff210
    87a0:	6bda6182 	blvs	ff6a0db0 <_end+0xff695dac>
    87a4:	641a60c1 	ldrvs	r6, [sl], #-193	; 0xffffff3f
    87a8:	22001c19 	andcs	r1, r0, #6400	; 0x1900
    87ac:	ff70f7ff 			; <UNDEFINED> instruction: 0xff70f7ff
    87b0:	b570bd08 	ldrblt	fp, [r0, #-3336]!	; 0xfffff2f8
    87b4:	694368c6 	stmdbvs	r3, {r1, r2, r6, r7, fp, sp, lr}^
    87b8:	1c0c1c05 	stcne	12, cr1, [ip], {5}
    87bc:	2e00640b 	cdpcs	4, 0, cr6, cr0, cr11, {0}
    87c0:	2201d003 	andcs	sp, r1, #3
    87c4:	ff64f7ff 			; <UNDEFINED> instruction: 0xff64f7ff
    87c8:	2002e013 	andcs	lr, r2, r3, lsl r0
    87cc:	1c221c29 	stcne	12, cr1, [r2], #-164	; 0xffffff5c
    87d0:	4798692b 	ldrmi	r6, [r8, fp, lsr #18]
    87d4:	d0052807 	andle	r2, r5, r7, lsl #16
    87d8:	d10a2808 	tstle	sl, r8, lsl #16
    87dc:	1c211c28 	stcne	12, cr1, [r1], #-160	; 0xffffff60
    87e0:	ff39f7ff 			; <UNDEFINED> instruction: 0xff39f7ff
    87e4:	6c211c30 	stcvs	12, cr1, [r1], #-192	; 0xffffff40
    87e8:	ff34f7ff 			; <UNDEFINED> instruction: 0xff34f7ff
    87ec:	f0001d20 			; <UNDEFINED> instruction: 0xf0001d20
    87f0:	f000fdb5 			; <UNDEFINED> instruction: 0xf000fdb5
    87f4:	b508fdaf 	strlt	pc, [r8, #-3503]	; 0xfffff251
    87f8:	2b0068c3 	blcs	22b0c <_end+0x17b08>
    87fc:	f7ffd102 			; <UNDEFINED> instruction: 0xf7ffd102
    8800:	e004ffa7 	and	pc, r4, r7, lsr #31
    8804:	640b6bcb 	strvs	r6, [fp], #-3019	; 0xfffff435
    8808:	f7ff2200 			; <UNDEFINED> instruction: 0xf7ff2200
    880c:	bd08ff41 	stclt	15, cr15, [r8, #-260]	; 0xfffffefc
    8810:	b5084770 	strlt	r4, [r8, #-1904]	; 0xfffff890
    8814:	2b006883 	blcs	22a28 <_end+0x17a24>
    8818:	1c01d002 	stcne	0, cr13, [r1], {2}
    881c:	47982001 	ldrmi	r2, [r8, r1]
    8820:	b510bd08 	ldrlt	fp, [r0, #-3336]	; 0xfffff2f8
    8824:	29041c04 	stmdbcs	r4, {r2, sl, fp, ip}
    8828:	1c08d805 	stcne	8, cr13, [r8], {5}
    882c:	fd6cf000 	stc2l	0, cr15, [ip, #-0]
    8830:	11031105 	tstne	r3, r5, lsl #2
    8834:	20020011 	andcs	r0, r2, r1, lsl r0
    8838:	2002e00c 	andcs	lr, r2, ip
    883c:	d1092b00 	tstle	r9, r0, lsl #22
    8840:	d8072a0f 	stmdale	r7, {r0, r1, r2, r3, r9, fp, sp}
    8844:	18a24082 	stmiane	r2!, {r1, r7, lr}
    8848:	9a026851 	bls	a2994 <_end+0x97990>
    884c:	60111c18 	andsvs	r1, r1, r8, lsl ip
    8850:	2001e000 	andcs	lr, r1, r0
    8854:	b51fbd10 	ldrlt	fp, [pc, #-3344]	; 7b4c <__libc_init@plt-0x838>
    8858:	ab031c0a 	blge	cf888 <_end+0xc4884>
    885c:	93002100 	movwls	r2, #256	; 0x100
    8860:	f7ff1c0b 			; <UNDEFINED> instruction: 0xf7ff1c0b
    8864:	9803ffde 	stmdals	r3, {r1, r2, r3, r4, r6, r7, r8, r9, sl, fp, ip, sp, lr, pc}
    8868:	bd00b005 	stclt	0, cr11, [r0, #-20]	; 0xffffffec
    886c:	1c04b510 	cfstr32ne	mvfx11, [r4], {16}
    8870:	d8052904 	stmdale	r5, {r2, r8, fp, sp}
    8874:	f0001c08 			; <UNDEFINED> instruction: 0xf0001c08
    8878:	1105fd47 	tstne	r5, r7, asr #26
    887c:	00111103 	andseq	r1, r1, r3, lsl #2
    8880:	e00c2002 	and	r2, ip, r2
    8884:	2b002002 	blcs	10894 <_end+0x5890>
    8888:	2a0fd109 	bcs	3fccb4 <_end+0x3f1cb0>
    888c:	9902d807 	stmdbls	r2, {r0, r1, r2, fp, ip, lr, pc}
    8890:	68094082 	stmdavs	r9, {r1, r7, lr}
    8894:	605118a2 	subsvs	r1, r1, r2, lsr #17
    8898:	e0001c18 	and	r1, r0, r8, lsl ip
    889c:	bd102001 	ldclt	0, cr2, [r0, #-4]
    88a0:	1c0bb51f 	cfstr32ne	mvfx11, [fp], {31}
    88a4:	21009203 	tstcs	r0, r3, lsl #4
    88a8:	9200aa03 	andls	sl, r0, #12288	; 0x3000
    88ac:	1c0b1c1a 	stcne	12, cr1, [fp], {26}
    88b0:	ffdcf7ff 			; <UNDEFINED> instruction: 0xffdcf7ff
    88b4:	bd00b005 	stclt	0, cr11, [r0, #-20]	; 0xffffffec
    88b8:	4c1ab5f0 	cfldr32mi	mvfx11, [sl], {240}	; 0xf0
    88bc:	44a56bd3 	strtmi	r6, [r5], #3027	; 0xbd3
    88c0:	1c056413 	cfstrsne	mvf6, [r5], {19}
    88c4:	a8171c0e 	ldmdage	r7, {r1, r2, r3, sl, fp, ip}
    88c8:	22401d11 	subcs	r1, r0, #1088	; 0x440
    88cc:	fd4af000 	stc2l	0, cr15, [sl, #-0]
    88d0:	425b2301 	subsmi	r2, fp, #67108864	; 0x4000000
    88d4:	ac169316 	ldcge	3, cr9, [r6], {22}
    88d8:	6c214668 	stcvs	6, cr4, [r1], #-416	; 0xfffffe60
    88dc:	fe3af7ff 	mrc2	7, 1, pc, cr10, cr15, {7}
    88e0:	d0012800 	andle	r2, r1, r0, lsl #16
    88e4:	e0142709 	ands	r2, r4, r9, lsl #14
    88e8:	210c1c20 	tstcs	ip, r0, lsr #24
    88ec:	f7ff466a 			; <UNDEFINED> instruction: 0xf7ff466a
    88f0:	1c20ffd7 	stcne	15, cr15, [r0], #-860	; 0xfffffca4
    88f4:	47a81c31 			; <UNDEFINED> instruction: 0x47a81c31
    88f8:	d1f32800 	mvnsle	r2, r0, lsl #16
    88fc:	20089b04 	andcs	r9, r8, r4, lsl #22
    8900:	1c224669 	stcne	6, cr4, [r2], #-420	; 0xfffffe5c
    8904:	1e074798 	mcrne	7, 0, r4, cr7, cr8, {4}
    8908:	d0022f05 	andle	r2, r2, r5, lsl #30
    890c:	d1e22809 	mvnle	r2, r9, lsl #16
    8910:	1c20e7e8 	stcne	7, cr14, [r0], #-928	; 0xfffffc60
    8914:	fe70f7ff 	mrc2	7, 3, pc, cr0, cr15, {7}
    8918:	238f1c38 	orrcs	r1, pc, #56, 24	; 0x3800
    891c:	449d009b 	ldrmi	r0, [sp], #155	; 0x9b
    8920:	46c0bdf0 			; <UNDEFINED> instruction: 0x46c0bdf0
    8924:	fffffdc4 			; <UNDEFINED> instruction: 0xfffffdc4
    8928:	b08db5f0 	strdlt	fp, [sp], r0
    892c:	1c169303 	ldcne	3, cr9, [r6], {3}
    8930:	1c022303 	stcne	3, cr2, [r2], {3}
    8934:	9201401a 	andls	r4, r1, #26
    8938:	90076cca 	andls	r6, r7, sl, asr #25
    893c:	1c0c9803 	stcne	8, cr9, [ip], {3}
    8940:	a9091d17 	stmdbge	r9, {r0, r1, r2, r4, r8, sl, fp, ip}
    8944:	92096812 	andls	r6, r9, #1179648	; 0x120000
    8948:	2800604f 	stmdacs	r0, {r0, r1, r2, r3, r6, sp, lr}
    894c:	0212d106 	andseq	sp, r2, #-2147483647	; 0x80000001
    8950:	466a9209 	strbtmi	r9, [sl], -r9, lsl #4
    8954:	724a7b12 	subvc	r7, sl, #18432	; 0x4800
    8958:	e00c720b 	and	r7, ip, fp, lsl #4
    895c:	2b029b03 	blcs	af570 <_end+0xa456c>
    8960:	0c13dc09 	ldceq	12, cr13, [r3], {9}
    8964:	0412724b 	ldreq	r7, [r2], #-587	; 0xfffffdb5
    8968:	600a061b 	andvs	r0, sl, fp, lsl r6
    896c:	22020e1b 	andcs	r0, r2, #432	; 0x1b0
    8970:	18ff4093 	ldmne	pc!, {r0, r1, r4, r7, lr}^	; <UNPREDICTABLE>
    8974:	9b01720a 	blls	651a4 <_end+0x5a1a0>
    8978:	d1002b02 	tstle	r0, r2, lsl #22
    897c:	6d226ba7 	fstmdbxvs	r2!, {d6-d88}	;@ Deprecated
    8980:	40132301 	andsmi	r2, r3, r1, lsl #6
    8984:	e0ddd000 	sbcs	sp, sp, r0
    8988:	683b9305 	ldmdavs	fp!, {r0, r2, r8, r9, ip, pc}
    898c:	2b009302 	blcs	2d59c <_end+0x22598>
    8990:	e0d9d100 	sbcs	sp, r9, r0, lsl #2
    8994:	2b029b03 	blcs	af5a8 <_end+0xa45a4>
    8998:	687bd104 	ldmdavs	fp!, {r2, r8, ip, lr, pc}^
    899c:	93041c3d 	movwls	r1, #19517	; 0x4c3d
    89a0:	e0043508 	and	r3, r4, r8, lsl #10
    89a4:	9302883b 	movwls	r8, #10299	; 0x283b
    89a8:	887b1d3d 	ldmdahi	fp!, {r0, r2, r3, r4, r5, r8, sl, fp, ip}^
    89ac:	9b049304 	blls	12d5c4 <_end+0x1225c0>
    89b0:	27016ca2 	strcs	r6, [r1, -r2, lsr #25]
    89b4:	189b43bb 	ldmne	fp, {r0, r1, r3, r4, r5, r7, r8, r9, lr}
    89b8:	1c30210f 	ldfnes	f2, [r0], #-60	; 0xffffffc4
    89bc:	f7ff9306 			; <UNDEFINED> instruction: 0xf7ff9306
    89c0:	9b06ff4a 	blls	1c86f0 <_end+0x1bd6ec>
    89c4:	42832100 	addmi	r2, r3, #0, 2
    89c8:	9902d805 	stmdbls	r2, {r0, r2, fp, ip, lr, pc}
    89cc:	185943b9 	ldmdane	r9, {r0, r3, r4, r5, r7, r8, r9, lr}^
    89d0:	41804288 	orrmi	r4, r0, r8, lsl #5
    89d4:	9b044241 	blls	1192e0 <_end+0x10e2dc>
    89d8:	403b9a02 	eorsmi	r9, fp, r2, lsl #20
    89dc:	403a005b 	eorsmi	r0, sl, fp, asr r0
    89e0:	2b014313 	blcs	59634 <_end+0x4e630>
    89e4:	2b00d019 	blcs	3ca50 <_end+0x31a4c>
    89e8:	2b02d002 	blcs	bc9f8 <_end+0xb19f4>
    89ec:	e0cdd057 	sbc	sp, sp, r7, asr r0
    89f0:	1d2f9b01 	fstmdbxne	pc!, {d9-d8}	;@ Deprecated
    89f4:	d0c82b00 	sbcle	r2, r8, r0, lsl #22
    89f8:	d0c62900 	sbcle	r2, r6, r0, lsl #18
    89fc:	f7ff1c28 			; <UNDEFINED> instruction: 0xf7ff1c28
    8a00:	63a7fd4f 			; <UNDEFINED> instruction: 0x63a7fd4f
    8a04:	1c201c05 	stcne	12, cr1, [r0], #-20	; 0xffffffec
    8a08:	fcb0f000 	ldc2	0, cr15, [r0]
    8a0c:	d1002800 	tstle	r0, r0, lsl #16
    8a10:	1c30e0bc 	ldcne	0, cr14, [r0], #-752	; 0xfffffd10
    8a14:	1c2a210f 	stfnes	f2, [sl], #-60	; 0xffffffc4
    8a18:	9a01e0b4 	bls	80cf0 <_end+0x75cec>
    8a1c:	d1262a00 	teqle	r6, r0, lsl #20
    8a20:	d0392900 	eorsle	r2, r9, r0, lsl #18
    8a24:	0fd7682a 	svceq	0x00d7682a
    8a28:	1c91686a 	ldcne	8, cr6, [r1], {106}	; 0x6a
    8a2c:	e0add100 	adc	sp, sp, r0, lsl #2
    8a30:	31581c21 	cmpcc	r8, r1, lsr #24
    8a34:	32019108 	andcc	r9, r1, #8, 2
    8a38:	1d28d00b 	stcne	0, cr13, [r8, #-44]!	; 0xffffffd4
    8a3c:	fe01f7ff 	mcr2	7, 0, pc, cr1, cr15, {7}	; <UNPREDICTABLE>
    8a40:	ab081c3a 	blge	20fb30 <_end+0x204b2c>
    8a44:	1c201c01 	stcne	12, cr1, [r0], #-4
    8a48:	fc94f000 	ldc2	0, cr15, [r4], {0}
    8a4c:	d0231e07 	eorle	r1, r3, r7, lsl #28
    8a50:	1c1fe000 	ldcne	0, cr14, [pc], {-0}
    8a54:	210d1c30 	tstcs	sp, r0, lsr ip
    8a58:	fefdf7ff 	mrc2	7, 7, pc, cr13, cr15, {7}
    8a5c:	62209b08 	eorvs	r9, r0, #8, 22	; 0x2000
    8a60:	d0002f02 	andle	r2, r0, r2, lsl #30
    8a64:	62e3e09a 	rscvs	lr, r3, #154	; 0x9a
    8a68:	332c1c23 	teqcc	ip, #8960	; 0x2300
    8a6c:	1c30e096 	ldcne	0, cr14, [r0], #-600	; 0xfffffda8
    8a70:	6a27210d 	bvs	9d0eac <_end+0x9c5ea8>
    8a74:	feeff7ff 	mcr2	7, 7, pc, cr15, cr15, {7}	; <UNPREDICTABLE>
    8a78:	d10d4287 	smlabble	sp, r7, r2, r4
    8a7c:	429d6aa3 	addsmi	r6, sp, #667648	; 0xa3000
    8a80:	1c28d10a 	stfned	f5, [r8], #-40	; 0xffffffd8
    8a84:	fd0cf7ff 	stc2	7, cr15, [ip, #-1020]	; 0xfffffc04
    8a88:	1c02210f 	stfnes	f2, [r2], {15}
    8a8c:	f7ff1c30 			; <UNDEFINED> instruction: 0xf7ff1c30
    8a90:	1c30ff07 	ldcne	15, cr15, [r0], #-28	; 0xffffffe4
    8a94:	e0482100 	sub	r2, r8, r0, lsl #2
    8a98:	1c2f3508 	cfstr32ne	mvfx3, [pc], #-32	; 8a80 <__cxa_type_match@plt+0x6a8>
    8a9c:	682be775 	stmdavs	fp!, {r0, r2, r4, r5, r6, r8, r9, sl, sp, lr, pc}
    8aa0:	085b005b 	ldmdaeq	fp, {r0, r1, r3, r4, r6}^
    8aa4:	9b019302 	blls	6d6b4 <_end+0x626b0>
    8aa8:	d11c2b00 	tstle	ip, r0, lsl #22
    8aac:	d0402900 	suble	r2, r0, r0, lsl #18
    8ab0:	071b9b07 	ldreq	r9, [fp, -r7, lsl #22]
    8ab4:	9b02d502 	blls	bdec4 <_end+0xb2ec0>
    8ab8:	d13a2b00 	teqle	sl, r0, lsl #22
    8abc:	9b029f01 	blls	b06c8 <_end+0xa56c4>
    8ac0:	d065429f 	mlsle	r5, pc, r2, r4	; <UNPREDICTABLE>
    8ac4:	1c233701 	stcne	7, cr3, [r3], #-4
    8ac8:	335800b8 	cmpcc	r8, #184	; 0xb8
    8acc:	93081828 	movwls	r1, #34856	; 0x8828
    8ad0:	fdb7f7ff 	ldc2	7, cr15, [r7, #1020]!	; 0x3fc
    8ad4:	ab082200 	blge	2112dc <_end+0x2062d8>
    8ad8:	1c201c01 	stcne	12, cr1, [r0], #-4
    8adc:	fc4af000 	mcrr2	0, 0, pc, sl, cr0	; <UNPREDICTABLE>
    8ae0:	d0ec2800 	rscle	r2, ip, r0, lsl #16
    8ae4:	1c30e025 	ldcne	0, cr14, [r0], #-148	; 0xffffff6c
    8ae8:	6a27210d 	bvs	9d0f24 <_end+0x9c5f20>
    8aec:	feb3f7ff 	mrc2	7, 5, pc, cr3, cr15, {7}
    8af0:	d11e4287 	tstle	lr, r7, lsl #5
    8af4:	429d6aa3 	addsmi	r6, sp, #667648	; 0xa3000
    8af8:	9b02d11b 	blls	bcf6c <_end+0xb1f68>
    8afc:	230462a3 	movwcs	r6, #17059	; 0x42a3
    8b00:	27006323 	strcs	r6, [r0, -r3, lsr #6]
    8b04:	62e718eb 	rscvs	r1, r7, #15400960	; 0xeb0000
    8b08:	682b6363 	stmdavs	fp!, {r0, r1, r5, r6, r8, r9, sp, lr}
    8b0c:	da0e42bb 	ble	399600 <_end+0x38e5fc>
    8b10:	30019802 	andcc	r9, r1, r2, lsl #16
    8b14:	18280080 	stmdane	r8!, {r7}
    8b18:	fcc2f7ff 	stc2l	7, cr15, [r2], {255}	; 0xff
    8b1c:	1c02210f 	stfnes	f2, [r2], {15}
    8b20:	f7ff1c30 			; <UNDEFINED> instruction: 0xf7ff1c30
    8b24:	1c30febd 	ldcne	14, cr15, [r0], #-756	; 0xfffffd0c
    8b28:	1c221c39 	stcne	12, cr1, [r2], #-228	; 0xffffff1c
    8b2c:	2301e02a 	movwcs	lr, #4138	; 0x102a
    8b30:	682b9305 	stmdavs	fp!, {r0, r2, r8, r9, ip, pc}
    8b34:	da002b00 	ble	1373c <_end+0x8738>
    8b38:	9b023504 	blls	95f50 <_end+0x8af4c>
    8b3c:	009b3301 	addseq	r3, fp, r1, lsl #6
    8b40:	e72218ef 	str	r1, [r2, -pc, ror #17]!
    8b44:	93052300 	movwls	r2, #21248	; 0x5300
    8b48:	2b029b03 	blcs	af75c <_end+0xa4758>
    8b4c:	f7ffdd02 			; <UNDEFINED> instruction: 0xf7ffdd02
    8b50:	e003fd7f 	and	pc, r3, pc, ror sp	; <UNPREDICTABLE>
    8b54:	a9091c30 	stmdbge	r9, {r4, r5, sl, fp, ip}
    8b58:	fa6df000 	blx	1b84b60 <_end+0x1b79b5c>
    8b5c:	d1152800 	tstle	r5, r0, lsl #16
    8b60:	20089b05 	andcs	r9, r8, r5, lsl #22
    8b64:	d01c2b00 	andsle	r2, ip, r0, lsl #22
    8b68:	1c30210f 	ldfnes	f2, [r0], #-60	; 0xffffffc4
    8b6c:	fe73f7ff 	mrc2	7, 3, pc, cr3, cr15, {7}
    8b70:	1c02210e 	stfnes	f2, [r2], {14}
    8b74:	f7ff1c30 			; <UNDEFINED> instruction: 0xf7ff1c30
    8b78:	4a0bfe93 	bmi	3085cc <_end+0x2fd5c8>
    8b7c:	447a1c30 	ldrbtmi	r1, [sl], #-3120	; 0xfffff3d0
    8b80:	210f6812 	tstcs	pc, r2, lsl r8	; <UNPREDICTABLE>
    8b84:	fe8cf7ff 	mcr2	7, 4, pc, cr12, cr15, {7}	; <UNPREDICTABLE>
    8b88:	e00a2007 	and	r2, sl, r7
    8b8c:	e0082009 	and	r2, r8, r9
    8b90:	210d1c30 	tstcs	sp, r0, lsr ip
    8b94:	fe5ff7ff 	mrc2	7, 2, pc, cr15, cr15, {7}
    8b98:	62209b08 	eorvs	r9, r0, #8, 22	; 0x2000
    8b9c:	62632006 	rsbvs	r2, r3, #6
    8ba0:	b00d62a5 	andlt	r6, sp, r5, lsr #5
    8ba4:	46c0bdf0 			; <UNDEFINED> instruction: 0x46c0bdf0
    8ba8:	0000244e 	andeq	r2, r0, lr, asr #8
    8bac:	2300b508 	movwcs	fp, #1288	; 0x508
    8bb0:	febaf7ff 	mrc2	7, 5, pc, cr10, cr15, {7}
    8bb4:	b508bd08 	strlt	fp, [r8, #-3336]	; 0xfffff2f8
    8bb8:	f7ff2301 			; <UNDEFINED> instruction: 0xf7ff2301
    8bbc:	bd08feb5 	stclt	14, cr15, [r8, #-724]	; 0xfffffd2c
    8bc0:	2302b508 	movwcs	fp, #9480	; 0x2508
    8bc4:	feb0f7ff 	mrc2	7, 5, pc, cr0, cr15, {7}
    8bc8:	b5f0bd08 	ldrblt	fp, [r0, #3336]!	; 0xd08
    8bcc:	b0c51c05 	sbclt	r1, r5, r5, lsl #24
    8bd0:	d9002904 	stmdble	r0, {r2, r8, fp, sp}
    8bd4:	1c08e085 	stcne	0, cr14, [r8], {133}	; 0x85
    8bd8:	1c141c1e 	ldcne	12, cr1, [r4], {30}
    8bdc:	fb94f000 	blx	fe544be6 <_end+0xfe539be2>
    8be0:	2a811d03 	bcs	fe04fff4 <_end+0xfe044ff0>
    8be4:	20020055 	andcs	r0, r2, r5, asr r0
    8be8:	d0002b00 	andle	r2, r0, r0, lsl #22
    8bec:	0411e112 	ldreq	lr, [r1], #-274	; 0xfffffeee
    8bf0:	0c096bab 	stceq	11, cr6, [r9], {171}	; 0xab
    8bf4:	20011d2a 	andcs	r1, r1, sl, lsr #26
    8bf8:	40b71c07 	adcsmi	r1, r7, r7, lsl #24
    8bfc:	d0024239 	andle	r4, r2, r9, lsr r2
    8c00:	3304681f 	movwcc	r6, #18463	; 0x481f
    8c04:	36016017 			; <UNDEFINED> instruction: 0x36016017
    8c08:	2e103204 	cdpcs	2, 1, cr3, cr0, cr4, {0}
    8c0c:	2000d1f4 	strdcs	sp, [r0], -r4
    8c10:	d50004a2 	strle	r0, [r0, #-1186]	; 0xfffffb5e
    8c14:	63abe0fe 			; <UNDEFINED> instruction: 0x63abe0fe
    8c18:	2304e0fc 	movwcs	lr, #16636	; 0x40fc
    8c1c:	439a1c32 	orrsmi	r1, sl, #12800	; 0x3200
    8c20:	d15e2a01 	cmple	lr, r1, lsl #20
    8c24:	04240c23 	strteq	r0, [r4], #-3107	; 0xfffff3dd
    8c28:	93010c24 	movwls	r0, #7204	; 0x1c24
    8c2c:	2e0118e7 	cdpcs	8, 0, cr1, cr1, cr7, {7}
    8c30:	e050d159 	subs	sp, r0, r9, asr r1
    8c34:	d1542b03 	cmple	r4, r3, lsl #22
    8c38:	0c160414 	cfldrseq	mvf0, [r6], {20}
    8c3c:	19a30c24 	stmibne	r3!, {r2, r5, sl, fp}
    8c40:	d84e2b10 	stmdale	lr, {r4, r8, r9, fp, sp}^
    8c44:	2208682b 	andcs	r6, r8, #2818048	; 0x2b0000
    8c48:	d0064213 	andle	r4, r6, r3, lsl r2
    8c4c:	43931c28 	orrsmi	r1, r3, #40, 24	; 0x2800
    8c50:	602b3051 	eorvs	r3, fp, r1, asr r0
    8c54:	f00030ff 			; <UNDEFINED> instruction: 0xf00030ff
    8c58:	af22fb91 	svcge	0x0022fb91
    8c5c:	00f61c38 	rscseq	r1, r6, r8, lsr ip
    8c60:	fb8cf000 	blx	fe344c6a <_end+0xfe339c66>
    8c64:	19be0064 	ldmibne	lr!, {r2, r5, r6}
    8c68:	1c316bab 	ldcne	11, cr6, [r1], #-684	; 0xfffffd54
    8c6c:	3a011c22 	bcc	4fcfc <_end+0x44cf8>
    8c70:	1b88d303 	blne	fe23d884 <_end+0xfe232880>
    8c74:	c10158c0 	smlabtgt	r1, r0, r8, r5
    8c78:	00a4e7f9 	strdeq	lr, [r4], r9	; <UNPREDICTABLE>
    8c7c:	63ac191c 			; <UNDEFINED> instruction: 0x63ac191c
    8c80:	f0001c38 			; <UNDEFINED> instruction: 0xf0001c38
    8c84:	2000fb5f 	andcs	pc, r0, pc, asr fp	; <UNPREDICTABLE>
    8c88:	2b00e0c4 	blcs	40fa0 <_end+0x35f9c>
    8c8c:	2a10d129 	bcs	43d138 <_end+0x432134>
    8c90:	682bd827 	stmdavs	fp!, {r0, r1, r2, r5, fp, ip, lr, pc}
    8c94:	42132210 	andsmi	r2, r3, #16, 4
    8c98:	1c28d006 	stcne	0, cr13, [r8], #-24	; 0xffffffe8
    8c9c:	30d14393 	smullscc	r4, r1, r3, r3
    8ca0:	30ff602b 	rscscc	r6, pc, fp, lsr #32
    8ca4:	fb6ef000 	blx	1bc4cae <_end+0x1bb9caa>
    8ca8:	1c30ae22 	ldcne	14, cr10, [r0], #-136	; 0xffffff78
    8cac:	fb6af000 	blx	1ac4cb6 <_end+0x1ab9cb2>
    8cb0:	23006baa 	movwcs	r6, #2986	; 0xbaa
    8cb4:	1c082101 	stfnes	f2, [r8], {1}
    8cb8:	42044098 	andmi	r4, r4, #152	; 0x98
    8cbc:	6817d003 	ldmdavs	r7, {r0, r1, ip, lr, pc}
    8cc0:	32040098 	andcc	r0, r4, #152	; 0x98
    8cc4:	33015037 	movwcc	r5, #4151	; 0x1037
    8cc8:	d1f42b04 	mvnsle	r2, r4, lsl #22
    8ccc:	1c3063aa 	ldcne	3, cr6, [r0], #-680	; 0xfffffd58
    8cd0:	fb3cf000 	blx	f44cda <_end+0xf39cd6>
    8cd4:	2f10e7d7 	svccs	0x0010e7d7
    8cd8:	9b01d803 	blls	7ecec <_end+0x73ce8>
    8cdc:	d8002b0f 	stmdale	r0, {r0, r1, r2, r3, r8, r9, fp, sp}
    8ce0:	2002e092 	mulcs	r2, r2, r0
    8ce4:	2f20e096 	svccs	0x0020e096
    8ce8:	9b01d8fb 	blls	7f0dc <_end+0x740d8>
    8cec:	d9022b0f 	stmdble	r2, {r0, r1, r2, r3, r8, r9, fp, sp}
    8cf0:	d1521e27 	cmple	r2, r7, lsr #28
    8cf4:	2f10e010 	svccs	0x0010e010
    8cf8:	e085d800 	add	sp, r5, r0, lsl #16
    8cfc:	d1f02e05 	mvnsle	r2, r5, lsl #28
    8d00:	682b3f10 	stmdavs	fp!, {r4, r8, r9, sl, fp, ip, sp}
    8d04:	42132201 	andsmi	r2, r3, #268435456	; 0x10000000
    8d08:	2f00d168 	svccs	0x0000d168
    8d0c:	2e01d147 	mvfcssm	f5, f7
    8d10:	a822d17c 	stmdage	r2!, {r2, r3, r4, r5, r6, r8, ip, lr, pc}
    8d14:	fb3af000 	blx	ec4d1e <_end+0xeb9d1a>
    8d18:	27001c23 	strcs	r1, [r0, -r3, lsr #24]
    8d1c:	1c146baa 	ldcne	11, cr6, [r4], {170}	; 0xaa
    8d20:	dd102b00 	vldrle	d2, [r0, #-0]
    8d24:	469c005b 			; <UNDEFINED> instruction: 0x469c005b
    8d28:	a9229b01 	stmdbge	r2!, {r0, r8, r9, fp, ip, pc}
    8d2c:	18cb00db 	stmiane	fp, {r0, r1, r3, r4, r6, r7}^
    8d30:	46611c18 			; <UNDEFINED> instruction: 0x46611c18
    8d34:	d3033901 	movwle	r3, #14593	; 0x3901
    8d38:	58a41ac4 	stmiapl	r4!, {r2, r6, r7, r9, fp, ip}
    8d3c:	e7f9c010 			; <UNDEFINED> instruction: 0xe7f9c010
    8d40:	009b4663 	addseq	r4, fp, r3, ror #12
    8d44:	2f0018d4 	svccs	0x000018d4
    8d48:	9b01d010 	blls	7cd90 <_end+0x71d8c>
    8d4c:	d2002b10 	andle	r2, r0, #16, 22	; 0x4000
    8d50:	3b102310 	blcc	411998 <_end+0x406994>
    8d54:	00dbaa02 	sbcseq	sl, fp, r2, lsl #20
    8d58:	00f918d3 	ldrsbteq	r1, [r9], #131	; 0x83
    8d5c:	428a2200 	addmi	r2, sl, #0, 4
    8d60:	58a0d003 	stmiapl	r0!, {r0, r1, ip, lr, pc}
    8d64:	32045098 	andcc	r5, r4, #152	; 0x98
    8d68:	18a4e7f9 	stmiane	r4!, {r0, r3, r4, r5, r6, r7, r8, r9, sl, sp, lr, pc}
    8d6c:	d1002e01 	tstle	r0, r1, lsl #28
    8d70:	63ac3404 			; <UNDEFINED> instruction: 0x63ac3404
    8d74:	d1032e01 	tstle	r3, r1, lsl #28
    8d78:	f000a822 			; <UNDEFINED> instruction: 0xf000a822
    8d7c:	e782fadb 			; <UNDEFINED> instruction: 0xe782fadb
    8d80:	2b0f9b01 	blcs	3ef98c <_end+0x3e4988>
    8d84:	a822d802 	stmdage	r2!, {r1, fp, ip, lr, pc}
    8d88:	fad0f000 	blx	ff444d90 <_end+0xff439d8c>
    8d8c:	d1002f00 	tstle	r0, r0, lsl #30
    8d90:	a802e779 	stmdage	r2, {r0, r3, r4, r5, r6, r8, r9, sl, sp, lr, pc}
    8d94:	fad2f000 	blx	ff4c4d9c <_end+0xff4b9d98>
    8d98:	2e05e775 	mcrcs	7, 0, lr, cr5, cr5, {3}
    8d9c:	682bd1a1 	stmdavs	fp!, {r0, r5, r7, r8, ip, lr, pc}
    8da0:	42132204 	andsmi	r2, r3, #4, 4	; 0x40000000
    8da4:	4393d005 	orrsmi	sp, r3, #5
    8da8:	602b1c28 	eorvs	r1, fp, r8, lsr #24
    8dac:	f00030d0 			; <UNDEFINED> instruction: 0xf00030d0
    8db0:	2e01faf1 	mcrcs	10, 0, pc, cr1, cr1, {7}	; <UNPREDICTABLE>
    8db4:	9b01d00e 	blls	7cdf4 <_end+0x71df0>
    8db8:	d8022b0f 	stmdale	r2, {r0, r1, r2, r3, r8, r9, fp, sp}
    8dbc:	f000a822 			; <UNDEFINED> instruction: 0xf000a822
    8dc0:	2f00faed 	svccs	0x0000faed
    8dc4:	a802d0a8 	stmdage	r2, {r3, r5, r7, ip, lr, pc}
    8dc8:	fae4f000 	blx	ff944dd0 <_end+0xff939dcc>
    8dcc:	23109a01 	tstcs	r0, #4096	; 0x1000
    8dd0:	e7a31a9b 			; <UNDEFINED> instruction: 0xe7a31a9b
    8dd4:	f000a822 			; <UNDEFINED> instruction: 0xf000a822
    8dd8:	e7f7fad9 	ubfx	pc, r9, #21, #24
    8ddc:	43911c19 	orrsmi	r1, r1, #6400	; 0x1900
    8de0:	1c0a1c28 	stcne	12, cr1, [sl], {40}	; 0x28
    8de4:	30486029 	subcc	r6, r8, r9, lsr #32
    8de8:	d1072e05 	tstle	r7, r5, lsl #28
    8dec:	431a2302 	tstmi	sl, #134217728	; 0x8000000
    8df0:	f000602a 			; <UNDEFINED> instruction: 0xf000602a
    8df4:	2f00fad3 	svccs	0x0000fad3
    8df8:	e7dfd1d1 			; <UNDEFINED> instruction: 0xe7dfd1d1
    8dfc:	43932203 	orrsmi	r2, r3, #805306368	; 0x30000000
    8e00:	f000602b 			; <UNDEFINED> instruction: 0xf000602b
    8e04:	e780fac3 	str	pc, [r0, r3, asr #21]
    8e08:	e77a2700 	ldrb	r2, [sl, -r0, lsl #14]!
    8e0c:	2b0f9b01 	blcs	3efa18 <_end+0x3e4a14>
    8e10:	e781d9d4 			; <UNDEFINED> instruction: 0xe781d9d4
    8e14:	bdf0b045 	ldcllt	0, cr11, [r0, #276]!	; 0x114
    8e18:	e2801034 	add	r1, r0, #52	; 0x34
    8e1c:	e8910038 	ldm	r1, {r3, r4, r5}
    8e20:	e92d0038 	push	{r3, r4, r5}
    8e24:	e8900fff 	ldm	r0, {r0, r1, r2, r3, r4, r5, r6, r7, r8, r9, sl, fp}
    8e28:	e89de000 	ldm	sp, {sp, lr, pc}
    8e2c:	ec900b21 	fldmiax	r0, {d0-d15}	;@ Deprecated
    8e30:	e12fff1e 	bx	lr
    8e34:	ec800b21 	fstmiax	r0, {d0-d15}	;@ Deprecated
    8e38:	e12fff1e 	bx	lr
    8e3c:	ec900b20 	vldmia	r0, {d0-d15}
    8e40:	e12fff1e 	bx	lr
    8e44:	ec800b20 	vstmia	r0, {d0-d15}
    8e48:	e12fff1e 	bx	lr
    8e4c:	ecd00b20 	vldmia	r0, {d16-d31}
    8e50:	e12fff1e 	bx	lr
    8e54:	ecc00b20 	vstmia	r0, {d16-d31}
    8e58:	e12fff1e 	bx	lr
    8e5c:	ecf00102 	ldfe	f0, [r0], #8
    8e60:	ecf01102 	ldfe	f1, [r0], #8
    8e64:	ecf02102 	ldfe	f2, [r0], #8
    8e68:	ecf03102 	ldfe	f3, [r0], #8
    8e6c:	ecf04102 	ldfe	f4, [r0], #8
    8e70:	ecf05102 	ldfe	f5, [r0], #8
    8e74:	ecf06102 	ldfe	f6, [r0], #8
    8e78:	ecf07102 	ldfe	f7, [r0], #8
    8e7c:	ecf08102 	ldfp	f0, [r0], #8
    8e80:	ecf09102 	ldfp	f1, [r0], #8
    8e84:	ecf0a102 	ldfp	f2, [r0], #8
    8e88:	ecf0b102 	ldfp	f3, [r0], #8
    8e8c:	ecf0c102 	ldfp	f4, [r0], #8
    8e90:	ecf0d102 	ldfp	f5, [r0], #8
    8e94:	ecf0e102 	ldfp	f6, [r0], #8
    8e98:	ecf0f102 	ldfp	f7, [r0], #8
    8e9c:	e12fff1e 	bx	lr
    8ea0:	ece00102 	stfe	f0, [r0], #8
    8ea4:	ece01102 	stfe	f1, [r0], #8
    8ea8:	ece02102 	stfe	f2, [r0], #8
    8eac:	ece03102 	stfe	f3, [r0], #8
    8eb0:	ece04102 	stfe	f4, [r0], #8
    8eb4:	ece05102 	stfe	f5, [r0], #8
    8eb8:	ece06102 	stfe	f6, [r0], #8
    8ebc:	ece07102 	stfe	f7, [r0], #8
    8ec0:	ece08102 	stfp	f0, [r0], #8
    8ec4:	ece09102 	stfp	f1, [r0], #8
    8ec8:	ece0a102 	stfp	f2, [r0], #8
    8ecc:	ece0b102 	stfp	f3, [r0], #8
    8ed0:	ece0c102 	stfp	f4, [r0], #8
    8ed4:	ece0d102 	stfp	f5, [r0], #8
    8ed8:	ece0e102 	stfp	f6, [r0], #8
    8edc:	ece0f102 	stfp	f7, [r0], #8
    8ee0:	e12fff1e 	bx	lr
    8ee4:	fcb08101 	ldc2	1, cr8, [r0], #4
    8ee8:	fcb09101 	ldc2	1, cr9, [r0], #4
    8eec:	fcb0a101 	ldc2	1, cr10, [r0], #4
    8ef0:	fcb0b101 	ldc2	1, cr11, [r0], #4
    8ef4:	e12fff1e 	bx	lr
    8ef8:	fca08101 	stc2	1, cr8, [r0], #4
    8efc:	fca09101 	stc2	1, cr9, [r0], #4
    8f00:	fca0a101 	stc2	1, cr10, [r0], #4
    8f04:	fca0b101 	stc2	1, cr11, [r0], #4
    8f08:	e12fff1e 	bx	lr
    8f0c:	e92de000 	push	{sp, lr, pc}
    8f10:	e92d1fff 	push	{r0, r1, r2, r3, r4, r5, r6, r7, r8, r9, sl, fp, ip}
    8f14:	e3a03000 	mov	r3, #0
    8f18:	e92d000c 	push	{r2, r3}
    8f1c:	e28d1004 	add	r1, sp, #4
    8f20:	e28fc004 	add	ip, pc, #4
    8f24:	e38cc001 	orr	ip, ip, #1
    8f28:	e12fff1c 	bx	ip
    8f2c:	fc10f7ff 	ldc2	7, cr15, [r0], {255}	; 0xff
    8f30:	b0129b10 	andslt	r9, r2, r0, lsl fp
    8f34:	46c04718 			; <UNDEFINED> instruction: 0x46c04718
    8f38:	e92de000 	push	{sp, lr, pc}
    8f3c:	e92d1fff 	push	{r0, r1, r2, r3, r4, r5, r6, r7, r8, r9, sl, fp, ip}
    8f40:	e3a03000 	mov	r3, #0
    8f44:	e92d000c 	push	{r2, r3}
    8f48:	e28d1004 	add	r1, sp, #4
    8f4c:	e28fc004 	add	ip, pc, #4
    8f50:	e38cc001 	orr	ip, ip, #1
    8f54:	e12fff1c 	bx	ip
    8f58:	fc2bf7ff 	stc2	7, cr15, [fp], #-1020	; 0xfffffc04
    8f5c:	b0129b10 	andslt	r9, r2, r0, lsl fp
    8f60:	46c04718 			; <UNDEFINED> instruction: 0x46c04718
    8f64:	e92de000 	push	{sp, lr, pc}
    8f68:	e92d1fff 	push	{r0, r1, r2, r3, r4, r5, r6, r7, r8, r9, sl, fp, ip}
    8f6c:	e3a03000 	mov	r3, #0
    8f70:	e92d000c 	push	{r2, r3}
    8f74:	e28d1004 	add	r1, sp, #4
    8f78:	e28fc004 	add	ip, pc, #4
    8f7c:	e38cc001 	orr	ip, ip, #1
    8f80:	e12fff1c 	bx	ip
    8f84:	fc37f7ff 	ldc2	7, cr15, [r7], #-1020	; 0xfffffc04
    8f88:	b0129b10 	andslt	r9, r2, r0, lsl fp
    8f8c:	46c04718 			; <UNDEFINED> instruction: 0x46c04718
    8f90:	e92de000 	push	{sp, lr, pc}
    8f94:	e92d1fff 	push	{r0, r1, r2, r3, r4, r5, r6, r7, r8, r9, sl, fp, ip}
    8f98:	e3a03000 	mov	r3, #0
    8f9c:	e92d000c 	push	{r2, r3}
    8fa0:	e28d3004 	add	r3, sp, #4
    8fa4:	e28fc004 	add	ip, pc, #4
    8fa8:	e38cc001 	orr	ip, ip, #1
    8fac:	e12fff1c 	bx	ip
    8fb0:	fbf5f7ff 	blx	ffd86fb6 <_end+0xffd7bfb2>
    8fb4:	b0129b10 	andslt	r9, r2, r0, lsl fp
    8fb8:	46c04718 			; <UNDEFINED> instruction: 0x46c04718
    8fbc:	e92de000 	push	{sp, lr, pc}
    8fc0:	e92d1fff 	push	{r0, r1, r2, r3, r4, r5, r6, r7, r8, r9, sl, fp, ip}
    8fc4:	e3a03000 	mov	r3, #0
    8fc8:	e92d000c 	push	{r2, r3}
    8fcc:	e28d2004 	add	r2, sp, #4
    8fd0:	e28fc004 	add	ip, pc, #4
    8fd4:	e38cc001 	orr	ip, ip, #1
    8fd8:	e12fff1c 	bx	ip
    8fdc:	fc6cf7ff 	stc2l	7, cr15, [ip], #-1020	; 0xfffffc04
    8fe0:	b0129b10 	andslt	r9, r2, r0, lsl fp
    8fe4:	46c04718 			; <UNDEFINED> instruction: 0x46c04718
    8fe8:	1c037a02 	stcne	10, cr7, [r3], {2}
    8fec:	d10c2a00 	tstle	ip, r0, lsl #20
    8ff0:	20b07a42 	adcscs	r7, r0, r2, asr #20
    8ff4:	d00e2a00 	andle	r2, lr, r0, lsl #20
    8ff8:	725a3a01 	subsvc	r3, sl, #4096	; 0x1000
    8ffc:	1d11685a 	ldcne	8, cr6, [r1, #-360]	; 0xfffffe98
    9000:	601a6812 	andsvs	r6, sl, r2, lsl r8
    9004:	22036059 	andcs	r6, r3, #89	; 0x59
    9008:	3a01e000 	bcc	81010 <_end+0x7600c>
    900c:	721a6818 	andsvc	r6, sl, #24, 16	; 0x180000
    9010:	0e000202 	cdpeq	2, 0, cr0, cr0, cr2, {0}
    9014:	4770601a 			; <UNDEFINED> instruction: 0x4770601a
    9018:	2100b51f 	tstcs	r0, pc, lsl r5
    901c:	9300ab03 	movwls	sl, #2819	; 0xb03
    9020:	1c0b220c 	sfmne	f2, 4, [fp], {12}
    9024:	fbfdf7ff 	blx	fff8702a <_end+0xfff7c026>
    9028:	b0059803 	andlt	r9, r5, r3, lsl #16
    902c:	b508bd00 	strlt	fp, [r8, #-3328]	; 0xfffff300
    9030:	fff2f7ff 			; <UNDEFINED> instruction: 0xfff2f7ff
    9034:	b5f0bd08 	ldrblt	fp, [r0, #3336]!	; 0xd08
    9038:	b0872300 	addlt	r2, r7, r0, lsl #6
    903c:	1c0f1c05 	stcne	12, cr1, [pc], {5}
    9040:	1c389302 	ldcne	3, cr9, [r8], #-8
    9044:	ffd0f7ff 			; <UNDEFINED> instruction: 0xffd0f7ff
    9048:	2cb01e04 	ldccs	14, cr1, [r0], #16
    904c:	9b02d114 	blls	bd4a4 <_end+0xb24a0>
    9050:	42a32400 	adcmi	r2, r3, #0, 8
    9054:	e12dd000 	teq	sp, r0
    9058:	1c21ae05 	stcne	14, cr10, [r1], #-20	; 0xffffffec
    905c:	96001c23 	strls	r1, [r0], -r3, lsr #24
    9060:	220e1c28 	andcs	r1, lr, #40, 24	; 0x2800
    9064:	fbddf7ff 	blx	ff78706a <_end+0xff77c066>
    9068:	1c289600 	stcne	6, cr9, [r8], #-0
    906c:	220f1c21 	andcs	r1, pc, #8448	; 0x2100
    9070:	f7ff1c23 			; <UNDEFINED> instruction: 0xf7ff1c23
    9074:	e11dfbfb 			; <UNDEFINED> instruction: 0xe11dfbfb
    9078:	1c02237f 	stcne	3, cr2, [r2], {127}	; 0x7f
    907c:	0613439a 			; <UNDEFINED> instruction: 0x0613439a
    9080:	d1140e1b 	tstle	r4, fp, lsl lr
    9084:	22ff0086 	rscscs	r0, pc, #134	; 0x86
    9088:	aa054016 	bge	1590e8 <_end+0x14e0e4>
    908c:	92009203 	andls	r9, r0, #805306368	; 0x30000000
    9090:	220d1c19 	andcs	r1, sp, #6400	; 0x1900
    9094:	f7ff1c28 			; <UNDEFINED> instruction: 0xf7ff1c28
    9098:	9a05fbc4 	bls	187fb0 <_end+0x17cfac>
    909c:	18b33604 	ldmne	r3!, {r2, r9, sl, ip, sp}
    90a0:	d5000661 	strle	r0, [r0, #-1633]	; 0xfffff99f
    90a4:	93051b93 	movwls	r1, #23443	; 0x5b93
    90a8:	93009b03 	movwls	r9, #2819	; 0xb03
    90ac:	260fe02f 	strcs	lr, [pc], -pc, lsr #32
    90b0:	43b31c03 			; <UNDEFINED> instruction: 0x43b31c03
    90b4:	0e1b061b 	mrceq	6, 0, r0, cr11, cr11, {0}
    90b8:	d1182b80 	tstle	r8, r0, lsl #23
    90bc:	1c380204 	lfmne	f0, 4, [r8], #-16
    90c0:	ff92f7ff 			; <UNDEFINED> instruction: 0xff92f7ff
    90c4:	02362680 	eorseq	r2, r6, #128, 12	; 0x8000000
    90c8:	42b04320 	adcsmi	r4, r0, #32, 6	; 0x80000000
    90cc:	2409d101 	strcs	sp, [r9], #-257	; 0xfffffeff
    90d0:	0502e0f0 	streq	lr, [r2, #-240]	; 0xffffff10
    90d4:	01042100 	mrseq	r2, (UNDEF: 20)
    90d8:	1c280c12 	stcne	12, cr0, [r8], #-72	; 0xffffffb8
    90dc:	f7ff1c0b 			; <UNDEFINED> instruction: 0xf7ff1c0b
    90e0:	2800fd74 	stmdacs	r0, {r2, r4, r5, r6, r8, sl, fp, ip, sp, lr, pc}
    90e4:	4234d1f3 	eorsmi	sp, r4, #-1073741764	; 0xc000003c
    90e8:	2301d0ab 	movwcs	sp, #4267	; 0x10ab
    90ec:	2b90e7a8 	blcs	fe442f94 <_end+0xfe437f90>
    90f0:	230dd114 	movwcs	sp, #53524	; 0xd114
    90f4:	2b0d4003 	blcs	359108 <_end+0x34e104>
    90f8:	1c02d0e9 	stcne	0, cr13, [r2], {233}	; 0xe9
    90fc:	2100ac05 	tstcs	r0, r5, lsl #24
    9100:	94004032 	strls	r4, [r0], #-50	; 0xffffffce
    9104:	1c0b1c28 	stcne	12, cr1, [fp], {40}	; 0x28
    9108:	fb8bf7ff 	blx	fe30710e <_end+0xfe2fc10a>
    910c:	21009400 	tstcs	r0, r0, lsl #8
    9110:	220d1c28 	andcs	r1, sp, #40, 24	; 0x2800
    9114:	f7ff1c0b 			; <UNDEFINED> instruction: 0xf7ff1c0b
    9118:	e792fba9 	ldr	pc, [r2, r9, lsr #23]
    911c:	d10f2ba0 	smlatble	pc, r0, fp, r2	; <UNPREDICTABLE>
    9120:	011b23ff 			; <UNDEFINED> instruction: 0x011b23ff
    9124:	43822207 	orrmi	r2, r2, #1879048192	; 0x70000000
    9128:	41111c19 	tstmi	r1, r9, lsl ip
    912c:	401a1c0a 	andsmi	r1, sl, sl, lsl #24
    9130:	d5020703 	strle	r0, [r2, #-1795]	; 0xfffff8fd
    9134:	01db2380 	bicseq	r2, fp, r0, lsl #7
    9138:	1c28431a 	stcne	3, cr4, [r8], #-104	; 0xffffff98
    913c:	e0822100 	add	r2, r2, r0, lsl #2
    9140:	d1552bb0 	ldrhle	r2, [r5, #-176]	; 0xffffff50
    9144:	d10c28b1 			; <UNDEFINED> instruction: 0xd10c28b1
    9148:	f7ff1c38 			; <UNDEFINED> instruction: 0xf7ff1c38
    914c:	1e02ff4d 	cdpne	15, 0, cr15, cr2, cr13, {2}
    9150:	1c03d0bd 	stcne	0, cr13, [r3], {189}	; 0xbd
    9154:	061b43b3 			; <UNDEFINED> instruction: 0x061b43b3
    9158:	d1b80e1b 			; <UNDEFINED> instruction: 0xd1b80e1b
    915c:	1c191c28 	ldcne	12, cr1, [r9], {40}	; 0x28
    9160:	28b2e0a2 	ldmcs	r2!, {r1, r5, r7, sp, lr, pc}
    9164:	2100d128 	tstcs	r0, r8, lsr #2
    9168:	220dae05 	andcs	sl, sp, #5, 28	; 0x50
    916c:	96001c0b 	strls	r1, [r0], -fp, lsl #24
    9170:	f7ff1c28 			; <UNDEFINED> instruction: 0xf7ff1c28
    9174:	1c38fb56 	ldcne	11, cr15, [r8], #-344	; 0xfffffea8
    9178:	ff36f7ff 			; <UNDEFINED> instruction: 0xff36f7ff
    917c:	23802402 	orrcs	r2, r0, #33554432	; 0x2000000
    9180:	4003227f 	andmi	r2, r3, pc, ror r2
    9184:	99054694 	stmdbls	r5, {r2, r4, r7, r9, sl, lr}
    9188:	4662d009 	strbtmi	sp, [r2], -r9
    918c:	40a24002 	adcmi	r4, r2, r2
    9190:	90051888 	andls	r1, r5, r8, lsl #17
    9194:	34071c38 	strcc	r1, [r7], #-3128	; 0xfffff3c8
    9198:	ff26f7ff 			; <UNDEFINED> instruction: 0xff26f7ff
    919c:	2281e7ef 	addcs	lr, r1, #62652416	; 0x3bc0000
    91a0:	18890092 	stmne	r9, {r1, r4, r7}
    91a4:	40024662 	andmi	r4, r2, r2, ror #12
    91a8:	188c40a2 	stmne	ip, {r1, r5, r7, lr}
    91ac:	96009405 	strls	r9, [r0], -r5, lsl #8
    91b0:	1c191c28 	ldcne	12, cr1, [r9], {40}	; 0x28
    91b4:	e7ae220d 	str	r2, [lr, sp, lsl #4]!
    91b8:	d10b28b3 			; <UNDEFINED> instruction: 0xd10b28b3
    91bc:	f7ff1c38 			; <UNDEFINED> instruction: 0xf7ff1c38
    91c0:	1c02ff13 	stcne	15, cr15, [r2], {19}
    91c4:	060043b0 			; <UNDEFINED> instruction: 0x060043b0
    91c8:	0e004032 	mcreq	0, 0, r4, cr0, cr2, {1}
    91cc:	03003201 	movweq	r3, #513	; 0x201
    91d0:	e00a4302 	and	r4, sl, r2, lsl #6
    91d4:	400323fc 	strdmi	r2, [r3], -ip
    91d8:	d1002bb4 			; <UNDEFINED> instruction: 0xd1002bb4
    91dc:	2307e777 	movwcs	lr, #30583	; 0x7777
    91e0:	2280401c 	addcs	r4, r0, #28
    91e4:	03123401 	tsteq	r2, #16777216	; 0x1000000
    91e8:	1c284322 	stcne	3, cr4, [r8], #-136	; 0xffffff78
    91ec:	e02a2101 	eor	r2, sl, r1, lsl #2
    91f0:	d1492bc0 	smlalbtle	r2, r9, r0, fp
    91f4:	d10b28c6 	smlabtle	fp, r6, r8, r2
    91f8:	f7ff1c38 			; <UNDEFINED> instruction: 0xf7ff1c38
    91fc:	1c02fef5 	stcne	14, cr15, [r2], {245}	; 0xf5
    9200:	060043b0 			; <UNDEFINED> instruction: 0x060043b0
    9204:	0e004032 	mcreq	0, 0, r4, cr0, cr2, {1}
    9208:	03003201 	movweq	r3, #513	; 0x201
    920c:	e0184302 	ands	r4, r8, r2, lsl #6
    9210:	d10c28c7 	smlabtle	ip, r7, r8, r2
    9214:	f7ff1c38 			; <UNDEFINED> instruction: 0xf7ff1c38
    9218:	1e02fee7 	cdpne	14, 0, cr15, cr2, cr7, {7}
    921c:	e756d100 	ldrb	sp, [r6, -r0, lsl #2]
    9220:	400323f0 	strdmi	r2, [r3], -r0
    9224:	e752d000 	ldrb	sp, [r2, -r0]
    9228:	21041c28 	tstcs	r4, r8, lsr #24
    922c:	23f8e03c 	mvnscs	lr, #60	; 0x3c
    9230:	2bc04003 	blcs	ff019244 <_end+0xff00e240>
    9234:	230fd109 	movwcs	sp, #61705	; 0xf109
    9238:	22a0401c 	adccs	r4, r0, #28
    923c:	03123401 	tsteq	r2, #16777216	; 0x1000000
    9240:	1c284322 	stcne	3, cr4, [r8], #-136	; 0xffffff78
    9244:	1c0b2103 	stfnes	f2, [fp], {3}
    9248:	28c8e02e 	stmiacs	r8, {r1, r2, r3, r5, sp, lr, pc}^
    924c:	1c38d10c 	ldfned	f5, [r8], #-48	; 0xffffffd0
    9250:	fecaf7ff 	mcr2	7, 6, pc, cr10, cr15, {7}	; <UNPREDICTABLE>
    9254:	1c03220f 	sfmne	f2, 4, [r3], {15}
    9258:	061b4393 			; <UNDEFINED> instruction: 0x061b4393
    925c:	33100e1b 	tstcc	r0, #432	; 0x1b0
    9260:	031b4002 	tsteq	fp, #2
    9264:	e01b3201 	ands	r3, fp, r1, lsl #4
    9268:	d00028c9 	andle	r2, r0, r9, asr #17
    926c:	1c38e72f 	ldcne	7, cr14, [r8], #-188	; 0xffffff44
    9270:	febaf7ff 	mrc2	7, 5, pc, cr10, cr15, {7}
    9274:	1c02230f 	stcne	3, cr2, [r2], {15}
    9278:	06004398 			; <UNDEFINED> instruction: 0x06004398
    927c:	0e00401a 	mcreq	0, 0, r4, cr0, cr10, {0}
    9280:	03003201 	movweq	r3, #513	; 0x201
    9284:	e00c4302 	and	r4, ip, r2, lsl #6
    9288:	1c032207 	sfmne	f2, 4, [r3], {7}
    928c:	061b4393 			; <UNDEFINED> instruction: 0x061b4393
    9290:	2bd00e1b 	blcs	ff40cb04 <_end+0xff401b00>
    9294:	e71ad000 	ldr	sp, [sl, -r0]
    9298:	23804002 	orrcs	r4, r0, #2
    929c:	031b3201 	tsteq	fp, #268435456	; 0x10000000
    92a0:	1c28431a 	stcne	3, cr4, [r8], #-104	; 0xffffff98
    92a4:	23052101 	movwcs	r2, #20737	; 0x5101
    92a8:	fc8ff7ff 	stc2	7, cr15, [pc], {255}	; 0xff
    92ac:	d0002800 	andle	r2, r0, r0, lsl #16
    92b0:	e6c6e70d 	strb	lr, [r6], sp, lsl #14
    92b4:	b0071c20 	andlt	r1, r7, r0, lsr #24
    92b8:	b51fbdf0 	ldrlt	fp, [pc, #-3568]	; 84d0 <__cxa_type_match@plt+0xf8>
    92bc:	ab016cc2 	blge	645cc <_end+0x595c8>
    92c0:	02046850 	andeq	r6, r4, #80, 16	; 0x500000
    92c4:	30081c10 	andcc	r1, r8, r0, lsl ip
    92c8:	20039002 	andcs	r9, r3, r2
    92cc:	1c087218 	sfmne	f7, 4, [r8], {24}
    92d0:	1c1979d2 	ldcne	9, cr7, [r9], {210}	; 0xd2
    92d4:	725a9401 	subsvc	r9, sl, #16777216	; 0x1000000
    92d8:	feadf7ff 	mcr2	7, 5, pc, cr13, cr15, {7}	; <UNPREDICTABLE>
    92dc:	bd10b004 	ldclt	0, cr11, [r0, #-16]
    92e0:	f7ffb508 			; <UNDEFINED> instruction: 0xf7ffb508
    92e4:	6c80fea4 	stcvs	14, cr15, [r0], {164}	; 0xa4
    92e8:	b508bd08 	strlt	fp, [r8, #-3336]	; 0xfffff2f8
    92ec:	fe9ff7ff 	mrc2	7, 4, pc, cr15, cr15, {7}
    92f0:	79d86cc3 	ldmibvc	r8, {r0, r1, r6, r7, sl, fp, sp, lr}^
    92f4:	30080080 	andcc	r0, r8, r0, lsl #1
    92f8:	bd081818 	stclt	8, cr1, [r8, #-96]	; 0xffffffa0
    92fc:	f000b508 			; <UNDEFINED> instruction: 0xf000b508
    9300:	b508f829 	strlt	pc, [r8, #-2089]	; 0xfffff7d7
    9304:	f826f000 			; <UNDEFINED> instruction: 0xf826f000
    9308:	4671b402 	ldrbtmi	fp, [r1], -r2, lsl #8
    930c:	00490849 	subeq	r0, r9, r9, asr #16
    9310:	00495c09 	subeq	r5, r9, r9, lsl #24
    9314:	bc02448e 	cfstrslt	mvf4, [r2], {142}	; 0x8e
    9318:	46c04770 			; <UNDEFINED> instruction: 0x46c04770
    931c:	46c04778 			; <UNDEFINED> instruction: 0x46c04778
    9320:	eafffc1d 	b	839c <puts@plt>
    9324:	46c04778 			; <UNDEFINED> instruction: 0x46c04778
    9328:	eafffc1e 	b	83a8 <__gnu_Unwind_Find_exidx@plt>
    932c:	46c04778 			; <UNDEFINED> instruction: 0x46c04778
    9330:	eafffec1 	b	8e3c <__cxa_type_match@plt+0xa64>
    9334:	46c04778 			; <UNDEFINED> instruction: 0x46c04778
    9338:	eafffebb 	b	8e2c <__cxa_type_match@plt+0xa54>
    933c:	46c04778 			; <UNDEFINED> instruction: 0x46c04778
    9340:	eafffec1 	b	8e4c <__cxa_type_match@plt+0xa74>
    9344:	46c04778 			; <UNDEFINED> instruction: 0x46c04778
    9348:	eafffec3 	b	8e5c <__cxa_type_match@plt+0xa84>
    934c:	46c04778 			; <UNDEFINED> instruction: 0x46c04778
    9350:	eafffee3 	b	8ee4 <__cxa_type_match@plt+0xb0c>
    9354:	46c04778 			; <UNDEFINED> instruction: 0x46c04778
    9358:	eafffc15 	b	83b4 <abort@plt>
    935c:	46c04778 			; <UNDEFINED> instruction: 0x46c04778
    9360:	eafffeac 	b	8e18 <__cxa_type_match@plt+0xa40>
    9364:	46c04778 			; <UNDEFINED> instruction: 0x46c04778
    9368:	eafffc14 	b	83c0 <memcpy@plt>
    936c:	46c04778 			; <UNDEFINED> instruction: 0x46c04778
    9370:	eafffc15 	b	83cc <__cxa_begin_cleanup@plt>
    9374:	46c04778 			; <UNDEFINED> instruction: 0x46c04778
    9378:	eafffc16 	b	83d8 <__cxa_type_match@plt>
    937c:	46c04778 			; <UNDEFINED> instruction: 0x46c04778
    9380:	eafffec6 	b	8ea0 <__cxa_type_match@plt+0xac8>
    9384:	46c04778 			; <UNDEFINED> instruction: 0x46c04778
    9388:	eafffeda 	b	8ef8 <__cxa_type_match@plt+0xb20>
    938c:	46c04778 			; <UNDEFINED> instruction: 0x46c04778
    9390:	eafffea7 	b	8e34 <__cxa_type_match@plt+0xa5c>
    9394:	46c04778 			; <UNDEFINED> instruction: 0x46c04778
    9398:	eafffead 	b	8e54 <__cxa_type_match@plt+0xa7c>
    939c:	46c04778 			; <UNDEFINED> instruction: 0x46c04778
    93a0:	eafffea7 	b	8e44 <__cxa_type_match@plt+0xa6c>
```

我们可以从上面看到他用汇编显示了这个文件的内容

plt:主要用于函数重定位

text:程序代码段

# ida pro

可以说是最强大的反汇编器，具体使用方法时将so拖入ida创建

## for















