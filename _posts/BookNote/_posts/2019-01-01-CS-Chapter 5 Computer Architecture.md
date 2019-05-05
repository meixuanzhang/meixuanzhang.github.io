---
layout: post
title: Chapter 5 Computer Architecture
date:   2019-03-25
categories: ["The Elements Of Computing Systems"]
---

# 背景知识

## 存储程序概念

计算机基于固定的硬件平台，能够知晓固定的指令集。指令能够被当成构件模块，组成任意的程序，程序被存储到计算机的存储设备，和数据一样，称为“软件”。

## 冯诺依结构  
冯诺伊曼体系结构的基础是一个中央处理单元(CPU),它与记忆设备(memory device)即内存进行交互，负责从输入设备(input device)接收数据,向输出设备(output device)发送数据。计算机内存不仅存储要进行操作的数据，还存储着指数数据。

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image90.png)

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image91.png)  

### 内存(Memory)

内存有两种类的信息，数据项(data items)和程序指令(programming instructions)。通常计算机里，它们被分布存储到不同的内存区中。尽管功能不同，但两种信息都以二进制数形式存储在相同的通用的随机访问结构中(a continuous array of cells of some fixed width, also called words or locations, each having a unique address.)，因此an individual word (representing either a data item or an instruction) is specified by supplying its address.

**数据内存**： 高级程序操作抽象的元件例如变量(variables),数组(array)和对象。数据抽象被翻译成机器语言，变成二进制数存储在计算机内存中。通过指定的地址，individual word在数据内存中被找到，就可以对其进行读操作和写操作。读就是读取这个individual word的值，写就是将新值存入individual word。

**指令内存**： 高级命令被翻译成机器语言时，它变成binary words,代表机器的指令。指令存储在计算机指令内存中，计算机操作的每一步，CPU从指令中取出一个word，对其进行解码，从而执行指定的指令，然后计算下一条将要执行的指令。

## 中央处理器CPU  

CPU负责执行已被加载到指令内存中的指令。CPU主要通过三个主要硬件执行任务：算术逻辑单元(ALU),寄存器(registers)和控制单元(control unit)。

**算术逻辑单元**：负责执行计算机中所有底层的算术操作和逻辑操作

**寄存器**： 为了能够快速执行简单计算，将和运算相关的数据暂存在某个局部存储器中，每个CPU都配有一组高速寄存器，每个寄存器保存a single word。

**控制单元**： 在指令执行之前，须对其进行解码，指令里面包含的信息向不同的硬件设备(ALU,寄存器,内存)发送信号，指使它们如何执行指令，指令的解码过程是通过某些控制单元完成。

CPU操作：从内存中取一条指令，将其解码，执行该指令，取下一条指令。

## 寄存器(CPU内的)   

当CPU被指示去取内存中地址j的内容时，j从CPU传到RAM，RAM的直接访问逻辑选择地址为j的寄存器，RAM[j]的内容传回到CPU。CPU内部寄存器，能提供同样的数据访问功能，但没有来回的数据传递和寻址开销。CPU内部寄存器分为：  

数据寄存器(Date registers): 为CPU提供短期记忆服务。如计算(a-b)*c时，首先记住(a-b)的值并记住它，这个结果可以暂时被存储在内存中，但更好办法是存储在CPU内数据寄存器中。

寻址寄存器(Addressing registers) :为了进行读写，CPU需连续访问内存中的数据。这样必须确定被访问数据的word所在的内存地址。在某些情况下这个地址作为当前指令的一部分给出，而某些情况下它依赖于前面一条指令的执行结果。后者地址应被存储到某个寄存器，该寄存器内容在今后的操作中能够被当做内存的地址。

程序计数寄存器(Program counter register) 执行程序时，CPU必须总是知道下一条指令内存中的地址，这个地址保存在程序计数器寄存器中。程序计数器内容被当作从指令内存中取指令的地址。

## 输入和输出

I/O映像基本思想：常见I/O设备的二进制仿真，使其对于CPU而言就像普通的内存段。每个I/O设备在内存都分配了独立的区域，作为内存映像。对于输入设备(键盘、鼠标)，内存映像能连续不断地反映设备的物理状态。对于输出设备(屏幕，扬声器),内存映像连续地驱动设备的物理状态。


