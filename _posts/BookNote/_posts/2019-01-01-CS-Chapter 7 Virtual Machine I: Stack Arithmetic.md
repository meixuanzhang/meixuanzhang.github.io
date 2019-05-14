---
layout: post
title: Chapter 7 Virtual Machine I :Stack Arithmetic
date:   2019-03-25
categories: ["The Elements Of Computing Systems"]
---

从这一讲开始内容围绕是software hierachy

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems2/image1.png)  

将高级语言程序看作是抽象化的

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems2/image2.png)    

通过汇编编译器，虚拟机，编译程序，操作系统使高级语言程序能够运行

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems2/image3.png)  

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems2/image4.png)  



# 程序编译(program compilation)   

许多设备使用不同的工艺流程(different processes),不同工艺流程使用不同的机器语言，只有一个编译器(compiler)是不够的，需要根据不同的工艺流程，设计不同的编译器，对于软件开发人员需要根据不同的平台对程序进行翻译，需要控制多个版本的代码，这会非常麻烦。


![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems2/image5.png)  

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems2/image6.png)  

为了只写一次编译器compiler，使用虚拟机，JVM是将字节码(bytecode)翻译成目标平台的对应代码的程序，通过JVM根据不同平台对虚拟机程序进行翻译(不同平台有不同的JVM)

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems2/image7.png)  

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems2/image8.png)  

# Stack(堆栈)  

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems2/image8.png)  

VM语言包含4种类型的命令

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems2/image14.png) 


**堆栈的结构和操作**

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems2/image9.png)  

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems2/image10.png)  

存储器存取命令，pop会将stack顶端内容删除，同时存进对应的存储器：  

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems2/image11.png)  


**堆栈的算术命令**

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems2/image12.png) 

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems2/image13.png)  

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems2/image17.png)  

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems2/image15.png)  

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems2/image16.png)  

# VM(虚拟机代码)  

左边是高级语言代码，右边是VM代码，VM代码需要保留对象的类型，否则会出错  

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems2/image18.png)  

不同类型变量使用不同的存储器存储，修改VM代码

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems2/image19.png)  

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems2/image20.png)  

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems2/image21.png)  

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems2/image22.png)  

汇编语言：

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems2/image23.png) 

p变量存储的值是地址，$$*p$$指向该地址存储的内容

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems2/image24.png)   

堆栈的实现,堆栈指针指向的位置放在RAM的第0位,从VM代码到汇编代码：   

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems2/image25.png)

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems2/image26.png)  

# 存储器分割  

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems2/image27.png)

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems2/image28.png)   

以local为例：  


![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems2/image29.png)

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems2/image30.png)  

local在RAM存储位置存储在RAM[1]上，pop local 2 指的是local当前存储位置后移两位     

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems2/image31.png)

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems2/image32.png)


the implementation of this constant is trivial because this is a truly virtual segment(虚拟分割). It doesn't really exist. 

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems2/image33.png)  

static segment 会映射到RAM特定某一块内存，static变量会根据其在代码出现的先后依次映射在RAM上，这里RAM的static映射区域是从RAM[16]开始到RAM[25]，注意static变量在汇编语言上的代码形式    

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems2/image34.png)

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems2/image35.png)

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems2/image36.png) 

临时存储： 

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems2/image37.png)

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems2/image38.png)  

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems2/image40.png)  

when the compiler translates a method, it has to remember the base addresses of the this and that segments. These are the segments that represent the current object and the current array that the method may be processing. 

pointer的值只能取0或1   

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems2/image41.png)  

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems2/image42.png)  

#   

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems2/image43.png)  


