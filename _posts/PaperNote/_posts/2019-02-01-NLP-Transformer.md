---
layout: post
title: 读《Attention Is All You Need》
date:   2019-01-24
categories: 深度学习
---
## 概述
论文提出了Transformer网络架构,其完全基于注意力机制(attention mechanisms),免去了RNN和CNN

## 模型架构
模型由Encoder和Decoder两大部分组成,按模块可以分为五大模块分别是：Embeddings、(Masked)Multi-Head Atention、Add&Norm、FeedForward、Linear&Softmax
![_config.yml]({{ site.baseurl }}/images/Attention Is All You Need/image1.jpg)
### Encoder
#### Embeddings
Notation:
m:字的个数或句子的长度
n:词汇量数
dmodel:Embedding后字向量的长度
Input: $$X_{m*n}$$
Embedding matrix: $$V_{n*dmodel}$$ 

### Embeddings
### Add&Norm
###
## Decoder

