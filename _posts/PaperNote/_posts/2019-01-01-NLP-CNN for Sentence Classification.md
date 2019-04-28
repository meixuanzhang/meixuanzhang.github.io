---
layout: post
title: 读《Convolutionl Neural Networks for Sentence Classification》
date:   2019-01-01
categories: 深度学习
---

# 概述

论文展示将简单CNN模型应用于句子分类问题，模型仅学习除静态词汇向量外(word vector不进行更新)其他参数。模型可以进行fine-tuneing(预训练)学习，在不同分类任务中获得不错效果

# 模型

Notation:    

$$x_{i}\in R^k$$:句子中第i个word vector  
$$X_{1:n}$$:长度为n的句子  
$$X_{i:i+j}$$:词汇向量$$x_{i},x_{i+1}...x_{i+j}$$拼接  
$$\oplus$$:向量拼接符号   
$$W^r\in R^{hk}$$:第r个filter(卷积核),过滤h个词汇   
$$c_{i}^r$$:$$X_{i:i+h-1}$$经过第r个卷积核过滤后向量  


$$X_{1:n}=x_{1}\oplus x_{2}\oplus...\oplusx_{n}$$

$$c_{i}^r=f(W^r\cdot X_{i:i+j}+b)$$ 

$$C^r=[c_{1}^r,c_{2}^r,...,c_{n-h+1}^r]$$  

$$$$

