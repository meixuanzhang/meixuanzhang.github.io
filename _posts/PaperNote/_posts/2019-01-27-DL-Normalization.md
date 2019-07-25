---
layout: post
title: 读《Normalization》相关论文
date:   2019-01-27
categories: 深度学习
---

**涉及论文**  
《Batch Normalization: Accelerating Deep Network Training by Reducing Internal Covariate Shift》   
《Layer Normalization》   
《Instance Normalization:The Missing Ingredient for Fast Stylization》  
《Group Normalization》   
《DIFFERENTIABLE LEARNING-TO-NORMALIZE VIA SWITCHABLE NORMALIZATION》   

# 1、Batch Normalization  
训练深度神经网络很复杂，因为每个层的输入分布在训练期间会发生变化，因为前一层的参数会发生变化。这通过要求较低的学习速率和仔细的参数初始化来减慢训练，并且使得训练具有饱和非线性的模型变得非常困难。  

Batch Normalization优势在于使标准化成为模型体系结构的一部分，对每个小批量训练样本进行标准化。Batch Normalization允许我们使用更高的学习速率并且不需要过于担心初始化问题。

SGD(stochastic gradient descent)已经被证明是非常有效训练方式，其通过优化参数$$\theta$$来最小化损失函数：   

$$\theta=\mathop{\arg\max}_{\theta}\frac{1}{N}\sum_{i=1}^{N}l(x_{i},\theta) $$


$$x_{1..N}$$是训练集，$$x_{1..m}$$是mini-batch   

计算梯度：  

$$\frac{1}{m}\frac{\partial l(x_{i},\theta)}{\partial \theta}$$  

**问题一**   

对于多层的神经网络，由于每层的输入都受到所有前面层的参数的影响，因此训练变得复杂，因此随着网络变得更深，网络参数的微小变化会放大。层的输入分布的变化导致层需要不断适应新的分布。将层输入分布变化问题，称为covariate shift。   

如：  

$$l=F_{2}(F_{1}(u,\theta_{1}),\theta_{2})$$   
$$x=F_{1}(u,\theta_{1})$$  
$$l=F_{2}(x,\theta_{2})$$  
$$\theta_{2} \gets \frac{\alpha}{m}\sum_{i=1}^{m}\frac{\partial F_{2}(x_{i},\theta_{2})}{\partial \theta_{2}}$$  

$$F_{1},F_{2}$$是任意的转换函数，$$\theta_{1},\theta_{2}$$是参数，由于$$x$$受$$F_{1}(u,\theta_{1})$$影响，因此出现了covariate shift问题。   

假设$$F_{2}$$是单独的网络，$$x$$是输入，不受$$F_{1}(u,\theta_{1})$$影响，有固定的分布，则在训练和测试时，$$x$$会具有相同的分布，让训练变得更有效。   


**问题二**    

考虑激活函数为sigmoid：  

$$z=g(Wu+b)\\
g(x)=\frac{1}{1+exp(-x)}$$   

$$u$$为层的输入，当$$\mid x\mid$$增加时，$$g'(x)$$(微分)会趋向于0,这意味着除了$$x=Wu+b$$绝对值较小的值外，所有流向$$u$$的梯度将会消失，模型训练的特别慢。由于$$x$$受$$W,b$$参数影响，在训练期间参数的一点变化将使$$x$$移动到非线性的饱和状态并且收敛减慢。这个问题可以通常使用$$ReLu(x)=max(x,0)$$激活函数及小的学习率进行改善。   

论文提出Batch Normalization，减少了内部covariate shift，并且这样做大大加速了深层神经网络的训练。它通过一个标准化步骤来实现这一点，该步骤确定了层输入的平均值和方差。Batch Normalization减少梯度对参数及自身初始值依赖性。这使我们可以使用更高的学习率。此外，Batch Normalization有regularize作用，减少了对Dropout的需求（Srivastava等，2014）。最后，Batch Normalization可以通过防止网络陷入饱和模式来使用饱和非线性激活函数。   


## 算法  

先按batch Normalizing Transform转换多个批量数据，计算批量均值的期望，以及批量方差的期望，以均值期望和方差期望，作为标准化的均值和方差，转换数据并进行训练。 这里激活函数输入通过均值和方差标准化后还要经历一次线性转换，才能输入到激活函数里。

