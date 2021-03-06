---
layout: post
title: 《Visualizing Data using t-SNE》
date:   2019-01-28
categories: 深度学习
---  

# 概述 

t-SNE一种可视化高维数据方法，为每个数据点在二维或三维地图中提供位置。  

# Stochastic Neighbor Embedding(SNE)  

SNE将数据点之间的高维欧氏距离转换为表示相似性的条件概率,数据点$$x_{j}$$到数据点$$x_{i}$$的相似度是条件概率$$P_{j\mid i}$$,如果以$$x_{i}$$为中心的高斯分布下，$$x_{j}$$的概率密度相对较大，$$x_{i}$$选择$$x_{j}$$作为邻近点。对于相邻的数据点，$$P_{j\mid i}$$相对较高，而对于不相邻的数据点，$$P_{j\mid i}$$将几乎无穷小（在选择合理的高斯方差$$\sigma_{i}$$下）。

$$
p_{j\mid i}=\frac{exp(-\parallel x_{i}-x_{j}\parallel^2/2\sigma_{i}^2)}{\sum_{k\ne i }exp(-\parallel x_{i}-x_{k}\parallel^2/2\sigma_{i}^2))}
$$

$$\sigma_{i}$$是以$$x_{i}$$为均值高斯分布的方差。$$\sigma_{i}$$的值不是手动优化或指定的，而是通过二分搜索找到$$\sigma_{i}$$以匹配预先指定的困惑值Perp。

因为只关心成对相似性所以可以把$$p_{i\mid i}$$设置为0。高维度数据点$$x_{i},x_{j}$$在低维度对应点为$$y_{i},y_{j}$$,将低维度的数据条件概率定义为$$q_{j\mid i}$$，将其对应的高斯分布方差设定为$$\frac{1}{\sqrt{2}}$$。  

$$q_{j\mid i}=\frac{exp(-\parallel y_{i}-y_{j}\parallel^2)}{\sum_{k\ne i }exp(-\parallel y_{i}-y_{k}\parallel^2))}$$

同理将$$q_{i\mid i}$$设置为0.

如果$$y_{i},y_{j}$$能在图中正确表示$$x_{i},x_{j}$$相关性，则$$q_{j\mid i}=p_{j\mid i}$$,衡量两个分布的差异可以使用Kullback-Leibler divergence，SNE使用梯度下降法最小化所有数据点Kullback-Leibler散度的总和。  

损失函数为：   

$$C=\sum_{i}KL(P_{i}\parallel Q_{i})=\sum_{i}\sum_{j}p_{j\mid i}log \frac{p_{j\mid i}}{q_{j\mid i}}$$  

$$P_{i}$$表示给定数据点$$x_{i}$$情况下所有其他数据点的条件概率分布  
$$Q_{i}$$表示给定数据点$$y_{i}$$情况下所有其他数据点的条件概率分布    

KL散度具有不对称性，使用相距较远的低维数据点来表示相近的高维数据点，惩罚较小，但使用相距较近的低维数据来表示相远的高维数据点，惩罚较大，如：

$$
q_{j\mid i}=0.2,p_{j\mid i}=0.8,cost=0.8log\frac{0.8}{0.2}=1.11\\
q_{j\mid i}=0.8,p_{j\mid i}=0.2,cost=0.2log\frac{0.2}{0.8}=0.277\\
$$  

SNE损失函数侧重于保留数据的局部结构,低维空间中的聚类应该可解释为在高维空间中也非常相似的数据点

**Perplexity**  

不同$$\sigma_{i}$$对于不同的分布$$P_{i}$$,每个分布会有对应的熵，熵会随着$$\sigma_{i}$$增大而增大，Perplexity和熵关系如下：  


$$Perp(P_{i}) = 2^{H(P_{i})}\\
H(P_{i})=-\sum_{j}p_{j\mid i}log_{2}p_{j\mid i}$$

Perplexity可以解释为对有效邻近点数量的一种平滑测量，设置Perplexity，通过二分搜索找到对应的$$\sigma_{i}$$。  

