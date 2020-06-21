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
=\prod_{m}\prod_{i}P(x_{i}[m]\mid pa_{x_{i}}[m];\mathbf{\theta})\\
=\prod_{i}[\prod_{m}P(x_{i}[m]\mid pa_{x_{i}}[m];\mathbf{\theta})]  
$$

用$$\mathbf{\theta}_{X_{i}\mid pa_{x_{i}}}$$来表示模型中确定$$P(X_{i}\mid pa_{x_{i}})$$的参数的子集。那么，有如下表示： 

$$L(\mathbf{\theta};\mathcal{D})= \prod_{i} L_{i}(\mathbf{\theta}_{X_{i}\mid pa_{x_{i}}};\mathcal{D})$$

其中$$X_{i}$$的局部似然函数是：  

$$L_{i}(\mathbf{\theta}_{X_{i}\mid pa_{x_{i}}};\mathcal{D})=\prod_{m}P(x_{i}[m]\mid pa_{x_{i}}[m];\mathbf{\theta}_{X_{i}\mid pa_{x_{i}}})$$   

这个公式在参数集$$\mathbf{\theta}_{X_{i}\mid pa_{x_{i}}}$$不相交时特别有用。即，每个CPD由不重叠的参数的分离集参数化。   

结论：  

令$$\mathcal{D}$$为$$X_{1},..,X_{n}$$的一个完备数据集，$$g$$为这些变量上的一个网络结构，并假定对于所有的$$j\ne i$$,参数$$\mathbf{\theta}_{X_{i}\mid pa_{x_{i}}}$$与$$\mathbf{\theta}_{X_{j}\mid pa_{x_{j}}}$$不相交。令$$\hat{\mathbf{\theta}}_{X_{i}\mid pa_{x_{i}}}$$是最大化$$L_{i}(\mathbf{\theta}_{X_{i}\mid pa_{x_{i}}};\mathcal{D})$$的参数，那么$$\hat{\mathbf{\theta}}=<\hat{\mathbf{\theta}}_{X_{1}\mid pa_{x_{1}}},..,\hat{\mathbf{\theta}}_{X_{n}\mid pa_{x_{n}}}>$$最大化$$L(\mathbf{\theta};\mathcal{D})$$   

换句话说，可以独立于其他的网络来对每个局部似然函数最大化，然后合并这些结构得到一个MLE的解

# 贝叶斯参数估计

用一个概率分布表示参数$$\theta$$的先验知识，这个分布代表了我们先验地相信参数的不同选择的可能性有多大。一旦关于$$\theta$$的可能取值有了可量化的信息，我们就可以在$$\theta$$和观测数据$$X[1],..X[M]$$上建立一个联合分布。 

似然估计中假设硬币不同的抛掷之间是相互独立的，这个假设是$$\theta$$固定时做出的。如果我们不知道$$\theta$$,那么这些抛掷的边缘独立性不存在，每次抛掷都可以传递给我们一些有关参数$$\theta$$的信息，并且因此传递给我们下一次抛掷的概率。一旦我们已知$$\theta$$，就不能通过观测其他抛掷的结果来了解一次抛掷的结果。我们假定，这些抛掷在给定条件下独立。使用图描述：      

![_config.yml]({{ site.baseurl }}/images/10708s/image1.png)   

这里$$\theta$$是一个随机变量   

## 参数独立性和全局分解  

**示例**  

假设对包含两个变量$$X$$和$$Y$$的简单网络估计参数，$$X$$是$$Y$$的父节点。训练数据由观测到的$$X[m],Y[m]$$组成，其中$$m=1,..,M$$。有未知的参数向量$$\mathbf{\theta}_{X},\mathbf{\theta}_{Y\mid X}$$,变量之间依赖关系如图所示：  

![_config.yml]({{ site.baseurl }}/images/10708s/image2.png)  

从网络结构可知，当给定未知参数时，实例之间是相互独立的,即一旦观测到参数变量，$$(X[m],Y[m])$$与$$(X[m'],Y[m'])$$是相互独立   

此外，网络结构还体现出单个参数变量的先验是先验独立的假设，即知道其中一个参数的参数值并不能告诉我们另一个参数的任何信息。定义：  

令$$g$$是一个具有参数$$\mathbf{\theta}=(\mathbf{\theta}_{X_{1}\mid pa_{x_{1}}},...,\mathbf{\theta}_{X_{n}\mid pa_{x_{n}}})$$的贝叶斯网结构。先验$$P(\mathbf{\theta})$$称为满足全局的参数独立性(global parameter independence),假如它具有如下形式:  

$$P(\mathbf{\theta})=\prod_{i}P(\mathbf{\theta}_{X_{i}\mid pa_{x_{i}}})$$  

