---
layout: post
title: 激活函数(Activate function)
date:   2019-01-28
categories: 函数
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

$$\hat{p} = \sigma(x)=\frac{1}{1+e^{-x}}$$

**导数**：  $$\frac{\partial \hat{p} }{\partial x} = \sigma(x)\cdot(1-\sigma(x))$$

## tanh双曲正切

$$tanh(x)=\frac{sinh(x)}{cosh(x)}=\frac{e^x-e^{-x}}{e^x+e^{-x}}\\
=\frac{e^{2x}-1}{e^{2x}+1}$$ 

**导数**：  $$1-tanh^2(x)=1-(\frac{e^{2x}-1}{e^{2x}+1})^2$$

## ReLU  

$$f(x)=max(0,x)$$

**导数**： 

$$
\left\{ \begin{array}{rl}
& 1 &\qquad if \ x > 0\\
& 0 &\qquad if \ x \le 0\\
\end{array} \right.
$$


An advantage to ReLU other than avoiding vanishing gradients problem(梯度消失) is that it has much lower run time. max(0,a) runs much faster than any sigmoid function (logistic function for example = 1/(1+e^(-a)) which uses an exponent which is computational slow when done often).


## Leaky ReLU  & PReLU(Parametric ReLU)


$$
f(x) = \left\{ \begin{array}{rl}
& x &\qquad if \ x > 0\\
& ax &\qquad if \ x \le 0\\
\end{array} \right.
$$  


Leaky ReLU :$$a$$是一个固定值，根据先验知识决定，取值范围$$a \in (0,1)$$   
PReLU : $$a$$是参数，需要神经网络学习

**导数**： 

$$
\left\{ \begin{array}{rl}
& a &\qquad if \ x > 0\\
& 1 &\qquad if \ x \le 0\\
\end{array} \right.
$$

## RReLU(Randomized Leaky ReLU)  

$$
f(x) = \left\{ \begin{array}{rl}
& x &\qquad if \ x > 0\\
& ax &\qquad if \ x \le 0\\
\end{array} \right.
$$  

$$a$$是一个随机值，其服从均匀分布$$U(l,u)$$，其中$$l<u$$且$$l,u\in[0,1)$$

**导数**： 

$$
\left\{ \begin{array}{rl}
& 1 &\qquad if \ x > 0\\
& a &\qquad if \ x \le 0\\
\end{array} \right.
$$

## Mazout  

Notation:  
$$h_{i}$$:隐藏层的第 i 个神经元 
$$z_{ij}$$:第 i 个神经元的第j个输入  
$$W_{..ij}$$:计算第 i 个神经元对应第 j 个权重向量，i对应$$W$$的第二维,j对应$$W$$的第三维

$$h_{i}(x)=\mathop{max}_{j\in [1,k]}z_{ij}\\
where \ z_{ij}=x^TW_{...ij}+b_{ij},and \  W\in R^{d*m*k} $$  

对于隐藏层第i个神经元，计算出$$k$$个$$z_{ij}$$,取值最大的作为神经元$$i$$的输入

## ELU(Expoential Linear Units)  

$$
elu(x)= \left\{ \begin{array}{rl}
& x &\qquad if \ x > 0\\
& a(e^x-1)x &\qquad if \ x \le 0\\
\end{array} \right.
$$  

**导数**： 

$$
\left\{ \begin{array}{rl}
& 1 &\qquad if \ x > 0\\
& elu(x)+a &\qquad if \ x \le 0\\
\end{array} \right.
$$

## SELU(Scaled exponential Linear Unit)  

$$
selu(x)=\lambda\left\{ \begin{array}{rl}
& x &\qquad if \ x > 0\\
& a(e^x-1)x &\qquad if \ x \le 0\\
\end{array} \right.
$$

**导数**： 

$$
\left\{ \begin{array}{rl}
& \lambda &\qquad if \ x > 0\\
& selu(x)+\lambda a &\qquad if \ x \le 0\\
\end{array} \right.
$$

## Loss: Softmax 

Notation:  

$$z_{j}$$: 最后一层隐藏层第j个神经元  
$$a_{j}$$: 是第j个神经元类别概率输出  
$$y$$: 是one-hot向量  

$$
a_{j}=\frac{e^{z_{j}}}{\sum_{k=1}^K e^{z_{k}}}  \ for \ j =1,..K   
$$

$$C=-\sum_{j}y_{j}lna_{j}$$

$$\frac{\partial C}{\partial z_{j}}=a_{j}\sum_{k}y_{k}-y_{j}\\
=a_{j}-y_{j}$$  

y向量只有一个维度为1，其余为0


参考：  

[激活函数中的硬饱和，软饱和，左饱和和右饱和](https://blog.csdn.net/donkey_1993/article/details/81662065)
