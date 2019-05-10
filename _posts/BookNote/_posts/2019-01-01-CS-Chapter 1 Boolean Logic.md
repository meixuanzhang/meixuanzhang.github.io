---
layout: post
title: Chapter 1 Boolean Logic
date:   2019-03-23
categories: ["The Elements Of Computing Systems"]
---

**整个The Elements Of Computing Systems笔记课程来自coursera的Build a Modern Computer from First Principles Part I和Part II**

# 布尔代数(Boolean Algebra)  

布尔型函数(Boolean function):是指输入输出数值均为布尔型数值的函数。
描述方法:
+ 真值表表示法(Truth Table Representation):枚举出函数所有可能的输入变量组合，写出每一种组合对应的函数输出值。

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image1.png)  

+ 规范表示法(Canonical Representation):每个布尔函数都至少由一个布尔表达式来描述。

布尔表达式(Boolean Expressions):布尔函数可以在输入变量上使用布尔算子(Boolean operator)。布尔算子有“And”,"Or","Not"。上图中布尔表达式是$$f(x,y,z)=(x+y)\cdot \bar{z}$$

$$
xAndy:x\cdot y,xy\\
xOry:x+y\\
\bar{x}:Not x
$$

每个布尔函数不管有多复杂都可以只由“And”,"Or","Not"来完全表达。

所有两个变量的布尔函数:  

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image2.png) 

“And”,"Or","Not"都可以由Nand或Nor来构建，即每个布尔函数都可以仅使用Nand构成，一旦物理上实现了Nand功能，就可以使用很多这样的物理设备，通过特定的连接方式来构建任何布尔函数的硬件实现。  

# 逻辑门(Gate Logic)

门是用来实现布尔函数的物理设备。如果布尔函数f有n个输入变量，返回m个二进制的结果，那么用来实现这个函数f的门将会有n个输入管脚(input pins)和m个输出管脚(output pins)。 

把值$$v_{1}..v_{n}$$从门的输入管脚输入，它的内部结构即门的逻辑会计算然后输出$$f(v_{1}..v_{n})$$。  

最简单的门是由微小开关设备(晶体管，transistor)构成，微小开关设备安装设计的拓扑结构进行连接，实现整个门的功能。  

下图primitive gate(原始门)可以看作是黑箱子，通过黑箱子实现逻辑操作。同时通过设计将primitive gate进行连接，可以实现更复杂的函数，构建composite gate(复合门)。 

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image3.png) 

下图描述的是构建一个简单的门逻辑(gate logic),也称为逻辑设计(logic design),逻辑设计是一种连接门的电路艺术，目的是构建更复杂的函数，即实现composite gate。  
左图是门的外部接口(interface)，即输入和输出管脚。右图是内部结构。

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image4.png)  

# Nand门  

所有其他的门和芯片都能够通过Nand门构建。Nand门用于实现以下布尔函数 

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image5.png) 

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image6.png) 

# 基本逻辑门

**Not**  

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image7.png) 

**And**  

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image8.png) 

**Or**  

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image9.png) 

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image10.png) 

**Xor**  

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image11.png) 

**Multiplexor**   

是有三个输入的门，其中一个输入称为"选择位"(Selection-bit)。另外两个输入称为“数据位”(data bits)。选择性输出。

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image12.png)

**Demultiplexor** 

根据"选择位"，选择"数据位"输出的通道 

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image13.png) 

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image14.png) 

# 多位基本门（Multi-Bit Versions of Basic Gates）  

基本逻辑门输入是一位的。

Computer hardware is typically designed to operate on multi-bit arrays called "buses".

**多位Not(Multi-Bit Not)**  

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image15.png) 

**多位And(Multi-Bit And)**  

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image16.png) 

**多位Or(Multi-Bit Or)** 

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image17.png) 

**多位 Multiplexor(Multi-Bit Multiplexor)**  

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image18.png) 

# 多通道逻辑门(Multi-Way Versions of Basic Gates)   

2个输入的门扩展到了任意输入

**多通道Or(Multi-way Or)** 

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image19.png) 

**多通道/多位 Multiplexor(Multi-way/Multi-Bit Multiplexo)** 

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image20.png)  

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image21.png) 

**多通道/多位 Demultiplexor(Multi-way/Multi-Bit Demultiplexo)** 

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image22.png)  


注意之间的区别：一个输入变量可以是多位或一位的，输入变量是多位则是Multi-Bit，一个芯片输入可以是多个，在基本逻辑门基本输入个数下扩展成多个输入则是Multi-way





