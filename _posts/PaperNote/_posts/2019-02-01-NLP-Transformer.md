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
由图可知X作为输入首先经过Embeddings,输出为$$A_{m*dmodel}$$,同时X作为输入经过Positional Encoding,输出为$$B_{m*dmodel}$$,A+B作为模块的最终输出,注意Positional Encoding 式子中i的取值范围是(0~dmodel/2-1)
![_config.yml]({{ site.baseurl }}/images/Attention Is All You Need/image2.jpg)  
dmodel取不同值时PE值:  
![_config.yml]({{ site.baseurl }}/images/Attention Is All You Need/image3.png) 
###  Multi-Head Atention

$$MultiHead(Q,K,V) = Concat(head_{1},...head_{h})W^{o}$$
$$where head_{i} = Attention(QW^Q_{i},KW^K_{i},VW^V_{i})$$
![_config.yml]({{ site.baseurl }}/images/Attention Is All You Need/image4.jpg)  
###  Add&Norm  
ADD指的是模块(Masked)Multi-Head Atention、FeedForward输入和输出相加，作为下一个步骤的输入  
Norm指的是，在模型中数据按层进行标准化
![_config.yml]({{ site.baseurl }}/images/Attention Is All You Need/image5.jpg)  
###  FeedForward
全连接模块输出和输入会保持相同的维度   
假设输入为$$F_{m*model}$$,则输出为$$G_{dmodel}$$
$$F_{m*dmodel}}W_{dmodel*dmodel}=G_{m*dmodel}$$
##  Decoder
Decoder与Encoder有区别的地方主要是Multi-Head Attention
###  Multi-Head Atention
训练时是
###  Linear&Softmax 

