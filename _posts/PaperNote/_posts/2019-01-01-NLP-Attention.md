---
layout: post
title: 读《Attention》相关论文
date:   2019-01-01
categories: 深度学习
---
# 概述  
文中涉及论文包括:    
《Effective Approaches to Attention-based Neural Machine Translation》  
《Key-value Attention Mechanism for Neural Machine Translation》  
《A STRUCTURED SELF - ATTENTIVE SENTENCE EMBEDDING》  
《Hierarchical Attention Network for Documnet Classification》  
《Attention over Attention Neural Netwarks for Reading Comprehension》  
以上论文提到了不同的Attention机制  

## 无Attention机制的NMT( Neural Machine Translation)：    
图中蓝色是Encoder，红色是Decoder    
NMT使用了recurrent architecture:




## Hard attention&Soft attention  
## Global attention model&Local attention model  
图中蓝色是Encoder，红色是Decoder  
Notation:  
$$\bar{h_{s}}$$:Encoder s时刻的隐藏层状态,$$\bar{H}=(\bar{h_{1}},..\bar{h_{S}})$$  
$$h_{t}$$:Deocder t 时刻的隐藏层状态,$$H=(\bar{h_{1}},..\bar{h_{T}})$$  
$$\tilde{h_{t}}$$:t时刻最后输出的隐藏层  
$$a_{t}$$:是t时刻计算Encoder隐藏层状态算术平均和的权重向量，$$a_{t}(s)$$Encoder s时刻隐藏层的权重    
$$c_{t}$$:Encoder 隐藏层状态算术平均和  
$$E$$:Encoder部分信息
$$D$$:局部关注选取的前后长度  
$$p_{t}$$:对其位置，即局部   


### Global attention model： 

$$a_{t}(s)=align(h_{t},\bar{h_{s}})\\
=\frac{exp(score(h_{t},\bar{h_{s}}))}{\sum_{s'}exp(score(h_{t},\bar{h_{s'}}))}$$

score计算方法： 

$$
score(h_{t},\bar{h_{s}}) = \left\{ \begin{array}{rl}
& h_{t}^T\bar{h_{s}} &\qquad dot\\
& h_{t}^TW_{a}\bar{h_{s}} &\qquad general\\
& v_{a}^Ttanh(W_{a}[h_{t};\bar{h_{s}}])  & \qquad concat\\
& W_{a}h_{t} & \qquad location-based\\
\end{array} \right.
$$  

$$c_{t}=\bar{H}a_{t}$$  

$$\tilde{h_{t}}=tanh(W_{c}[c_{t};h_{t}])$$

$$y_{t}=W_{t}\tilde{h_{t}}$$

$$P(y_{t}\mid y_{<t},E)=softmax(y_{t})$$

### Local attention model  


## Key-value Attention Mechanism  
## Self-Attention  
