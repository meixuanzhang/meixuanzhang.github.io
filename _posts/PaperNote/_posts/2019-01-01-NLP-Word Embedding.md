---
layout: post
title: 读《Word Embedding》相关论文(word2vec、Glove)
date:   2019-01-01
categories: 深度学习
---  

**涉及论文：**  

《Efficient Estimation of Word Representations in Vector Space》  
《Distributed Representations ofWords and Phrases and their Compositionality》  
《Distributed Representations of Sentences and Documents》  
《GloVe: Global Vectors forWord Representation》  

# word2vec模型

word2vec模型优点：训练后单向向量能捕获句法信息和单词语义间关系

word2vector总共有两种类型，分别是CBOW(Continuous Bag-of-Words)、Skip-gram,为了减少计算成本每种类型有两种算法策略,分别是Hierarchical Softmax、Negative Sampling。


CBOW是从窗口文本词推出中心词，如假设窗口大小为5，则“我喜欢吃梨”，“我喜吃梨” $$\to$$ “欢”  
Skip-gram是从中心词推出文本词,如“我喜欢吃梨”，“欢” $$\to$$ “我喜吃梨”  

## CBOW模型架构 

![_config.yml]({{ site.baseurl }}/images/15Word Embedding/image1.png)

Notation: 

V:词汇表  
$$W:$$Embedding matrix,维度$$N*V$$  
$$U:$$Embedding matrix,维度$$V*N$$   
$$k:$$是(窗口大小-1)/2   

假设给定一个训练序列$$w_{1},..w_{T}$$,$$w_{i}$$是onehot行向量，其目标函数为

$$L=\frac{1}{T}\sum_{t=k}^{T-k}logP(w_{t}\mid w_{t-k}...w_{t+k})$$

$$P(w_{t}\mid w_{t-k}...w_{t+k})=\frac{e^{y_{w_{t}}}}{\sum_{j}e^{y_{j}}}$$

$$y=b+Uh(w_{t-k}...w_{t+k};W)$$

y是行向量维度为V  

h输出是$$w_{t-k}...w_{t+k}$$在W Embedding matrix 对应vector的均值，是行向量。 

向量在W对应vector计算： 

![_config.yml]({{ site.baseurl }}/images/15Word Embedding/image5.png)


## Skip-gram模型架构   

Notation: 

V:词汇表  
$$W:$$Embedding matrix,维度$$N*V$$  
$$U:$$Context matrix,维度$$V*N$$   
$$c:$$是(窗口大小-1)/2 

![_config.yml]({{ site.baseurl }}/images/15Word Embedding/image3.png)  

![_config.yml]({{ site.baseurl }}/images/15Word Embedding/image2.png)  

假设给定一个训练序列$$w_{1},..w_{T}$$,$$w_{i}$$是onehot行向量，其目标函数为 

$$
L= \frac{1}{T}\sum_{t=1}^{T}\sum_{-c\le j\le c,j\ne 0}logP(w_{t+j}\mid w_{t})
$$

$$
P(w_{t+j}\mid w_{t})=\frac{e^{y_{w_{t+j}}}}{\sum_{j}e^{y_{j}}}
$$  

$$y=b+Uh(w_{t};W)$$  

y是行向量维度为V  

h输出是$$w_{t}$$在W Embedding matrix对应vector，是行向量。 

## 算法

### Hierarchical Softmax  

1、构建Huffman tree  

根据单词在词汇表出现的频率构建Huffman tree。树需要包含所有在词汇表中出现过的单词。例子(假设词汇表大小是8)： 

按频率高到低对单词进行排序  
{and:14,in:7,today:4,fat:3,potato:3,fridge:2,kangaroo:2,zebra:1}  

将频率最低的两个单词进行合并，并重新排序  
{and:14,in:7,today:4,fat:3,potato:3,(kangaroo,zebra):3,fridge:2} 

将频率最低的两个单词或合并词进行合并，并重新排序  
{and:14,in:7,(kangaroo,zebra,fridge):5,today:4,fat:3,potato:3} 

将频率最低的两个单词或合并词进行合并，并重新排序  
{and:14,in:7,(fat,potato):6,(kangaroo,zebra,fridge):5,today:4} 

以此类推就形成图中所示(单词频率越高，越靠近根部)：  

![_config.yml]({{ site.baseurl }}/images/15Word Embedding/image4.png)  

2、计算$$P(w\mid context(w))$$ 或  $$P(context(w)\mid w)$$  


![_config.yml]({{ site.baseurl }}/images/15Word Embedding/image6.png) 

$$w:$$表示中心词  
$$context(w):$$表示窗口文本  

图中$$X$$是Huffman tree输入向量，当我们求解$$P(w\mid context(w))$$时$$X$$为context(w)在W对应vector的均值，求解$$P(context(w)\mid w)$$时$$X$$为中心词$$w$$ 在W对应vector  



