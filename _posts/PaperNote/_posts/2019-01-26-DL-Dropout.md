---
layout: post
title: 读《Dropout A Simple Way to Prevent Neural Networks from Overfitting》
date:   2019-01-27
categories:  深度学习
---

# 摘要  

具有大量参数的深度神经网络是非常强大的机器学习系统。然而，过度拟合是这种网络中的严重问题。通过组合许多不同大型神经网络的预测结果来处理过度拟合，在测试时非常缓慢。   
Dropout是一种解决此问题的技术，其关键的想法是在训练时，随机删除神经网络的神经元（及其连接）。这可以防止神经元间过度协同(co-adapting)。在训练中，Dropout从指数级不同“稀疏”网络中采样，获得不同的网络结构。在测试时，使用缩放权重了的整个神经网络预测，其可近似为平均所有这些 “稀疏” 网络的预测的效果。这显着减少过度拟合，比起其他正则化方法有了重大改进。   
Dropout提高了神经网络在(视觉，语音识别，文档分类和计算生物学等)监督学习任务的表现。

# 背景

对于有限的训练数据，采样噪声(sampling noise抽样误差)会造成输入和输出关系复杂，噪声存在于训练集中但不存在于真实的测试数据中，即使数据从相同的分布中提取。由于训练时深度神经网络学习了输入和输出之间复杂的关系，但真实数据不存在这样复杂关系，就会导致真实数据中模型表现并不好，这就是过拟合（overfitting）。有许多方法可以解决这个问题如：L1 and L2 regularization，soft weight sharing。  
不考虑计算成本最好的方法是固定模型大小下，对模型不同参数设置下预测结果平均，根据给定训练数据的后验概率对每个设置进行加权。


  































参考：  
[What is Sampling Noise?](http://economistjourney.blogspot.com/2018/06/what-is-sampling-noise.html)
