---
layout: post
title: 读《Convolutionl Neural Networks for Sentence Classification》
date:   2019-01-01
categories: 深度学习(NLP)
---

# 概述

论文展示将简单CNN模型应用于句子分类问题，模型仅学习除静态词汇向量外(word vector不进行更新)其他参数。模型可以进行fine-tuneing(预训练)学习，在不同分类任务中获得不错效果

# 模型 

![_config.yml]({{ site.baseurl }}/images/99CnnForSentenceClassfication/image1.png)

Notation:    

$$x_{i}\in R^k$$:句子中第i个word vector  
$$X_{1:n}$$:长度为n的句子  
$$X_{i:i+j}$$:词汇向量$$x_{i},x_{i+1}...x_{i+j}$$拼接  
$$\oplus$$:向量拼接符号   
$$W^r\in R^{hk}$$:第r个filter(卷积核),过滤h个词汇   
$$c_{i}^r$$:$$X_{i:i+h-1}$$经过第r个卷积核过滤后向量     
$$Z$$：CNN最后提取句子特征向量   

$$X_{1:n}=x_{1}\oplus x_{2}\oplus...\oplus x_{n}$$

f():非线性函数： 

$$c_{i}^r=f(W^r\cdot X_{i:i+j}+b^r)$$  

stride=1,filter将扫过$${x_{1:h},x_{2:h+1},..x_{n-h+1}}$$

$$c^r=[c_{1}^r,c_{2}^r,...,c_{n-h+1}^r]$$  

$$\hat{c}^r=max\{c^r\}$$

m:filter个数：

$$Z=[\hat{c}^1,\hat{c}^2..\hat{c}^m],Z\in R^m$$  


最后一层全连接： 

$$y=W'\cdot Z+b$$   

为了防止过拟合训练时加入regularization：   

$$y=W'\cdot (Z \circ d)+b$$  

$$d\in R^m$$表示dropout，训练时d中每个元素服从贝努力分布以一定概率p取值1，测试时则全部取1.$$\circ$$表示向量元素两两对应相乘  

在损失函数中加入矩阵范数$$\Vert W' \Vert_{2}$$  


测试时则不再使用dropout,同时因为训练时神经元的期望输出是 pZ+(1-p)0=pZ,在测试时需要对$$W'$$进行缩放$$\hat{W}=pW'$$  

$$y=\hat{W} \cdot Z+b$$