**梯度计算**  

$$
\frac{\partial C}{\partial y_{i}}=2\sum_{j}(p_{j\mid i}-q_{j\mid i}+p_{i\mid j}-q_{i\mid j})(y_{i}-y_{j})
$$  

为了加快优化速度，避免局部极小值的出现，在梯度上增加了一个相对较大的动量项:  

$$
y^{(t)}=y^{(t-1)}+\eta \frac{\partial C}{\partial y}+\alpha(t)(y^{(t-1)}-y^{(t-2)}) 
$$

$$y^{(t)}$$:第t次迭代的结果    
$$h$$: learning rate(学习率)   
$$\alpha(t)$$:第t次迭代的的momentum    

# t-Stochastic Neighbor Embedding(t-SNE) 

**Symmetric(对称) SNE**  

设置$$p_{ii}=0,q_{ii}=0,p_{ij}=p_{ji},q_{ij}=q_{ji}$$  

$$q_{ij}=\frac{exp(-\parallel y_{i}-y_{j}\parallel^2)}{\sum_{k\ne l }exp(-\parallel y_{k}-y_{l}\parallel^2))}\\
p_{ij}=\frac{exp(-\parallel x_{i}-x_{j}\parallel^2/2\sigma_{i}^2)}{\sum_{k\ne l }exp(-\parallel x_{k}-x_{l}\parallel^2/2\sigma_{i}^2))}
$$   

对称SNE存在问题，当$$x_{i}$$是离群值时，$$p_{ij}$$对于所有的$$j$$会非常的小，在低维图点$$y_{i}$$对损失函数影响非常小，结果是这个点所在位置没有根据其他点位置设置。所以t-SNE修改为：  

$$
p_{ij}=\frac{p_{j\mid i}+p_{i\mid j}}{2n}\\
\sum_{j}p_ {ij}>\frac{1}{2n}
$$

梯度：  

$$\frac{\partial C}{\partial y_{i}}=4\sum_{j}(p_{ij}-q_{ij})(y_{i}-y_{j})$$

**Crowding promblem**  

高维图中邻近关系有时候不能在低维图中保留  

如图，2维图中4个点$$x_{1},x_{2},x_{3},x_{4}$$关系如图，将2维图中点距离关系映射到1维图中，在确定$$x_{1},x_{2},x_{3}$$关系后，$$x_{4}$$无论是放在$$x_{3}$$还是$$x_{1}$$旁边都无法保留2维图中邻近关系，$$x_{4}$$与$$x_{1}$$和$$x_{3}$$的距离应比$$x_{2}$$小


![_config.yml]({{ site.baseurl }}/images/62tSNE/image1.png)

为了解决“Crowding promblem”，Cook et al. (2007)提出加入slight repulsio,即UNI-SNE,但优化中低维度开始距离较远的两个聚类点，后续无法再拉近，论文则提出在低维度中使用t分布，解释参考：  

[t-SNE完整笔记](http://www.datakit.cn/blog/2017/02/05/t_sne_full.html#77)    
[从SNE到t-SNE再到LargeVis](https://bindog.github.io/blog/2016/06/04/from-sne-to-tsne-to-largevis/)

$$q_{ij}$$为：  

$$
q_{ij}=\frac{(1+\parallel y_{i}-y_{j}\parallel^2)^{-1}}{\sum_{k \ne l}(1+\parallel y_{k}-y_{l}\parallel^2)^{-1}}
$$

梯度为：  

$$
\frac{\partial C}{\partial y_{i}}=4\sum_{j}(p_{ij}-q_{ij})(y_{i}-y_{j})(1+\parallel y_{i}-y_{j}\parallel^2)^{-1}
$$



参考： 

[Automatic Selection of t-SNE Perplexity](https://arxiv.org/pdf/1708.03229.pdf)

[Crowding Problem(t-SNE)](https://www.youtube.com/watch?v=hMUrZ708PFk)
