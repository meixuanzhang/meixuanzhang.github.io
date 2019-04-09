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

## 无Attention机制的MNT：    
图中蓝色是Encoder，红色是Decoder    
NMT使用了recurrent architecture  


## Hard attention&Soft attention  
## Global attention model&Local attention model  
图中蓝色是Encoder，红色是Decoder  
Notation:  
$$\bar{h_{s}}$$:Encoder的隐藏层状态，下标s代表第几个隐藏层状态  
$$\tilde{h_{t}}$$:Deocder的隐藏层状态，下标t代表是t时刻的隐藏层状态  
$$a_{t}$$:是t时间计算隐藏层状态算术平均和的权重  
$$c_{t}$$:隐藏层状态算术平均和
$$D$$:局部关注选取的前后长度
$$p_{t}$$:对其位置，即局部


### Global attention model：  

### Local attention model  


## Key-value Attention Mechanism  
## Self-Attention  
