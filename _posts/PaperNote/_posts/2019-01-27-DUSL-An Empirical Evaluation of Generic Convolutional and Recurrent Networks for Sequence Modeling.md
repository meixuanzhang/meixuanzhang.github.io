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



## Dilated causal convolutional  

一个简单的causal convolutions只能访问与神经网络深度成线性比的历史。这使得将causal convolutions应用于需要更长历史的序列任务是困难的。解决的方法是使用Dilated convolutional。   

Dilated convolutional:   

![_config.yml]({{ site.baseurl }}/images/64TCN/image4.jpg)  

Dilated causal convolutional:  

![_config.yml]({{ site.baseurl }}/images/64TCN/image2.png) 

Notation:  

$$x \in R^n$$:序列输入   
$$f:\{0,..,k-1\}\to R:$$卷积的filter  
$$d:$$dilation factor   
$$k:$$filter size  
$$s-d \cdot i:$$解释了过去的方向

$$F(s)=(x*_{d}f)(s)=\sum_{i=0}^{k-1}f(i)\cdot x_{s-d \cdot i}$$  

使用较大的dilation可以使输出表示更宽范围的输入，从而有效的扩展ConvNet的感受野。选择更大的filter以及增加dilation factor 可以增大感受野，每一层在前一层有效历史是(k-1)d

使用dilated convolutions时，通常会随着网络深度以指数形式增加dilation factor大小(即$$d=O(2^i)$$)，这可以确保每一个输入都会有一些filter，同时允许使用深度网络获得极大的有效历史


![_config.yml]({{ site.baseurl }}/images/64TCN/image3.png)  





## Residul Connection  

由于TCN的感受野取决于网络深度$$n$$以及filter尺寸$$k$$和dilation factor$$d$$，因此，对于更深和更大TCN的稳定变得非常重要。例如，在预测可能依赖于大小为$$2^{12}$$的历史和高维输入序列的情况下，可能需要最多12层的网络。更具体地说，每一层都由多个filter组成，用于特征提取。因此，在我们的通用TCN模型设计中，我们使用Residul模块代替卷积层。由于输入和输出长度是不一致的，因此加入了$$1*1$$convolution。模型还使用了weight normalization,以及Dropout


## 优点  

+ Parallelism(平行运算)   
+ Flexible receptive field size(灵活的感受野)   
+ Stable gradients(避免了梯度爆炸和消失问题)  
+ Low memory requirement for training
+ Variable length inputs



参考： 
[WAVENET: A GENERATIVE MODEL FOR RAW AUDIO](https://arxiv.org/abs/1609.03499)
