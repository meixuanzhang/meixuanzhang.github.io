---
layout: post
title: 读《Convolutional Sequence to Sequence Learning》
date:   2019-01-25
categories: 深度学习
---

# 概述

论文提出了由CNN构成的Seq2Seq模型，相比由RNN构成的Seq2Seq模型效果更好并且可以进行并行运算。

# 模型结构  

![_config.yml]({{ site.baseurl }}/images/80CNNSeq2SeqLearning/image1.png)

**1、Position Embeddings**   

input(输入)长度为m的句子:$$x=(x_{1},..x_{m}),x_{j}$$是one-hot vector 维度是V，实际中m是句子最大长度，如果句子长度小于m则需要在句子后面补零向量。     

input embedding matrix： $$D\in R^{V*f}$$    

embedding input: $$W=(w_{1}....w_{m}),w_{j}\in R^f$$  W=XD   

position :$$\hat(p)=(\hat{p}_{1}...\hat{p}_{m}),\hat{p}_{1}$$是one-hot vector,维度是L   

position embedding matrix： $$D'\in R^{L*f}$$    

embedding Position: $$p=(p_{1}....p_{m}),p_{j}\in R^f$$    

CNN输入：$$e=(w_{1}+p_{1}+,...,w_{m}+p_{m})$$   



**2、GLU(gated linear units)**  

模型采样GLU做为gate mechanism,类似于LSTM，GRU门机制作用。    
$$A,B \in R^{d}$$是向量,$$\otimes$$对应元素两两相乘:

$$Y=v([A B])=A\otimes \sigma(B)\\
v([A B])\in R^d$$  

**3、Encoder**  

图片中只展示了一层CNN下模型，实际模型中采用了层叠CNN： 

$$W^l\in R^{2f*kf},b_{w}^l \in R^{2f}$$表示第l层的卷积,一共有2f个卷积核，每个卷积核大小是$$k*f$$ , $$b_{w}^l$$是bias    

假设卷积步长stride=1

层叠CNN第l层encoder state输出为$$z^{l}=(z_{1}^l..z_{m}^l) z_{i}^l\in R^f$$,元素$$z_{i}^l$$为：  

$$z_{i}^l=v(W^l[z^{l-1}_{i:i+k}]+b_{w}^{l-1})+z_{i}^{l-1}$$     

Encoder层叠CNN最后一层encoder state输出第j个元素为$$z_{j}^u\in R^f$$  

CNN每层的encoder state输出向量的维度都需要与输入的维度一致，都是$$m*f$$维，因此需要在开头和结尾加入padding:

$$p=((m-1)*s-m+k)/2\\
=(k-1)/2,when \ s=1$$

m句子的长度，k卷积核过滤词汇窗口的大小，p是单侧padding大小，s是stride大小    

Encoder最终输出的第i元素为:$$z_{j}^u+e_{j}$$


**4、Decoder**   

Decoder采用了核Encoder相同的卷积结构，但是同时加入了attention机制    

Decoder第l层的i时刻decoder state输出为$$h_{i}^l$$，i-1时刻目标输出为 $$g_{i}$$   

$$d_{i}^l=W_{d}^lh_{i}^l+b_{d}^l+g_{i}$$   

计算i时刻attention概率分布：  

$$\alpha_{ij}^l=\frac{exp(d_{i}^l\cdot z_{j}^u)}{\sum_{t=1}^m exp(d_{i}^l\cdot z_{t}^u)}$$   

$$c_{i}^l=\sum_{j=1}^m\alpha_{ij}^l(z_{j}^u+e_{j})$$   

$$z_{j}^u$$可以看作是key,$$z_{j}^u+e_{j}$$可以看作是value(《Key-value Attention Mechanism for Neural Machine Translation》)   

$$h_{i}^l=v(W^l[h^{l-1}_{i:i+k}]+b_{w}^{l-1})+h_{i}^{l-1}+c_{i}^l$$   

Decoder最后一层输出为$$h^L$$

$$y_{t}=softmax(W_{o}h_{i}^L+b_{o})$$  


由于训练时候会将目标g(整个句子)全部作为输入，存在问题是当预测i时刻输出时，会受到i时刻后面词汇影响，出现信息泄露问题，为此对长度为m的句子在开头和结尾加入padding,假设单侧padding长度为n-1,删除当前层CNN输出末尾n个state。如图所示n=3：  

![_config.yml]({{ site.baseurl }}/images/80CNNSeq2SeqLearning/image2.png)


参考：  
[Understanding incremental decoding in fairseq](http://www.telesens.co/2019/04/21/understanding-incremental-decoding-in-fairseq/)






