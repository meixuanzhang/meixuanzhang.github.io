---
layout: post
title: 读《Visualizing and Understanding Convolutional Networks》(ZFNet)  
date:   2019-01-28
categories: 深度学习
---  

# 概述  

论文提出一种新的可视化技术，它可以深入理解中间特征层的功能和分类器的操作。这种可视化有助于找到更优的模型架构。 

# 模型结构  

![_config.yml]({{ site.baseurl }}/images/112ZFNet/image1.jpg)    

模型由两部分组成左边是deconvnet用来可视化，右边是convnet。convnet是一个做分类任务的神经网络结构。下图Alexnet是实现了分类任务神经网络结构(论文还提到尝试了LeNet结构)： 

![_config.yml]({{ site.baseurl }}/images/112ZFNet/image2.jpg)  

论文根据deconvnet可视化对Alexnet进行修改，获得了更佳的效果。  

## Visualization with a Deconvnet   

论文提出了一种新颖的方法来将这些激活了某个Activation的特征映射回输入像素空间，以显示最初由哪种输入激活了这个Activation(激活函数神经元)。

对于一个给定的Activation，将其他Activations

convnet卷积层主要由三部分组成convolutional filter，rectified linear function，max pooling

Deconvnet提供了返回图像像素的连续路径，其不需要进行训练，只需要将原来


 
  






