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


CBOW是从窗口文本词推出中心词，如“我喜欢吃梨”，“我喜吃梨” $$\to$$ “梨”  
Skip-gram是从中心词推出文本词,如“我喜欢吃梨”，“梨” $$\to$$ “我喜吃梨”  

## CBOW模型架构 

![_config.yml]({{ site.baseurl }}/images/15Word Embedding/image1.png)

Notation: 

V:词汇表  
$$W:$$Embedding matrix,维度$$N*V$$  
$$U:$$Embedding matrix,维度$$V*N$$   
$$k:$$是窗口大小   

假设给定一个训练序列$$w_{1},..w_{T}$$,$$w_{i}$$是行向量，其目标函数为

$$L=\frac{1}{T}\sum_{t=k}^{T-k}logP(w_{t}\mid w_{t-k}...w_{t+k})$$

$$P(w_{t}\mid w_{t-k}...w_{t+k})=\frac{e^{y_{w_{t}}}}{\sum_{j}e^{y_{j}}}$$

$$y=b+Uh(w_{t-k}...w_{t+k};W)$$

y是行向量维度为V  

h输出是$$w_{t-k}...w_{t+k}$$在W对应vector的均值，是行向量。 


## Skip-gram模型架构   

Notation: 

V:词汇表  
$$W:$$Embedding matrix,维度$$N*V$$  
$$U:$$Context matrix,维度$$V*N$$   
$$c:$$是窗口大小   

![_config.yml]({{ site.baseurl }}/images/15Word Embedding/image3.png)  

![_config.yml]({{ site.baseurl }}/images/15Word Embedding/image2.png)  

假设给定一个训练序列$$w_{1},..w_{T}$$,$$w_{i}$$是行向量，其目标函数为 

$$
L= \frac{1}{T}\sum_{t=1}^{T}\sum_{-c\le j\le c,j\ne 0}logP(w_{t+j}\mid w_{t})
$$

$$
P(w_{t+j}\mid w_{t})=\frac{e^{y_{w_{t+j}}}}{\sum_{j}e^{y_{j}}}
$$  

$$y=b+Uh(w_{t};W)$$  

y是行向量维度为V  

h输出是$$w_{t}$$在W对应vector，是行向量。 

## 算法

### Hierarchical Softmax  

1、构建Huffman tree  

根据窗口单词在词汇表出现的频率构建Huffman tree。例子： 

按频率高到低对单词进行排序{and:14,in:7,today:4,fat:3,potato:3,fridge:2,kangaroo:2,zebra:1}  

将频率最低的两个单词进行合并，并重新排序{and:14,in:7,today:4,fat:3,potato:3,(kangaroo,zebra):3,fridge:2} 

将频率最低的两个单词或合并词进行合并，并重新排序{and:14,in:7,(kangaroo,zebra,fridge):5,today:4,fat:3,potato:3} 

将频率最低的两个单词或合并词进行合并，并重新排序{and:14,in:7,(fat,potato):6,(kangaroo,zebra,fridge):5,today:4} 

以此类推就形成图中所示：  

![_config.yml]({{ site.baseurl }}/images/15Word Embedding/image4.png)  

2、


### Negative Sampling 

# doc2vec模型

# Glove模型  



参考：  
[Learning Word Embedding](https://lilianweng.github.io/lil-log/2017/10/15/learning-word-embedding.html)  
[Hierarchical Softmax](http://building-babylon.net/2017/08/01/hierarchical-softmax/)