## 系统中信息传递  

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image92.png)

总的来说会有三种信息在系统中传递：

数据(data)：When we have a number that needs to be added, the number needs to be moved from the data in memory to the registers, to the actual other systematic logic unit that's going to do something with them, and back。

地址(address)：What instruction are we actually executing now? What piece of data within the memory do we need to access now? These are in addresses. 

控制(control)：That actually tell each part of the system what to do at this particular point 

三种信息通过 wires(电线)传输，称为bus 


**ALU**：The ALU loads information from the Data bus and manipulates it using the Control bits.ALU need to have some information from the databus .And then feeds the output value back into the databus. ALU needs to know what kind of operation it does every time,according to the results of the arithmetic or logical operations that it does. It's going to be able to, have to be able to tell the other parts of the system what to do.
 

**registers**: we store intermediate results in the registers. So we have to be able to take data from the data bus into the registers and then also take data's from the register then feeds them back into the data bus. And of course where would they go from the data bus to other parts of the system such, as the ALU. 
some registers are used to specify addresses. The way we actually achieve indirect addressing into a RAM or jump into a ROM address, the way we do it is usually we put numbers, addresses into a register and then that specifies where we want to access
   
**memory**: There are two pieces to the memory, there is a data memory and there is a program memory.

 we're going to need to put the address of **the next program instruction** into the program memory because this is where we're taking our program instructions. We need to be able to put an address into the program memory address, and then get the instructions from there. Now the instructions that we get from the program memory, both may have data in it. **we need to be able to actually take information from the next instruction, from the data output of the program memory. And feed it into the control bus.**
 
 ![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image94.png)
 
 ![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image93.png)   
 
 
# 获取(Fetch)-执行(Execute)指令循环
 
## Fetch    

Program Counter将下一个要执行的指令address传入Program memory，在Program memory里下一个要执行的指令除了包含下一个要执行任务同时包含下下一个指令信息(we need to jump into a new location or we need to just increase and go to the next instruction)

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image95.png) 

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image96.png)
 

## Execute   

Executie 意味获得指令，并执行指令

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image97.png)

the instruction we already got from our fetch, that is now going to feed into the control bus of our CPU, of our computer. And that control bus, basically controls everything

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image98.png)

这里存在一个冲突，图中只有一个内存，输入address可能是指令地址也可能是数据地址，因此需要multiplexer，在fetch cycle将内存设置为指向访问的下一个指令地址，在execute cycle时将内存设置为指向访问的数据地址。

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image99.png)

在fetch cycle，获得了下一个要执行的instruction，将存储在instruction register，当execute cycle，要执行的指令已经在instruction寄存器
   
![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image100.png)
 
![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image101.png)
 
 
# CPU   

CPU执行当前指令，计算下一个要执行的指令

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image102.png) 

CPU输入和输出

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image103.png) 

输出：
+ Date value
+ Writer to memroy?(yes/no)
+ Memory Address
+ Address of next instruction

**Hack CPU 实现**

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image104.png)   

**Instruction handling**  

A指令：第一位表明指令的类型是A还是C，后面15位被解释为数组，将数值存储在A寄存器,( 图中指令 seeks to load the value 3,001 into a register. )

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image105.png) 

C指令：指令解码成4个方面，op-code，ALU control bit,Destination load bit,jump bits

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image106.png) 

16位C指令可以分解成"i xx a cccccc ddd jjj"，i表明了指令类型，a决定ALU是把A register的输入当作操作数还是把memory register的输入当作操作数，则c表明要执行什么计算

如果是A指令，A register的输入是A指令后15位代表数值，如果是C指令，A register的输入是ALU的输出

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image107.png) 

相同的ALU output可以输入三个不同的寄存器，每个寄存器是否被输入由指令码的d决定即Destination bit  

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image108.png) 

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image109.png) 

**reset**： 相当于开机，计算机中已经有编写好的指令程序，当按下reset就开始执行  

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image110.png)  

Program Counter输出的address,将由C指令码的j决定。 

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image111.png)  

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image112.png)  

