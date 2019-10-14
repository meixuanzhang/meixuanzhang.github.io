---
layout: post
title: Loss Function
date:   2019-01-01
categories: 其他
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

L(y_{i},f(x_{i}))=\frac{1}{n}\sum_{i=1}^n(log(y_{i}+1)-log(f(x_{i})+1))

$$  



$$
log(y_{i}+1)-log(f(x_{i})+1)=log\frac{y_{i}+1}{f(x_{i})+1}

$$

# Binary Classification Loss Functions   

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
p(y_{i}mid x_{i})=\frac{1}{1+exp(-y_{i}f(x_{i}))}\\
$$


**Hinge Loss**  

$$  

L(y_{i},f(x_{i})) = \sum_{i=1}^n max(0,1-y_{i}f(x_{i}))

$$  

**Squared hinge**  

$$  

L(y_{i},f(x_{i})) = \sum_{i=1}^n (max(0,1-y_{i}f(x_{i})))^2  

$$  

**Exponential loss**   

AdaBoost使用指数损失：  

$$  

L(y_{i},f(x_{i}))=\frac{1}{n}\sum_{i=1}^n exp(y_{i}f(x_{i}))   

$$  

其损失是分类错误的上限  


# Multi-class Classification Loss Functions  






 