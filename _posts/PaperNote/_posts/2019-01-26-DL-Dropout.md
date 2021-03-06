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

不考虑计算成本最好的方法是固定模型大小下，对模型不同参数设置下预测结果平均，根据给定训练数据的后验概率对每个设置进行加权。 论文通过近似等加权几何平均指数级架构个共享参数的模型预测来做到这一点。    

模型组合能提升机器学习的表现，但平均多个分别训练的网络输出计算成本非常高，Dropout是一种解决这两个问题的技术，其防止过拟合同时提供了一种近似组合指数多种不同神经网络架构的有效方法。   

**模型提出动机**   

在生物学中，共适应(co-adaptation)是指两个或两个以上的物种、基因或表型性状作为一对或一组进行适应的过程。   
适合度(fitness)：生物体或生物群体对环境适应的量化特征。   

有性繁殖通过将父母双方各一半的基因以及少量的随机突变进行组合产生后代。无性繁殖是拷贝带有稍许突变的父代基因产生后代。无性繁殖似乎是一种更好的方法来优化个体的适合度(fitness)，因为一组很好的基因可以直接传递给后代。另一方面，有性繁殖可能会破坏这些共适应集合里的基因，如果这些集合很大，直观地说这会降低已经进化出复杂共适应的生物体的适合度(fitness)。然而，有性繁殖是大多数先进生物进化的方式。   

对有性繁殖优越性的一种可能解释是，从长远来看，自然选择的标准可能不是个体适应性(fitness)，而是基因的混合能力。 一组基因能够与另一组随机基因良好协作的能力使它们更加健壮。 由于基因不能依赖其合作伙伴在任何时候出现，它必须学会自己做一些有用的事情或与其他少数基因合作。 

根据这一理论，有性繁殖的作用不仅仅是让有用的新基因在整个种群中传播，而且还通过减少复杂的共适应来促进这一过程，共适应会降低新基因改善个体适合度的机会。 类似地，受过dropout训练的神经网络中的,每个隐藏单元必须学会与其他随机选择的隐藏单元一起工作，这使每个隐藏单元更加健壮，并推动其自行创建有用的特征，而不依赖于其他隐藏单元来纠正其错误。 无论如何，单层中的隐藏单元彼此间会学会做不同的事情。   


# 模型结构  

Notation:  
$$z^{l+1}$$:神经网络$$l+1$$层的输入   
$$y^{l+1}$$:$$l+1$$层的输出(当$$y^{0}=x$$,是神经网络输入)    
$$y_{i}^{l+1}$$:$$l+1$$层第i个神经元的输出  
$$W^{l+1},b^{l+1}$$:神经网络$$l+1$$层的权重和偏差     


![_config.yml]({{ site.baseurl }}/images/81Dropout/image1.png)  
![_config.yml]({{ site.baseurl }}/images/81Dropout/image2.png)   
![_config.yml]({{ site.baseurl }}/images/81Dropout/image3.png)  


$$z_{i}^{l+1}=w_{i}^{l+1}y_{l}+b_{i}^{l+1}\\
y_{i}^{l+1}=f(z_{i}^{l+1})$$ 

$$f$$是激活函数：  

$$f(x)=1/(1+exp(-x))$$ 

$$r_{j}\sim Bernoulli(p)\\
\tilde{y}^l=r^l*y^l\\
z_{i}^{l+1}=w_{i}^{l+1}\tilde{y}^l+b_{i}^{l+1}\\
y_{i}^{l+1}=f(z_{i}^{l+1})$$  

测试时：

$$W_{test}^l=pW^l$$  

因为训练时每个神经元输出期望为$$E(y)=py+(1-p)0$$

# Backpropagation  

训练采用的是stochastic gradient descent 方式，同时使用momentum,annealed learning rates 和L2 weight decay提升训练效果，其中一个被证实有效的正则化方法是max-norm regularization,对于每个神经元对应的向量$$w$$,当$$\parallel w \parallel_{2}<c$$时才进行乘法，$$c$$是常数参数，需要通过验证集设置。   

# unsupersived pretraining  

Neural networks can be pretrained using stacks of RBMs (Hinton and Salakhutdinov, 2006), autoencoders (Vincent et al., 2010) or Deep Boltzmann Machines (Salakhutdinov and Hinton, 2009).   

假设预训练权重为$$\tilde{w}$$,目标任务训练权重为$$w$$，因为dropout,权重期望为$$wp$$,因此$$w=\frac{1}{p} \tilde{w}$$,才能保证预训练权重与目标训练权重期望一致，当测试时$$w_{test}=pw=\tilde{w}$$。   

(未完待续)


















参考：  
[What is Sampling Noise?](http://economistjourney.blogspot.com/2018/06/what-is-sampling-noise.html)
