---
layout: post
title: Chapter 4 Hack computer
date:   2019-03-24
categories: ["The Elements Of Computing Systems"]
---  

# Hack Computer

16位 Hack computer 硬件主要由三部分组成：RAM(数据内存)、ROM(指令内存)、CPU  

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image68.png) 

Hack 语言包含两种指令：A-指令(地址指令),C-指令(计算指令)：  

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image69.png) 

ROM加载Hack程序，reset按钮是执行程序   

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image70.png) 

CPU有两个寄存器：A(存储数据或地址)，D(存储数据)  

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image71.png) 

@value指令会将内存单元地址存(地址是个数字)储在A寄存器

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image72.png) 

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image73.png) 

当调用M时，调用的是RAM的一个寄存器，M代表是RAM[address],address是上一句@value中的value

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image74.png) 

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image75.png) 


# Hack machine language

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image76.png) 

图中Example，第一个0是操作码。后面15个bit是代表数值，加载到A寄存器  

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image77.png)  

C指令： 

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image78.png) 

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image79.png) 

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image80.png) 

Hack程序，使用Symbolic code需要编译器翻译成binary code,计算机才能执行  

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image81.png) 

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image82.png)   

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image83.png) 

# Input和Output 

外部的键盘(用户输入)和屏幕(展示输出)设备：  

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image84.png) 

可以通过高级语言或低价语言操控(manipulate)I/O设备  

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image85.png)   

## Hack computer platform:Output

the screen memory map is a designated area which is part of the data memory of what is sometimes called RAM. So the deal is such, that the physical display unit is continuously refreshed from the contents of the memory map. And this happens many times each second.(
Screen memroy map是RAM的一部分,RAM会由多个芯片组成，Screen 内存芯片是其中一个。其会连续不断的更新)

I'm restricted to working with zeroes and ones only, if I want to write something on the display unit, what I can do is simply manipulate some bits in the memory map. And I can count on, on the fact that in the next refresh cycle, what I change in the memory is going to be reflected on the screen.(将屏幕的每个位置与memory map(Screen芯片/内存)里的每个bit对应，操控bit改变屏幕)


it's a table, or a matrix, consisting of 256 rows and 512 columns. And in each intersection of a, a row and a column, we have what is known as a pixel. This is a black and white screen, so we can either turn the pixel on or we can turn it off. This is the physical display on it that the hack computer assumes. Now how do we control it? Well, as I just explained, we have something called a memory map. And the memory map is a sequence of 16-bit values. Every one of these values is sometimes called a word. So we have altogether, 8k, 16-bit words. Why do we have 8k, 16-bit words? Because it turns out that 8k times 16 gives something like 13,000 and something, and this is the number of pixels that we have on the physical display unit. So, for every pixel on the physical display unit, we have a bit that represents this pixel in the screen memory map. And if I want to turn on this pixel, I put one in this bit. If I want to turn it off, I put zero in this bit.(注意每次操控会取出16-bit即一个register)  

**if I access the Screen chip, I use the address that you see here. But if I access the overall RAM, I have to take this relative address and add to it the base address of the memory of the memory map in in the overall memory, which happens to be 16384.** So this is just a technical detail. You know, if you want to write to the screen using the screen chip directly, use the first meth, the first algebraic expression. And if you want to if you are told that the Screen is part of a larger memory, you have to add up the the base address。

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image86.png) 

## Hack computer platform:Input
 
![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image87.png) 

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image88.png) 

And by the way, when you don't touch the keyboard, when, when nothing when the keyboard is idle, the number that we see in the memory map is 0. 

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image89.png) 
i




