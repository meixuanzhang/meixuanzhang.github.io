---
layout: post
title: 读《Attention Is All You Need》
date:   2019-01-24
categories: 深度学习
---
# 概述
论文提出了Transformer网络架构,其完全基于注意力机制(attention mechanisms)，免去了RNN和CNN

# 模型架构
模型由Encoder和Decoder两大部分组成，按模块可以分为五大模块分别是：Embeddings&Positional Encoding、(Masked)Multi-Head Atention、Add&Norm、FeedForward、Linear&Softmax  
下图的N是代表框框里模块重复叠加数  
![_config.yml]({{ site.baseurl }}/images/Attention Is All You Need/image1.jpg)
## Encoder
### Embeddings&Positional Encoding
Notation:  
m:句子的长度  
n:词汇量数  
dmodel:Embedding后字向量的长度  
Input: $$X_{m*n}$$  
Embedding matrix: $$S_{n*d_{model}}$$  
i:向量的第i维  
pos: 字在句子中的位置,第pos个  
由图可知X作为输入首先经过Embeddings，输出为$$A_{m*d_{model}}$$,同时X作为输入经过Positional Encoding,输出为$$B_{m*d_{model}}$$,A+B作为模块的最终输出(C)，注意Positional Encoding 式子中i的取值范围是$$(0 \thicksim d_{model}/2-1)$$，上下两个式子输出的维度是$$m*d_{model}/2$$,需要进行concat
![_config.yml]({{ site.baseurl }}/images/Attention Is All You Need/image2.jpg)  

dmodel取不同值时PE值:  
![_config.yml]({{ site.baseurl }}/images/Attention Is All You Need/image3.png) 

###  Multi-Head Atention
原本$$Q=K=V=C_{m*dmodel}$$  

$$MultiHead(Q,K,V) = Concat(head_{1},...head_{h})W^{o}$$  
$$where\quad head_{i} = Attention(QW^Q_{i},KW^K_{i},VW^V_{i})$$  
下面Q、K、V是经过$$W^Q_{i},W^K_{i},W^V_{i}$$线性变换后的Q、K、V  
Scaled Dot-Dot Product Attention：  
$$Attention(Q,K,V)=softmax(\frac{QK^T}{\sqrt{d_{k}}})V$$  
相关参数的维度$$W^Q_{i}\in R^{d_{model}*d_{k}},W^K_{i}\in R^{d_{model}*d_{k}},W^V_{i}\in R^{d_{model}*d_{v}},W^{o}\in R^{hd_{v}*d_{model}}$$

![_config.yml]({{ site.baseurl }}/images/Attention Is All You Need/image4.jpg)  
PS:源代码实现是对Q、K、V进行了一次线性变换，维度变为m*hiddensize，然后将Q、K、V分成h份,每份维度是$$m*hiddensize/h$$，每份进行Attention,再concat，而不是对其进行h次线性变换  
注意hiddensize/h要能整除  
$$Q_{m*hiddensize}=QW_{Q}$$  
$$K_{m*hiddensize}=KW_{K}$$  
$$V_{m*hiddensize}=VW_{V}$$  

![_config.yml]({{ site.baseurl }}/images/Attention Is All You Need/image9.jpg) 


###  Add&Norm  
Add指的是模块(Masked)Multi-Head Atention、FeedForward输入和输出相加，作为下一个步骤的输入  
Norm指的是，数据按层进行标准化
![_config.yml]({{ site.baseurl }}/images/Attention Is All You Need/image5.jpg)  
###  FeedForward
全连接模块输出和输入会保持相同的维度   
假设输入为$$F_{m*model}$$,则输出为$$G_{m*dmodel}$$  
$$F_{m*dmodel}W_{dmodel*dmodel}=G_{m*dmodel}$$
##  Decoder
Decoder与Encoder区别在于Decoder使用了两个Multi-Head Attention，第一个是带masked,第二个是不带masked，其中第二个的输入K，V等于Encoder的输出
###  第一个Multi-Head Atention
训练时使用的是Masked-Multi-Head Atention  
在t时刻预测下一个字时，不应该出现t时刻后面的字，否则会有信息泄露，因此在训练时加入了masked  
![_config.yml]({{ site.baseurl }}/images/Attention Is All You Need/image6.jpg) 
测试时使用的是Multi-Head Atention  
注意测试时K,V行维度是随着t不断增加的，Q维度则是不变的，模块输出行维度是由Q决定的  
![_config.yml]({{ site.baseurl }}/images/Attention Is All You Need/image7.jpg) 
###  Linear&Softmax 
训练时输出是$$m*n$$    
测试时输出维度是$$1*n$$    

![_config.yml]({{ site.baseurl }}/images/Attention Is All You Need/image8.jpg) 

## 为什么使用Positional Encoding  

$$head_{i} = Attention(QW^Q_{i},KW^K_{i},VW^V_{i})=softmax(\frac{QW^Q_{i}(KW^K_{i})^T}{\sqrt{d_{k}}})VW^V_{i}$$  

没有Positional Encoding情况下图中$$W=W^Q_{i}W^K_{i}^T$$： 

图中可以看到不同顺序句子attention后输出除了顺序变了，关注内容是一致的，也就是说attention没有捕捉到句子顺序信息。

![_config.yml]({{ site.baseurl }}/images/Attention Is All You Need/image10.png)  

![_config.yml]({{ site.baseurl }}/images/Attention Is All You Need/image11.png)  

加入Positional Encoding情况下：

![_config.yml]({{ site.baseurl }}/images/Attention Is All You Need/image12.png) 

