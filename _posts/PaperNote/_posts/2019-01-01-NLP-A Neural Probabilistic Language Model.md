---
layout: post
title: 《A Neural Probabilistic Language Model》
date:   2019-01-01
categories: 深度学习
---  

# 概述    

论文提出的模型同时学习words的distributed representation(类似Embedding matrix)，以及单词序列的概率函数，通过学习distributed representation对抗words高维度问题，distributed representation允许每个训练句子让模型学会指数个语义相邻的句子，因为distributed representation中含有语义信息，并且相似的词在词向量上也是相似，学会一个句子同时也学会相似句子。  

模型有很好泛化能力，因为如果一个从未见过的单词序列是与一个已经见过的句子的单词相似，那么的未见过的单词概率会跟相似单词相近。  


# 模型架构  

**Notation:**  

V：词汇表
$$w_{1},..w_{T}$$:长度为T的训练序列，$$w_{t}\in V$$ 
$$w_{1}^{t-1}=(w_{1}...w_{t-1})$$  
$$C:$$distributed representation矩阵，维度为$$|V|*m,C(i)\in R^m$$表示V词汇表里第i个单词在C的映射向量，即distributed feature vectors  


**模型函数: **

通过 f 函数计算在已知的单词$$w_{1}^{t-1}$$条件下，下一个单词是$$w_{t}$$的概率，f 函数的输入是$$w_{t}$$的前n个单词

$$f(w_{t}..w_{t-n+1})=P(w_{t}\mid w_{1}^{t-1})$$  

在已知的单词$$w_{1}^{t-1}$$条件下，第i个单词的概率：

$$f(i,w_{t-1},..,.w_{t-n+1})=g(i,C(w_{t-1}),..C_{w_{t-n+1}})$$

$$y=b+Wx+Utanh(d+Hx)$$
$$$$