![_config.yml]({{ site.baseurl }}/images/19Normalization/image1.png)
![_config.yml]({{ site.baseurl }}/images/19Normalization/image2.png)

在测试时同样以均值期望和方差期望，作为标准化所需的均值和方差：  

$$
\hat{x}=\frac{x-E[x]}{\sqrt{var[x]+\epsilon}}
$$


## Batch-Normalized Convolutional-Network   

CNN filter 激活函数输入前值为:   

$$x=Wu+b$$

filter 激活函数输出为：  

$$z=g(Wu+b)$$  

batch-Normalized Convolutional-Network需要对$$x$$进行标准化,(这里$$x$$没有加b,因为偏差量加到了后面的标准化$$\beta$$参数中)：   

$$z=g(BN(Wu))$$   

假设feature map 维度是$$p*q$$,mini-batch的大小是$$m$$,由于CNN网络feature map神经元之间不是独立的需要根据$$m*p*q$$计算标准化所需均值和方差，而不是单独对每一个激活函数输入单独在批量维度进行标准化，$$BN(Wu)$$除了包含均值和方差标准化，还包含线性转换，每个feature map有对应的线性转换参数$$\gamma^k,\beta^k$$  

## Batch Normalization允许更高的学习率，具有正则化能力   

假设训练过程中将权重缩放$$\alpha$$倍：  

$$
BN(Wu)=BN((\alpha W)u)\\
\frac{\partial BN((\alpha W)u)}{\partial u }=\frac{\partial BN(Wu)}{\partial u}\\
\frac{\partial BN((\alpha W)u)}{\partial (\alpha W) }=\frac{1}{\alpha}\frac{\partial BN(Wu)}{\partial W}\\
$$ 

可以发现$$\alpha$$不影响Jacobian层，权重$$W$$成倍增大会导致更小的梯度。  

此外论文推测Batch Normalization 让 Jacobians层($$\beta$$)的奇异值接近1，两个标准化转换关系为$$\hat{z}=F(\hat{x})$$，假设$$\hat{x},\hat{z}$$各自维度间不相关且每个维度服从高斯分布，$$F(\hat{x})\approx J\hat{x}$$，$$\hat{x}$$和$$\hat{z}$$有单位的协方差矩阵，则： 




$$
I=Cov[\hat{z}]=JCov[\hat{x}]J^T=JJ^T\\
$$

证明(这里x是矩阵，行代表特征维度，列是样本)：  

$$Cov(x)=E((x-E(x))(x-E(x))^T)\\
z=Jx\\
E(z)=E(Jx)=JE(x)\\
z-E(z)=J(x-E(x))\\
Cov(z)=E((z-E(z))(z-E(z))^T)\\
=E[J(x-E(x))(x-E(x))^TJ^T]\\
=JE[J(x-E(x))(x-E(x))^T]J^T\\
=JCov(x)J^T$$

$$J$$是实正交矩阵，奇异值为1，防止出现巨大的梯度。  

In reality, the transformation is not linear, and the normalized values are not guaranteed to be Gaussian nor independent, but we nevertheless expect Batch Normalization to help make gradient propagation better behaved. 

当使用Batch Normalization进行训练时，训练样本与小批量中的其他样本结合使用，训练网络不再为给定的训练样本产生确定性值，这有利于网络的泛化。   

# 2、Layer Normalization   

Notation:  

$$H$$:神经网络某层神经元总数    
$$u^{l}$$:神经网络第$$l$$层神经元均值    
$$\sigma^l$$:神经网络第$$l$$层神经元标准差  
$$a^l$$:神经网络第$$l$$层所有神经元  

$$u^{l}=\frac{1}{H}\sum_{i=1}^H a_{i}^l\\
\sigma^l=\sqrt{\frac{1}{H}\sum_{i=1}^H(a_{i}^l-u^{l})^2}$$

$$\tilde{a}^l=\frac{g}{\sigma^l}\odot (a^l-u^{l})+b$$  

$$g,b$$是bias，偏差   

## layer normalized recurrent nerural networks  

Notation:  

$$H$$:t时刻循环神经网络隐藏层神经元总数    
$$u^{t}$$:t时刻循环神经网络隐藏层输入均值    
$$\sigma^l$$:t时刻循环神经网络隐藏层输入标准差   
$$a^t$$:t时刻循环神经网络隐藏层输入  
$$h^t$$:t时刻循环神经网络隐藏层输出  

