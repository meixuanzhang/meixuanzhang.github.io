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
 
grep搜索是匹配搜索，搜索出特定模式(词结构)的词，语料量大时速度慢，输入"Caesar"只能搜索出"Caesar",对于文档不包含"Calpurnia"词需要遍历文档所有词，同时无法进行更复杂的操作，如找出与"countrymen"词附近位置"Romans",对检索结果排序返回   

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

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image259.png)  

先从 document frequency 少的单词开始，"Calpurnia"和"Brutus"执行merge 算法，有相同文档id则与"Caesar"执行merge 算法,有相同则将同时有三个词的文档id保存，然后回到"Calpurnia"和"Brutus"执行merge 算法，不断循环   



