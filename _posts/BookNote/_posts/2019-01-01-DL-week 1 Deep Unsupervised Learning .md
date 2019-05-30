---
layout: post
title: week 1 Motivation、 Autoregressive Models
date:   2019-03-23
categories: ["Deep Unsupervised Learning"]
---

# Motivation(动机)

1、为什么学习非监督学习？

+ 监督学习需要标注数据，会花费大量时间和钱
+ 非监督学习有更多的数据和信息
+ 智能就是压缩(compression)，如从几个想法中找出所有模式(规则)=找出原始数据简短描述，找出压缩数据最小程序，找出最短代码推断在数据中发现，这些都是非监督学习   


![_config.yml]({{ site.baseurl }}/images/30Deep Unsupervised Learning/image1.png)


2、非监督学习有两个方法
+ 基于生成的非监督学习(generative models-based unsupervised learning) 对数据建模，创建数据概率分布
+ 自监督学习 self-supervised learning  

3、非监督学习的应用
+ 生成数据
+ 压缩
+ 提升下游任务
+ 构建可以重复使用的模块，解决其他问题


# Autoregressive Models

1、Likelihood Models :Autoregressive Models    

压缩就是构建有效的代码，就像你想用一个很小文件替代10g电影，而压缩和生成模型关系是，生成模型就是预测，能预测好意味越少数据的传输，实现了压缩，例如你可以预测(生成)我打算说的每个单词，你不需要写下任何东西，你不需要保存信息(压缩)，如果你不能预测，就需要保存所有东西。  

基于似然的模型，就是数据联合概率分布
你有样本数据$$x^{(1)},..,x^{(n)}$$，它们是通过独立同分布$$P_{data}$$采样获得的，似然模型就是通过获得的样本数据估计数据的联合概率分布$$P_{data}$$,
分布P是一个函数，输入是数据点，输出是0到1的概率,如果输出是0，说明数据点不属于这个分布(Anomal detection)异常检测   

我们希望既能估计高维度数据分布同时保持计算和统计效率 

![_config.yml]({{ site.baseurl }}/images/30Deep Unsupervised Learning/image2.png) 

![_config.yml]({{ site.baseurl }}/images/30Deep Unsupervised Learning/image3.png)

2、Histogram 模型——最基本的基于似然的生成模型   

生成模型的目标是通过样本数据估计数据概率分布，然后从估计概率分布生成数据
假设样本取值是1到k,生成模型分布函数输入是1到k,模型就是集合$$p_{1}...p_{k}$$,histogram生成模型就是通过数据集频数估计$$p_{1}...p_{k}$$    

![_config.yml]({{ site.baseurl }}/images/30Deep Unsupervised Learning/image4.png)
![_config.yml]({{ site.baseurl }}/images/30Deep Unsupervised Learning/image5.png)


histogram生成模型没办法解决高维度数据生成问题。例如MINIST数据集，样本维度是$$28*28$$，每个像素的取值是0或1，则样本取值空间是$$2^{784}$$，样本数据量是60000，远小于样本空间，在数据集外你没办法估计样本分布。使用histogram模型，只有60000个参数不为零(样本取值空间对应的P就是所有参数)，这是样本中出现过的数据，当我们生成数据时，只能生成这60000个样本中的一个。每个样本只能影响其自身对应的参数p，不影响其他参数   

![_config.yml]({{ site.baseurl }}/images/30Deep Unsupervised Learning/image6.png)

解决的办法是function approximation,使用$$\theta$$作为函数的参数，输入数据会映射到对应概率，每个数据点更新$$\theta$$时，相比起histogram模型不再是只更新自身对应p，会影响到其他$$p_{1}..p_{k}$$.$$\theta$$维度会远小于k。  
$$P_{\theta}$$是模型架构，如带权重参数的神经网络。使用最大似然估计法估计参数，这相当于最小化KL散度。KL散度是大于等于0的。     

![_config.yml]({{ site.baseurl }}/images/30Deep Unsupervised Learning/image7.png) 

![_config.yml]({{ site.baseurl }}/images/30Deep Unsupervised Learning/image8.png) 

