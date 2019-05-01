---
layout: post
title: Chapter 4 Machine Language
date:   2019-03-23
categories: ["The Elements Of Computing Systems"]
---

# 背景知识

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image52.png) 

**机器语言(machine lanuage)**: 是一种约定的形式，用来对底层程序进行编码，从而形成一系列机器指令。应用指令，可以命令处理器执行算术和逻辑操作，在内存中进行存取操作。(利用处理器和寄存器来操控内存)。

**内存(memory)** ：用来存储数据和指令的硬件设备，内存具有相同的结构：A continuous array of cells of some fixed width, also called words or locations, each having a unique address(具有一定固定宽度的连续单元序列，单元也称为字或位置，内存每个单元具有唯一的地址) 

**处理器(Processor)** ：执行一组固定基本操作的设备。操作通常包括算术操作和逻辑操作，内存存取操作和控制操作。操作的对象是二进制数值，它们来自寄存器和指定的内存单元(指定的内存位置，内存里的寄存器) ，操作的结果(处理器的输出)即可以存储在寄存器内，也可以存储在指定的内存位置。

**寄存器(Registers)** ：内存访问(内存里寄存器)是相对比较慢的操作，需要很长的指令格式(一个地址可能需要32位),大多数处理器都配有一些寄存器，每个寄存器只存储1 bit。它紧挨着处理器，相当于处理器的一个高速本地内存，使得处理器能快速地操控数据和指令。



![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image53.png)  

What exactly does the instruction tell the computer to do?(指令告诉电脑做什么)Program里是指令...   
 
![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image54.png) 

which instruction to perform at any given stage and time?(什么时候执行哪个指令)

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image55.png) 


add two numbers. the software has to tell the hardware, how exactly, where exactly will it get these two values that it's going to, that it needs to add and where should it put the result. (执行指令涉及到对象在哪里，执行结果保存到哪里)

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image56.png) 

# 语言  

机器语言程序是一系列的编码指令。图中二进制码最左边是操作编码，剩下是操作对象。二进制码下方是symbolic mnemonics(抽象助记符)。   

这种"symbolic form" 不是真实存在的，它是一种方便助记符用来向人描述机器语言指令含义。 这种“symbolic notation(抽象符号)”称为汇编语言(assembly language)。  

人可以使用汇编语言写机器语言指令，汇编编译器(Assembler)会将汇编程序翻译成二进制码程序  

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image58.png) 

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image57.png)  


# 命令 

直接寻址(Direct addressing) 使用内存地址或使用一个符号表达内存地址(Memory[address],RAM[address],M[address],表示内存单元)

$$LOAD R1,67  //R1 \leftarrow Memory[67]\\
LOAD R1,bar // R1 \leftarrow Memory[67] $$

立即寻址(Immediate addressing) 用来加载常数,加载出现在指令代码里面的数值，直接将指令数据域中的内容当作要操作的数据装入寄存器，而不是将数值当作内存单元的地址

间接寻址(Indirect addressing) 要访问的内存地址没有直接出现在指令中，指令指定了一个保存所需地址的内存位置，这种寻址模型被用来处理指针(pointer),如高级语言命令$$x=foo[j]$$, foo是数组变量，x和j是整数变量。foo在高级语言程序里被声明和初始化时，编译器分配一组连续内存单元保存这个数组数据，符号foo指代内存单元组的基地址(base address)

编译器后来遇到数组单元的符号(foo[j])时，第j个数组入口是某个内存单元的物理地址，该地址相对于数组基地址的偏移量为j。$$x=foo[j]$$在C语言程序中相当于$$x=^*(foo+j)$$,foo+j表示地址，*获取地址指向内容。这里$$^* n$$代表Memory[n]。


The basic idea is instead of having just one large block of memory, we're going to have a whole sequence of memories that are getting bigger and bigger. The smallest memories are going to be very easy to access. First of all, because we don't have to specify large address space because there are only going to be a very few of them. Second of all, because there are only very few of them, we can actually get information from them very quickly. And then, there is going to be slightly larger memories, usually called cache, and even larger memories, sometimes called the big, the main memory. And maybe even, even larger memories that are going to sit on disk. At each time we get farther away from the arithmetic unit itself, our memory be, gets bigger. Accessing it becomes harder borth, both in terms of giving a larger, a wider address. And in terms of the time we need to wait until we get the value. But we have more information there. The ways that the different levels of the memory hierarchy are handled differs according to the different levels. But, what we're going to discuss now is the way that registers, the smallest, the smallest memory that usually resides really inside the CPU, and how we handle that.
