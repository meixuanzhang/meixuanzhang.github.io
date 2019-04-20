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

![_config.yml]({{ site.baseurl }}/images/12Attention/image1.png)



## Hard attention&Soft attention  
## Global attention model&Local attention model  

图中蓝色是Encoder，红色是Decoder  

![_config.yml]({{ site.baseurl }}/images/12Attention/image4.png)

Notation:  
$$\bar{h_{s}}$$:Encoder s时刻的隐藏层状态,$$\bar{H}=(\bar{h_{1}},..\bar{h_{S}})$$  
$$h_{t}$$:Deocder t 时刻的隐藏层状态,$$H=(\bar{h_{1}},..\bar{h_{T}})$$  
$$\tilde{h_{t}}$$:t时刻最后输出的隐藏层  
$$a_{t}$$:是t时刻计算Encoder隐藏层状态算术平均和的权重向量，$$a_{t}(s)$$Encoder s时刻隐藏层的权重    
$$c_{t}$$:Encoder 隐藏层状态算术平均和  
$$E$$:Encoder部分信息   

### Global attention model： 

![_config.yml]({{ site.baseurl }}/images/12Attention/image2.png)


$$a_{t}(s)=align(h_{t},\bar{h_{s}})\\
=\frac{exp(score(h_{t},\bar{h_{s}}))}{\sum_{s'}exp(score(h_{t},\bar{h_{s'}}))}$$

score计算方法： 

$$
score(h_{t},\bar{h_{s}}) = \left\{ \begin{array}{rl}
& h_{t}^{\top}\bar{h_{s}} &\qquad dot\\
& h_{t}^{\top}W_{a}\bar{h_{s}} &\qquad general\\
& v_{a}^{\top}tanh(W_{a}[h_{t};\bar{h_{s}}])  & \qquad concat\\
& W_{a}h_{t} & \qquad location-based\\
\end{array} \right.
$$  

$$c_{t}=\bar{H}a_{t}$$  

$$\tilde{h_{t}}=tanh(W_{c}[c_{t};h_{t}])$$

$$y_{t}=W_{t}\tilde{h_{t}}$$

$$P(y_{t}\mid y_{<t},E)=softmax(y_{t})$$  




### Local attention model:  

![_config.yml]({{ site.baseurl }}/images/12Attention/image3.png)

Notation:  

$$p_{t}$$:Decoder t时刻，对齐Encoder的位置  
$$D$$:1/2窗口大小(选取Encoder部分长度)    
$$S$$:Encoder的长度  

Global attention缺点是Decoder每个时刻需要考虑Encoder序列每个字，计算会随着句子长度增加而增加，如果句子非常长，计算会非常昂贵。因此提出了 Local attention只考虑Encoder序列部分的字，Decoder t时刻，在Encoder选取对齐位置$$p_{t}$$,只考虑Encoder[$$p_{t}-D,p_{t}+D$$]窗口里字。

$$
p_{t}=S \cdot sigmoid(v_{p}^{\top} tanh(W_{p}h_{t}))\\
p_{t} \in [0,S]\\
a_{t}(s) =align(h_{t},\bar{h_{s}})exp(-\frac{(s-p_{t})^2}{2\sigma^2})\\
\sigma =\frac{D}{2},s\in [p_{t}-D,p_{t}+D]
$$

论文将上述对齐方式称为,Predictive alignment(local-p),另一种$$p_{t}=t$$的对齐方式称为Monotonic alignment(local-m)




## Key-value Attention Mechanism  
## Self-Attention  
