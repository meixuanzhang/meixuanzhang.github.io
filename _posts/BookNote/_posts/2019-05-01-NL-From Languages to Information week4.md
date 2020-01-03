---
layout: post
title: Week 4 Information Retrieval
date:   2019-05-01
categories: From Languages to Information
---  

# 7.1 Introduction to Information Retrieval 信息检索 

## Information Retrieval定义  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image231.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image232.png)  

## The classic search model  

检索过程： 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image233.png)   

## 检索评估  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image234.png)  

# 7.2 Term Document Incidence Matrices   

## Unstructured data in 1620  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image235.png)  

grep （缩写来自Globally search a Regular Expression and Print）一种强大的文本搜索工具，它能使用特定模式匹配（包括正则表达式）搜索文本，并默认输出匹配行。
 
grep搜索是匹配搜索，搜索出特定模式(词结构)的词，语料量大时速度慢，输入"Caesar"只能搜索出"Caesar",对于文档不包含"Calpurnia"词需要遍历文档所有词确定，同时无法进行更复杂的操作，如发现"Romans"与"countrymen"位置相近,对检索结果排序返回   

## Term-documnent incidence matrices   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image236.png) 

矩阵横轴是文档，纵轴是words，文档出现了word则标记1，否则0  

## Incidence vectors  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image237.png) 

将word转化成vector，每一维代表一个文档，通过and运算，可以找出同时含有"Brutus","Caesar","Calpurnia"词的文档   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image238.png) 

## big collections  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image239.png) 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image240.png) 

假设有大量文档，每个文档word都不同，矩阵中会存在大量0，这会浪费大量储存空间

# 7.3 The Inverted Index  

## Inverted index  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image241.png) 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image242.png)   

使用类似字典结构存储，“word”是键，"文档"是值  

## Inverted index  construction  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image243.png)   

将文档中句子进行分词(Tokenizer),对词进行处理(规范化)，构建索引   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image244.png)   

## Indexer steps   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image245.png) 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image246.png) 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image247.png) 

## Where do we play in storage?

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image248.png)   


# 7.4 Query Processing with the Inverted Index

## Query processing :AND  

查找同时含有单词"Brutus"和"Caesar"的文档  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image249.png)   

## The merge  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image250.png)   

NIL 是list结尾

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image251.png)   

# 7.5 The Boolean Retrieval Model  

## Boolean queries:Exact match   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image252.png)  

通过AND,OR ,NOT组织检索问题  

## Example：WestLaw  

使用Boolean queries检索的系统  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image253.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image254.png)  

## Boolean queries:More general "merges"   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image255.png)  
 
![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image256.png)  

## Query optimization  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image257.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image258.png)  

先从 document frequency 少的单词开始，"Calpurnia"和"Brutus"执行merge 算法，有相同文档id则与"Caesar"执行merge 算法,有相同则将同时有三个词的文档id保存，然后回到"Calpurnia"和"Brutus"执行merge 算法，不断循环   


7.6 Phrase Queries and Positional Indexes  

## Phrase queries 短语查询  

查找由两个或以上的单词组成的短语。

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image260.png)  

## A first attempt ：Biword indexes

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image261.png) 

句子所有单词，前后两两组成短语。 

## Longer phrase queries  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image262.png)   

Biword方式文档是否确定是否包含两个单词短语，对于是否包含多于两个词短语，短语需要重新组合成多个两词短语，然后查询文档是否包含这些两词短语。这种方式不够准确。 

## Solution 2:Positional indexes    

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image263.png)   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image264.png)   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image265.png)  

先判断哪些文档都含有这些词，然后文档内词实施"merge"算法

## Proximty queries 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image266.png)   

## Positional index size  


![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image267.png)   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image268.png)   

 考虑一个word出现在一篇文档频率是0.1%，1000字文档，word应该会出现一次，但100000字文档会出现100次，Positional index 会非常长 
 
## Rules of thumb   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image269.png)   

web page 的Positional index 长度大概是 non-ositional index 2到3倍
 
Positional index 长度几乎是原始文本长度的35%-50%

## Combination schemes  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image270.png)   

将Positional index和Biword indexes结合，对于有些两词短语不再是拆分成单个单词。

----------------------------------------------------------------------------------------------------------------
