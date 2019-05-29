---
layout: post
title: 读《MADE Masked Autoencoder for Distribution Estimation》
date:   2019-01-26
categories:  深度非监督学习
---
# 概述

论文回顾了Autoencoder，Autoregression估计数据概率分布，提出Maked Autoencoder估计数据概率分布。  

数据概率分布估计指的是通过样本集$$\{ x^{(t)}\}_{t=1}^T $$估计变量$$X$$的联合概率分布，这里变量可以是多维的。  

分布估计模型可以使用在许多领域如，分类、去噪、缺失插补、数据合成等   

# Autoencoder    
假设训练样本集为$$\{ x^{(t)}\}_{t=1}^T $$,每个样本的维度为D，每个维度取值范围$$x_{d}\in \{ 0,1\}$$

模型架构：  

![_config.yml]({{ site.baseurl }}/images/31MADE/image1.png)   

$$h(x)=g(b+Wx)\\
\hat{x}= sigm(c+Vh(x))$$  

$$W$$是连接输入层和隐藏层的矩阵     
$$V$$是连接隐藏层和输出层的矩阵  
$$sigm(a)=\frac{1}{1+exp(-a)}$$   

cross-entropy loss(类似多标签(multilabel)问题损失函数)可以理解为negative log-likelihood function:     

$$l(x)=\sum_{d=1}^D -x_{d}log\hat{x_{d}}-(1-x_{d})log(1-\hat{x_{d}})$$   

联合概率估计为$$q(x)=\prod_{d}\hat{x_{d}}^{x_{d}}(1-\hat{x_{d}})^{1-x_{d}}$$   

Autoencoder 估计联合概率缺点是$$\sum_{x}q(x)\ne 1$$  

# Distribution Estimation as Autoregression   

autoregressive constraints: each input is reconstructed only from previous inputs in a given ordering.

autoregressive估计联合概率：   

$$
p(x)=\prod_{d=1}^D p(x_{d}\mid x_{<d})\\
x_{<d}=[x_{1},..x_{d-1}]^T
$$

令：  

$$p(x_{d}=1\mid x_{<d})=\hat{x_{d}}\\
p(x_{d}=0\mid x_{<d})=1-\hat{x_{d}}$$

则 negative log-likelihood：

$$
-logp(x)=\sum_{d=1}^D-logp(x_{d}\mid x_{<d})\\
=\sum_{d=1}^D-x_{d}logp(x_{d}=1\mid x_{<d})-(1-x_{d})logp(x_{d}=0\mid x_{<d})\\
=l(x)
$$

# Masked Autoencoders   

修改autoencoder使其满足autoregressive性质：output$$\hat{x_{d}}$$只能与先于$$x_{<d}$$的input有关，意味$$\hat{x_{d}}$$与$$x_{d},..x_{D}$$不应该存在连接计算路径，因此对于这种路径在矩阵$$W,V$$对于位置至少有一个为零。注意这里整个input是有序的序列。

$$ M^w,M^v$$是binary mask matrix,用来作elementwise-multiply(矩阵对应元素相乘)，使原本$$W,V$$部分路径元素为0.

模型架构：  

$$
h(x)=g(b+(W\odot M^w)x)\\
\hat{x}= sigm(c+(V\odot M^v)h(x))
$$

$$m(k)$$表示隐藏层第k个神经元能连接序列中第$$m(k)$$个及前面的input，例如$$m(k)=4$$,表示第k个隐藏神经元可以连接序列中位于1,2,3,4位置的input。
m的取值范围为 1 和 D-1，因为如果为零表示隐藏层中该神经元不与任何input相连。如果为D则表示隐藏层中该神经元与任何input都相连，那样该神经元无法与任何output相连，不然不满足autoregressive性质  

$$
M_{k,d}^w=1_{m(k)\ge d}=\left\{ \begin{array}{rl}
& 1 &\qquad if \ m(k)\ge d \\
& 0 &\qquad otherwise\\
\end{array} \right.
$$

$$
M_{d,k}^v=1_{m(k)\ge d}=\left\{ \begin{array}{rl}
& 1 &\qquad if \ d>m(k) \\
& 0 &\qquad otherwise\\
\end{array} \right.
$$



举个例子如图：$$m(5)=4$$意味4及其前面的input会与后面5,6位置output存在路径，第五个神经元会连接4及其前面的input，同时与5,6位置output相连

$$M^{v,w}=M^v M^w$$ 会是一个下三角矩阵(对角线为0)，从图中可以发现input位置数大于等于output位置数的元素总是为0。  

![_config.yml]({{ site.baseurl }}/images/31MADE/image3.jpg)

过去autoregressive神经网络研究发现，在input层和output层直接添加连接会提升表现，所以改造后$$\hat{x}$$：

$$\hat{x}=sigm(c+(V\odot M^v)h(x)+(A\odot M^A)x)$$

$$A$$是下三角矩阵(对角线为0)  

# Deep MADE  

Deep MADE隐藏层数L>1,图中展示了一个中间由两层隐藏层构成的MADE，以及对input序列采用了不同的排序，$$\{x_{2},x_{3},x_{1}\}$$

![_config.yml]({{ site.baseurl }}/images/31MADE/image2.png)


对于Deep MADE mask满足以下式子：

$$
M_{\dot{k},k}^{w^l}=1_{m^l(\dot{k})\ge m^{l-1}(k)}=\left\{ \begin{array}{rl}
& 1 &\qquad if \ m^l(\dot{k})\ge m^{l-1}(k)}\\
& 0 &\qquad otherwise\\
\end{array} \right.
$$

$$
M_{d,k}^v=1_{m(k)\ge d}=\left\{ \begin{array}{rl}
& 1 &\qquad if \ d>m(k) \\
& 0 &\qquad otherwise\\
\end{array} \right.
$$

训练采样了两种技巧:

**Order-agnostic training**  

对input序列sample an ordering before each stochastic/minibatch gradient update of the model.这样有两个优点，一是对于缺失值，we invoke an ordering where observed dimensions are all before unobserved ones, making inference straightforward.二是计算联合概率时，平均不同的ordering下的联合概率作为最后的结果。

**Connectivity-agnostic training**  

训练过程中，神经网络无法确定神经元输出为0是由于mask造成的还是由于神经元权重w与输入乘积值为0，因此加入companion weight $$U^l$$,$$l$$层隐藏层输出更新为：

$$
h^l(x)=g(b^l+(W^l\odot M^{w^l})h^{l-1}(x)+(U^l\odot M^{w^l})1)
$$

这样当神经元权重w与输入乘积值为0，mask不为0时，神经元输出不再是0。这个设置是一个超参数，也就是不一定会这样设置。

# 










参考：  
[Deep Autoencoders using Tensorflow](https://towardsdatascience.com/deep-autoencoders-using-tensorflow-c68f075fd1a3)
