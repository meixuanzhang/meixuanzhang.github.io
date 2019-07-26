---
layout: post
title: 《initialization》相关论文
date:   2019-01-28
categories: 深度学习
---  

**涉及论文**： 
《Understanding the difficulty of training deep feedforward neural networks》 
《On weight initialization in deep neural networks》   
   


# 概述  

参数Initialization策略及激活函数的选择影响深度模型的收敛速度以及效果。  


# 梯度计算  

以feedforward nerual network为例，下图展示了计算参数梯度时(来源：台大深度学习)影响因素，从最后结果可以看出对于$$l$$层参数梯度计算，其受上一层($$l-1$$层)神经元的输出$$a_{l-1}$$,当前层激活函数对其输入微分$$\sigma ' (z^l)$$,下一层(l+1层)参数$$W^l$$,损失函数对下一层激活函数输入微分$$\delta$$影响  
![_config.yml]({{ site.baseurl }}/images/65 initialization/image1.png)
![_config.yml]({{ site.baseurl }}/images/65 initialization/image2.png)
![_config.yml]({{ site.baseurl }}/images/65 initialization/image3.png)
![_config.yml]({{ site.baseurl }}/images/65 initialization/image4.png)



# 《Understanding the difficulty of training deep feedforward neural networks》   

论文对比了Softsign(x),tanh(x),sigmod(x)三种不同激活函数以及不同参数初始化方法下saturation情况及梯度变化情况 

##  Effect of Activation Functions and Saturation During Training  

这里参数初始化方式是：  
$$
W_{ij} \sim U[-\frac{1}{\sqrt{n}},\frac{1}{\sqrt{n}}]
$$

表示参数服从范围为$$[-\frac{1}{\sqrt{n}},\frac{1}{\sqrt{n}}]$$的均匀分布，$$n$$是神经网络前一层神经元数，$$W$$的列数  

### Experiments with the Sigmoid  

从图中可以发现训练开始，除了神经网络最后一层，其他层的激活值(激活函数输出值)围绕在0.5，随着神经网络加深，激活值有下降趋势，神经网络最后一层激活值在很长一段时间内值为0，处于饱和状态，对于神经网络中间层(图中第四层)，随着epoch增加激活值出现了从饱和状态“逃离”现象，同时第一层部分激活值开始出现了饱和状态，如果参数初始化是采用预训练的方式则不会出现这样的饱和现象。   

逻辑层输出$$softmax(b + Wh)$$最初可能更多地依赖于其偏差$$b$$（其学习非常快）而不是顶部隐藏激活$$h$$（因为$$h$$的变化方式不能预测y的变化，输出可能主要与x的其他更主要的变化相关)。因此，误差梯度倾向于将$$Wh$$推向0，这可以通过将$$h$$推向0来实现。在对称激活函数（例如双曲正切和softsign）的情况下，值在0附近是好的，因为它允许梯度向后流动(此时梯度大)。但是，将S形输出推到0将使它们进入饱和状态，这将防止梯度向后流动并防止较低层学习有用的特征。最终但缓慢地，较低层向更有用的特征移动，然后顶部隐藏层移出饱和状态。  




### Experiments with the Hyperbolic tangent

### Experiments with the Softsign


