---
layout: post
title: Week 6 Maxent Models
date:   2019-05-01
categories: ["From Languages to Information"]
---  

# 11.1 The Maximum Entropy Model Presentation

## Maximum Entropy Models  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image447.png)  

## Maxent Example  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image448.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image449.png)  

没有限制条件下$$-xlogx$$的最小值为$$\frac{1}{e}$$,对$$-xlogx$$求导$$logx=-1$$

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image450.png)  

the maximum entropy distribution is to say that each of those probabilities is 1/6 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image451.png)   

nouns are much more common than verbs in our data so we're going to add a feature the expected value of that feature is 32 over 36  

so if we add that constraint and then say what's the maximum Trippi distribution this constraint is satisfied the sum of these probabilities equals 32 over 36 but within that category probability mass is still going to be distributed uniformly because that that's the maximum entropy distribution   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image452.png)  

## Convexity   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image453.png)  

a convex function if we then take a sum of convex functions that's always convex

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image454.png)    


# 11.2 Feature Overlap Feature Interaction   

Feature Interaction 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image460.png)   

## Feature Overlap

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image455.png) 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image456.png) 

## Feature Interaction  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image457.png) 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image458.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image459.png)  

# 11.3 Conditional Maxent Models for Classification

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image461.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image462.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image463.png)   

## 11.4 Smoothing Regularization Priors for Maxent Models   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image464.png)  

每组数据包含$$h,t$$,模型根据$$h,t$$得出此时使用的硬币Heads和Tails的分布   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image465.png)   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image466.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image467.png)   

通过设定参数先验分布，对参数取值范围做限制。     

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image468.png)   

we take this mean to be zero which is saying that the feature is irrelevant to the classification zero weight features have no influence on the classification there's this extra parameter down here a hyper parameter as to how big is the variance and this is going to control how easy it is for the parameter to move away from zero if the variance is very small the optimization will keep the parameter values clustered close to zero if the variance is very weak they'll be allowed to walk far away as a starting off point   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image469.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image470.png)    

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image471.png)    

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image472.png)    

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image473.png)    

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image474.png)    

That's not practical for models with millions of parameters is it becomes almost impossible to know how to create artificial data in such a way that every parameter has a nonzero value without creating enormous(巨大) amounts of artificial data so that the amount of artificial data overwhelms the amount of real data


![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image475.png)    

对于出现频率少的特征去除，类似：  

we're going to estimate the weight of all rare features as 0 which you can also think of assigning them a Gaussian prior with zero variance and mean zero so that their weights can never move away from zero so dropping low counts does remove the features which are most in need of smoothing and it does speed up estimation of the model by reducing the model size but it's a very crude method of doing smoothing ,count cut-offs generally hurt accuracy

------------------------------------------------------------------------------------------------

# 12.1 An Intro to Parts of Speech and POS Tagging   

## Parts of Speech(词性标记)

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image476.png)    

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image477.png)    

## Open vs Closed classes  

closed classes don't get new members  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image478.png)  

## POS Tagging   

lots of words have more than one part of speech   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image479.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image480.png)    

Penn Treebank是一个项目的名称，项目目的是对语料进行标注，标注内容包括词性标注以及句法分析。   

## POS tagging performance   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image481.png)    

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image482.png)  

## Deciding on the correct part of speech can be difficult even for people  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image483.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image484.png)  

# 12.2 Some Methods and Results on Sequence Models for POS Tagging  

## Source of information   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image485.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image486.png)    

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image487.png)    

you can build a part of speech tagger that all gets 93.7% of words right

## Overview:POS Tagging Accuracies  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image488.png)    

## How to improve supervised result ?

if one wants to keep on working on improving things,normally the way one goes about that is by staring hard(凝视) at the output of your part of speech tag or whatever it is and looking at where it makes errors and thinking of ways in which you could encode some information into features that would let you detect that something has gone wrong and get the system to prefer some other configuration 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image489.png)   

## Tagging Without Sequence  Information   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image490.png)   

## Summary of POS Tagging  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image491.png)   

----------------------------------------------------------------------------------------  

# 13.1 Syntactic Structure Constituency vs Dependency  

syntactic constructions组合规则  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image492.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image493.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image494.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image495.png)  

# 13.2 Empirical Data Driven Approach to Parsing  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image496.png)  

millions of parses(这句话有数百万的解析)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image497.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image498.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image499.png)  

# 13.3 The Exponential Problem in Parsing 

## Attachment ambiguities(依恋歧义)  

图中展示介词短语修饰(依恋)对象  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image500.png)   

the number of possible structures  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image501.png)    

two prepositional phrases the number of possible structures is 5  

so the secret to building efficient parsers and getting away from doing an exponential amount of work is to avoid doing the same work twice we only want to find possible pieces of structure for a sentence precisely once and then we'll be able to turn parsing from an exponential problem into a polynomial time problem problem

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image502.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image503.png)   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image504.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image505.png)  
 
we'll do our statistical parsers will try and exploit such statistics about word combination which kind of preposition is likely to go with which nouns and which verbs to be able to choose the correct parses of sentences without having full understanding of them