---
layout: post
title: 《Attention Is All You Need》
date:   2019-02-01
categories:深度学习
---
[Toc]
#概述
论文提出了Transformer网络架构,其完全基于注意力机制(attention mechanisms),免去了RNN和CNN

#模型架构
模型由Encoder和Decoder两大部分组成,按模块可以分为五大模块分别是：Embeddings、(Masked)Multi-Head Atention、Add&Norm、FeedForward、Linear&Softmax


模型输入：$$X_{b*l*}$$
模型输出：Y 

##Encoder
Notation:
Embedding matrix: V  dim()
###Embeddings
###Add&Norm
###
##Decoder

