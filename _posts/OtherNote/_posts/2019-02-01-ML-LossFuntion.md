---
layout: post
title: Loss Function
date:   2019-01-01
categories: 函数
---

# Regression Loss Functions 

**Mean Squared Error Loss(均方误差)**  

$$

MSE=\frac{1}{n}\sum_{i=1}^n (y_{i}-f(x_{i}))^2 

$$

**Mean Absolute Error Loss**  

$$

MAE=\frac{1}{n}\sum_{i=1}^n \mid y_{i}-f(x_{i})\mid   

$$

**Huber Loss**  

huber损失结合了MSE和MAE的最佳特性。对于较小的误差，它是二次型的，否则它是线性的（其梯度也类似）。

单个样本loss:  

$$

L(y_{i},f(x_{i})) = \left\{ \begin{array}{rl}
& \frac{1}{2}(y_{i}-f(x_{i}))^2 &\qquad \mid y_{i}-f(x_{i})\mid \le \delta \\
& \delta \mid y_{i}-f(x_{i})\mid -\frac{1}{2} \delta^2 &\qquad otherwise\\
\end{array} \right.

$$

**Mean Bias Error**  

$$

MBE=\frac{1}{n}\sum_{i=1}^n (y_{i}-f(x_{i}))

$$  

**Mean squared logarithmic error(MSLE)**  

$$

MSLE=\frac{1}{n}\sum_{i=1}^n(log(y_{i}+1)-log(f(x_{i})+1))

$$  



$$
log(y_{i}+1)-log(f(x_{i})+1)=log\frac{y_{i}+1}{f(x_{i})+1}

$$

# Binary Classification Loss Functions   

考虑到分类的二进制性质，损失函数(假设假正和假负的成本相等)将是0-1损失函数(0-1指标函数)，预测的分类等于true类的值，则取0；预测的分类与true类不匹配，则取1。

**Binary Cross-Entropy**   

$$
Cross Entropy=\left\{ \begin{array}{rl}
& -\int p(x)log q(x)dx &\mbox{,x is continuous} \\
& -\sum_{x}p(x)log q(x) &\mbox{,x is discrete} \\
\end{array} \right.

$$

单个样本的loss,$$y_{i}\in {1,0}$$:  

$$
L(y_{i},p_{i})=-y_{i}*log(p_{i})-(1-y_{i})*log(1-p_{i})=\left\{ \begin{array}{rl}
& -log(1-p_{i}) &,y_{i}=0 \\
& -log(p_{i})&,y_{i}=1\\
\end{array} \right.
$$

This is also called Log-Loss.   

$$y_{i}\in {1,0}$$ :  

$$
p(y_{i}=1\mid x_{i})=\frac{1}{1+exp(-f(x_{i}))}\\
p(y_{i}=0\mid x_{i})=\frac{1}{1+exp(f(x_{i}))}\\
$$

$$y_{i}\in {1,-1}$$ :  


$$
p(y_{i}\mid x_{i})=\frac{1}{1+exp(-y_{i}f(x_{i}))}\\
$$


**Hinge Loss**  

$$  

Hinge Loss= \sum_{i=1}^n max(0,1-y_{i}f(x_{i}))

$$  

**Squared hinge**  

$$  

Squared Hinge Loss = \sum_{i=1}^n (max(0,1-y_{i}f(x_{i})))^2  

$$  

**Exponential loss**   

AdaBoost使用指数损失：  

$$  

L=\frac{1}{n}\sum_{i=1}^n exp(-y_{i}f(x_{i}))   

$$  

$$f(x_{i}) = log(\frac{p(1\mid x_{i})}{1-p(1\mid x_{i})}) = \theta^{T}x_{i}$$

$$p(1\mid x_{i})=\frac{1}{1+e^{-\theta^{T}x_{i}}}$$

其损失是分类错误的上限  


# Multi-class Classification Loss Functions  

**Multi-class Cross Entropy Loss**  

单个样本损失：  

$$
L(y_{i},f(x_{i}))=-\sum_{j=e}^c y_{i}^j *log p_{i}^j
$$ 

$$y_{i}$$是one-hot encoded target vector$$(y_{i}^1,y_{i}^2,...,y_{i}^c)$$   


$$  

y_{i}^j=\left\{ \begin{array}{rl}
& 1 &i_{th}\mbox{element is in class j} \\
& 0 &\mbox{otherwise} \\
\end{array} \right.
$$  

$$p_{i}^j=f(x_{i})$$=Probability that $$i_{th}$$ element is in class j. 

softmax function:   

$$
\sigma(Z)_{i}\frac{e^{z_{i}}}{\sum_{j=1}^K e^{z_{j}}}

$$

$$
Z=(z_{1},...z_{K})\in R^K
$$


**Kullback Leibler Divergence Loss**  

Expectation of logaritmic difference between P and Q with respect to P(真实分布)  

$$
D_{KL}(P\mid \mid Q)\left\{ \begin{array}{rl}
& -\sum_{x}P(x)log \frac{Q(x)}{P(x)}=\sum_{x}P(x)log\frac{P(x)}{Q(x)} &\mbox{discrete distributions} \\
& -\int P(x) log\frac{Q(x)}{P(x)}= \int P(x)log\frac{P(x)}{Q(x)}dx&\mbox{continuous distributions} \\
\end{array} \right.
$$  


$$
D_{KL}(P\mid \mid Q)=-\sum_{x}(P(x)logQ(x)-P(x)logP(x))=H(P,Q)-H(P,P)

$$









 