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


