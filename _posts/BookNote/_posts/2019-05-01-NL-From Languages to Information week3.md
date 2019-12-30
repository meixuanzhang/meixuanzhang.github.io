---
layout: post
title: week 3 Text Classification and Sentiment Analysis
date:   2019-05-01
categories: From Languages to Information
---  

# 5.1 What is Text Classification?  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image134.png) 

判断一篇邮件是否为垃圾邮件？  
判断一篇信件是谁写的？   
判断一本书作者是男是女？  
判断一部电影评价是 positive还是negative?(sentiment analysis)  
判断 scientific articles 属于什么主题？  

## Text Classification：definition  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image135.png)  

## Classification Methods   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image136.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image137.png)   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image138.png)  

# 5.2 Naive Bayes  

## Naive Bayes Intuition  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image139.png)  

使用文本中部分词作为文本特征：  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image140.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image141.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image142.png)  

提取待分类文本特征以及不同主题文本特征，通过计算将待分类文本归类  

# 5.3 Formalizing the Naive Bayes Classifier   

## Bayes’ Rule Applied to Documents and Classes  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image143.png)  


## Naive Bayes Classifier  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image144.png)  

式子的分母不影响c的选择  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image145.png)    

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image146.png)  

## Multinomial Naive Bayes Independence Assumptions  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image147.png) 

## Multinomial Naive Bayes Classifier   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image148.png) 

##  Applying Multinomial Naive Bayes Classifiers to Text Classification  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image149.png) 

# 5.4 Naive Bayes: Learning  

## Learning the Multinomial Naive Bayes Model 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image150.png)   

$$C$$表示文本主题，$$C=c_{j}$$表示文本属于$$c_{j}$$主题    
$$count(w_{i},c_{j})$$表示主题为$$c_{j}$$的所有文本共含有$$w_{i}$$词的数量

## Parameter estimation  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image151.png)   

## Promblem with Maximum Likelihood  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image152.png)  

增加平滑项  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image153.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image155.png)  

## Multinomial Naive Bayes：Learning  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image154.png)  

# 5.5 Naive Bayes: Relationship to Language   

## Generative Model for Multinomial Naive Bayes  

已知主题C下生成word  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image156.png) 

## Naive Bayes and Language Modeling  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image157.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image158.png)  

这类似不同主题代的语言模型，不同主题语言模型生成某个句子的可能性

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image159.png)  

# 5.6 Multinomial Naive Bayes: A Worked Example   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image160.png)   

$$p(c)=\frac{3}{4}$$，4个句子，3个属于c类   
$$p(Chinese\mid c)$$，c类句子共有8个词，其中5个是"Chinese"，1,6是平滑项(词汇表大小为6，每个词频数加了1)

## Summary: Naive Bayes is Not So Naive 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image161.png)   

以上介绍了Multinomial Naive Bayes，也称为多项式事件模型，注意与Naive Bayes model(朴素贝叶斯模型)区别   

# 5.7 Precision  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image162.png)   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image163.png)   

调和平均数（harmonic mean）又称倒数平均数  


# 5.8 Text Classification: Evaluation   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image164.png)   

图中"90"表示实际为"wheat"预测为"poultry"   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image165.png)   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image166.png)   

In macro-averaging, each class is going to participate equally.

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image167.png)   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image168.png)   

# 5.9  Practical Issues in Text Classification 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image169.png)   

假设您没有训练数据，正确的做法是使用手动编写的规则。  


![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image170.png)   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image171.png)  

决策树的一个很大的优势是用户可解释的，够修改规则，手动改变阈值。 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image172.png)   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image173.png)   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image174.png)   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image175.png)   


-----------------------------------------------------------------------------------------------

# 6.1  What is Sentiment Analysis?  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image176.png)   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image177.png)  


# 6.2 Sentiment Analysis: A Baseline Algorithm    

##Baseline Algorithm(adapted from Pang and Lee)   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image178.png)   

## Sentiment Tokenization Issues  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image179.png)  

Emoticons:表情   

## Extracting Features for Sentiment Classification  


![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image180.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image181.png)  


## Naive Bayes  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image182.png)  

## Binarized(Boolean feature)Multinomial Naive Bayes  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image183.png)  

一个词在句子中重复出现，可能并没有携带更多的信息，相比起统计词出现频率，word occurrence(只统计出现过哪些词，不统计词出现频次)可能更有。   

为此提出 Boolean Multinomial Naive Bayes 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image184.png)  

## Boolean Multinomial Naive Bayes on a test document d  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image185.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image186.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image187.png) 


## Cross-Validation 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image188.png)  

##Promblem  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image189.png)  

有些句子无法区分是positive还是negative   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image190.png)  

上述句子表达我希望电影是好的，但实际电影不是好的，这种顺序影响，需要更高级算法处理




