---
layout: post
title: 读《Regularization and variable selection via the elastic net》
date:   2020-01-28
categories: 机器学习
---  

文章提出了一种新的正则化以及选择变量的方法(Elastic Net )，当特征维度远大于样本量时 Elastic Net 非常有效。

# 动机 

普通最小二乘法(ordinary least squares，OLS)在预测和解释模型方面(简单的模型可以更清楚地反映响应变量和协变量之间的关系)相对较差。   

岭回归(ridge regression)作为一种连续收缩方法，通过偏差-方差折衷获得了更好的预测性能。岭回归不能产生一个简约模型，因为它总是将所有特征保留在模型中。L2-norm    

Lasso 同时进行连续收缩和特征自动选择。但它具有一些局限性:  

+ (a)当$$p>n$$时，[Lasso最多可以选择n个特征](https://stats.stackexchange.com/questions/38299/if-p-n-the-lasso-selects-at-most-n-variables),限制了变量选择    
+ (b)如果存在一组特征，其中两两相关性非常高，那么Lasso往往只从组中选择一个特征，而不关心选择哪一个   
+ (c)当$$n>p$$情形下，如果特征之间存在高度相关性，经验上观察到Lasso的性能主要受岭回归控制  

文章的目标是找到一种新的方法，只要Lasso做得最好，它就可以和Lasso一样工作，并且可以解决上面强调的问题，即它应该在场景(a)和(b)中模拟理想选择特征方法，并且它应该比Lasso有更好的表现在场景(c)中。因此文章提出Elastic Net，它能同时进行自动选择特征和连续收缩，以及可以将相关变量选出。
 

# Naive elastic net  

假设有$$n$$个样本和$$p$$个特征，$$\mathbf{y}=(y_{1},y_{2},...,y_{n})^T , \mathbf{X}=(\mathbf{x_{1}}\mid ....\mid \mathbf{x_{p}}),\mathbf{x_{j}}=(x_{1j},...x_{nj})^T,j=1,..p$$   

经过对$$\mathbf{y}$$进行中心化和对$$\mathbf{x_{j}}$$进行标准化有：   

$$\sum_{i=1}^n y_{i}=0,\sum_{i=1}^n x_{ij}=0,\sum_{i=1}^n x_{ij}^2=1,for j = 1,2,3...p$$


对于固定非负的$$\lambda_{1},\lambda_{2}$$,可以定义Naive elastic net损失函数为：  

$$L(\lambda_{1},\lambda_{2},\mathbf{\beta}) = \mid \mathbf{y} -  \mathbf{X}\mathbf{\beta} \mid^2+\lambda_{2}\mid \mathbf{\beta} \mid^2+\lambda_{1} \mid \mathbf{\beta} \mid_{1}$$   

$$\mid \mathbf{\beta} \mid^2 = \sum_{j=1}^p \beta_{j}^2$$   

$$\mid \mathbf{\beta} \mid_{1} = \sum_{j=1}^p \mid \beta_{j}\mid$$

Naive elastic net 估计$$\hat{\mathbf{\beta}}$$最小化式子$$L$$:  

$$\hat{\mathbf{\beta} }= \mathop{\arg\max}_{\mathbf{\beta}} \{ L(\lambda_{1},\lambda_{2},\mathbf{\beta}) \}$$   


# Elastic net