$$
a^t=W_{hh}h^{t-1}+W_{xh}X^t\\
u^{t}=\frac{1}{H}\sum_{i=1}^H a_{i}^t\\
\sigma^t=\sqrt{\frac{1}{H}\sum_{i=1}^H(a_{i}^t-u^{t})^2}\\
h^t=f[\frac{g}{\sigma^t}\odot (a^t-u^{t})+b]$$ 


+ 三种标准化方式对比： 

![_config.yml]({{ site.baseurl }}/images/19Normalization/image3.png)

# 3、Instance Normalization  

Notation:  

$$x\in R^{T*C*W*H}$$:没有经过激活函数的feature map ，其中$$T$$表示batch size,$$C$$是channel,$$W*H$$像素大小  
$$x_{tijk}$$:batch中第$$t$$张图片，第$$i$$个频道(第$$i$$个filter)，在feature map的$$jk$$位置的像素点，$$y_{tijk}$$是其标准化结果  

$$
u_{ti}=\frac{1}{HW}\sum_{l=1}^W \sum_{m=1}^H x_{tilm}\\
\sigma_{ti}^2=\frac{1}{HW}\sum_{l=1}^W \sum_{m=1}^H(x_{tilm}-u_{ti})^2\\
y_{tijk}=\frac{x_{tijk}-u_{ti}}{\sqrt{\sigma_{ti}^2+\epsilon}}
$$

# 4、Group Normalization  

**对比四种类型的Normalization**  

![_config.yml]({{ site.baseurl }}/images/19Normalization/image4.png)

Notation: 
$$\tilde{x_{i}}$$:feature map的一个像素点，索引为$$i$$,$$i=(i_{N},i_{C},i_{H},i_{W})$$是一个四维向量，向量空间是$$(N,C,H,W)$$  

为了标准化$$\tilde{x_{i}}$$： 

$$\tilde{x_{i}}=\frac{1}{\sigma_{i}}(x_{i}-u_{i})$$

需要计算$$\sigma_{i},u_{i}$$:   

$$u_{i}=\frac{1}{m}\sum_{k\in S_{i}}x_{k}\\
\sigma_{i}=\sqrt{\frac{1}{m}\sum_{k\in S_{i}}(x_{i}-u_{i})^2+\epsilon}
$$

$$S_{i}$$is the set of pixels in which the mean and std are computed, and $$m$$ is the size of this set.  

+ Bartch Norm  

$$S_{i}={k\mid k_{C}=i_{C}}$$  

CNN网络结构batch norm沿着$$(N,H,W)$$计算均值和标准差,每一个channel$$(N,H,W)$$是一个set

+ Layer Norm

$$S_{i}={k\mid k_{N}=i_{N}}$$  

沿着$$(C,H,W)$$计算均值和标准差,每一个样本$$(C,H,W)$$是一个set   

+ Instance Norm  

$$S_{i}={k\mid k_{N}=i_{N},k_{C}=i_{C}}$$  

沿着$$(H,W)$$计算均值和标准差,每一个样本每一个channel$$(H,W)$$是一个set   


+ Group Norm  

$$S_{i}={k\mid k_{N}=i_{N},\lfloor \frac{k_{C}}{C/G} \rfloor=\lfloor \frac{i_{C}}{C/G} \rfloor}$$  

将channel划分为G组，每组含有channel数为$$C/G$$   
沿着$$(H,W)$$以及 $$C/G$$个channel计算均值和标准差,每一个样本每个channel组的$$(C/G,H,W)$$是一个set

# 5、SWITCHABLE NORMALIZATION   

进行标准化需要计算均值和标准差：  

$$\tilde{h}_{ncij}=\gamma \frac{h_{ncij}-u}{\sqrt{\sigma^2+\epsilon}}+\beta\\

n\in [1,N],c\in [1,C],i\in [1,H],j\in [1,W]$$

SWITCHABLE NORMALIZATION 结合了IN,LN,BN:  


$$\tilde{h}_{ncij}=\gamma \frac{h_{ncij}-\sum_{k\in\Omega}w_{k}u_{k}}{\sqrt{\sum_{k\in\Omega}w_{k}^{'}\sigma_{k}^2+\epsilon}}+\beta$$





