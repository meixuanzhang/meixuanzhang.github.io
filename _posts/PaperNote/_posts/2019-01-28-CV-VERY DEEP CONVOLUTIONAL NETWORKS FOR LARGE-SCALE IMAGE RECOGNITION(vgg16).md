---
layout: post
title: 读《Very Deep Convolutional Networks For Large-Scale Image Recognition》(vgg16)
date:   2019-01-28
categories: 深度学习
---  

# The Architecture   

模型结构如下：  

![_config.yml]({{ site.baseurl }}/images/101vgg16/image1.png)     

   ![_config.yml]({{ site.baseurl }}/images/101vgg16/image10.png)    

cov3-64表示使用3 × 3的卷积核，卷积核个数为64  

对于卷积核选择，连续两层3 × 3卷积核(stride=1)，感受野面积等于一层5 × 5的卷积核感受野面积，三层3 × 3卷积核感受野面积等于一层7*7的卷积核感受野面积，获得同样感受野情况下，使用小的卷积参数比大的卷积核少：  

1 layer of 11×11 filter, 参数 11×11=121   
5 layer of 3×3 filter, 参数 3×3×5=45   
参数数量减少 63% 

1 layer of 7×7 filter, 参数 7×7=49  
3 layers of 3×3 filters, 参数  3×3×3=27  
参数数量减少 45%  

1 layer of 5×5 filter, 参数  5×5=25  
2 layers of 3×3 filters, 参数 3×3+3×3=18  
参数数量减少 28%   

更少的参数有利于收敛，以及减少过拟合  

![_config.yml]({{ site.baseurl }}/images/101vgg16/image6.png)  

# Multi-Scale Training  

论文模型的输入图像尺寸为224 × 224，对于尺寸为224 × 224原始图像可以直接进入模型，对于尺寸大于224 × 224$$()$$的原始图像则进行裁剪(crop)，使其尺寸为224 × 224，裁剪后图像可能包含目标或目标的一部分。  

对于使用哪种尺寸原始图像，文中提出两个方法： 

1、single-scale training：使用固定尺寸的原始图像裁剪获得224 × 224尺寸图像，通过不同裁剪(crop)作为抽样(note that image content within the sampled crops can still represent multiscale image statistics).文中使用了两种固定尺寸的图像,首先使用S=256图像训练,然后使用S=384图像加速训练(以S=256训练好参数作为S=384初始参数)，同时使用的learning rate调整为$$10^{-3}$$


2、multi-scale training：使用多种尺寸的原始图像裁剪获得224 × 224尺寸图像，原始图像尺寸范围为[256,512]。这种训练方式考虑了图像中目标具有不同尺寸的情况

![_config.yml]({{ site.baseurl }}/images/101vgg16/image7.png)  


从图中可以看出使用multi-scale training，错误率更低

![_config.yml]({{ site.baseurl }}/images/101vgg16/image2.png)  

# Multi-Scale Testing   

由于不知道测试图像中目标的尺寸，我们将测试图像缩放到不同的大小，可以增加正确分类的机会，降低错误率 

![_config.yml]({{ site.baseurl }}/images/101vgg16/image3.png) 

单尺寸训练采用多尺寸测试，同样降低了错误率  

# Dense (Convolutionalized) Testing  

文中提出两种评估方法：  

方法1: multi-crop，即对图像进行多样本的随机裁剪，然后通过网络预测每一个crop的结果，最终对所有结果平均
方法2: dense， 将原图直接送到网络进行预测，将最后面全连接层改为卷积层，这样最后会得出一个预测的score map，再对结果求平均

两种评估方法不需要更改模型结构，multi-crop测试时通过裁剪输入图片为224 × 224，最后一个maxpool输出是7 × 7 × 512，接第一个FC，参数个数是7 × 7 × 512 × 4096,输出4096，dense将原图直接送到网络，同时将原来FC改为卷积，卷积核是7 × 7 × 512,卷积核的个数是4096，结构其实是不变的，后面FC改卷积同理，但densely最后输出的是score map。  

假如采用dense，将256 × 256图像输入网络，最后一个maxpool输出是8 × 8 × 512，经历三层卷积输出是2 × 2 × 1000。  

Multi-crop evaluation works slightly better than dense evaluation, but the methods are somewhat complementary as averaging scores from both did better than each of them individually. The authors hypothesize that this is probably because of the different boundary conditions: when applying a ConvNet to a crop, the convolved feature maps are padded with zeros, while in the case of dense evaluation the padding for the same crop naturally comes from the neighbouring parts of an image (due to both the convolutions and spatial pooling), which substantially increases the overall network receptive field, so more context is captured.

![_config.yml]({{ site.baseurl }}/images/101vgg16/image4.png)   

此外还通过horizontal flip增强测试集，会将原本图片和水平翻转图片测试结果进行平均。

# Emsemble 

![_config.yml]({{ site.baseurl }}/images/101vgg16/image5.png)  

# Comparison Between VGGNet and GoogLeNet 

![_config.yml]({{ site.baseurl }}/images/101vgg16/image8.png)  

# Data Augmentation  

To further augment the training set, the crops underwent randomhorizontal flipping and randomRGB colour shift (Krizhevsky et al., 2012 Alexnet).

# Data Process

The only preprocessing we do is subtracting the mean RGB value, computed on the training set, from each pixel.

How: Sum up the intensities of the training set for each color channel separately and divide by the total number of pixels. You can do that manually in python with x_train.mean(axis=(0,1,2)).

Why: Once we know the mean, we can subtract it from all pixel values so the intensities are centered at 0. this helps to increase training speed and accuracy.


参考： [VGGNet — 1st Runner-Up (Image Classification), Winner (Localization) in ILSVRC 2014](https://medium.com/coinmonks/paper-review-of-vggnet-1st-runner-up-of-ilsvlc-2014-image-classification-d02355543a11)


