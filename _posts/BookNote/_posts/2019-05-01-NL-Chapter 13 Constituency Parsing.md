---
layout: post
title: Chapter 13 Constituency Parsing
date:   2019-05-01
categories: 自然语言处理综述
---  

句法剖析就是识别一个句子并给句子指派一个结构的过程。   

本章将具体说明如何给一个输入句子自动地指派一个上下文无关树(短语结构树)的各种可能算法。  

剖析树可以直接应用于词语处理系统中进行语法检查(grammar checking)。如果一个句子不能被剖析，它就很可能有语法错误。剖析是语义分析(semantic analysis)表示的一个重要中间阶段，因此在问答系统(question answering)，信息抽取(information extraction)的应用中起着重要作用


# 剖析就是搜索  

无论选择何种搜索算法，都存在着两种约束：  

+ 第一种约束来自数据，就是输入句子本身，如果剖析树是正确的，它必须有三个叶子(如例图,三个叶子应该分别是book,that,flight。   

+ 第二种约束来自语法，如果剖析树是正确的，它必须有一个根，这个根的初始符号$$S$$   

![_config.yml]({{ site.baseurl }}/images/18SpeechAndLanguageProcessing/image24.jpg)  

![_config.yml]({{ site.baseurl }}/images/18SpeechAndLanguageProcessing/image25.jpg)  

多数剖析算法使用两种搜索策略：自顶向下(top-down)或目标制导的搜索(goal-directed search)，自底向上(bottom-up)或数据制导的搜索(data-directed search)  

## 自顶向下   

自顶向下搜索空间的展开。每一层的树都是由上一层的树构造而成的，用可能的展开来代替最左的非终极符号，把这些树集中起来构成一个新的层 

![_config.yml]({{ site.baseurl }}/images/18SpeechAndLanguageProcessing/image26.jpg)  

## 自底向上   

![_config.yml]({{ site.baseurl }}/images/18SpeechAndLanguageProcessing/image27.jpg)  

![_config.yml]({{ site.baseurl }}/images/18SpeechAndLanguageProcessing/image28.jpg)  