---
layout: post
title: 读《Deep Residual Learning for Image Recognition》(ResNet)
date:   2019-01-28
categories: 深度学习
---  

# 概述  

Deep networks在图像分类方面取得了一系列突破性进展，Deep networks以端到端的多层方式自然地集成了低/中/高层次的特征和分类器，并且特征的“层次”可以通过层数（深度）来丰富。学习Deep networks过程中有可能出现梯度消失/爆炸问题,通过normalized initialization和intermediate normalization layers可以使具有数十层的网络收敛，实现反向传播的随机梯度下降，但随着deeper networks开始收敛出现了degradation problem：  

随着网络深度的增加，准确性达到饱和，然后迅速下降。这不是由过度拟合引起的,并且将更多的层添加到已经是适当深度的模型中会导致更高训练错误。为了解决这个问题提出了Residual learning结构。  

![_config.yml]({{ site.baseurl }}/images/102Resnet/image1.png)  

#  Residual learning

![_config.yml]({{ site.baseurl }}/images/102Resnet/image2.png)  

$$h(x)=x,$$ identity mapping(恒等映射),图中shortcut connections表示恒等映射     

$$H(x),$$ underlying mapping to be fit by a few stacked layers, with x denoting the inputs to the first of these layers. 通过数层网络将$$x$$映射到$$H(x)$$   


$$F(x):=H(x)-x,$$Instead of hoping each few stacked layers directly fit a desired underlying mapping, we explicitly let these layers fit a residual mapping. 原本通过神经网络模型的层将$$x$$映射到$$H(x)$$,改为将$$x$$映射到$$F(x)$$,再由$$F(x)+x=H(x)$$，想当于神经网络的层拟合残差$$H(x)-x$$      

We hypothesize that it is easier to optimize the residual mapping than to optimize the original, unreferenced mapping. To the extreme, if an identity mapping were optimal, it would be easier to push residual to zero than to fit an identity mapping by a stack of nonlinear layers  

building block通过式子表示为：  

$$y=F(x,\{W_{i}\})+ x$$ 

假如building block 为两层则，$$F=W_{2}\sigma(W_{1}x)$$, $$\sigma$$激活函数ReLU，这种shortcut connections称为Identity shortcut既不增加参数也不增加计算复杂度，但要求$$F(x)$$输出与$$x$$维度一致，假如不一致可以通过$$W_{s}$$对x进行映射,这种shortcut connections称为Projection Shortcuts 即：  

$$y=F(x,\{W_{i}\})+ W_{s}x$$ 


# Network Architectures  &  Implementation  

![_config.yml]({{ site.baseurl }}/images/102Resnet/image3.jpg)    

![_config.yml]({{ site.baseurl }}/images/102Resnet/image4.png)   
  

**模型实现**  

对原始图像随机调整大小,范围为[256,480],对调整了的图片随机水平翻转，随机裁剪成224 x 224,然后减去每个像素的均值作为模型输入。 

使用[“Kaiming Initialization”](https://arxiv.org/pdf/1502.01852.pdf)方式初始化权重    

在进入激活函数前对卷积输出实现batch normalization    

使用SGD进行优化，batch的大小为256    

学习率从0.1开始，当误差达到平稳状态时除以10，学习动量为 0.9，然后对模型进行多达$$60*10^4$$次迭代的训练。   

使用0.0001的权重衰减(L2正则化)  

在测试中，为了进行比较研究，采用Alexnet方法裁剪5个224 × 224的图像块(四个角上的图像块和中心的图像块)和它们的水平翻转(因此总共10个图像块)进行预测。为了得到最好的结果，采用vgg中fully convolutional以及Multi-Scale Testing方法平均多个尺寸下分数 (images are resized such that the shorter side is in {224,256,384,480,640})   

**处理模型shortcuts三种方式**：   

(A) zero-padding shortcuts are used for increasing dimensions, and all shortcuts are parameter-free;对输入和输出维度不一致的shortcut，采用补零使输入和输出维度一致，一致则不需要改变。       

(B) projection shortcuts are used for increasing dimensions, and other shortcuts are identity;对输入和输出维度不一致的shortcut，采用映射使输入和输出维度一致，一致则不需要改变。  

(C) all shortcuts are projections.对所有的shortcut都进行映射.   

对比三种处理方式效果对比：  

![_config.yml]({{ site.baseurl }}/images/102Resnet/image7.png)   

# Experiments  

图中可以看出ResNet解决了degradation problem问题，更深的模型，错误率更低

![_config.yml]({{ site.baseurl }}/images/102Resnet/image5.png)  


# Deeper Bottleneck Architectures  

考虑到训练时间，文中将building block 修改为了bottleneck，结构如图中右边所示，通过1 x 1减少chanel维度，又通过1 x 1 恢复chanel维度。较深的non-bottleneck ResNets也可以从增加的深度获得同样精度,但计算不如bottleneck  ResNets经济，所以bottleneck设计的使用主要是出于实践考虑。    

parameter-free(不增加参数) identity shortcuts 对于bottleneck结构非常重要，如果使用projection 取代identity shortcut，时间复杂度和模型尺寸将增加了一倍，当输入和输出两个高维度连接时，因此对于bottleneck，使用identity shortcuts模型更高效。      

![_config.yml]({{ site.baseurl }}/images/102Resnet/image6.png)   


参考：

[How does mean image subtraction work?](https://stackoverflow.com/questions/44788133/how-does-mean-image-subtraction-work)