$$
KL(\hat{p}_{data}(x)\parallel p_{\theta}(x))=\sum_{x}\hat{p}_{data}(x) log\frac{\hat{p}_{data}(x)}{p_{\theta}(x)}\\
=\sum_{x}\hat{p}_{data}(x) (-log\frac{p_{\theta}(x)}{\hat{p}_{data}(x)})\\
=E_{x\sim \hat{p}_{data}(x)}[-logp_{\theta}-log\hat{p}_{data}(x)]\\
=E_{x\sim \hat{p}_{data}(x)}[-logp_{\theta}]-H(\hat{p}_{data}(x))\\
=H(\hat{p}_{data}(x)p_{\theta}(x))-H(\hat{p}_{data}(x))
$$

![_config.yml]({{ site.baseurl }}/images/30Deep Unsupervised Learning/image9.png)

![_config.yml]({{ site.baseurl }}/images/30Deep Unsupervised Learning/image10.png)  

![_config.yml]({{ site.baseurl }}/images/30Deep Unsupervised Learning/image11.png) 

3、自回归模型(Autoregressive model)

原本定义： An autoregressive model is when a value from a time series is regressed on previous values from that same time series.   
图中autoregressive式子表明，维度 x 之间是有顺序的，只有前面的维度可以估计后面的维度，不能反过来。

![_config.yml]({{ site.baseurl }}/images/30Deep Unsupervised Learning/image13.png) 

在autoregressive性质下通过贝叶斯网络结构构建维度之间的关系然后通过神经网络计算维度间条件概率分布，能计算出每个样本联合概率，最后获得数据联合概率分布，这里存在问题是神经网格参数会随样本维度增加而增加，维度越大贝叶斯网络结构越复杂，需要计算的条件概率越多，神经网络数量增加(每个神经网络负责贝叶斯结构里一个条件概率,如图中$$P(J\mid A)$$和$$P(M\mid A)$$需要两个不同的神经网络)，神经网络间参数是相互独立的。

![_config.yml]({{ site.baseurl }}/images/30Deep Unsupervised Learning/image12.png) 

![_config.yml]({{ site.baseurl }}/images/30Deep Unsupervised Learning/image14.png) 

![_config.yml]({{ site.baseurl }}/images/30Deep Unsupervised Learning/image15.png) 

为此提出了条件分布间共享参数  

4、RNN autoregressive  

![_config.yml]({{ site.baseurl }}/images/30Deep Unsupervised Learning/image16.png) 

5、Masking-based autoregressive models   

MADE相比起RNN autoregressive和Bayes autoregressive训练时可以进行平行运算，不需要等待前面的条件概率计算完再进行后面计算，会一次性输出计算联合概率分布所需的条件概率   
  

生成过程不是平行的，如图中需要根据histogram选择$$x_{2}$$的值，然后将$$x_{2}$$作为网络输入，得到$$p(x_{3}\mid x_{2})$$分布，根据分布得到$$x_{3}$$的取值，然后将$$x_{2},x_{3}$$输入到网络得到$$p(x_{1}\mid x_{2},x_{3})$$的分布，根据分布得到$$x_{1}$$的取值。   

最后每个神经元如($$p(x_{1}\mid x_{2},x_{3})$$)输出的是一个向量，通过softmax表示条件下$$x_{1}$$取值分布    

[MADE论文笔记](https://meixuanzhang.github.io/DUSL-MADE-Masked-Autoencoder-for-Distribution-Estimation/)   


![_config.yml]({{ site.baseurl }}/images/30Deep Unsupervised Learning/image17.png)  

![_config.yml]({{ site.baseurl }}/images/30Deep Unsupervised Learning/image18.png) 

模型评估：  

使用测试集(没见过的图片)计算$$-logp$$    
没见过的图片联合概率不为零说明有一定泛化能力   
从生成结果看，会生成没有见过的图片，模型不仅仅是记住看过的图片    

![_config.yml]({{ site.baseurl }}/images/30Deep Unsupervised Learning/image20.png)  

![_config.yml]({{ site.baseurl }}/images/30Deep Unsupervised Learning/image21.png)   

代码实现:  

![_config.yml]({{ site.baseurl }}/images/30Deep Unsupervised Learning/image19.png) 


6、  Masked Temporal Convolution   

![_config.yml]({{ site.baseurl }}/images/30Deep Unsupervised Learning/image22.png)    

7、

valid autoregressive ordering


可以处理长度可变的情况
