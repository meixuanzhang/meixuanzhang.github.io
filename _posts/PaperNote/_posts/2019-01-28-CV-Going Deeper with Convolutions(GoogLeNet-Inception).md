---
layout: post
title: 读《Going Deeper with Convolutions》(GoogLeNet-Inception)
date:   2019-01-28
categories: 深度学习
---  

# 概述  

随着移动和嵌入式设备的推动，算法的效率是很重要的——尤其是它们的电力和内存使用。正是包含了这个因素的考虑才得出了本文中呈现的深度架构设计，而不是单纯的为了提高准确率。通过精心的手工设计，在增加了网络深度和广度的同时保持了计算预算不变。为了优化质量，架构的设计以赫布理论和处理多尺度直觉为基础。   

文中使用了一个高效的计算机视觉深度神经网络架构，名为Inception。  

受灵长类视觉皮层神经科学模型的启发，[Serre](https://mcgovern.mit.edu/wp-content/uploads/2019/01/04069258.pdf)等人使用了一系列固定的不同大小的Gabor滤波器来处理多尺度。文中使用了类似的策略。然而，与[Serre](https://mcgovern.mit.edu/wp-content/uploads/2019/01/04069258.pdf)固定的2层深度模型相反，Inception结构中所有的滤波器是学习到的。此外，Inception层重复了很多次，在GoogLeNet模型中得到了一个22层的深度模型。


# 动机和思考  

提高深度神经网络性能最直接的方式是增加它们的尺寸。这不仅包括增加深度(网络层次的数目)也包括它的宽度(每一层的神经元数目)。这是一种训练更高质量模型容易且安全的方法，尤其是在可获得大量标注的训练数据的情况下。但是这个简单方案有两个主要的缺点： 

1、更大的尺寸通常意味着更多的参数，这会使增大的网络更容易过拟合，尤其是在训练集的标注样本有限的情况下。这是一个主要的瓶颈，因为要获得强标注数据集费时费力且代价昂贵，经常需要专家评委在各种细粒度的视觉类别进行区分。  

2、另一个缺点是计算资源使用的显著增加。例如，在一个深度视觉网络中，如果两个卷积层相连，它们的滤波器数目的任何均匀增加都会引起计算量平方式的增加。如果增加的能力在使用时效率低下（例如大多数权重结束时接近于0），那么会浪费大量的计算能力。由于计算预算总是有限的，即使主要目标是提高性能质量，也要有效分配计算资源，而不是随意增加大小。 

解决这两个问题的一个基本方法是引入稀疏性(Sparsity means most of the weights are 0. This can lead to an increase in space and time efficiency.)，将全连接层替换为稀疏连接结构，甚至在卷积层内部也这样。由于[Arora](https://arxiv.org/abs/1310.6343)等人的开创性工作，这具有更坚固的理论基础。他们成果说明如果数据集的概率分布可以通过一个大型稀疏的深度神经网络表示，则最优网络拓扑可以通过对前一层激活值相关性分析，将输出具有高度相关的神经元进行聚类来逐层的构建。这个成果说明与赫布理论的想法类似，一个很通俗的现象，先摇铃铛，之后给一只狗喂食，久而久之，狗听到铃铛就会口水连连。这也就是狗的“听到”铃铛的神经元与“控制”流口水的神经元之间的链接被加强了，而Hebbian principle的精确表达就是如果两个神经元常常同时产生动作电位，或者说同时激动（fire），这两个神经元之间的连接就会变强，反之则变弱（neurons that fire together, wire together）

在实现方面，因为大多数硬件针对密集矩阵的计算进行了优化，所以在完全连接变为稀疏连接之后，实际的计算量不会得到实质性的改善。尽管稀疏矩阵的数据量很小，但是很难减少计算时间。

那么，需要一种方法既可以保持网络结构的稀疏性，又可以利用密集矩阵的高计算性能。   

稀疏连接有两种方法：

一种是 空间（spatial）维度的稀疏连接，也就是传统的CNN卷积结构,共享参数降低了总参数的数目,减少了计算量；  

另一种是在 特征（feature）维度进行稀疏连接，在多个不同的尺寸上进行卷积再聚合，把相关性强的特征聚集到一起，每一种尺寸的卷积只占输出特征中的一部分。



Inception体系结构最初是作为评估复杂网络拓扑构造算法的假设输出的一个案例研究，Inception试图通过密集的，易于获得的组件覆盖假设输出来近似视觉网络所隐含的稀疏结构。


# Architectural Details   

Inception架构的主要想法是考虑如何通过容易获得的密集组件(dense network中常见的组件，比如卷积、全连接等)逼近和覆盖卷积视觉网络的最佳局部稀疏结构。我们所需要的只是找到最佳的局部构造并在空间上进行重复。Arora等人提出了一个层次结构，分析某层输出的相关性并根据相关性对输出聚类得到clusters。这些clusters会构成下一层的神经元，同时与前一层中的神经元相连。

我们假设来自先前层的每个神经元(经过卷积、pooling得到的神经元)对应于输入图像的某个区域，并且这些神经元被分组到滤波器组中。在较低的层（靠近输入层）,相关的神经元集中在局部区域,。 聚类得到的clusters会集中在单个区域（单个位置）。因此，这些units可以被下一层的1*1卷积覆盖，得到下一层的clusters，也可能被更大的卷积覆盖，更大的卷积得到对应较大图像patches的clusters，但数量会相对较少，为了避免 patch-alignment问题目前Inception架构形式的滤波器的尺寸仅限于1×1、3×3、5×5，这个决定更多的是基于便易性而不是必要性。

Inception Module
The 1×1 Convolution

Global Average Pooling

![_config.yml]({{ site.baseurl }}/images/103GoogleNet/image1.png)   


参考：

[论文导读：GoogLeNet模型，Inception结构网络简化（Going deeper with convolutions）](https://blog.csdn.net/FJY_sunshine/article/details/82775583)
[Provable Bounds for Learning Some Deep Representations](https://arxiv.org/abs/1310.6343)  
[Inception V1](https://www.jianshu.com/p/22e3af789f4e)
[Review: GoogLeNet (Inception v1)— Winner of ILSVRC 2014 (Image Classification)](https://medium.com/coinmonks/paper-review-of-googlenet-inception-v1-winner-of-ilsvlc-2014-image-classification-c2b3565a64e7)
[图像分类(一)GoogLenet Inception_V1：Going deeper with convolutions](https://www.cnblogs.com/Lilu-1226/p/10588058.html])