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

式子分母不影响c的选择  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image145.png)  

$$d=(x_{1},x_{2}...,x_{n})$$每个位置代表一个word，当文本含有这个word，标记为1，否则为0   

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
$$count(w_{i},c_{j})$$表示含有$$w_{i}$$词且主题为$$c_{j}$$文本的个数 

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






