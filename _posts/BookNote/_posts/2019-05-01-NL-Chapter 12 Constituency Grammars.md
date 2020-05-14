---
layout: post
title: Chapter 12 Constituency Grammars
date:   2019-05-01
categories: 自然语言处理综述
---  

句法(syntax):把单词安排在一起的方法  

本章介绍三个主要的新思想：constituency(组成性)，语法关系(grammatical relations),次范畴化和依存关系(subcategorization and dependency)

constituency:单词的组合可以作为一个单独的单位(single unit)或者成分(constituent),也就是短语.      

grammatical relations：传统语法关于主语(SUBJECTS),宾语(OBJECTS)以及其他相关的概念的形式化(Formal methods)。 

Formal methods are system design techniques that use rigorously specified mathematical models to build software and hardware systems.   

subcategorization and dependency relation:单词和短语之间的关系   

# constituency   

单词是怎样组合一起的？如名词短语(noun phrase)也称为名词词组(noun group),包围着名词的单词序列，单词序列中至少有一个名词。

怎样判断哪些单词是组合在一起形成了一个成分(constituent)？组成的一些根据：  

1、它们出现在相同的句法环境中。如名词短语能够出现在动词之前(Noun Phrase can occur before verbs ),整个短语出现在动词之前，并不意味构成名词短语的每一个单独的单词都具有这种性质。  

![_config.yml]({{ site.baseurl }}/images/18SpeechAndLanguageProcessing/image5.png)  

使用星号“*”表示不合英语语法的单词片段  

![_config.yml]({{ site.baseurl }}/images/18SpeechAndLanguageProcessing/image6.png)  

2、constituency 来自称为前置(preposed)和后置(postposed)的结构。如前置短语(prepositional phrase)可以放在不同的位置。但短语的一个多部分的单词并不能放在不同的位置。   

![_config.yml]({{ site.baseurl }}/images/18SpeechAndLanguageProcessing/image7.png)  

![_config.yml]({{ site.baseurl }}/images/18SpeechAndLanguageProcessing/image8.png)  

# Context-Free Grammars(上下文无关语法)  

上下文无关语法(Context-Free Grammar, or CFG)又称为短语结构语法(Phrase-Structure Grammars)，它的形式化方法(formalism)等价于Backus-Naur Form, or BNF,基于成分结构构建语法的思想。

​formalism: a style or method in art, music, literature, etc. that pays more attention to the rules and the correct arrangement and appearance of things than to inner meaning and feelings.  

一个上下文无关语法由一套规则(rules)或产生方式(productions),以及含有单词和符号的一个词表(lexicon)组成。每一个规则表示语言中的符号的组成和排序方式。例如下图$$NP$$可以的组成：  

专有名词(ProperNoun),限定词(determiner (Det)),名词性成分(Nominal)

![_config.yml]({{ site.baseurl }}/images/18SpeechAndLanguageProcessing/image9.png)  

上下文无关规则可以按层级嵌套，所以前面的规则可以同下面表示词汇事实的规则结合起来：  

![_config.yml]({{ site.baseurl }}/images/18SpeechAndLanguageProcessing/image10.png)   

CFG所使用的符号分为两类，与语言中单词对应的符号((“the”, “nightclub”)称为终极符号(terminal symbols),词表是引入这些终端符号的规则的集合。表示这些终极符号的聚类或概括性的符号称为非终极符号(non-terminals)   

箭头$$\to$$右边的项是一个或者多个终极符号或非终极符号构成的有序表，左边是一个单独的非终极符号，表示某种聚类或概括性的符号。  

词表中，与每个单词相关联的非终极符号是它们词汇类别或词x性(part-of-speech)  

可以通过两种方式考虑CFG：作为生成句子的装置，作为给给定句子分配结构的装置。箭头$$\to$$读为“用右边的符号串重写左边的符号串”    

![_config.yml]({{ site.baseurl }}/images/18SpeechAndLanguageProcessing/image11.png)    

我们说a flight字符串可以从非终极符号NP推导(derived)出来。通常使用剖析树(parse tree)来表示一个推导。  

![_config.yml]({{ site.baseurl }}/images/18SpeechAndLanguageProcessing/image12.png)    

从图中表示的剖析树中，可以说，结点$$NP$$支配(dominate)这个树中所有的节点$$(Det, Nom, Noun, a, flight)$$,结点$$NP$$直接支配结点$$Det$$和$$Nom$$    

CFG定义的形式语言从指定的初始符号(start symbol)开始推导出字符串集合。每一个语法必须指定一个初始符号，初始符号通常为$$S$$。由于上下文无关语法通常用来定义句子，所以$$“S”$$通常解释为"句子"的结点。简化英语语法中，用$$S$$推导出的字符串的集合就是句子的集合。   

形式语言（英语：Formal language）是用精确的数学或机器可处理的公式定义的语言。 

例子：  

![_config.yml]({{ site.baseurl }}/images/18SpeechAndLanguageProcessing/image13.png)     

$$PP$$不一定总是表示方位，$$PP$$经常还可以表示时间和日期，也可以使用其他名词。ATIS语料库中的例子：  


![_config.yml]({{ site.baseurl }}/images/18SpeechAndLanguageProcessing/image14.png)   

词表和语法样例，$$\mid$$表示“或者”：  

![_config.yml]({{ site.baseurl }}/images/18SpeechAndLanguageProcessing/image15.png)   

![_config.yml]({{ site.baseurl }}/images/18SpeechAndLanguageProcessing/image16.png) 

根据语法生成的句子：  

![_config.yml]({{ site.baseurl }}/images/18SpeechAndLanguageProcessing/image17.png) 

