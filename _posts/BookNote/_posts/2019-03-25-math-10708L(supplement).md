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

$$L(\mathbf{\theta};\mathcal{D})= \prod_{m}P(\xi[m];\mathbf{\theta})$$  

最大似然估计：给定数据集$$\mathcal{D}$$,选择满足下式的参数$$\hat{\mathbf{\theta}}$$   

$$L(\hat{\mathbf{\theta}};\mathcal{D})=\mathop{max}_{\mathbf{\theta} \in \Theta} L(\mathbf{\theta};\mathcal{D})$$  

$$\Theta$$为参数空间  

# 贝叶斯网的MLE  

**简单示例**  

有仅包含两个二元变量$$X,Y$$的网络，网络结构为$$X \to Y$$.网络由一个参数向量$$\mathbf{\theta}$$参数化,这个参数向量定义了网络中所有CPD的参数集合。示例中参数化包含了如下参数：$$\theta_{x^1},\theta_{x^2}$$,指定了$$X$$两个值的概率;$$\theta_{y^1\mid x^1},\theta_{y^0\mid x^1}$$,指定了当$$X=x^1$$时 $$Y$$的概率;$$\theta_{y^1\mid x^0},\theta_{y^0\mid x^0}$$,指定了当$$X=x^0$$时 $$Y$$的概率.简单起见，用$$\mathbf{\theta}_{Y \mid x^0}$$表示$$\{\theta_{y^1\mid x^0},\theta_{y^0\mid x^0}\}$$,$$\mathbf{\theta}_{Y \mid X}$$表示$$\mathbf{\theta}_{Y \mid x^1}\bigcup \mathbf{\theta}_{Y \mid x^0}$$  

示例中，每个训练实例是一个描述$$X$$与$$Y$$的一个特定赋值的元组$$(x[m],y[m])$$,似然函数为  

$$L(\mathbf{\theta};\mathcal{D})= \prod_{m}P(x[m],y[m];\mathbf{\theta})\\
=\prod_{m}P(x[m];\mathbf{\theta})P(y[m]\mid x[m];\mathbf{\theta})\\
=(\prod_{m}P(x[m];\mathbf{\theta}))(\prod_{m}P(y[m]\mid x[m];\mathbf{\theta}))
$$  

$$\prod_{m}P(x[m];\mathbf{\theta})=\prod_{m}P(x[m];\mathbf{\theta}_{X})$$  

$$\prod_{m}P(y[m]\mid x[m];\mathbf{\theta}_{Y\mid X})=\prod_{m:x[m]=x^0}P(y[m]\mid x[m];\mathbf{\theta}_{Y\mid X})\prod_{m:x[m]=x^1}P(y[m]\mid x[m];\mathbf{\theta}_{Y\mid X})\\
=\prod_{m:x[m]=x^0}P(y[m]\mid x[m];\mathbf{\theta}_{Y\mid x^0})\prod_{m:x[m]=x^1}P(y[m]\mid x[m];\mathbf{\theta}_{Y\mid x^1})$$

进一步简化如每个单独项$$P(y[m]\mid x[m];\mathbf{\theta}_{Y\mid x^0})$$都可以根据$$y[m]$$的取值在两个不同的值中任取其一。如$$y[m]=y^0$$,那么值为$$\theta_{y^0\mid x^0}$$   

## 全局似然分解  

假设我们的目标是对一个具有结构$$g$$和参数$$\mathbf{\theta}$$的贝叶斯网进行参数学习。给定一个包含样本$$\chi[1],..,\chi[M]$$的数据集$$\mathcal{D}$$。将似然函数写下来，并重复在例子中的步骤，得到：  

$$
L(\mathbf{\theta};\mathcal{D}) = \prod_{m} P_{g}(\xi[m];\mathbf{\theta})\\
=\prod_{m}\prod_{i}P(x_{i}[m]\mid pa_{X_{i}}[m];\mathbf{\theta})\\
=\prod_{i}[\prod_{m}P(x_{i}[m]\mid pa_{X_{i}}[m];\mathbf{\theta})]  
$$

用$$\mathbf{\theta}_{X_{i}\mid pa_{X_{i}}}$$来表示模型中确定$$P(X_{i}\mid pa_{X_{i}})$$的参数的子集。那么，有如下表示： 

$$L(\mathbf{\theta};\mathcal{D})= \prod_{i} L(\mathbf{\theta}_{X_{i}\mid pa_{X_{i}}};\mathcal{D})=$$

其中$$X_{i}$$的局部似然函数是：  

$$L_{i}(\mathbf{\theta}_{X_{i}\mid pa_{X_{i}}};\mathcal{D})=\prod_{m}P(x_{i}[m]\mid pa_{X_{i}}[m];\mathbf{\theta}_{X_{i}\mid pa_{X_{i}}})$$   

这个公式在参数集$$\mathbf{\theta}_{X_{i}\mid pa_{X_{i}}}$$不相交时特别有用。即，每个CPD由不重叠的参数的分离集参数化。   

# 贝叶斯参数估计

   


参考：
[Lecture 6: Learning Partially Observed GM and the EM Algorithm](https://sailinglab.github.io/pgm-spring-2019/notes/lecture-06/)