对于路径$$\mathbf{\theta}_{X} \to X[m] \to Y[m] \gets \mathbf{\theta}_{Y\mid X} $$，$$X[m]$$观测同样会阻断这条路径。如果这两个参数变量是独立的先验，那么它们也是独立的后验。

$$P(\mathbf{\theta}_{X},\mathbf{\theta}_{Y\mid X}\mid \mathcal{D})=P(\mathbf{\theta}_{X}\mid D)P(\mathbf{\theta}_{Y\mid X}\mid \mathcal{D})$$

完整的数据可以d-separates 不同CPD的参数。如，如果对于所有的$$m$$，$$X[m],Y[m]$$是可观测的，那么$$\mathbf{\theta}_{X}$$和$$\mathbf{\theta}_{Y\mid X} $$是d-separates的。

**一般情况下的网络**  

假设已经给定一个具有参数$$\mathbf{\theta}$$的网络结构$$g$$。在贝叶斯框架下，我们需要在网络的所有可能参数化上指定一个先验$$P(\mathbf{\theta})$$。在给定数据样本$$\mathcal{D}$$的情况下，参数上的后验分布：  

$$P(\mathbf{\theta}\mid \mathcal{D}) = \frac{P(\mathcal{D} \mid \mathbf{\theta})P(\mathbf{\theta})}{P(\mathcal{D})}$$  

$$P(\mathbf{\theta})$$是先验分布，$$P(\mathcal{D} \mid \mathbf{\theta})$$是给定一个特定的参数环境时数据的概率，也就是似然函数。最后，$$P(\mathcal{D})$$是归一化尝试,这一项称为边缘似然(marginal likelihood),它并不依赖于$$\mathbf{\theta}$$，仅仅用于规范后验。   

前面将似然分解为一些局部的似然：  

$$P(\mathcal{D} \mid \mathbf{\theta}) = \prod_{i} L_{i}(\mathbf{\theta}_{X_{i}\mid pa_{x_{i}}};\mathcal{D})$$

假定全局的参数独立性成立，那么   

$$P(\mathbf{\theta})=\prod_{i}P(\mathbf{\theta}_{X_{i}\mid pa_{x_{i}}})$$   

将两个分解结合起来。得到:    

$$P(\mathbf{\theta}\mid \mathcal{D})=\frac{1}{P(\mathcal{D})}\prod_{i}[ L_{i}(\mathbf{\theta}_{X_{i}\mid pa_{x_{i}}};\mathcal{D})P(\mathbf{\theta}_{X_{i}\mid pa_{x_{i}}})]$$    

每个$$\mathbf{\theta}$$的子集$$\mathbf{\theta}_{X_{i}\mid pa_{x_{i}}}$$仅仅在乘积的一项中出现。因此，后验可以被表示为局部项的乘积。  

命题：假定$$ \mathcal{D}$$是$$\chi$$的一个完整数据集，令$$g$$是这些变量上的一个网络结构。如果$$P(\mathbf{\theta})$$满足全局的参数独立性，那么  

$$P(\mathbf{\theta}\mid \mathcal{D})= \prod_{i}P(\mathbf{\theta}_{X_{i}\mid pa_{x_{i}}}\mid \mathcal{D})$$     

## 局部分解  

示例中图17.7所描述的设置，假设$$X$$和$$Y$$都是二元的。我们需要在给定数据时表示$$\mathbf{\theta},\mathbf{\theta}_{Y\mid X}$$上的后验。 

$$P(\mathbf{\theta}_{X},\mathbf{\theta}_{Y\mid X}\mid \mathcal{D})=P(\mathbf{\theta}_{X}\mid D)P(\mathbf{\theta}_{Y\mid X}\mid \mathcal{D})$$  

前面已经说明如何处理$$\mathbf{\theta}_{X}$$，下面将说明如何处理$$\mathbf{\theta}_{Y\mid X}\mid \mathcal{D}$$,从似然分解中可以发现$$\mathbf{\theta}_{Y\mid X}$$可以分解为$$\mathbf{\theta}_{Y\mid x^0}$$和$$\mathbf{\theta}_{Y\mid x^1}$$    

将图中$$\mathbf{\theta}_{Y\mid X}$$替换为$$\mathbf{\theta}_{Y\mid x^1},\mathbf{\theta}_{Y\mid x^0}$$如图：  

![_config.yml]({{ site.baseurl }}/images/10708s/image3.png)   


$$P(\mathbf{\theta}_{Y\mid X})=P(\mathbf{\theta}_{Y\mid x^1})P(\mathbf{\theta}_{Y\mid x^0})$$

$$P()$$

参考：
[Lecture 6: Learning Partially Observed GM and the EM Algorithm](https://sailinglab.github.io/pgm-spring-2019/notes/lecture-06/)



