---
layout: post
title: 读《Word Embedding》相关论文(word2vec、Glove)
date:   2019-01-01
categories: 深度学习
---  

**涉及论文：**  

《Efficient Estimation of Word Representations in Vector Space》  
《Distributed Representations ofWords and Phrases and their Compositionality》  
《Distributed Representations of Sentences and Documents》  
《GloVe: Global Vectors forWord Representation》  

# word2vec模型

word2vec模型优点：训练后单向向量能捕获句法信息和单词语义间关系

word2vector总共有两种类型，分别是CBOW(Continuous Bag-of-Words)、Skip-gram,为了减少计算成本每种类型有两种算法策略,分别是Hierarchical Softmax、Negative Sampling。

## CBOW模型架构 

Notation: 

V:词汇表  
$$W:$$前Embedding matrix,维度$$|V|*l$$  
$$U:$$后Embedding matrix,维度$$|V|*l$$  

假设给定一个训练序列$$w_{1},..w_{T}$$,其目标函数为

$$L=\frac{1}{T}\sum_{t=k}^{T-k}logP(w_{t}\mid w_{t-k}...w_{t+k})$$

$$P(w_{t}\mid w_{t-k}...w_{t+k})=\frac{e^{y_{w_{t}}}}{\sum_{i}e^{y_{i}}}$$

$$y=b+Uh(w_{t-k}...w_{t+k};W)$$

y是向量维度为|V|  

h是$$w_{t-k}...w_{t+k}$$在W对应vector的均值


## Skip-gram模型架构

# doc2vec模型

# Glove模型


