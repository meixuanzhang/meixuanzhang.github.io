---
layout: post
title: 读《ImageNet Classification with Deep Convolutional Neural Networks》(Alexnet)
date:   2019-01-28
categories: 深度学习
---  

# The Architecture   

![_config.yml]({{ site.baseurl }}/images/100Alexnet/image1.png)   

模型由卷积层,Local Response Normalization,max pooling,全连接层(fully-connected layer),dropout组成,鉴于当时计算能力，模型在channel维度上分割成两部分，使用两个GPU进行计算  

模型输入图片尺寸应为227*227  


# Local Response Normalization  

$$a_{x,y}^i$$表示经kernel i 卷积后产生的feature map 位置为x,y对应的元素，局部标准化即，N个kernel会产生N个feature map,对在第i个feature map位置为($$x,y$$)元素标准化，选取同位置前后其他feature map元素进行标准化。

$$b_{x,y}^i=a_{x,y}^i / (k+\alpha\sum_{j=max(0,i-n/2)}^{min(N-1,i+n/2)}}(a_{x,y}^j)^2)^{\beta}$$

式子中$$k,\eta,\alpha,\beta$$为超参数，论文中设置为$$k=2,\eta=5,\alpha=10^{-4},\beta=0.75$$,这里$$\eta$$越大local(局部)选取越大。  



# Overlapping Pooling & Dropout  

模型使用了Overlapping max Pooling 图中下方的方式，Pooling参数设置stride=2,filter大小为3*3    

![_config.yml]({{ site.baseurl }}/images/100Alexnet/image5.png)    

模型在fully-connected layer 加入dropout防止过拟合，参数设置0.5，训练时只保留50%的神经元，测试时不加入dropout，为了使分布与训练时一致，输出需要乘以0.5。  

At test time, we use all the neurons but multiply their outputs by 0.5, which is a reasonable approximation to taking the geometric mean of the predictive distributions produced by the exponentially-many dropout networks.  


# Optimization  

优化使用的是stochastic gradient descent with a batch size of 128,权重更新策略：  

$$
v_{i+1} := 0.9 \cdot v_{i}-0.0005 \cdot \epsilon  \cdot w_{i} -\epsilon <\frac{\partial L}{\partial w_{i}}>_{D_{i}}\\
w_{i+1} :=w_{i}+v_{i+1}
$$

$$\epsilon$$:learning rate   

通过均值为0,方差为0.01高斯分布随机初始化每层权重。  

We used an equal learning rate for all layers, which we adjusted manually throughout training. The heuristic which we followed was to divide the learning rate by 10 when the validation error rate stopped improving with the current learning rate. The learning rate was initialized at 0.01 and reduced three times prior to termination.

# Data Augmentation  

论文另外使用了两种Data Augmentation 方法：  

1、图像变换和水平翻转    

从256×256图像上通过随机提取227 × 227的图像块，可以获得29*29张新图片，此外并对图像块进行水平翻转，再获得29*29张新图片(文中提取是224*224图片，新生成32*32*2=2048)  

在测试时，网络会提取5个227 × 227的图像块(四个角上的图像块和中心的图像块)和它们的水平翻转(因此总共10个图像块)进行预测  

2、改变训练图像的RGB通道的强度 

通过主成分分析（PCA）颜色增强，红色值大、绿色值小的图像的红色值变化最大。


# 卷积核可视化  

论文对模型第一层所用到的96个11*11*3的卷积核进行了可视化，图中每一个小格是一个卷积核可视化结果，可以看到每个卷积核捕捉到的图像边缘   

![_config.yml]({{ site.baseurl }}/images/100Alexnet/image2.png)  


参考： 


