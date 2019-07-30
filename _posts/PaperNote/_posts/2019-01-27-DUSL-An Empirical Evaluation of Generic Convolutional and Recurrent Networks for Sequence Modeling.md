---
layout: post
title: 读《An Empirical Evaluation of Generic Convolutional and Recurrent Networks for Sequence Modeling》
date:   2019-01-27
categories:  深度非监督学习
---

# 概述  
论文认为应重新考虑序列建模和循环网络(recurrent networks)之间的共同关联，并应将卷积网络视为序列建模任务的起点。文中描述了一种通用的Temporal Convolutional Network (TCN)结构。

# TCN模型结构  

序列模型Notation:    

$$x_{0},..,x_{T}:$$序列输入  
$$y_{0},..y_{T}:$$序列输出   
$$f:$$函数，$$X^{T+1}\to Y^{T+1}$$   

$$\hat{y}_{0},...\hat{y}_{T}=f(x_{0},..x_{T})$$   

损失函数：  $$L(y_{0},..y_{T},f(x_{0},..x_{T}))$$    



## causal convolutions   

TCN模型基于两个原则：神经网络输出与输入有相同长度，以及从未来到过去不会泄漏的事实。为此TCN使用了1D fully-convolutional network (FCN)结构，每层隐藏层的长度与输入长度相同，为了维持层之间长度相同，每层使用了zero padding ,其长度为(kernel size -1)，这里stride=1。同时为了根据前一个点作为输入获得输出下一个点，模型使用了causal convolutions，时间 t 的输出仅与来自前一层中的时间t和更早的元素卷积。

![_config.yml]({{ site.baseurl }}/images/64TCN/image1.png)   

一个简单的causal convolutions只能访问与神经网络深度成线性比的历史。这使得将causal convolutions应用于需要更长历史的序列任务是困难的。

## Dilated causal convolutional  

Nation

![_config.yml]({{ site.baseurl }}/images/64TCN/image2.png)  


![_config.yml]({{ site.baseurl }}/images/64TCN/image3.png)  


![_config.yml]({{ site.baseurl }}/images/64TCN/image4.png)  

参考： 
[WAVENET: A GENERATIVE MODEL FOR RAW AUDIO](https://arxiv.org/abs/1609.03499)
