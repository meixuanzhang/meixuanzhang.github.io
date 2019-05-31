---
layout: post
title: 读《Learned in Translation ContextualizedWord Vectors》
date:   2019-01-25
categories: 深度学习
---  

# 概述  

在计算机视觉中，convolutional neural networks (CNNs)通过在ImageNet(数据集)进行预训练，然后迁移到其他计算机视觉任务中，获得了非常好的效果。  

在NLP下游任务中，使用word2Vec，GloVe获得的词向量比随机初始化词向量更能使任务获得好的效果。词语不是单独出现的，词义与上下文有关。

论文使用deep LSTM encoder(编码器)，获得带有语境的词向量(contextualize word vectors)，编码器是通过训练机器翻译任务attentional sequence-to-sequence model中获得。论文主要关注通过大型NLP任务训练编码器，将编码器迁移到其他任务中(迁移学习)。  

# 模型框架  

Word Vectors 是使用GloVe训练获得的词向量，Encoder是双层双向的LSTM，Decoder是attention+双层单向的LSTM


**Encoder**  

Encoder会根据输入序列输出对应的hidden states

$$
h=MT-LSTM(GloVe(w^x))
$$

**Decoder**  

$$z_{t-1}$$:前一个时刻的target embedding,相当于LSMT中的input vector
$$h_{t}^{dec}$$:当前时刻的隐藏状态，实际相当于LSTM中的Memory state
$$\tilde{h}_{t-1}$$:前一个时刻的context-adjusted hidden state,实际相当于LSTM中Hidden state，但不同的是计算中没有用Output Gate，输入也不只是Memory state   
$$H$$:Encoder输出的隐藏状态序列

[LSTM模型](https://meixuanzhang.github.io/NLP-RNN-LSTM-GRU/)   

当前时刻Decoder输出的hidden state:

$$
h_{t}^{dec}=LSTM([z_{t-1};\tilde{h}_{t-1}],h_{t-1}^{dec})
$$

当前时刻attention权重：  


$$
\alpha_{t}=softmax(H(W_{1}h_{t}^{dec})+b_{1})$$

当前时刻context-adjusted hidden state(与一般LSTM相比省去了Output Gate，同时将attention后的vector与当前时刻Memory state相连):    

$$
\tilde{h}_{t}=tanh(W_{2}[H^T\alpha_{t};h_{t}^{dec}]+b_{2})
$$ 

当前时刻output word的概率分布：  

$$
p(w_{t}^z\mid H,w_{1}^z,...,w_{t-1}^z)=softmax(W_{out}\tilde{h}_{t}+b_{out})
$$