$$l^w$$表示从树开始到达底端字 w 时经历的分叉次数，$$d_{j}^w$$表示在第 j 个分叉处选择，例如上图中足球,经历了4次分叉，$$l^w=4$$,每次选择分别是  
$$\{d_{1}^w:1,d_{2}^w:0,d_{3}^w:0,d_{4}^w:1\}$$ 

树每个节点都有一个$$\theta$$向量参数，$$\theta_{j}^{w}$$表示到达单词 w ,经历的第 j 个分叉处的$$\theta$$向量参数

$$P(w\mid context(w))=\prod_{j=1}^{l^w}P(d_{j}^w\mid X;\theta_{j}^{w})$$  

$$P(context(w) \mid w)=\prod_{u\in context(w)}\prod_{j=1}^{l^u}P(d_{j}^u\mid X;\theta_{j}^{w})$$   

$$P(d_{j}^w\mid X_{w};\theta_{j}^{w})=[\sigma(X^T \theta_{j}^{w})]^{1-d_{j}^w}[1-\sigma(X^T \theta_{j}^{w})]^{d_{j}^w}$$  

3、梯度更新参数$$W,\theta$$   

CBOW损失函数：  

$$
L=\frac{1}{T}\sum_{t=k}^{T-k}logP(w_{t}\mid context(w_{t}))
$$


Skip-gram损失函数：  

$$
L= \frac{1}{T}\sum_{t=1}^{T}logP(context(w) \mid w)
$$

CBOW更新了context(w) 在 W 矩阵对应的向量,以及计算过程中涉及的$$\theta$$   
Skip-gram只更新了中心词 w 在 W 矩阵对应的向量,以及计算过程中涉及的$$\theta$$      
最后求得的 W 矩阵就是单词的distributed representation    

### Negative Sampling 

基础：**Noise contrastive estimation (NCE)**  

假设二分类样本通过以下方式生成，根据$$p(c)$$分布采样，获得一个$$c$$,根据$$\tilde{p}(w \mid c)$$分布采样，获得一个$$w$$，把样本标记为$$D=1$$,根据$$q(w)$$“noise”分布采样，获得$$k$$个$$w$$,把样本标记为$$D=0$$,则：  

$$
p(d,w\mid c)= \left\{ \begin{array}{rl}
& \frac{k}{1+k}*q(w) &if \ d=0\\
& \frac{1}{1+k}*\tilde{p}(w\mid c) &if \ d=1\\
\end{array} \right.
$$  

$$p(d=1,w,c)$$当 d=1 已经确定时，d 与 (w,c) 独立    

$$
p(d=1,w\mid c)=\frac{p(d=1,w,c)}{p(c)}\\
=\frac{p(d=1)p(w,c)}{p(c)}=\frac{p(d=1)p(w\mid c)p(c)}{p(c)}\\
=p(d=1)p(w\mid c)=p(d=1)\tilde{p}(w\mid c)
$$

$$p(w\mid c)$$当 d=0 已经确定时，w 和 c 相互独立   

$$
p(d=0,w\mid c)\\
=p(d=0)p(w\mid c)=p(d=0)q(w)
$$  


因此： 

$$
p(D\mid c,w)=\frac{p(D,w,c)}{p(w,c)}\\
=\frac{\frac{p(D,w,c)}{p(c)}}{\frac{p(w,c)}{p(c)}}\\
=\frac{p(D,w\mid c)}{p(w\mid c)}
$$

$$
p(D=0\mid c,w)=\frac{\frac{k}{1+k}*q(w)}{\frac{1}{1+k}*\tilde{p}(w\mid c)+\frac{k}{1+k}*q(w)}\\
=\frac{k*q(w)}{\tilde{p}(w\mid c)+k*q(w)}
$$


$$
p(D=1\mid c,w)=\frac{\tilde{p}(w\mid c)}{\tilde{p}(w\mid c)+k*q(w)}
$$

损失函数：

$$
L_{NCE_{k}}=\sum_{(w,c)\in D}(logp(D=1\mid c,w)+kE_{\bar{w}\sim q}logp(D=0\mid c,\bar{w}))
$$

使用Monte Carlo approximation则：

$$
L_{NCE_{k}}^{MC}=\sum_{(w,c)\in D}(logp(D=1\mid c,w)+k*\sum_{\bar{w}\sim q}^k \frac{1}{k} logp(D=0\mid c,\bar{w}))\\
=\sum_{(w,c)\in D}(logp(D=1\mid c,w)+\sum_{\bar{w}\sim q}^k logp(D=0\mid c,\bar{w}))
$$

# doc2vec模型
 
# Glove模型  



参考：  
[Learning Word Embedding](https://lilianweng.github.io/lil-log/2017/10/15/learning-word-embedding.html)  
[Hierarchical Softmax](http://building-babylon.net/2017/08/01/hierarchical-softmax/)
[Notes on Noise Contrastive Estimation and Negative Sampling](http://demo.clab.cs.cmu.edu/cdyer/nce_notes.pdf)


