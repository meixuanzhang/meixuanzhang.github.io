---
layout: post
title: 读《A Neural Probabilistic Language Model》
date:   2019-01-01
categories: 深度学习(NLP)
---  

# 概述    

论文提出的模型同时学习words的distributed representation(类似Embedding matrix)和单词序列的概率函数，通过学习distributed representation对抗words高维度问题，distributed representation允许每个训练句子让模型学会指数个语义相邻的句子，因为distributed representation中含有语义信息，并且相似的词在词向量上也是相似，学会一个句子同时也学会相似句子。  

模型有很好泛化能力，因为如果一个从未见过的单词序列是与一个已经见过的句子的单词相似，那么的未见过的单词概率会跟相似单词相近。  


# 模型架构  

**Notation:**  

V：词汇表  
$$w_{1},..w_{T}$$:一个长度为T的训练序列，$$w_{t}\in V$$  
$$w_{1}^{t-1}=(w_{1}...w_{t-1})$$，训练词$$w_{t}$$所在句子其前t-1个词    
$$C:$$distributed representation矩阵，维度为$$|V|*m,C(i)\in R^m$$表示V词汇表里第i个单词在C的映射向量，即distributed feature vectors   


$$\theta=(b,d,W,U,H,C)$$:模型参数    
$$R(\theta)$$：惩罚项   
$$\varepsilon$$:学习率  


**模型函数:**  

通过 f 函数计算在已知单词$$w_{1}^{t-1}$$条件下，下一个单词是$$w_{t}$$的概率：

$$f(w_{t}..w_{t-n+1})=P(w_{t}\mid w_{1}^{t-n+1})\approx P(w_{t}\mid w_{1}^{t-1})$$  

在已知单词$$ w_{1}^{t-n+1}$$条件下，下一个单词是 i 的概率：

$$f(i,w_{t-1},..,.w_{t-n+1})=g(i,C(w_{t-1}),..C(w_{t-n+1}))$$ 


**整个神经网络计算如下：** 


![_config.yml]({{ site.baseurl }}/images/NlpPaper/image1.png)

网络以前n个单词的distributed feature vectors作为输入,经过隐藏层,跳跃连接及softmax输出层，获得每个单词的条件概率。

H是隐藏层参数，维度为$$(h*(n-1)m)$$，d是隐藏层的bias,维度为$$(|V|)$$，tanh是隐藏层激活函数。   
U,W是输出层的参数，维度分别为$$(|V|*h)，(|V|*(n-1)m)$$，b是输出层的bias，维度为$$(|V|)$$。   
当W全为0时则不存在跳跃连接。  
$$y_{i}$$表示单词 i 非标准化的log概率。   

$$
x=(C(w_{t-1}),C(w_{t-2}),..C(w_{t-n+1}))\\
y=b+Wx+Utanh(d+Hx)\\
P(w_{t}\mid w_{t-1}..w_{t-n+1})=\frac{e^{y_{w_{t}}}}{\sum_{i}e^{y_{i}}}
$$

假设训练数据集为$$w_{1},..w_{T}$$序列,损失函数为(最大化)： 

$$
L=\frac{1}{T}\sum_{t}logf(w_{t}..w_{t-n+1};\theta)+R(\theta)
$$

在随机梯度下降中序列里每个字概率对参数更新：  

$$
\theta \gets \theta +\varepsilon\frac{\partial logP(w_{t}\mid w_{t-1},..w_{t-n+1})}{\partial \theta}
$$







