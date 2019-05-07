---
layout: post
title: Chapter 6 Assembler
date:   2019-03-25
categories: ["The Elements Of Computing Systems"]
---

# 背景知识

机器语言一般分为两类，符号型(symbolic)和二进制型(binary),二进制码代表一条实际的机器指令，它能被底层硬件所理解。符号化的语言称为汇编(assembly)，翻译程序称为汇编编译器(assembler)。汇编编译器对每个汇编命令的所有部分进行解析，将每个部分翻译成它对应的二进制码，并将生成的二进制码汇编成真正能被硬件执行的二进制指令，汇编程序在被计算机执行之前，必须被翻译成计算机的二进制语言。

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image119.png)

符号在汇编程序通常有两种用途：  

变量(Variable):使用符号的变量名称，翻译器会"自动地"为其分配内存地址。这些地址的实际值是没有意义的，只要在程序的整个编译过程中，每个符号始终都被指代为同一地址就可以了。

标签(Labels):程序中用符号来标注不同的位置。

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image123.png)

**Hack汇编编译器逻辑**

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image120.png)  

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image121.png)  

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image122.png)  

**符号表(symbol table)**:在源代码中，每遇到一个新符号xxx，会在符号表中添加一行(xxx,nn)。根据规则约定，n是分配给对应符号的内存地址。符号表建立完成后，利用它来将程序翻译成无符号版本。

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image124.png)


**forward reference**：sometimes we can jump into a label before the label was actually defined. This is called a forward reference. (label在被定义前使用了)

解决方法：  

One way,is to basically remember that I've seen the labels, and I don't know where it is yet. Keep it in a side table. And when I actually get into the definition of the correct address, fix it back.

another way, The first pass keeps the labels and variables in a symbol table. and the second pass of the assembler translates all of the commands,

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image125.png)

#  The Assembly Process - Handling Instructions

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image126.png)  

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image127.png)  

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image128.png)  

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image129.png)   

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image130.png)  

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image131.png)  

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image132.png)  

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image133.png)  

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image134.png)  

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image135.png)  

#  The Assembly Process - Handling Symbols

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image136.png)  


![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image137.png)  

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image138.png)  

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image139.png)  

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image140.png)  

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image144.png)  

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image141.png)  

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image142.png)  

#Developing a Hack Assembler

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image143.png)  

![_config.yml]({{ site.baseurl }}/images/87TheElementsOfComputingSystems/image145png) 
