---
layout: post
title: Loss Function
date:   2019-01-01
categories: 其他
---

# Regression Loss Functions 

**Squared Error Loss(均方误差)**  

MSE=\frac{1}{n}\sum_{i=1}^n (y_{i}-f(x_{i}))

**Absolute Error Loss**  

MAE=\frac{1}{n}\sum_{i=1}^n \mid y_{i}-f(x_{i})\mid   

**Huber Loss**  

huber损失结合了mse和mae的最佳特性。对于较小的误差，它是二次型的，否则它是线性的（其梯度也类似）。

$$
L(y_{i},f(x_{i}))= \frac{1}{2}(y_{i}-f(x_{i}))^2


L(y_{i},f(x_{i})) = \left\{ \begin{array}{rl}
& \frac{1}{2}(y_{i}-f(x_{i}))^2 &\qquad \mid y_{i}-f(x_{i})\mid \le \delta \\
& \delta \mid y_{i}-f(x_{i})\mid -\frac{}{1}{2} \delta^2 &\qquad otherwise\\
\end{array} \right.


$$