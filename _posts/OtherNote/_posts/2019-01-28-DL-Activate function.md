---
layout: post
title: 激活函数(Activate function)
date:   2019-01-28
categories: 深度学习
---  

# 饱和激活函数与非饱和激活函数    

假设$$g(x)$$是一个激活函数

1、当x取值趋近于正无穷时，激活函数的导数趋近于0，此称之为右饱和 

$$\mathop{lim}_{x\to +\infty }h'(x)=0$$

2、当x取值趋近于负无穷时，激活函数的导数趋近于0，此称之为左饱和

$$\mathop{lim}_{x\to -\infty }h'(x)=0$$

3、当一个函数既满足左饱和又满足右饱和的时候我们就称之为饱和，典型的函数有Sigmoid，Tanh函数。  

![_config.yml]({{ site.baseurl }}/images/66Activate function/image2.png)

## sigmoid  

## tanh

## ReLU
