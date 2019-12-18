---
layout: post
title: week 1 
date:   2019-05-01
categories: From Languages to Information
---  

# Regular expressions(正则化)

$$\bullet$$ 如何对下面单词进行查找? 

woodchuck、woodchucks、Woodchuck、Woodchucks  

+ Disjunctions(分离)

$$\bullet$$ 下列括号表示匹配，括号内字母或数字表示可以选择的匹配范围      

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image1.png)  

$$\bullet$$ 下列是匹配范围另一种表示  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image2.png) 

+ Negation in Disjunctions  

$$\bullet$$ 下列表示匹配的否定，使用$$^$$符号  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image3.png) 


$$\bullet$$ Errors 

正则化两类错误：False positives: 匹配了不想匹配的，False negative： 没有匹配到想匹配的

通过以下两个方面减少错误率：  

提升accracy和precision(减少False positives)   
提升coverage和recall(减少False negative)    


# Sentence Segmentation  

$$!,?$$符号相对来说没有什么歧义

$$.$$符号是有歧义的：它可以是句子的结束，可以是数字小数点如4.5 

需要建立模型(hand-writter rules,regular expressions,or machine-learning)进行区分如：  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image4.png) 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image5.png) 




# Word Tokenization  

+ Text Normalization   

 $$\bullet$$ NL任务中需要对文本进行标准化：  
 1、在运行文本中segmenting(分割）/tokenizing(标记)words 
 2、标准化 words的格式
 3、在运行文本中分割句子   
 
 + 下列句子有多少words?   
 
 ![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image6.png)  
 
 "main-mainly"是片段(fragments) 
 "uh"表示停顿，需要计算 
 
 
 
 word type:an element of the vocabulary  
 word token: an instance of that type in running text
 