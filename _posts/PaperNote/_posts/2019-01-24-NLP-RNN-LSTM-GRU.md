---
layout: post
title: RNN、LSTM、GRU
date:   2019-01-24
categories: 深度学习
---  

**来源论文**    

《A Critical Review of Recurrent Neural Networks for Sequence Learning》

# 概述
feedforward neural network假设输入样本间是独立同分布的，在处理完一个样本(数据点)之后，网络会丢失样本整个状态信息，然后再处理下一个样本，如果每个样本都是独立生成的，则没问题。 但如果样本在时间或空间上相关(样本之间不独立)，则不符合假设。   
feedforward neural network每次输入，输出长度是固定的。不能很好对输入，输出长度不固定情境建模。  

为了能对具有时间或序列结构的数据及输入和输出长度不固定的情境进行建模，产生了RNNs(Recurrent neural networks)。   
递归神经网络（RNN）具有选择性地跨序列传递信息的能力。 因此可以对输入或输出由不独立的元素序列组成的数据建模。    

RNN的输入或输出，至少有一个是序列。当两个都是序列时，输入(Input)序列的表示为：$$(x^{(1)},x^{(2)},..x^{(T)})$$,每个$$x^{(t)}$$是一个向量，同样目标输出(target)序列的表示为：$$(o^{(1)},o^{(2)},..o^{(T)})$$。训练集中一个样本包含一对输入序列和目标输出序列，尽管输入和输出序列中对应的元素才是一个数据点。 当序列长度有限时，T表示序列最大时间索引。

序列中有时间索引的数据点可以来自现实中连续过程的等间隔样本。 

# Basic RNN 结构  

Notation:   

$$y^{(t)}:$$t时刻的输出  
$$x^{(t)}:$$t时刻的输入  
$$h^{(t)}:$$t时刻的隐藏层  
$$\sigma(\cdot):\sigma$$激活函数，可以使用不同的激活函数  
$$softmax(\cdot):softmax$$函数，可以根据情况使用其他函数   

$$h^{(t)}=\sigma(Ux^{(t)}+Wh^{(t-1)}+b_{h})\\
y^{(t)}=softmax(Vh^{(t)}+b_{y})$$

![_config.yml]({{ site.baseurl }}/images/10RNN/image1.png)  

## Deep RNN  

Deep RNN即多层RNN，通过增加中间隐藏层层数实现。我们以两层RNN为例:

Notation:   

$$W^1:$$第一层隐藏层权重,$$W^2:$$第一层隐藏层权重   
$$h^{(t)}:$$t时刻第一层隐藏层,$$Z^{(t)}:$$t时刻第二层隐藏层   

$$h^{(t)}=\sigma(Ux^{(t)}+W^1h^{(t-1)}+b_{h})\\
Z^{(t)}=\sigma(Gh^{(t)}+W^2Z^{(t-1)}+b_{z})\\
y^{(t)}=softmax(VZ^{(t)}+b_{y})$$

![_config.yml]({{ site.baseurl }}/images/10RNN/image2.png)  


## Bidirectional RNN 


Bidirectional RNN隐藏层由两部分构成:forward layer和backward layer

Notation:  
$$\overrightarrow{h}^{(t)}$$:t时刻forward layer  
$$\overleftarrow{h}^{(t)}$$:t时刻backward layer  

$$\overrightarrow{h}^{(t)}=\sigma(\overrightarrow{U}x^{(t)}+\overrightarrow{W}\overrightarrow{h}^{(t-1)}+\overrightarrow{b}_{h})\\
$$\overleftarrow{h}^{(t)}=\sigma(\overleftarrow{U}x^{(t)}+\overleftarrow{W}\overrightarrow{h}^{(t-1)}+\overleftarrowb}_{h})\\
h=[\overrightarrow{h};\overleftarrow{h}]
y^{(t)}=softmax(Vh+b_{y})$$

![_config.yml]({{ site.baseurl }}/images/10RNN/image3.png)  

## 训练

# LSTM结构

# GRU

