---
layout: post
title: week 1 
date:   2019-05-01
categories: From Languages to Information
---  

# Regular expressions(正则化)

$$\bullet$$ 如何对下面单词进行查找? 

woodchuck、woodchucks、Woodchuck、Woodchucks  

## Disjunctions(分离)


$$\bullet$$ 下列括号表示匹配，括号内字母或数字表示可以选择的匹配范围      

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image1.png)  

$$\bullet$$ 下列是匹配范围另一种表示  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image2.png) 

## Negation in Disjunctions  

$$\bullet$$ 下列表示匹配的否定，使用$$^$$符号  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image3.png) 


$$\bullet$$ Errors 

正则化两类错误：False positives: 匹配了不想匹配的，False negative： 没有匹配到想匹配的

通过以下两个方面减少错误率：  

提升accracy和precision(减少False positives)   
提升coverage和recall(减少False negative)    


# Sentence Segmentation  

$$"!,?"$$符号相对来说没有什么歧义

$$"."$$符号是有歧义的：它可以是句子的结束，可以是数字小数点如4.5 

需要建立模型(hand-writter rules,regular expressions,or machine-learning)进行区分如：  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image4.png) 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image5.png) 


# Word Tokenization  

## Text Normalization   


$$\bullet$$ NL任务中需要对文本进行标准化：  
1、在运行文本中segmenting(分割）/tokenizing(标记)words   
2、标准化 words的格式  
3、在运行文本中分割句子     
 
## 下列句子有多少words?   
 
![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image6.png)  
 
"main-mainly"是片段(fragments) 
"uh"表示停顿，需要计算 
 
![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image7.png)  
 
将"San Francisco"作为一个words，则句子有14个words，将"San Francisco"作为两个words，则句子有15个words.   
Type 重复words算一个，如句子中"the"  


![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image8.png)   

N表示文本的单词数，V则是表示文本单词集合数(单词不重复计算) 


## Tokenization: language issues   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image9.png)  
![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image10.png)  
![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image11.png)   

# Word Normalization and Stemming  

根据不同需求对文本进行预处理  

## Normalization   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image12.png)   

## Case Folding(大小写转换)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image13.png)   

## Lemmatization(词形还原)  

找出词的原型 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image14.png)   

## Morphology(词态学)

研究各种语句的变化规律，各种词型（例如：动词，名词等）和语干的规则变化与不规则变化,(如名词复数，动词过去式变化)   
![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image15.png)  

## Stemming(词干)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image16.png)  
![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image17.png)  

土耳其一个单词有很多的词干  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image18.png)  


----------------------------------------------------------------------------------------------------------------

# Defining Minimum Edit Distance  

## 如何评价两个字符串(strings)相似？  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image19.png)  

两个字符串相似评价对机器翻译,信息提取,语言识别等非常有用  

## Edit Distance  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image20.png)  

将一个单词转换成另一个单词所需的操作数(insertion 插入，deletion 删除，substitution替换)

## Mininun Edit Distance  

为了对齐插入了星号

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image21.png)  

将I删除，N替换成E，T替换成X，插入C，N替换成U

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image22.png)  

## Other uses of Edit Distance in NLP  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image23.png)  

## 计算 Mininun Edit Distance  过程  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image24.png)  

## 数学符号表示Min Edit Distance   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image25.png) 

# Computing Mininun Edit Distance   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image26.png) 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image27.png) 

三条计算公式对应删除，插入，替换

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image28.png)  

Y轴表示待变换的单词，X轴表示目标单词   

图中"#"号表示位置0，根据算法初始化表格$$D(i,0)=i,D(0,j)=j$$，即表格两个轴填写的(1-9)   

如何计算剩下空格举例：  

Y轴"#"变换为X轴"#",没有操作填0  

Y轴"#I"变换为X轴"#E",首先经过前个步骤已将Y轴"#"变换为X轴"#"(操作0),只需"I"变换为"E",需要替换(操作2)，整个变换操作为2  

Y轴"#I"变换为X轴"#EX",首先经过前面步骤已将Y轴"#I"变换为X轴"#E"(操作2),只需插入"X"(操作1),整个变换操作为3  

最后绘制出整张图：  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image29.png)  

8就是将"INTENTION"变换为X轴"EXECUTION"所需最小操作数



