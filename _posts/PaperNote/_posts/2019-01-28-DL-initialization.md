---
layout: post
title: 《initialization》相关论文
date:   2019-01-28
categories: 深度学习
---  

**涉及论文**： 
《On weight initialization in deep neural networks》
《Understanding the difficulty of training deep feedforward neural networks》


# 概述  

参数Initialization策略及激活函数的选择影响深度模型的收敛速度以及效果。  


# 梯度计算  

以feedforward nerual network为例，下图展示了计算参数梯度时(来源：台大深度学习)影响因素，从最后结果可以看出对于$$l$$层参数梯度计算，其受上一层($$l-1$$层)神经元的输出$$a_{l-1}$$,当前层激活函数对其输入微分$$\sigma ' (z^l)$$,下一层(l+1层)参数$$W^l$$,损失函数对下一层激活函数输入微分$$\delta$$影响  
![_config.yml]({{ site.baseurl }}/images/65 initialization/image1.png)
![_config.yml]({{ site.baseurl }}/images/65 initialization/image2.png)
![_config.yml]({{ site.baseurl }}/images/65 initialization/image3.png)
![_config.yml]({{ site.baseurl }}/images/65 initialization/image4.png)
