---
layout: post
title: 10bit二进制数反转位序后转换十六进制
comments: true
tags:
  - EXCEL
date: 2025-04-09 16:50:16
---
例如二进制数11111，通过EXCEL先扩展成10bit的二进制数，再首位翻转后，转换成十六进制
<!--more-->
首先在EXCEL中键入如下函数，将“11111”的显示转换成“0000011111”的显示。
```
  =TEXT(11111,"0000000000")
```
![插入图片](/assets/images/250409_1.jpg)

然后在EXCEL中键入如下函数，将“0000011111”的显示首位翻转成“1111100000”的显示。
```
  =CONCAT(MID(0000011111,{10,9,8,7,6,5,4,3,2,1},1))
```
![插入图片](/assets/images/250409_2.jpg)

最后在EXCEL中键入如下函数，将“1111100000”的显示转换成十六进制“3E0”的显示。
```
  =DEC2HEX(SUMPRODUCT(--MID(1111100000,ROW(INDIRECT("1:10")),1),2^(10-ROW(INDIRECT("1:10")))))
```
![插入图片](/assets/images/250409_3.jpg)

***
如果直接使用=BIN2HEX(1111100000)函数，则输出为“FFFFFFFFE0”，原因是把首位的1当成了负数标记。

