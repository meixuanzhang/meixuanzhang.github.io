---
layout: post
title: 《initialization》相关论文
date:   2019-01-28
categories: 深度学习
---  

**涉及论文**：    
《Understanding the difficulty of training deep feedforward neural networks》   
《On weight initialization in deep neural networks》   
   


# 概述  

参数Initialization策略及激活函数的选择影响深度模型的收敛速度以及效果。  


# 梯度计算  

以feedforward nerual network为例，下图展示了计算参数梯度时(来源：台大深度学习)影响因素，从最后结果可以看出对于$$l$$层参数梯度计算，其受上一层($$l-1$$层)神经元的输出$$a^{l-1}$$,当前层激活函数对其输入微分$$\sigma ' (z^l)$$,下一层($$l+1$$层)参数$$W^l$$,损失函数对下一层激活函数输入微分$$\delta$$影响  
![_config.yml]({{ site.baseurl }}/images/65 initialization/image1.png)   
![_config.yml]({{ site.baseurl }}/images/65 initialization/image2.png)   
![_config.yml]({{ site.baseurl }}/images/65 initialization/image3.png)  
![_config.yml]({{ site.baseurl }}/images/65 initialization/image4.png)  



# 《Understanding the difficulty of training deep feedforward neural networks》   

论文对比了Softsign(x),tanh(x),sigmod(x)三种不同激活函数以及不同参数初始化方法下saturation情况及梯度变化情况 

##  Effect of Activation Functions and Saturation During Training  

这里参数初始化方式是：  
$$
W_{ij} \sim U[-\frac{1}{\sqrt{n}},\frac{1}{\sqrt{n}}]
$$

表示参数服从范围为$$[-\frac{1}{\sqrt{n}},\frac{1}{\sqrt{n}}]$$的均匀分布，$$n$$是神经网络前一层神经元数，$$W$$的列数  

### Experiments with the Sigmoid  

![_config.yml]({{ site.baseurl }}/images/65 initialization/image5.png)    

从图中可以发现训练开始，除了神经网络最后一层，其他层的激活值(激活函数输出值)围绕在0.5，随着神经网络加深，激活值有下降趋势，神经网络最后一层激活值在很长一段时间内值为0(此时激活函数梯度接近0)，处于饱和状态，对于神经网络中间层(图中第四层)，随着epoch增加激活值出现了从饱和状态“逃离”现象，同时第一层部分激活值开始出现了饱和状态，如果参数初始化是采用预训练的方式则不会出现这样的饱和现象。   

逻辑层输出$$softmax(b + Wh)$$最初可能更多地依赖于其偏差$$b$$（其学习非常快）而不是顶部隐藏激活$$h$$（因为$$h$$的变化方式不能预测y的变化，输出可能主要与x的其他更主要的变化相关)。因此，误差梯度倾向于将$$Wh$$推向0，这可以通过将$$h$$推向0来实现。在对称激活函数（例如双曲正切和softsign）的情况下，值在0附近是好的，因为它允许梯度向后流动(此时梯度大)。但是，将S形输出推到0将使它们进入饱和状态，这将防止梯度向后流动并防止较低层学习有用的特征。最终但缓慢地，较低层向更有用的特征移动，然后顶部隐藏层移出饱和状态。  


### Experiments with the Hyperbolic tangent  

![_config.yml]({{ site.baseurl }}/images/65 initialization/image6.png)  

上图是tanh(x)激活函数，下图是Softsign(x)激活函数，从图中可以看出tanh(x)激活最后一层(顶层，第五层)开始并没有出现饱和的情况(激活函数梯度不为0)，但第一层出现了，随着epoch增加，其他层也开始出现饱和现象，Softsign(x)激活函数情况则好些。Softsign饱和度不会像tanh那样一层接一层地出现。它在开始时更快然后变慢，并且所有层一起朝向更大的权重移动。tanh激活函数值越大或越小，梯度会接近0.

![_config.yml]({{ site.baseurl }}/images/65 initialization/image8.png)  

### Experiments with the Softsign  

$$softsign(x)=x/(1+\mid x\mid )$$

![_config.yml]({{ site.baseurl }}/images/65 initialization/image7.png)   

上图显示的是训练结束时激活值的直方图，上图是tanh，下图是Softsign，tanh激活值主要分布在0，和渐近线-1，1，Softsign激活值主要分布在0，-1和1之间  

## Studying Gradients and their Propagation  

Notation:  

$$s^i$$:神经网络第i层神经元的输入,$$s^i=z^iW^i+b^i$$   
$$z^i$$:神经网络第i层上一层神经元的输出，$$z^{i+1}=f(s^i)$$     
$$n_{i}$$:神经网络第i层的神经元数量   
$$x$$:是input   

$$
\frac{\partial Cost}{\partial s_{k}^i}=f'(s_{k}^i)W_{k,\bullet}^{i+1}\frac{\partial Cost}{\partial s^{i+1}}\\
\frac{\partial Cost}{\partial w_{l,k}^i}=z_{l}^i\frac{\partial Cost}{\partial s_{k}^{i}}
$$


