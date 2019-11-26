---
layout: post
title: 读《Deep Residual Learning for Image Recognition》(ResNet)
date:   2019-01-28
categories: 深度学习
---  

# 概述  

Deep networks在图像分类方面取得了一系列突破性进展，Deep networks以端到端的多层方式自然地集成了低/中/高层次的特征和分类器，并且特征的“层次”可以通过层数（深度）来丰富。学习Deep networks过程中有可能出现梯度消失/爆炸问题,通过normalized initialization和intermediate normalization layers可以使具有数十层的网络收敛，实现反向传播的随机梯度下降，随着deeper networks开始收敛出现了degradation problem：  

随着网络深度的增加，准确性达到饱和，然后迅速下降。这不是由过度拟合引起的,并且将更多的层添加到已经是适当深度的模型中会导致更高训练错误。为了解决这个问题提出了Residual learning结构。  

![_config.yml]({{ site.baseurl }}/images/102Resnet/image1.png)  

#  Residual learning

![_config.yml]({{ site.baseurl }}/images/102Resnet/image2.png)  

$$h(x)=x,$$ identity mapping(恒等映射),图中shortcut connections表示恒等映射    
$$H(x),$$ underlying mapping to be fit by a few stacked layers, with x denoting the inputs to the first of these layers.  
$$F(x):=H(x)-x,$$Instead of hoping each few stacked layers directly fit a desired underlying mapping, we explicitly let these layers fit a residual mapping.   

原本通过神经网络模型的层将$$x$$映射到$$H(x)$$,改为将$$x$$映射到$$F(x)$$,再由$$F(x)+x=H(x)$$，想当于神经网络的层拟合残差$$H(x)-x$$     

We hypothesize that it is easier to optimize the residual mapping than to optimize the original, unreferenced mapping. To the extreme, if an identity mapping were optimal, it would be easier to push residual to zero than to fit an identity mapping by a stack of nonlinear layers  

building block通过式子表示为：  

$$y=F(x,\{W_{i}\})+ x$$ 

假如building block 为两层则，$$F=W_{2}\sigma(W_{1}x)$$,$$\sigma$$激活函数ReLU，这种shortcut connections既不增加参数也不增加计算复杂度，但要求$$F(x)$$输出与$$x$$维度一致，假如不一致可以通过$$W_{s}$$对x进行映射即：  

$$y=F(x,\{W_{i}\})+ W_{s}x$$ 


# Network Architectures  &  Implementation  

![_config.yml]({{ site.baseurl }}/images/102Resnet/image3.png)    

![_config.yml]({{ site.baseurl }}/images/102Resnet/image4.png)    

The image is resized with its shorter side randomly sampled in [256,480] for scale augmentation .(对原始图片随机调整大小，范围为[256,480])  

A 224 x 224 crop is randomly sampled from an image or its horizontal flip, with the per-pixel mean subtracted.(对调整了大小的图片随机水平翻转，随机裁剪成224 x 224,减去每个像素的均值)  

We adopt batch normalization (BN) right after each convolution and before activation  在进入激活函数前对卷积输出进入batch normalization

We initialize the weights as in [13] and train all plain/residual nets from scratch  ??

We use SGD with a mini-batch size of 256. 使用SGD进行优化，batch的大小为256  

The learning rate starts from 0.1 and is divided by 10 when the error plateaus, and the models are trained for up to $$60*10^4$$ iterations. 

We use a weight decay of 0.0001 and a momentum of 0.9. 

In testing, for comparison studies we adopt the standard 10-crop testing(参考Alexnet). For best results, we adopt the fullyconvolutional form as in [41, 13], and average the scores at multiple scales (images are resized such that the shorter side is in {224,256,384,480,640}

 
# Experiments  

图中可以看出ResNet解决了degradation problem问题，更深的模型，错误率更低

![_config.yml]({{ site.baseurl }}/images/102Resnet/image5.png)  


# Deeper Bottleneck Architectures

![_config.yml]({{ site.baseurl }}/images/102Resnet/image6.png)   


参考：

[How does mean image subtraction work?](https://stackoverflow.com/questions/44788133/how-does-mean-image-subtraction-work)
