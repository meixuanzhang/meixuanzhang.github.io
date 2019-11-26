---
layout: post
title: 读《Going Deeper with Convolutions》(GoogLeNet-Inception)
date:   2019-01-28
categories: 深度学习
---  

# 概述  

随着移动和嵌入式设备的推动，算法的效率是很重要的——尤其是它们的电力和内存使用。正是包含了这个因素的考虑才得出了本文中呈现的深度架构设计，而不是单纯的为了提高准确率。通过精心的手工设计，在增加了网络深度和广度的同时保持了计算预算不变。为了优化质量，架构的设计以赫布理论和处理多尺度直觉为基础。   

文中使用了一个高效的计算机视觉深度神经网络架构，名为Inception。以“Inception module”的形式引入了一种新层次的组织方式，在更直接的意义上增加了网络的深度。  

受灵长类视觉皮层神经科学模型的启发，[Serre](https://mcgovern.mit.edu/wp-content/uploads/2019/01/04069258.pdf)等人使用了一系列固定的不同大小的Gabor滤波器来处理多尺度。文中使用了类似的策略。然而，与[Serre](https://mcgovern.mit.edu/wp-content/uploads/2019/01/04069258.pdf)固定的2层深度模型相反，Inception结构中所有的滤波器是学习到的。此外，Inception层重复了很多次，在GoogLeNet模型中得到了一个22层的深度模型。


# 动机和思考  

高深度神经网络性能最直接的方式是增加它们的尺寸。这不仅包括增加深度——网络层次的数目——也包括它的宽度：每一层的单元数目。这是一种训练更高质量模型容易且安全的方法，尤其是在可获得大量标注的训练数据的情况下。但是这个简单方案有两个主要的缺点。更大的尺寸通常意味着更多的参数，这会使增大的网络更容易过拟合，尤其是在训练集的标注样本有限的情况下。这是一个主要的瓶颈，因为要获得强标注数据集费时费力且代价昂贵，经常需要专家评委在各种细粒度的视觉类别进行区分，


![_config.yml]({{ site.baseurl }}/images/102Resnet/image6.png)   


参考：

[How does mean image subtraction work?](https://stackoverflow.com/questions/44788133/how-does-mean-image-subtraction-work)
