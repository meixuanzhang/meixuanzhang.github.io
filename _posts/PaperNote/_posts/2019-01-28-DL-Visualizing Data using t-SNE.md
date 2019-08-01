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
P_{i\mid i}=\frac{exp(-\parallel x_{i}-x_{j}\parallel^2/2\sigma_{i}^2)}{\sum_{k\ne exp(-\parallel x_{i}-x_{k}\parallel^2/2\sigma_{i}^2))}}
$$





# t-Stochastic Neighbor Embedding(t-SNE) 













参考： 

[Automatic Selection of t-SNE Perplexity](https://arxiv.org/pdf/1708.03229.pdf)