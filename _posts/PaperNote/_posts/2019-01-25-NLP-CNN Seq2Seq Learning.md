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

input(输入)长度为m的句子:$$x=(x_{1},..x_{m}),x_{j}$$是one-hot vector 维度是V，实际中m是句子最大长度，如果句子长度小于m则需要在句子后面补零向量。     

input embedding matrix： $$D\in R^{V*f}$$    

embedding input: $$W=(w_{1}....w_{m}),w_{j}\in R^f$$  W=XD   

position :$$\hat(p)=(\hat(p)_{1}...\hat(p)_{m}),\hat(p)_{1}$$是one-hot vector,维度是L   

position embedding matrix： $$D'\in R^{L*f}$$    

embedding Position: $$p=(p_{1}....p_{m}),p_{j}\in R^f$$    

CNN输入：$$e=(w_{1}+p_{1}+,...,w_{m}+p_{m})$$   



**GLU(gated linear units)**  

模型采样GLU做为gate mechanism,类似于LSTM，GRU门机制作用。    
$$A,B \in R^{d}是向量,$$\otimes$$对应元素两两相乘:

$$Y=v([A B])=A\otimes \sigma(B)\\
v([A B])\in R^d$$  

**Encoder**  

图片中只展示了一层CNN下模型，实际模型中采用了层叠CNN： 

$$W^l\in R^{2f*kf},b_{w}^l \in R^{2f}$$:l层的卷积,一共有2d个卷积核，每个卷积核大小是$$k*d$$ , $$b_{w}^l$$是bias    

层叠CNN第l层输出为$$z_{l} \in R^{m*f}$$，其第i维为： 

$$z_{i}^l=v(W^l[z_{i-k/2},...,z_{i+k/2}+z_{w}^l]+b_{w}^l)+z_{i}^{l-1}\\
z_{i}^l \in R^f$$     

Encoder层叠CNN最后一层第j维输出为$$z_{j}^u\in R^f$$  

CNN每层的输出向量的维度都需要与输入的维度一致，都是$$m*f$$维，因此需要在开头和结尾加入padding:

$$p=((m-1)*s-m+k)/2$$

m句子的长度，k是窗口大小，p是单侧padding大小，s是stride

