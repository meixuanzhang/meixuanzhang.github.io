---
layout: post
title: 蒙特卡罗方法（Monte Carlo method）
date:   2019-01-01
categories: 
---

# 基础概念
蒙特卡罗方法（或蒙特卡罗实验、随机抽样技术），是一类广泛的计算算法，依赖于重复随机抽样来获得数值结果。基本思想是使用随机性来解决原则上可能确定的问题。 
蒙特卡罗方法主要用于三个问题类：优化，数值积分和从概率分布生成抽取。

**优化问题Optimization problems**  

就是求x使函数f(x)达到极大值或极小值，用式子表达如下：  

Given: a function $$\mathbf{f:A \to R}$$ from some set $$A$$ to the real numbers(实数)   
Sought: an element $$\mathbf{x_{0} \in A}$$ such that $$\mathbf{f(x_{0})\le f(x)}$$ for all $$\mathbf{x \in A}$$ ("minimization") or such that $$\mathbf{f(x_{0}) \ge f(x)}$$ for all $$\mathbf{x \in A}$$("maximization").

**数值积分Numerical integration**
Numerical integration is used to calculate a numerical approximation for the value $$S$$, the area under the curve defined by$$f(x)$$.
就是估计面积S

**按概率分布生成样本**

# MC求解数值积分问题

# MC求解按概率分布采样（生成样本）——直接采样
通过均匀分布采样，实现对任意分布采样  
流程：  
从Uniform(0,1)随机产生一个样本z
令z=h(y),其中h(y)为y的CDF(累积分布函数)
计算$$y=h^-1(z)$$  
结果y为对P(y)的采样  

# 接受——拒绝采用




在解决实际问题的时候应用蒙特卡罗方法主要有两部分工作：
用蒙特卡罗方法模拟某一过程时，需要产生各种概率分布的随机变量。
 用统计方法把模型的数字特征估计出来，从而得到实际问题的数值解。

参考：  
[Monte Carlo methodi](https://en.wikipedia.org/wiki/Monte_Carlo_method)       
[Mathematical optimization](https://en.wikipedia.org/wiki/Mathematical_optimization)    
[Numerical integration](https://en.wikipedia.org/wiki/Numerical_integration)  
