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

**触发器(Flip-Flops)**:是最基本的sequential element。书里使用其变体数据触发器(DFF,data flip-flop),其接口包含a single-bit输入和a single-bit输出。DFF有个时钟输入，根据主时钟信号连续地交变。数据和时钟的输入使得DFF能够实现基于时间的行为$$out(t)=in(t-1)$$,in和out是门的输入和输出值，t是当前时钟周期。

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image38.png)  

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image39.png)  

**寄存器(Registers)** ：具有记忆功能的设备，能够存储某一时刻的值，实现$$out(t)=out(t-1)$$。
设计中使用多路转换器(multiplexor),这个多路转换器的“选择位(select bit)”可以成为整个寄存器芯片的“加载位(load bit)”。如果希望寄存器开始存储一个新值，可以把这个值置于in输入门，然后将load位设为1；如果希望寄存器一直存储它的内部值直到新的指令到来，可以将load位设为0。 

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image40.png)  

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image41.png) 

Once we have developed the basic mechanism for remembering a single bit over time, we can easily construct arbitrarily wide registers. This can be achieved by forming an array of as many single-bit registers as needed, creating a register that holds multi-bit values . The basic design parameter of such a register is its width—the number of bits that it holds—e.g., 16, 32, or 64. The multi-bit contents of such registers are typically referred to as **words**.(可以构建多位寄存器)

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image42.png) 

**内存(Memories)**:具备表达word的能力(多位寄存器)，就可以构建任意长度的存储块。可以将很多寄存器堆叠起来实现RAM单元。随机存储内存(RAM,Ramdom Access Memory)上能够随机访问被选择的word，也就是要求内存中的任何word都以相等的速度被直接访问。为此通过以下方式实现：

n位RAM中每个记忆单元分配一个唯一的地址(address，0到n-1之间的整数)
构建一个由n-寄存器构成的阵列，再构建一个逻辑门，使得该逻辑门能够对给定的地址j，找到地址j对应的记忆单元。

典型的RAM设备接收三种输入：数据输入、地址输入、和加载位。地址指定了当前时钟周期里哪一个RAM寄存器被访问，进行读操作(Load=0),RAM的输出立即发出被选中的记忆单元的值。在进行写操作(Load=1)时，被选择的记录单元将在下一个时间周期内被赋予新输入值。  

RAM设备的基本设计参数是它的数据宽度(每个word的宽度)，和它的大小(RAM中word的数目)，现代计算机一般采用32或64位宽的RAM。
 
![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image43.png) 

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image44.png)

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image50.png)

**计数器(Counter)** ：是一种时序芯片，它的状态是整数，每经过一个时间周期，该整数增加1个单位，执行函数$$out(t)=out(t-1)+1$$。典型的CPU包括一个程序计数器(program counter),输出是当前程序下一步将要执行的指令地址。

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image45.png)  

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image46.png)


**时序芯片(Sequential chip)** : 直接或间接嵌入一个或多个DFF门的芯片。功能角度就是被DFF赋予了维持状态(内存单元)或对状态进行操作(如计数器)的能力

对比Combinatorial Logic 和 Sequential Logic chip：

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image47.png)

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image48.png)

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image49.png) 


注意：在实际实现中一个时间周期包含了tick-tock，当寄存器在当前时间周期选择位为1时，会在当前时间周期tock存储一个新值，而不是在下一个时间周期才开始存储新值 (0+ 是tick,1是tock...以此类推)

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image51.png)   


