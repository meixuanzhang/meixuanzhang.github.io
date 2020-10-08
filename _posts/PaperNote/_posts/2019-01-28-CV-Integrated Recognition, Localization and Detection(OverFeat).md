---
layout: post
title: 读《Integrated Recognition, Localization and Detection using Convolutional Networks》(OverFeat)
date:   2019-01-28
categories: 深度学习(CV)
---  

# 概述  

这篇论文提出了一个使用卷积网络进行分类、定位、检测的集成框架。展示了多尺度(multiscale)和滑动窗口(sliding window)可以在ConvNet中有效地实施。意味在一定程度上模型不限制图像尺寸。  
论文模型是通过预测对象边界来定位。边界框(Bounding boxes)是通过累积而不是抑制方式来增加检测置信度。  
可以使用单个共享网络同时学习不同的任务。(类似迁移学习TransferLearning)。  


# 模型架构  

## ConvNets and Sliding Window Efficiency

Sliding Window Algorithm滑窗法：在图像上使用不同滑动窗口获得候选预测区域,使用模型对候选区域进行目标识别预测。  

如图所示：在图像上滑动一个3*3大小窗口，从图像中获得多个区域，然后模型对候选区域进行目标识别。    

![_config.yml]({{ site.baseurl }}/images/110Overfeat/image1.jpg)    


下图是alexnet的结构图，其用于解决分类任务，模型末尾接了两层全连接(fully-connected),模型输入图像的尺寸是固定的，输出响应的是整张图，对于不同尺寸的图，需要按模型输入尺寸对图像进行裁剪。

![_config.yml]({{ site.baseurl }}/images/110Overfeat/image3.png)  

论文使用了全卷积架构(这个网络由卷积构成没有全连接)，使其能自动实现滑窗效果，如图：  

![_config.yml]({{ site.baseurl }}/images/110Overfeat/image2.png)    

16 x 16 图的每个输出在图像中有对应的感受野(receptive field),类似使用了14 x 14窗口获得不同的候选区，并且它能一次性计算出所有候选的输出。  

##  Multi-Scale Classification

alexnet模型输入是单一尺寸的图像，为提高robustness,论文同一个图像使用了6种不同的尺寸同时作为输入。

图像分类任务中，alexnet模型测试时，对图像以及水平翻转图像裁剪四个角上的图像块和中心的图像块，共获得10个图像块，对预测结果取均值作为最后预测。这种方法忽略图像的许多区域，同时当目标集中在一个区域时，计算上是多余是的(裁剪的图像可能不含预测类别)，此外模型运行一次只能获得一个图像裁剪预测，效率低。  

论文中使用的模型，每个输出在图像对应感受野(receptive field)尺度为6 x 6，窗口可能存在对齐的问题，即窗口只包含了目标的一部分，为此采用以下方法(类似使用了多种裁剪图像方法)获得候选区：  

图中展示了模型第五层pooling前feature map 某个维度(长)大小为20，3 x 3 pooling在这个维度上采用3个不同的位置作为起始，相当于裁掉了图像的一部分，进行pooling计算,如果在另一个维度(宽)上也是如此，那每一层feature map经过pooling后会有3 x 3 层feature map

![_config.yml]({{ site.baseurl }}/images/110Overfeat/image4.png)    

同一尺寸的图像，为了不同起始位置pooling，最后输出空间维度一致，对图像尺寸是有要求的。模型使用了下列的图像尺寸：  

![_config.yml]({{ site.baseurl }}/images/110Overfeat/image5.png)   

图像输入到模型，根据输入图像尺寸大小，会有不同空间大小输出(长宽不同，空间每个位置channel为类别数)，预测一张图像时，会将其调整成6种尺寸(相当于6张图片分别输入到模型)，每个尺寸图片，又需经过不同的位置作为起始的pooling，最终预测一张图片需要对不同尺寸，不同起始的pooling，不同空间位置所有输出进行处理。每个位置输出维度是C(类别数)。

不同尺寸，不同起始pooling，每个空间位置只保留output中值最大的类别及其值，对将保留下的同类别的值取平均，作为这个类别最后预测，最后取预测值top1 或 top5。   

##  Model Design and Training 

模型设计了两个版本，fast model和accurate model如图： 

conv + max 表示使用了卷积和max pooling ,具体参数写在表格中， full 表示使用的是1 x 1的卷积层。full之前的层都是feature extraction layers ,分类模型训练好后可以固定，后面层迁移学习时需要重新训练的。

![_config.yml]({{ site.baseurl }}/images/110Overfeat/image7.png)   

![_config.yml]({{ site.baseurl }}/images/110Overfeat/image8.png)     


##  Localization  

图像分类和定位区别在于输出是不同的，定位结构：  

除了图像分类的softmax的输出，还需要加Bounding boxes输出，注意输出时，每个类别都是有Bounding boxes，而不是只输出一维的Bounding boxes向量，使用L2计算loss时，只计算目标对应的box。  

![_config.yml]({{ site.baseurl }}/images/110Overfeat/image6.png)   

由于有多个输出，所以会有多个box。预测时需要处理重叠的box。

![_config.yml]({{ site.baseurl }}/images/110Overfeat/image9.png)  

## Combining Predictions  

论文采用以下累计预测算法处理Bounding boxes： 

$$s \in 1,2,3,4,5,6$$:表示(Talbe 5)图像不同尺寸  

1、对预测图像的不同尺寸分别计算出前k个类别，获得每个尺寸前k个类别的bounding box(这里每个尺寸每个空间位置输出取置信值最大的类别和box,然后只取前面计算出前k类的box)   
2、合并不同尺寸前k个类别的bounding box得到集合B，重复以下步骤：  

$$(b_{1}^*,b_{2}^*)=argmin_{b_{1} \ne b_{2}\in B}match_score(b_{1},b_{2})$$, 即从B中找出使match_score(两个bounding box中心距离及box交叉面积和)最小的组合($$b_{1},b_{2}$$)。
如果$$match_score(b_{1}^*,b_{2}^*)>t$$,则停止，否则对$$b_{1}^*,b_{2}^*$$进行合并(使用两个box坐标平均值获得新box)  


目标检测任务，考虑一个图像没有目标时，类别上应增加一个背景类。

