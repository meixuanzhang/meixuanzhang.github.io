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

为了只写一次编译器，使用虚拟机，JVM是将字节码(bytecode)翻译成目标平台的对应代码的程序，通过JVM根据不同平台对虚拟机程序进行翻译

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems2/image7.png)  

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems2/image8.png)  

# Stack(堆栈)  

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems2/image8.png)  

**堆栈的结构和操作**

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems2/image9.png)  

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems2/image10.png)  

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems2/image11.png)  

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems2/image14.png) 

**堆栈的算术命令**

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems2/image12.png) 

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems2/image13.png)  

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems2/image17.png)  

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems2/image15.png)  

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems2/image16.png)  
