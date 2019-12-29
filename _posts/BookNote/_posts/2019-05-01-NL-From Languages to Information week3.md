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

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image165.png)   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image166.png)   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image167.png)   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image168.png)   

In macro-averaging, each class is going to participate equally.

# 5.9  Practical Issues in Text Classification 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image169.png)   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image170.png)   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image171.png)   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image172.png)   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image173.png)   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image174.png)   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image175.png)   

Let's suppose you have no training data.
00:22
Well, in that case, the right thing to do is to use manually written rules.
00:26
So here's a rule for deciding if a document's about grain, let's say.
00:30
We might say, if the word wheat or the word grain is there and

a big advantage of decision trees, is they are user-interpretable.
02:07
And that's helpful, because people like to be able to modify a rule or
02:11
hacking a classifier.

And it's very much easier to modify your decision tree at a at a role,
02:17
change your threshold by hand.

Although there is a cost, many classifiers just take a long time SVMs,
02:32
especially k nearest neighbors can be very slow to train a classifier.
02:38
Logistic regression can be somewhat better.
02:41
But really, if you have a huge amount of data,
02:44
then it may just be efficient to train Naive Bayes, which is quite fast.

So a real world system in general will combine this kind of automatic
03:41
classification, whether it's from rules or supervised machine
03:46
learning with manual review of uncertain or difficult or new cases.

Finally, we're going to want to tweak performance and
04:56
domain-specific features for your particular task.
04:58
Domain-specific weights are very important in the performance of real systems.
05:02
So for example, sometimes we're going to want to collapse terms.
05:05
Let's say, we're dealing with part numbers in some inventory task.
05:09
Now, we might want to collapse all part numbers together into a part number kind
05:14
of word or chemical formula.
05:16
We might want to have just one named entity called chemical formula.
05:19
But other kinds of collapsing such as stemming, generally doesn't help.

