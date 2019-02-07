---
layout: post
title: 读《Attention Is All You Need》
date:   2019-01-24
categories: 深度学习
---
# 概述
论文提出了Transformer网络架构,其完全基于注意力机制(attention mechanisms),免去了RNN和CNN

# 模型架构
模型由Encoder和Decoder两大部分组成,按模块可以分为五大模块分别是：Embeddings&Positional Encoding、(Masked)Multi-Head Atention、Add&Norm、FeedForward、Linear&Softmax  

![_config.yml]({{ site.baseurl }}/images/Attention Is All You Need/image1.jpg)
## Encoder
### Embeddings&Positional Encoding
Notation:  
m:句子的长度  
n:词汇量数  
dmodel:Embedding后字向量的长度  
Input: $$X_{m*n}$$  
Embedding matrix: $$V_{n*dmodel}$$
i:向量的第i维  
pos: 字在句子中的位置,第pos个
由于图可知X作为输入首先经过Embeddings,输出为$$A_{m*dmodel}$$,同时X作为输入经过Positional Encoding,输出为$$B_{m*dmodel}$$,A+B作为模块的最终输出,注意Positional Encoding 式子中i的取值范围是(0~dmodel/2)
![_config.yml]({{ site.baseurl }}/images/Attention Is All You Need/image2.jpg)  

### Add&Norm
###
## Decoder

