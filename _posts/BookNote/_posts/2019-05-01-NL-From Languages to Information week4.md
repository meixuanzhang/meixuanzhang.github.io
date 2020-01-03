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


