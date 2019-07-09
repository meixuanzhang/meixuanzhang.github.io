---
layout: post
title: 读《Normalization》相关论文
date:   2019-01-27
categories: 深度学习
---

**涉及论文**  
《Batch Normalization: Accelerating Deep Network Training by Reducing Internal Covariate Shift》



# Batch Normalization  
训练深度神经网络很复杂，因为每个层的输入分布在训练期间会发生变化，因为前一层的参数会发生变化。这通过要求较低的学习速率和仔细的参数初始化来减慢训练，并且使得训练具有饱和非线性的模型变得非常困难。  

Batch Normalization优势在于使标准化成为模型体系结构的一部分，对每个小批量训练样本进行标准化。Batch Normalization允许我们使用更高的学习速率并且不需要过于担心初始化问题。

SGD(stochastic gradient descent)已经被证明是非常有效训练方式，其通过优化参数$$\theta$$来最小化损失函数：   

$$\theta=\mathop{\arg\max}_{\theta}\frac{1}{N}\sum_{i=1}^{N}l(x_{i},\theta) $$
