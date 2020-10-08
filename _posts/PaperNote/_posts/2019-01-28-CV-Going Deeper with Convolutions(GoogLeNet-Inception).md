---
layout: post
title: 读《Going Deeper with Convolutions》(GoogLeNet-Inception)
date:   2019-01-28
categories: 深度学习(CV)
---  

# 概述  

随着移动和嵌入式设备的推动，算法的效率是很重要的——尤其是它们的电力和内存使用。正是包含了这个因素的考虑才得出了本文中呈现的深度架构设计，而不是单纯的为了提高准确率。通过精心的手工设计，在增加了网络深度和广度的同时保持了计算预算不变。为了优化质量，架构的设计以赫布理论和处理多尺度直觉为基础。   

文中使用了一个高效的计算机视觉深度神经网络架构，名为Inception。  

受灵长类视觉皮层神经科学模型的启发，[Serre](https://mcgovern.mit.edu/wp-content/uploads/2019/01/04069258.pdf)等人使用了一系列固定的不同大小的Gabor滤波器来处理多尺度。文中使用了类似的策略。然而，与[Serre](https://mcgovern.mit.edu/wp-content/uploads/2019/01/04069258.pdf)固定的2层深度模型相反，Inception结构中所有的滤波器是学习到的。此外，Inception层重复了很多次，在GoogLeNet模型中得到了一个22层的深度模型。


# 动机和思考  

提高深度神经网络性能最直接的方式是增加尺寸。增加深度(网络层次的数目)和宽度(每一层的神经元数目)。但是这个方案有两个主要的缺点：   

1、更大的尺寸通常意味着更多的参数，但这会使网络更容易过拟合，在训练集的标注样本有限的情况下。这是一个主要的瓶颈，因为要获得强标注数据集费时费力且代价昂贵。  

2、另一个缺点是计算资源使用的显著增加。例如，在一个深度视觉网络中，如果两个卷积层相连，它们的滤波器数目的任何均匀增加都会引起计算量平方式的增加。如果增加的能力在使用时效率低下(例如大多数权重结束时接近于0),那么会浪费大量的计算能力。  

解决这两个问题的基本方法是引入稀疏性,将全连接层替换为稀疏连接结构，甚至在卷积层内部也这样。由于[Arora](https://arxiv.org/abs/1310.6343)等人的开创性工作，这具有更坚固的理论基础。他们成果说明如果数据集的概率分布可以通过一个大型稀疏的深度神经网络表示，则最优网络拓扑可以根据前一层激活值相关统计分析，将输出具有高度相关的神经元进行聚类来逐层的构建。(说明可以通过这种构建方法达到稀疏效果？)这个成果说明与赫布理论的想法类似，一个很通俗的现象，先摇铃铛，之后给一只狗喂食，久而久之，狗听到铃铛就会口水连连。这也就是狗的“听到”铃铛的神经元与“控制”流口水的神经元之间的链接被加强了，而Hebbian principle的精确表达就是如果两个神经元常常同时产生动作电位，或者说同时激动（fire），这两个神经元之间的连接就会变强，反之则变弱（neurons that fire together, wire together）

在实现方面，因为大多数硬件针对密集矩阵的计算进行了优化，所以在完全连接变为稀疏连接之后(Sparsity means most of the weights are 0. This can lead to an increase in space and time efficiency.意味大部分权重为0),实际的计算量不会得到实质性的改善。尽管稀疏矩阵的数据量很小，但是很难减少计算时间。  

文中提出稀疏矩阵乘法的大量文献认为对于稀疏矩阵乘法，将稀疏矩阵聚类为相对密集的子矩阵会有更佳的性能。在未来会利用类似的方法来进行非均匀深度学习架构的自动构建。

举例：稀疏矩阵分解成2个子密集矩阵,再和2x2矩阵进行卷积,稀疏矩阵中0较多的区域就可以不用计算，计算量就大大降低。  

![_config.yml]({{ site.baseurl }}/images/103GoogleNet/image4.png)   

目前还无法实现,需要一种方法既可以保持网络结构的稀疏性,又可以利用密集矩阵的高计算性能。    

Inception体系结构最初是作为评估复杂网络拓扑构造算法的假设输出的一个案例研究，Inception试图通过密集的，易于获得的组件覆盖假设输出来近似视觉网络所隐含的稀疏结构。

Inception由卷积构成实现在空间（spatial）维度的稀疏连接，也就是传统的CNN卷积结构，同时实现特征（feature）维度的稀疏连接，在多个不同的尺寸上进行卷积再聚合。

我的理解不确定：  

特征维度上稀疏，意味卷积核稀疏，譬如原本5 x 5卷积核，部分权重应为0相当于选取部分特征达到稀疏，但是这种稀疏计算量降低较少，将其分解成多个尺度的密集卷积核(5 x 5卷积核部分权重为0时,相当于1 x 1,3 x 3卷积核),减少原本稀疏矩阵中零的计算。


# Architectural Details   

Inception架构的主要想法是考虑如何通过容易获得的密集组件(dense network中常见的组件，比如卷积、全连接等)逼近和覆盖卷积视觉网络的最优局部稀疏结构。我们所需要的只是找到最佳的局部构造并在空间上进行重复。   

Arora等人提出了一个层次结构，先分析前一层神经元输出的相关统计数据，将神经元聚集成具有高相关性的单元组(多个clusters)。这些clusters形成了下一层的神经元，并与前一层的神经元连接。我们假设前些层的每个神经元都对应input image的某些区域，并且这些单元被分入filter banks(不同的卷积计算)。在较低的层（接近输入的层）相关神经元集中在局部区域。因此，我们最终会有许多clusters集中在单个区域，它们可以通过下一层的卷积层覆盖，得到下一层的clusters。
 
不同尺寸卷积核会得到对应不同大小 patches(图像块) 的 clusters ,数量也不同(输出尺寸不同),为了避图像免块校正(patch-alignment)的问题(位置对齐，同一个chanel上不同卷积输出对应的patch区域相同)，目前Inception架构形式的滤波器的尺寸仅限于1×1、3×3、5×5，这个决定更多的是基于便易性而不是必要性。这也意味着提出的架构是所有这些层的组合，其输出滤波器组连接成单个输出向量形成了下一阶段的输入。另外，由于池化操作对于目前卷积网络的成功至关重要，因此在层次结构中添加一个pooling替代的并行池化路径 。   


![_config.yml]({{ site.baseurl }}/images/103GoogleNet/image5.png)  

![_config.yml]({{ site.baseurl }}/images/103GoogleNet/image6.png)   


由于这些“Inception模块”堆叠，其输出的相关统计数据必然有变化：由于较高层网络会捕获抽象较高的特征，其集聚空间会降低(面积减小)。这表明随着转移到更高层，3×3和5×5卷积数量的比例应该会增加。

下图图a“Inception模块”的一个大问题是随着堆叠channel维度不断增加，即使适量的5×5卷积也可能是非常昂贵的。池化单元添加，这个问题甚至会变得更明显：因为pooling输出的数量等于前一阶段滤波器的数量(所有尺度卷积核数)。池化层输出和卷积层输出的合并会导致这一阶段到下一阶段输出数量不可避免的增加。虽然这种架构可能会覆盖最优稀疏结构，但它会非常低效，导致在几个阶段内计算量爆炸。   

![_config.yml]({{ site.baseurl }}/images/103GoogleNet/image1.png)   

这导致了Inception架构的第二个想法,如上图图b：使用1x1卷积进行降维，减少了需要训练的参数个数，降低了计算复杂度。    

举例：  

Without the Use of 1×1 Convolution:    

![_config.yml]({{ site.baseurl }}/images/103GoogleNet/image7.png)     

Number of operations = (14×14×48)×(5×5×480) = 112.9M

With the Use of 1×1 Convolution:   

![_config.yml]({{ site.baseurl }}/images/103GoogleNet/image8.png)     

Number of operations for 1×1 = (14×14×16)×(1×1×480) = 1.5M  
Number of operations for 5×5 = (14×14×48)×(5×5×16) = 3.8M  
Total number of operations = 1.5M + 3.8M = 5.3M   


# Overall Architecture  


通常，Inception网络是一个由上述类型的模块互相堆叠组成的网络，偶尔会有步长为2的最大池化层将网络分辨率减半。出于技术原因（训练过程中内存效率），只在更高层开始使用Inception模块而在更低层仍保持传统的卷积形式似乎是有益的。这不是绝对必要的，只是反映了目前实现模型中一些基础结构效率低下。

给定深度相对较大的网络，有效传播梯度反向通过所有层的能力是一个问题。在这个任务上，更浅网络的强大性能表明网络中部层产生的特征应该是非常有识别力的。通过将辅助分类器添加到这些中间层，可以期望较低阶段分类器的判别力。这被认为是在提供正则化的同时克服梯度消失问题。这些分类器采用较小卷积网络的形式，放置在Inception (4a)和Inception (4b)模块的输出之上。在训练期间，它们的损失以折扣权重（辅助分类器损失的权重是0.3）加到网络的整个损失上。在推断时，这些辅助网络被丢弃。后面的控制实验表明辅助网络的影响相对较小（约0.5），只需要其中一个就能取得同样的效果。

![_config.yml]({{ site.baseurl }}/images/103GoogleNet/image9.png)    

![_config.yml]({{ site.baseurl }}/images/103GoogleNet/image2.png)    

在测试中，使用比Krizhevsky等人更积极的裁剪方法：将图像调整为四个尺度，分别为256，288，320和352，取这些调整后的图像的左，中，右方块（在肖像图片中，采用顶部，中心和底部方块）。对于每个方块，将采用4个角及中心224×224裁剪图像，方块调整尺寸为224×224的图像，这些图像镜像版本。那每张图像会得到4×3×6×2 = 144的张图像。在实际应用中，这种积极裁剪可能是不必要的，因为存在合理数量的裁剪图像后，更多裁剪图像的好处会变得很微小。    

参考：

[论文导读：GoogLeNet模型，Inception结构网络简化（Going deeper with convolutions）](https://blog.csdn.net/FJY_sunshine/article/details/82775583)
[Provable Bounds for Learning Some Deep Representations](https://arxiv.org/abs/1310.6343)  
[Inception V1](https://www.jianshu.com/p/22e3af789f4e)
[Review: GoogLeNet (Inception v1)— Winner of ILSVRC 2014 (Image Classification)](https://medium.com/coinmonks/paper-review-of-googlenet-inception-v1-winner-of-ilsvlc-2014-image-classification-c2b3565a64e7)
[图像分类(一)GoogLenet Inception_V1：Going deeper with convolutions](https://www.cnblogs.com/Lilu-1226/p/10588058.html])