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


