---
layout: post
title: Chapter 3 Sequential Logic
date:   2019-03-23
categories: ["The Elements Of Computing Systems"]
---
简单的芯片提供了很多处理功能，但它们不能维持状态，计算机不仅要能实现计算，还需要存取数据，它们必须配备可以随时间保存数据的内存单元(memory elements)。内存单元由时序芯片(sequential chips)组成。

memory elements的实现涉及了synchronization(同步),clocking(时钟), feedback loops(反馈回路)，大部分复杂的部分会封装到触发器(flip-flops)的low-level sequential gates逻辑操作中。  

将flip-flops作为基本构建模块，我们将构建典型现代计算机的所有存储设备(memory devices),从二进制单元(binary cells)到寄存器(registers)到存储块( memory banks)和计数器(counters.)

# 背景知识  

**时钟(Clock)**:大多数计算机里，时间的流逝(时间的体现)是通过master clock表示，master clock提供连续的交变信号序列。硬件实现是基于oscillator(振荡器)，振荡器在信号值0–1, low-high, tick-tock之间交替变换。从"tick"开始到后续"tock"结束之间经过的时间称为周期(cycle).每个周期用于模拟一个离散时间单位。当前时钟相位（tick或tock）由二进制信号表示。就是单位时间内所处波峰还是波谷。使用硬件电路，该信号同时会广播到整个计算机平台的每个时序芯片(sequential chips)。

图中描述了时钟变换：

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image37.png)  

**触发器(Flip-Flops)**:是最基本的sequential element。书里使用其变体数据触发器(DFF,data flip-flop)

