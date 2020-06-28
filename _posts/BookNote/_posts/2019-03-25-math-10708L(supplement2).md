---
layout: post
title: 第6章 基于模板的表示(补充)   
date:   2019-03-25
categories: ["Probabilistic Graphical Models"]
---  

所有个体都可以用相同的属性集进行描述，只是属性的值因个体的不同而不同。由于这种表示的关注点是随机变量的集合，因此这类模型称为基于变量的模型。  

构建一个单一、紧凑的模型，为同一类型的整个分布类提供模板：不同长度的轨迹，不同谱系。本章中定义了表示形式(representation)，允许我们在丰富结构空间上定义分布，结构由多个对象组成，并以各种方式互相关联。这是基于模板表示方法。  

# 时间模型(Temporal Models)    

对动态环境建模，对随着时间变化的世界状态进行推理。我们可以根据系统状态对此类环境进行建模，其在t时刻的值是系统的相关属性(隐藏或可观测)在t时刻的值。假定系统状态可以通过一组随机变量(随机变量集)$$\chi$$里的变量的赋值来表示。令$$X_{i}^{(t)}$$表示变量$$X_{i}$$在时刻t的实例化。$$X_{i}$$不再是去某个值的变量，而是一个模板变量(template variable).该模板在不同时刻t被实例化，每个$$X_{i}^{(t)}$$是变量，取值为$$Val(X_{i})$$.  

对变量集$$\mathbf{X}\subseteq \chi$$，使用$$\mathbf{X}^{t_{1}:t_{2}}(t_{1} < t_{2})$$定义变量集合$$\{\mathbf{X}^{t}:t\in [t_{1},t_{2}]\}$$ ，使用$$\mathbf{x}^{t:t'}$$表示对这个变量集合的一个赋值

现在，每一个“可能世界”在概率空间中是一条轨迹(trajectory)：对每个相关的时刻t,为每个变量$$X_{i}^{t}$$赋值  



![_config.yml]({{ site.baseurl }}/images/10708s/image2.png)  



参考：
[Lecture 6: Learning Partially Observed GM and the EM Algorithm](https://sailinglab.github.io/pgm-spring-2019/notes/lecture-06/)



