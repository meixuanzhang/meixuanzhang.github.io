---
layout: post
title: Chapter 4 Machine Language
date:   2019-03-23
categories: ["The Elements Of Computing Systems"]
---

# 背景知识

**机器语言(machine lanuage)**: 是一种约定的形式，用来对底层程序进行编码，从而形成一系列机器指令。应用指令，可以命令处理器执行算术和逻辑操作，在内存中进行存取操作。(利用处理器和寄存器来操控内存)。

**内存(memory)** ：用来存储数据和指令的硬件设备，内存具有相同的结构：A continuous array of cells of some fixed width, also called words or locations, each having a unique address(具有一定固定宽度的连续单元序列，单元也称为字或位置，内存每个单元具有唯一的地址) 

**处理器(Processor)** ：执行一组固定基本操作的设备。操作通常包括算术操作和逻辑操作，内存存取操作和控制操作。操作的对象是二进制数值，它们来自寄存器和指定的内存单元(指定的内存位置，内存里的寄存器) ，操作的结果(处理器的输出)即可以存储在寄存器内，也可以存储在指定的内存位置。

**寄存器(Registers)** ：内存访问(内存里寄存器)是相对比较慢的操作，需要很长的指令格式(一个地址可能需要32位),大多数处理器都配有一些寄存器，每个寄存器只存储1 bit。它紧挨着处理器，相当于处理器的一个高速本地内存，使得处理器能快速地操控数据和指令。


