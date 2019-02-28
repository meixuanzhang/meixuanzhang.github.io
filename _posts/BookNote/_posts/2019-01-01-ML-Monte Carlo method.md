---
layout: post
title: 蒙特卡罗方法（Monte Carlo method）
date:   2019-01-01
categories: 
---

# 基础概念
蒙特卡罗方法（或蒙特卡罗实验）是一类广泛的计算算法，依赖于重复随机抽样来获得数值结果。 他们的基本思想是使用随机性来解决原则上可能确定的问题。  
蒙特卡罗方法主要用于三个问题类：优化，数值积分和从概率分布生成抽取。

**优化问题Optimization problems**  
就是求x使函数f(x)达到极大值或极小值，用式子表达如下：  

Given: a function $$\mathbf{f:A \to R}$$ from some set $$A$$ to the real numbers   
Sought: an element $$\mathbf{(x_{0} \in A}$$ such that $$\mathbf(f(x_{0})\le f(x))$$ for all $$\mathbf{x \in A}$$ ("minimization") or such that $$\mathbf{f(x_{0}) \ge f(x)} for all $$\mathbf{x \in A}$$("maximization").


参考：[Monte Carlo methodi](https://en.wikipedia.org/wiki/Monte_Carlo_method)

