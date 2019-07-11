---
layout: post
title: 激活函数(Activate function)
date:   2019-01-28
categories: 深度学习
---  

# 饱和激活函数与非饱和激活函数    

假设$$h(x)$$是一个激活函数

1、当x取值趋近于正无穷时，激活函数的导数趋近于0，此称之为右饱和 

$$\mathop{lim}_{x\to +\infty }h'(x)=0$$

2、当x取值趋近于负无穷时，激活函数的导数趋近于0，此称之为左饱和

$$\mathop{lim}_{x\to -\infty }h'(x)=0$$

3、当一个函数既满足左饱和又满足右饱和的时候我们就称之为饱和，典型的函数有Sigmoid，Tanh函数。    

![_config.yml]({{ site.baseurl }}/images/66Activate function/image2.png)  

4、对于任意的$$x$$，如果存在常数$$c$$，当$$x>c$$时，恒有$$h'(x)=0$$，则称其为右硬饱和。如果对于任意的$$x$$，如果存在常数$$c$$，当$$x<c$$时，恒有$$h'(x)=0$$,则称其为左硬饱和。既满足左硬饱和又满足右硬饱和的我们称这种函数为硬饱和。

5、对于任意的$$x$$，如果存在常数$$c$$，当$$x>c$$时，恒有$$h'(x)$$趋近于0，则称其为右软饱和。如果对于任意的$$x$$，如果存在常数$$c$$，当$$x<c$$时，恒有$$h'(x)$$趋近于0,则称其为左软饱和。既满足左软饱和又满足右软饱和的我们称这种函数为软饱和。



## sigmoid  

$$\sigma(x)=\frac{1}{1+e^{-x}}$$

## tanh双曲正切

$$tanh(x)=\frac{sinh(x)}{cosh(x)}=\frac{e^x-e^{-x}}{e^x+e^{-x}}$$  

## ReLU  

$$f(x)=max(0,x)$$

## Leaky ReLU  


$$
f(x) = \left\{ \begin{array}{rl}
& x &\qquad if \ x \ge 0\\
& ax &\qquad if \ x \le 0\\
\end{array} \right.
$$  



## RReLU(Randomized Leaky ReLU)  

## PReLU

## Mazout  

## ELU(Expoential Linear Units)  

参考：  

[激活函数中的硬饱和，软饱和，左饱和和右饱和](https://blog.csdn.net/donkey_1993/article/details/81662065)
