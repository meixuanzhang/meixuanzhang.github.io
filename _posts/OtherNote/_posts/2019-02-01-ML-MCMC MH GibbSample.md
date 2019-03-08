---
layout: post
title: MCMC采样方法：MH、GibbSample
date:   2019-01-01
categories: 
---

# MCMC方法(Markov Chain Monte Carlo)
马尔可夫链蒙特卡罗（MCMC）方法包括一类用于从概率分布中采样的算法。通过构建一条马尔可夫链，它的平稳分布是所需分布(要采样的概率分布)，通过观察马尔可夫链随机过程，从而获得所需分布的样本。目前常用MCMC采样方法有Metropolis-Hastings、Gibb Sample。 
# Metropolis-Hastings  
Notation:  
$$P(x)=\pi_{x}$$：所需分布(要采样的概率分布)、马尔可夫链平稳分布  
$$P(x_{t+1}\mid x_{t})$$：$$P(x)$$作为平稳分布的马尔可夫链真实的转移概率分布  
$$g(x_{t+1}\mid x_{t})$$：建议的转移概率分布(proposal distribution)  
$$A$$：接受率(acceptance ratio)  
步骤：  
1、Generate：从g(x'\mid x)分布中生成一个候选样本$$x'$$    
2、Calculate:计算接受率$$A(x',x)=min(1,\frac{P(x')g(x \mid x')}{P(x)g(x' \mid x) })$$  
因为P(x)是平稳分布所以$$P(x'\mid x)P(x)=P(x',x)=P(x|x')P(x')$$，即：   

$$
\frac{P(x' \mid x)}{P(x|x')}=\frac{P(x')}{P(x)}
$$    

$$g(x'\mid x)$$是在条件x情况下生成x'的概率，$$A(x',x)$$是接受候选样本x'的概率。真实转移概率可以写成：   

$$P(x' \mid x)=g(x' \mid x)A(x',x)$$   

因此有：  

$$\frac{A(x',x)}{A(x,x')}=\frac{P(x')g(x \mid x')}{P(x)g(x' \mid x) }$$    

如果x'接受率高于或等于x（$$P(x')g(x \mid x') \ge P(x)g(x' \mid x)$$），我们总是接受x'，否则我们将以$$\frac{P(x')g(x \mid x')}{P(x)g(x' \mid x) }$$概率随机接受x',或拒绝x'。因此：  

$$A(x',x)=min(1,\frac{P(x')g(x \mid x')}{P(x)g(x' \mid x)})$$

3、Accept or Reject：  
+ 从[0,1]均匀分布中生成样本u
+ 如果$u \le A(x'x)$$,接受x_{t+1}=x'
+ 如果$u \ge A(x'x)$$,拒绝x'，x_{t+1}=x_{x_{t}}=x

4,Increment：设t=t+1
# Gibb Sample