假设初始时是线性范围的，权重是独立初始化的，每一个权重方差相同$$Var[W^{i'}]$$,输入特征方差是相同的为$$Var[x]$$

$$
f'(s_{k}^i)\approx 1,\\
Var[z^i]=Var[x]\prod_{i'=0}^{i-1}n_{i'}Var[W^{i'}]
$$

$$z^{i-1},W^{i-1}$$相互独立，且因为$$f'(s_{k}^i)\approx 1$$所有$$z^{i+1}\approx s^i$$,$$z^{i}$$特征方差是相同的都为$$Var[z^i]$$  


$$
Var[z^i] = Var[z_{k}^i]=Var[\sum_{j=1}^{n_{i-1}}z_{j}^{i-1}W_{j,k}^{i-1}]\\
=\sum_{j=1}^{n_{i-1}}Var[z_{j}^{i-1}W_{j,k}^{i-1}]\\
=\sum_{j=1}^{n_{i-1}}Var[z_{j}^{i-1}]Var[W_{j,k}^{i-1}]\\
=n_{i-1}Var[z^{i-1}]Var[W^{i-1}]\\
$$ 

$$
Var[\frac{\partial Cost}{\partial s^i}]=Var[\frac{\partial Cost}{\partial s^d}]\prod_{i'=i+1}^{d}n_{1'+1}Var[W^{i'}]
$$

$$
Var[\frac{\partial Cost}{\partial s^i}]=Var[\frac{\partial Cost}{\partial s_{k}^i}]\\
=Var[\sum_{j=1}^{n_{i+2}}\frac{\partial Cost}{\partial s_{j}^{i+1}} \frac{\partial s_{j}^{i+1}}{\partial z_{k}^{i+1}}f'(s_{k}^i)]\\
=n_{i+2}Var[W_{k}^{i+1}]Var[\frac{\partial Cost}{\partial s_{j}^{i+1}}]
$$

$$n_{o}$$是输入$$x$$的维度，$$z^0=x^0$$,$$s^0=z^0W^0+b^0)$$,$$s^0$$维度为$$n_{1}$$  


$$
Var[\frac{\partial Cost}{\partial W^i}]=Var[x]\prod_{i'=0}^{i-1}n_{i'}Var[W^{i'}]\prod_{i'=i+1}^{d}n_{i'+1}Var[W^{i'}]*Var[x]Var[\frac{\partial Cost}{\partial s^d}]   
$$

为了保持信息的流动，希望对于任意$$\forall(i,i')$$有： 

$$
Var[z^i]=Var[z^{i'}]\\
Var[\frac{\partial Cost}{\partial s^i}]=Var[\frac{\partial Cost}{\partial s^{i'}}]
$$

因此对于任意的$$i$$有：  

$$
n_{i}Var[W^i]=1 \\
n_{i+1}Var[W^i]=1\\
Var[W']=\frac{2}{n_{i}+n_{i+1}}
$$ 

$$
Var[\frac{\partial Cost}{\partial s^i}]=[nVar[W]]^{d-i}Var[x]\\
Var[\frac{\partial Cost}{\partial W^i}]=[nVar[W]]^dVar[x]Var[\frac{\partial Cost}{\partial s^d}]
$$

对于参数标准的初始化方法$$W_{ij} \sim U[-\frac{1}{\sqrt{n}},\frac{1}{\sqrt{n}}]$$，有： 

$$
Var[W]=\frac{(\frac{1}{\sqrt{n}}+\frac{1}{\sqrt{n}})^2}{12}\\
=\frac{\frac{4}{n}}{12}=\frac{1}{3n}\\
nVar[W]=\frac{1}{3}
$$ 

采用$$W_{ij} \sim U[-\frac{6}{\sqrt{n_{j}+n_{j+1}}},\frac{6}{\sqrt{n_{j}+n_{j+1}}}]$$参数初始化方式(**normalized initialization**)，对比两种初始化方式有：  

![_config.yml]({{ site.baseurl }}/images/65 initialization/image9.png)  

![_config.yml]({{ site.baseurl }}/images/65 initialization/image10.png)   

![_config.yml]({{ site.baseurl }}/images/65 initialization/image11.png)  



为了防止激活函数饱和，输入不应该分布在激活函数梯度值太低的位置，对于以0为对称的激活函数，如果输入值为0，激活函数梯度值虽然不为零，但参数梯度值依然为0，参数梯度分布应该均值为0，有一定方差  

为了防止参数梯度为零，各层激活函数不应全部出现饱和现象，各层激活值不全为零，激活值均值在激活函数梯度值高的位置，同时有一定方差(方差不应太大，那会有很大机会落入饱和区域)


![_config.yml]({{ site.baseurl }}/images/65 initialization/image12.png)  

![_config.yml]({{ site.baseurl }}/images/65 initialization/image13.png) 



 
