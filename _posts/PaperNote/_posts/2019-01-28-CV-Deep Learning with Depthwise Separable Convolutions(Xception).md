---
layout: post
title: 读《Deep Learning with Depthwise Separable Convolutions》(Xception)
date:   2019-01-28
categories: 深度学习(CV)
---  

# 概述  



![_config.yml]({{ site.baseurl }}/images/103GoogleNet/image2.png)    

在测试中，使用比Krizhevsky等人更积极的裁剪方法：将图像调整为四个尺度，分别为256，288，320和352，取这些调整后的图像的左，中，右方块（在肖像图片中，采用顶部，中心和底部方块）。对于每个方块，将采用4个角及中心224×224裁剪图像，方块调整尺寸为224×224的图像，这些图像镜像版本。那每张图像会得到4×3×6×2 = 144的张图像。在实际应用中，这种积极裁剪可能是不必要的，因为存在合理数量的裁剪图像后，更多裁剪图像的好处会变得很微小。    

参考：

[论文导读：GoogLeNet模型，Inception结构网络简化（Going deeper with convolutions）](https://blog.csdn.net/FJY_sunshine/article/details/82775583)
[Provable Bounds for Learning Some Deep Representations](https://arxiv.org/abs/1310.6343)  
[Inception V1](https://www.jianshu.com/p/22e3af789f4e)
[Review: GoogLeNet (Inception v1)— Winner of ILSVRC 2014 (Image Classification)](https://medium.com/coinmonks/paper-review-of-googlenet-inception-v1-winner-of-ilsvlc-2014-image-classification-c2b3565a64e7)
[图像分类(一)GoogLenet Inception_V1：Going deeper with convolutions](https://www.cnblogs.com/Lilu-1226/p/10588058.html])