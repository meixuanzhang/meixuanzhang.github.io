---
layout: post
title: 读《MADE Masked Autoencoder for Distribution Estimation》
date:   2019-01-26
categories:  深度非监督学习
---
# 概述

论文回顾了Autoencoder，Autoregression估计数据概率分布，提出Maked Autoencoder估计数据概率分布。  

数据概率分布估计指的是通过样本集$$\{ x^{(t)}\}_{t=1}^T $$估计变量$$X$$的联合概率分布，这里变量可以是多维的。  

分布估计模型可以使用在许多领域如，分类、去噪、缺失插补、数据合成等   

# Autoencoder    
假设训练样本集为$$\{ x^{(t)}\}_{t=1}^T $$,每个样本的维度为D，每个维度取值范围$$x_{d}\in \{ 0,1\}$$

模型架构：  

![_config.yml]({{ site.baseurl }}/images/31MADE/image1.png)

$$h(x)=g(b+Wx)\\
\hat{x}= sigm(c+Vh(x))$$  

$$W$$是连接输入层和隐藏层的矩阵     
$$V$$是连接隐藏层和输出层的矩阵  
$$sigm(a)=\frac{1}{1+exp(-a)}$$   

cross-entropy loss(类似多标签(multilabel)问题损失函数)可以理解为negative log-likelihood function:     

$$l(x)=\sum_{d=1}^D -x_{d}log\hat{x_{d}}-(1-x_{d})log(1-\hat{x_{d}})$$   

联合概率估计为$$q(x)=\prod_{d}\hat{x_{d}}^{x_{d}}(1-\hat{x_{d}})^{1-x_{d}}$$   

Autoencoder 估计联合概率缺点是$$\sum_{x}q(x)\ne 1$$  

# Distribution Estimation as Autoregression   

autoregressive constraints: each input is reconstructed only from previous inputs in a given ordering.

autoregressive估计联合概率：   

$$
p(x)=\prod_{d=1}^D p(x_{d}\mid x_{<d})\\
x_{<d}=[x_{1},..x_{d-1}]^T
$$

令：  

$$p(x_{d}=1\mid x_{<d})=\hat{x_{d}}\\
p(x_{d}=0\mid x_{<d})=1-\hat{x_{d}}$$

则 negative log-likelihood：

$$
-logp(x)=\sum_{d=1}^D-logp(x_{d}\mid x_{<d})\\
=\sum_{d=1}^D-x_{d}logp(x_{d}=1\mid x_{<d})-(1-x_{d})logp(x_{d}=0\mid x_{<d})\\
=l(x)
$$

# Masked Autoencoders


# Deep MADE  












参考：  
[Deep Autoencoders using Tensorflow](https://towardsdatascience.com/deep-autoencoders-using-tensorflow-c68f075fd1a3)
