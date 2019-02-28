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
就是求x使function f(x)达到极大值或极小值，用公式表达如下，
Given: a function {\displaystyle f\colon A\to \mathbb {R} } {\displaystyle f\colon A\to \mathbb {R} } from some set {\displaystyle A} A to the real numbers
Sought: an element {\displaystyle \mathbf {x} _{0}\in A} {\displaystyle \mathbf {x} _{0}\in A} such that {\displaystyle f\left(\mathbf {x} _{0}\right)\leq f\left(\mathbf {x} \right)} {\displaystyle f\left(\mathbf {x} _{0}\right)\leq f\left(\mathbf {x} \right)} for all {\displaystyle \mathbf {x} \in A} {\displaystyle \mathbf {x} \in A} ("minimization") or such that {\displaystyle f\left(\mathbf {x} _{0}\right)\geq f\left(\mathbf {x} \right)} {\displaystyle f\left(\mathbf {x} _{0}\right)\geq f\left(\mathbf {x} \right)} for all {\displaystyle \mathbf {x} \in A} {\displaystyle \mathbf {x} \in A} ("maximization").


参考：[Monte Carlo methodi](https://en.wikipedia.org/wiki/Monte_Carlo_method)

