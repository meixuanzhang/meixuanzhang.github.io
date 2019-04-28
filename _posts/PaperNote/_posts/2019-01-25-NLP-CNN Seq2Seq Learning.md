---
layout: post
title: 读《Convolutional Sequence to Sequence Learning》
date:   2019-01-25
categories: 深度学习
---

# 概述

论文提出了由CNN构成的Seq2Seq模型，相比由RNN构成的Seq2Seq模型效果更好并且可以进行并行运算。

# 模型结构  

**1、Position Embeddings**   

input(输入)长度为m的句子:$$x=(x_{1},..x_{m}),x_{j}$$是one-hot vector 维度是V   

input embedding matrix： $$D\in R^{V*f}}$$    

embedding input: $$W=(w_{1}....w_{m}),w_{j}\in R^f$$  W=XD   

position :$$\hat(p)=(\hat(p)_{1}...\hat(p)_{m}),\hat(p)_{1}$$是one-hot vector,维度是L   

position embedding matrix： $$D'\in R^{L*f}}$$    

embedding Position: $$p=(p_{1}....p_{m}),p_{j}\in R^f$$    

CNN输入：$$e=(w_{1}+p_{1}+,...,w_{m}+p_{m})$$   

图片中只展示了一层CNN下模型：

**GLU(gated linear units)**  

$$A,B \in R^{d}是向量,$$\otimes$$对应元素两两相乘:

$$Y=v([A B])=A\otimes \sigma(B)\\
v([A B])\in R^d$$  



**Encoder** 

$$W^l\in R^{2d*kd},b_{w}^l \in R^{2d}$$:l层的卷积,一共有2d个卷积核，每个卷积核大小是$$k*d$$,$$b_{w}^l$$是bias  



