---
layout: post
title: 读《Visualizing and Understanding Convolutional Networks》(ZFNet)  
date:   2019-01-28
categories: 深度学习(CV)
---  

# 概述  

论文提出一种新的可视化技术，它可以深入理解中间特征层的功能和分类器的操作。这种可视化有助于找到更优的模型架构。 

# 模型结构  

![_config.yml]({{ site.baseurl }}/images/112ZFNet/image1.jpg)    

模型由两部分组成左边是deconvnet用来可视化，右边是convnet。convnet是一个做分类任务的神经网络结构。下图Alexnet是实现了分类任务神经网络结构(论文还提到尝试了LeNet结构)： 

![_config.yml]({{ site.baseurl }}/images/112ZFNet/image2.jpg)  

论文根据deconvnet可视化对Alexnet进行修改，获得了更佳的效果。  

## Visualization with a Deconvnet   

论文提出了一种新颖的方法来将这些激活了Activation的特征映射回原始输入像素空间，以找到哪种类型输入能激活了这个Activation(激活函数神经元)。

convnet卷积层主要由三部分组成convolutional filter，rectified linear function，max pooling，input经过convolutional filter输出feature Map ,feature Map经过rectified linear function输出rectified feature Map，rectified feature Map 经过 Max Pooling 输出Pooled Map. Activation 相当于与 feature Map每个位置对应的rectified linear function。

为了研究哪种类型输入能激活(通过)某个位置的Activation，需将其他Activation设置为零，以rectified feature Map作为输入，经过rectified linear function(除了研究位置的Activation，其他设置为零,则输出也会为0)输出 rectified unpooled Map，rectified unpooled Map经过Transposed Convolution输出Reconstruction,Reconstruction 经过 Max Unpooling 输出Unpooled Map,Unpooled Map经过rectified linear function输出 rectified unpooled Map，不断返回直到回到图片输入层。

对于一个给定的Activation，将其他Activations

convnet卷积层主要由三部分组成convolutional filter，rectified linear function，max pooling



Deconvnet提供了返回图像像素的连续路径，其不需要进行训练，只需要将原来


 
  






