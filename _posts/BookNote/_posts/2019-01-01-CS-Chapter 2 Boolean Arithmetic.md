---
layout: post
title: Chapter 2 Boolean Arithmetic
date:   2019-03-23
categories: ["The Elements Of Computing Systems"]
---

ALU是核心芯片，执行所有算术和逻辑操作。要理解中央处理器(Central Processing Unit,CPU)及整个计算机的工作方式，构建ALU功能模块是很重要的一步。  

# 背景知识

**二进制数**：十进制是以10为基底，而二进制系统是以2为基底。不同基底b转换为十进制：  

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image23.png)

二进制小数转为十进制小数:

$$(0.001)_{two}=0\cdot 2^{0}+0\cdot 2^{-1}+0\cdot 2^{-2}+ 1\cdot 2^{-3}$$=0.125$$

**二进制加法**:将两个二进制数从右到左逐位相加，逢2进1。两个二进制数最右边一位相加，称为LSB(Least Significant Bites),最左边一位相加称为MSB(Most Significant Bits)。如果最左边两位数相加产生进位1，称为溢出。 

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image24.png)

**有符号的二进制数**  

对于有符号的二进制数算术，几乎所有计算机采样补码(2’s complement method)的方式计算。

**原码**：是最简单的机器数表示法。用最高位表示符号位，‘1’表示负号，‘0’表示正号。其他位存放该数的二进制的绝对值。   
使用原码进行算术计算，原码能正确计算正数相加，但正数与负数相加、负数相加会出现计算错误(如：0001+1001=1010,1-1=-2)，同时原码将0分为+0和-0。

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image25.png)

**反码**：正数的反码还是等于原码，负数的反码就是他的原码除符号位外，按位取反。使用反码进行算术计算，反码能正确计算正数相加，正数与负数相加(如0001+1101=1110,1+(-2)=-1)，但负数相加仍会出现计算错误(如：1110+1100=1010,-1+(-3)=-5)，同时反码同样将0分为+0和-0。 

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image26.png)

**补码**：正数的补码等于他的原码，负数的补码等于反码+1。

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image27.png)

+ 补码的定义： 
![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image28.png)

补码溢出舍弃操作:
0001+1111=0000，1+(-1)=0
1111+1110=1101，-1+(-2)=-3 
0010000+11111011=00001011


参考：
(转原码，反码，补码的深入理解与原理)[https://blog.csdn.net/zhiwen_a/article/details/81192087]
(转原码，反码，补码的深入理解与原理)[https://www.imooc.com/article/16813?block_id=tuijian_wz]
