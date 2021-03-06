---
layout: post
title: 读《Character-Aware Neural Language Models》
date:   2019-01-25
categories: 深度学习(NLP)
---  

# 概述

论文展示CNN-LSTM结构的神经语言模型，模型的输入是character-level,输出仍然是word-level，word的character是CNN的输入，CNN的输出是LSTM的输入。

# 模型结构    

![_config.yml]({{ site.baseurl }}/images/99Character-Aware Neural Language Models/image1.png)


## Character-level Convolutional Neural Network  


Notation:   
$$\bar{C}:$$ the vocabulary of characters,词汇的所有字符(字母)   
$$d:$$ 字符embedding的维度    
$$Q\in R^{d*\mid \bar{C} \mid}:$$matrix character embeddings,字符的embedding矩阵   
$$c_{j}:$$是Q的第$$j$$列向量   

假设词语$$k$$是由长度为$$l$$序列字符组成$$[c_{1}...c_{l}]$$，词语$$k$$的character-level representation是矩阵$$C^k \in R^{d*l}$$,将$$C^k$$作为CNN的输入，CNN应用窄卷积(不使用padding的方法)，kernel为$$H\in R^{d*w}$$,输出的feature-map$$f^k\in R^{l-w+1}$$.  

feature-map$$f^k$$第i个元素为： 

$$f^k[i]=tanh(<C^k[*,i:i+w-1],H>+b)$$  

$$b:$$是偏差bias   
$$C^k[*,i:i+w-1]$$表示$$C^k$$的第$$i$$到$$i+w-1$$列    
$$<A,B>$$表示Frobenius inner product(内积)，就是A,B对应位置元素相乘的和   

CNN的一个kernel(or filter)的输出为：  

$$y^k=max_{i}f^k[i]$$

假设CNN有h个kernel分别为$$H_{1}..H_{j}$$,则对于词语k，CNN输出为$$Y^k=[y_{1}^k,..y_{h}^k]$$  

## LSTM Neural Network Language Model  

t时刻CNN的输出为$$Y_{t}$$，以CNN的输出作为LSTM的输入，LSTM的结构为:    

[LSTM结构](https://meixuanzhang.github.io/NLP-RNN-LSTM-GRU/)

相比起直接将$$Y_{t}$$作为LSTM的输入，论文在CNN和LSTM中间增加了Highway Network，Highway Network以CNN的输出$$Y$$作为输入,输出$$z$$作为LSTM的输入：   

$$
z=t\odot g(W_{H}Y+b_{H})+(1-t)\odot Y\\
t=\sigma(W_{T}Y+b_{T})
$$  

$$g$$是非线性函数     
$$W_{H}$$、$$W_{T}$$是权重矩阵，$$b_{H}$$和$$b_{T}$$是偏差   


## 损失函数negative log-likelihood 

将$$w_{1:T}=[w_{1},..w_{T}]$$定义为训练语料库中的词语序列，我们的目标是最小化negative log-likelihood(NNL)函数：  

$$
NLL=-\sum_{t=1}^TlogPr(w_{t}\mid w_{1:t-1})
$$

$$Pr(w_{t}\mid w_{1:t-1})$$由LSTM输出获得,表示$$w_{1:t-1}$$条件下$$w_{t}$$发生的概率   

# 效果评估  

论文中采用perplexity(PPL)评估模型表现，对于序列$$[w_{1},..w_{T}]$$其perplexity(PPL)值为：   

$$
PPL=exp(\frac{NLL}{T})
$$




