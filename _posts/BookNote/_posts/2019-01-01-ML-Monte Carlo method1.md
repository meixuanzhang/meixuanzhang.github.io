---
layout: post
title: 蒙特卡罗方法（Monte Carlo method）
date:   2019-01-11
categories: 
---

# 基础概念   

蒙特卡罗方法（或蒙特卡罗实验、随机抽样技术），是一类广泛的计算算法，依赖于重复随机抽样来获得数值结果。基本思想是使用随机性来解决原则上可能确定的问题。   
蒙特卡罗方法主要用于三个问题类：优化，数值积分和从概率分布采样。    

就是从概率分布采样，解决优化和数值积分问题   

**优化问题Optimization problems**   

就是求x使函数f(x)达到极大值或极小值，用式子表达如下：  

Given: a function $$\mathbf{f:A \to R}$$ from some set $$A$$ to the real numbers(实数)   
Sought: an element $$\mathbf{x_{0} \in A}$$ such that $$\mathbf{f(x_{0})\le f(x)}$$ for all $$\mathbf{x \in A}$$ ("minimization") or such that $$\mathbf{f(x_{0}) \ge f(x)}$$ for all $$\mathbf{x \in A}$$("maximization").

**数值积分Numerical integration**    

Numerical integration is used to calculate a numerical approximation for the value $$S$$, the area under the curve defined by$$f(x)$$.  
就是估计图中面积S   

![_config.yml]({{ site.baseurl }}/images/Monte Carlo method/image1.png)

**按概率分布生成样本**   

# MC直接采样（按概率分布生成样本）   
通过均匀分布采样，实现对任意分布采样  

流程： 

生成样本的概率密度函数为f(x)   

从均匀分布(0,1)随机产生一个样本z  

令 z=F(x),其中F(x)为x的CDF(累积分布函数)    

计算$$x^\ast=F^{-1}(z)$$（逆函数）       

结果$$x^\ast$$为对f(x)的采样    

不断循环产生符合f(x)分布的样本$$x^\ast$$   

例(离散变量)：

$$\xi :$$均匀分布产生的样本

![_config.yml]({{ site.baseurl }}/images/Monte Carlo method/image2.png)   
![_config.yml]({{ site.baseurl }}/images/Monte Carlo method/image4.png) 

# MC 接受——拒绝采样   

有一些分布CDF的逆函数不容易计算，所以提出接受——拒绝采样  

流程：(我们目的是要按f(x)分布生成样本)   

生成样本的的概率密度函数为f(x)   

寻找另一个概率密度函数g(x)(逆函数容易计算),对所有x满足：$$c \centerdot g(x)\ge f(x)$$    

从g(x)随机产生一个样本$$x^\ast$$   

从均匀分布$$(0,cg(x^\ast))$$随机产生一个样本z  

如果$$z\le f(x^\ast)$$,则接受$$x^\ast$$为对f(x)的采样,否则拒绝  

![_config.yml]({{ site.baseurl }}/images/Monte Carlo method/image5.png)

# MC求解数值积分问题   

**普通数值积分:** 将区间[a,b]分为N份，每份等间距为$$\bigtriangleup x$$:     

$$S=\sum_{i=1}^Nf(x_{i})\bigtriangleup x$$    

$$x_{i} = a+(i-0.5)\bigtriangleup x $$ and $$\bigtriangleup x =\frac{b-a}{N} $$     
$$x_{i}$$是每个间距的中点   

$$S=\frac{b-a}{N}\sum_{i=1}^Nf(x_{i})$$   

**标准MC求解数值积分:**  

$$
S = \int_{a}^b f(x)dx = \int_{a}^b w(x)h(x)d_{x}=E_{h}(w(x))\\
where \ h(x) = \frac{1}{b-a} \ and \ w(x)=f(x)\centerdot(b-a)
$$

其中$$h(x)=\frac{1}{b-a}$$是服从均匀分布U(a,b)随机变量的概率密度函数 

从均匀分布U(a,b)生成N个样本，计算：    

$$S =\frac{\sum_{i=1}^Nw(x_{i})}{N}$$      

如果f(x)是均匀分布则：   

$$S=\frac{b-a}{N}\sum_{i=1}^Nf(x_{i})$$    


**Importance sampling求解数值积分**    

$$S = \int w(x)h(x)d_{x}$$    

w是一个函数，h是随机变量x的概率密度函数    
当很难从h分布进行采样时，则使用Importance sampling，相比起从h采样，可以定义一个不同的概率密度函数g，从g进行采样  

$$
S = \int w(x)h(x)d_{x}\\
= \int w(x)\frac{h(x)}{g(x)}g(x)d_{x}\\
=  \int \frac{w(x)h(x)}{g(x)}g(x)d_{x}\\
$$  

从g分布生成N个样本：  

$$
E_{h}[w(x)] = \int\frac{w(x)h(x)}{g(x)}g(x)d_{x}=E_{g}[\frac{w(x)h(x)}{g(x)}]\\
=\frac{\sum_{i=1}^N\frac{w(x_{i})h(x_{i})}{g(x_{i})}}{N}
$$

$$r = \frac{h(x)}{g(x)}$$是importance weights，当$$h(x)>g(x)$$，比值会大于1，$$r \centerdot g>g$$  

![_config.yml]({{ site.baseurl }}/images/Monte Carlo method/image6.png)   

在解决实际问题的时候应用蒙特卡罗方法主要有两部分工作：  
用蒙特卡罗方法模拟某一过程时，需要产生各种概率分布的随机变量。  
用统计方法把模型的数字特征估计出来，从而得到实际问题的数值解。  

参考：  
[Monte Carlo methodi](https://en.wikipedia.org/wiki/Monte_Carlo_method)       
[Mathematical optimization](https://en.wikipedia.org/wiki/Mathematical_optimization)    
[Numerical integration](https://en.wikipedia.org/wiki/Numerical_integration)  
[Monte Carlo Sampling Methods](http://web.tecnico.ulisboa.pt/~mcasquilho/acad/theo/simul/Vujic.pdf)  
[Importance Sampling](http://astrostatistics.psu.edu/su14/lectures/cisewski_is.pdf)
