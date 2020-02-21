---
layout: post
title: week 3 Text Classification and Sentiment Analysis
date:   2019-05-01
categories: ["From Languages to Information"]
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

以上介绍了Multinomial Naive Bayes，也称为多项式事件模型，注意与Boolean Multinomial Naive Bayes(也称朴素贝叶斯模型)区别   

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

一个词在句子中重复出现，可能并没有携带更多的信息，相比起统计词出现频率，word occurrence(只统计出现过哪些词，不统计词出现频次)可能更有用。   

为此提出 Boolean Multinomial Naive Bayes 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image184.png)  

## Boolean Multinomial Naive Bayes on a test document d  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image185.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image186.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image187.png) 

Multinomial Naive Bayes，Boolean Multinomial Naive Bayes，Multinomial Bernoulli Naive Bayes 是三种不同的贝叶斯模型  

## Cross-Validation 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image188.png)  

## Promblem  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image189.png)  

有些句子无法区分是positive还是negative   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image190.png)  

上述句子表达我希望电影是好的，但实际电影不是好的，这种顺序影响，需要更高级算法处理

# 6.3 Sentiment Lexicons(情感词汇表)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image191.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image192.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image193.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image194.png) 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image195.png)   

一个词在不同的词汇表(Lexicons)中，是否会有相同的极性(polarity),是否同为positive或negative，从上图看大多数时候 the Opinion Lexicon, the General Inquirer lexicon, LIWC,MPQA在判断polarity时，词具有非常相似的情绪。  

## Analyzing the polarity of each word in IMDB  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image196.png)  

图中表格展示不同等级评价中，"bad"出现频次，发现10分的评论出现"bad"的频次高于2分的评论，这是由于人们更倾向于打积极的分数   

因此要观察词出现在不同评分类别中可能性时使用，likelihood式子，为了对比不同词出现可能性使用scaled likelihood  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image197.png)  

## 关于否定词  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image199.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image198.png)  

negation words (no, not, never )出现在低分评论可能性高于高分评论，这种逻辑否定也是一种很好的情感判断提示。

# 6.4Learning Sentiment Lexicons (学习情绪词汇)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image200.png) 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image201.png)   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image202.png)   

对一部分word标记为positive或negative  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image203.png)  

通过已经标记的词，查找与其通过"and"连接的词，这些词往往与其具有相同的polarity,而与其通过"but"连接的词往往与其具有相反的polarity  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image204.png)  

计算两个word相似性，句子中两个word之间出现"and"的频率或出现"but"频率

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image205.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image206.png)  

从使用这种方法输出结果看，有部分词polarity会误判 

## Turney Algorithm   

上述算法对处理短语polarity效果不是很好，Turney Algorithm 是另一种半监督式构建词汇方式  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image208.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image209.png) 

根据词性标记(Part-of-speech) 提取短语    

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image210.png) 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image211.png) 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image212.png) 

计算两个词一起出现可能性  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image213.png) 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image214.png)   

计算短语与积极词一起出现可能性更大还是与消极词出现可能性更大

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image215.png) 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image216.png) 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image217.png) 

对于有些短语direct deposit、virtual monopoly等的polarity可能并不在online polarity dictionary 或 online web中，通过半监督学习它们的polarity 

##  Using WordNet to learn polarity   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image218.png) 

将已经标记的positive词的同义词和已经标记的negative词反义词标记为positive，将已经标记的negative词的同义词和已经标记的positive词反义词标记为negative  

## Summary on Learning Lexicons

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image219.png) 

学习词汇可以帮助我们处理特定领域的问题。

# 6.5 Other Sentiment Tasks   

## Finding sentiment of a sentence   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image220.png) 


首先找出sentiment描述的对象  

## Finding aspect/attribute/target of sentiment  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image221.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image222.png)  

有时候想要评价的对象并不直接出现在句子中，如酒店评价，但可以通过句子中对食物、服务等各方面评价总和获得

## Putting it all together:Finding sentiment for aspects   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image223.png) 

提取句子，进行sentiment classifier,提取aspect(描述的对象),整合

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image224.png)  

## 	Baseline methods assume classs have equal frequencies  

样本类别间不平衡时，评估使用F-score,或使用下采样获得更多样本，或对类别少的样本误分是给更重的惩罚   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image225.png)  
  
##  How to deal with 7 stars?

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image226.png)  

## Summary on Sentiment  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image227.png)  

## Scherer Typology of Affective States  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image228.png)  

其他类似分类问题

## Computational work on other affective states  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image229.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image230.png)  

