---
layout: post
title: MCMC采样方法：MH、GibbSample
date:   2019-01-01
categories: 
---

# MCMC方法(Markov Chain Monte Carlo)
马尔可夫链蒙特卡罗（MCMC）方法包括一类用于从概率分布中采样的算法。通过构建一条马尔可夫链，它的平稳分布是所需分布(要采样的概率分布)，通过观察马尔可夫链随机过程，从而获得所需分布的样本。    
这条马尔可夫链的平稳分布是知道的$$\pi$$，但是转移概率P是未知的，任意初始状态分布x经过n次迭代后会收敛于$$\pi$$,目前问题是我们需要找打合适的P。  
目前常用MCMC采样方法有Metropolis-Hastings、Gibb Sample。
# Metropolis-Hastings  
Notation:  
$$P(x)=\pi_{x}$$：所需分布(要采样的概率分布)、马尔可夫链平稳分布  
$$P(y \mid x)$$：$$P(x)$$作为平稳分布的马尔可夫链的转移概率分布  
$$g(y \mid x)$$：候选的转移概率分布(proposal distribution)  
$$A$$：接受移动率(acceptance ratio)  

目前已知马尔可夫链平稳分布$$\pi_{x}=P(x)$$,希望通过$$P(y \mid x)$$转移概率分布进行采样，因$$P(y \mid x)$$未知，所以提出$$g(y \mid x)$$作为候选的转移概率分布。通过候选分布进行采样。

真实转移概率分布应满足：  

$$P(y \mid x)P(x)=P(x|y)P(y)$$   

左边表示从 x 移动到 y 的非条件概率,x是从$$\pi$$生成的,右边表示从y 移动到 x的非条件概率（x'是从$$\pi$$生成的），两个概率相等   

候选分布未必满足$$g(y \mid x)P(x)=g(x|y)P(y)$$，即x 移动到 y的频率与y 移动到 x频率不相等，因此引入A接受移动率。$$A<1$$,上极限是1。通过调节使两边相等：  

$$A(x,y)g(y \mid x)P(x)=A(y,x)g(x|y)P(y)$$

A(x,y):x移动到y的接受率
A(y,x):y移动到x的接受率

当g(y \mid x)P(x)>g(x|y)P(y)










$$
\frac{P(x' \mid x)}{P(x|x')}=\frac{P(x')}{P(x)}
$$    

$$g(x'\mid x)$$是在条件x情况下生成x'的概率，$$A(x',x)$$是接受候选样本x'的概率。真实转移概率可以写成：   

$$P(x' \mid x)=g(x' \mid x)A(x',x)$$   

因此有：  

$$\frac{A(x',x)}{A(x,x')}=\frac{P(x')g(x \mid x')}{P(x)g(x' \mid x) }$$    

如果x'接受率高于或等于x（$$P(x')g(x \mid x') \ge P(x)g(x' \mid x)$$），我们总是接受x'，否则我们将以$$\frac{P(x')g(x \mid x')}{P(x)g(x' \mid x) }$$概率随机接受x',或拒绝x'。因此：  

$$A(x',x)=min(1,\frac{P(x')g(x \mid x')}{P(x)g(x' \mid x)})$$

步骤：  
1、Generate：从$$g(y\mid x)$$分布中生成一个候选样本$$x'$$    
2、Calculate:计算接受率$$A(y,x)=min(1,\frac{P(y)g(x \midy)}{P(x)g(y \mid x) })$$  
3、Accept or Reject：  
+ 从[0,1]均匀分布中生成样本u
+ 如果$$u \le A(y,x)$$,接受$$x_{t+1}=y$$
+ 如果$$u > A(y,x)$$,拒绝x'，$$x_{t+1}=x$$

4,Increment：设t=t+1




# Gibb Sample




参考：    
[](https://eml.berkeley.edu/reprints/misc/understanding.pdf)
