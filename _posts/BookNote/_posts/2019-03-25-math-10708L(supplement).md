---
layout: post
title: 17章 参数估计(补充)   
date:   2019-03-25
categories: ["Probabilistic Graphical Models"]
---  

处理参数估计任务的主要方法有两种：一种基于最大似然的估计，另一种是使用贝叶斯方法   

# 最大似然估计  

假设从一个未知的分布$$P^*(\chi)$$观测到随机变量集$$\chi$$中的一些IDD(独立同分布)样本，并且假定事先知道将要处理的样本空间(有哪些随机变量，以及它们可以取值)。样本训练集表示为$$D$$,并且假定它包含了$$\chi$$中的$$M$$个实例：$$\xi[1],..,\xi[M]$$。

假定有一个参数模型，我们希望估计该模型的参数，一个参数模型是由关于参数集合的函数$$P(\xi;\mathbf{\theta})$$.当给定参数值的一个特定集合$$\mathbf{\theta}$$和$$\chi$$,这个模型为$$\xi$$分配了一个概率(或密度)   

对于给定$$\mathbf{\theta}$$下，似然函数是模型关于训练数据的概率(或密度)   

$$L(\mathbf{\theta};\mathcal{D})$$  

   


参考：
[Lecture 6: Learning Partially Observed GM and the EM Algorithm](https://sailinglab.github.io/pgm-spring-2019/notes/lecture-06/)



