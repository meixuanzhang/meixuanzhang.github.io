---
layout: post
title: 读《Attention》相关论文
date:   2019-01-01
categories: 深度学习
---
# 概述  
文中涉及论文包括:    
《Effective Approaches to Attention-based Neural Machine Translation》(Global&Local)  
《Key-value Attention Mechanism for Neural Machine Translation》  
《A STRUCTURED SELF - ATTENTIVE SENTENCE EMBEDDING》  
《Hierarchical Attention Network for Documnet Classification》  
《Attention over Attention Neural Netwarks for Reading Comprehension》  
《Show, Attend and Tell: Neural Image Caption Generation with Visual Attention》(Soft&Hard)  
以上论文提到了不同的Attention机制  

## 无Attention机制的NMT( Neural Machine Translation)：    
图中蓝色是Encoder，红色是Decoder    
NMT使用了recurrent architecture

Notation:  
Encoder 句子$$x=\{x_{1},..x_{n}\}$$    
Decoder 目标输出$$y=\{y_{1}...y_{m}\}$$       
$$h_{t}$$:Deocder t 时刻最后的隐藏层状态
$$W_{t}$$:参数   
D:数据集  

$$Y_{t}=softmax(W_{t}h_{t})$$  

$$P(y_{t}\mid y_{<t},x)\sim Y_{t}$$   

$$logP(y\mid x)=\sum_{t=1}^m logP(y_{t}\mid y_{<t},x)$$   

损失函数：

$$J=\sum_{(x,y)\in D}-logP(y\mid x)$$

![_config.yml]({{ site.baseurl }}/images/12Attention/image1.png)

## Global attention model&Local attention model  

图中蓝色是Encoder，红色是Decoder    

Notation:  
$$\bar{h_{s}}$$:Encoder s时刻的隐藏层状态,$$\bar{H}=(\bar{h_{1}},..\bar{h_{S}})$$  
$$h_{t}$$:Deocder t 时刻最后的隐藏层前一层,$$H=(h_{1},..h_{T})$$  
$$\tilde{h_{t}}$$:t时刻加入attention后最后输出的隐藏层  
$$a_{t}$$:是t时刻计算Encoder隐藏层状态算术平均和的权重向量，$$a_{t}(s)$$Encoder s时刻隐藏层的权重    
$$c_{t}$$:Encoder 隐藏层状态算术平均和  


![_config.yml]({{ site.baseurl }}/images/12Attention/image4.png)



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
\end{array} \right.
$$  

或：

$$a_{t}=softmax( W_{a}h_{t} ) \qquad location-based$$   ($$a_{t}$$是向量)

$$c_{t}=\bar{H}a_{t}$$  

$$\tilde{h_{t}}=tanh(W_{c}[c_{t};h_{t}])$$

$$Y_{t}=softmax(W_{t}\tilde{h_{t}})$$

$$P(y_{t}\mid y_{<t},x)\sim Y_{t}$$

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


## Hard attention&Soft attention  
论文《Show, Attend and Tell: Neural Image Caption Generation with Visual Attention》提出了Stochastic“Hard”和Deterministic"Soft"Attention
应用在Image Caption Generation (根据图像自动生成标题)任务。

模型主要框架：图片通过CNN提出特征作为Encoder，使用含有attention机制的RNN生成句子。

![_config.yml]({{ site.baseurl }}/images/12Attention/image5.png)

Decoder框架(论文中使用了LSTM模型)：

![_config.yml]({{ site.baseurl }}/images/12Attention/image6.png)

Notation:  

y:目标输出,$$y=\{y_{1}...y_{C}\},y_{i}\in R^K$$，y_{i}是one-hot向量   
a:image提取的特征，$$a=\{a_{1}...a_{L}\},a_{i}\in R^D$$   
$$\alpha_{ti}$$:t时刻image提取特征$$a_{i}$$对应的权重
$$h_{t}$$:Decoder t时刻的隐藏层  
$$y_{t}$$:t时刻的目标输出  
$$z_{t}$$:attention抓取的Encoder特征
E:embedding 矩阵
$$f_{att},f_{init,c},f_{init,h}:$$多层感知机MLP

LSTM的三个门和Candidate layer（相比没有attention的LSTM增加了$$z_{t}$$部分）：       

$$
f_{t}=\sigma(U_{f}Ey_{t-1}+W_{f}h_{t-1}+Z_{f}z_{t})\\
I_{t}=\sigma(U_{i}Ey_{t-1}+W_{i}h_{t-1}+Z_{i}z_{t})\\
O_{t}=\sigma(U_{o}Ey_{t-1}+W_{o}h_{t-1}+Z_{o}z_{t})\\
\bar{C}_{t}=tanh(U_{c}Ey_{t-1}+W_{c}h_{t-1}+Z_{c}z_{t})\\
$$  

$$
\alpha_{ti}=\frac{exp(f_{att}(a_{i},h_{t-1}))}{\sum_{i'=1}^L exp(f_{att}(a_{i'},h_{t-1}))}\\
z_{t}=\phi(\{a_{i}\},\{\alpha_{i}\})
$$

$$\phi$$函数在后面介绍  

LSTM的Memory state和Hidden stte:   

$$
C_{t} =f_{t}\cdot C_{t-1}+I_{t}\cdot \bar{C}_{t}\\
h_{t} = O_{t}\cdot tanh(C_{t})\\
$$

output:   

$$
Y_{t} = softmax(L_{o}(Ey_{t-1}+L_{h}h_{t}+L_{z}z_{t}))\\
P(y_{t}\mid a,y_{<t})\sim Y_{t}\\
L_{o}\in R^{K*m},L_{h}\in R^{m*n},L_{z}\in R^{m*D}
$$

###Stochastic “Hard” Attention  

Notation:  
$$s_{t}$$:是t时刻维度为L的one-hot向量，$$s_{t,i}=1$$表示$$s_{t}$$向量索引i元素等于1，其他为0，代表了选取$$a_{i}$$特征

$$
P(s_{t,i}=1\mid s_{<t},a)=\alpha_{ti}\\
z_{t}=\sum_{i}s_{t,i}a_{i}
$$  

$$z_{t}$$是一个随机变量根据$$\alpha_{t}$$分布随机选取 对应的$$a_{i}$$

###Deterministic “Soft” Attention  

$$E_{p(s_{t}\mid a)}=\sum_{i=1}^L \alpha_{ti}a_{i}$$

