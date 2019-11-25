---
layout: post
title: 读《Deep Residual Learning for Image Recognition》(ResNet)
date:   2019-01-28
categories: 深度学习
---  

# 概述  

Deep networks在图像分类方面取得了一系列突破性进展，Deep networks以端到端的多层方式自然地集成了低/中/高层次的特征和分类器，并且特征的“层次”可以通过层数（深度）来丰富。学习Deep networks过程中有可能出现梯度消失/爆炸问题,通过normalized initialization和intermediate normalization layers可以使具有数十层的网络收敛，实现反向传播的随机梯度下降，随着deeper networks开始收敛出现了degradation problem：  

随着网络深度的增加，准确性达到饱和，然后迅速下降。这不是由过度拟合引起的,并且将更多的层添加到已经是适当深度的模型中会导致更高训练错误。为了解决这个问题提出了Residual learning结构。  

#  Residual learning

![_config.yml]({{ site.baseurl }}/images/102Resnet/image2.png)  


# Network Architectures   

![_config.yml]({{ site.baseurl }}/images/102Resnet/image3.png)

![_config.yml]({{ site.baseurl }}/images/102Resnet/image4.png)    

![_config.yml]({{ site.baseurl }}/images/102Resnet/image5.png)  


# Deeper Bottleneck Architectures

![_config.yml]({{ site.baseurl }}/images/102Resnet/image6.png)  
