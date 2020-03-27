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









