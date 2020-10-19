---
layout: post
title: Adaboost GradientBoost Xgboost LightGBM Catboost
date:   2019-01-28
categories: 机器学习
---  

提升方法（Boosting），是一种可以用来减小监督式学习中偏差的机器学习算法。

# Adaboost  

![_config.yml]({{ site.baseurl }}/images/86Boost/image1.png)   

AdaBoost algorithm advantages:  

1、很好地利用弱分类器进行组合   
2、可以将不同的分类算法作为弱分类器   
3、adaboost具有很高的精度   
4、相对于bagging算法和随机森林算法，adaboost充分考虑了各分类器的权重；  

Adaboost algorithm disadvantages:    

1、adaboost迭代次数也是弱分类器集合数目,需通过交叉验证来确定；   
2、数据不平衡导致分类精度下降；  
3、训练很费时,每次需要重新选择当前分类最好切分点；   
 
# Gradient Boosting    

![_config.yml]({{ site.baseurl }}/images/86Boost/image2.png)   

Gradient Boosting  advantages:     

1、预测准确性高。   
2、由于树是通过优化目标函数得出的，因此基本上GBM可以用于求解几乎所有我们可以写出梯度的目标函数。  

Gradient Boosting disadvantages:     

1、如果数据有噪声，GBM对过拟合更敏感。   
2、训练通常需要更长的时间，因为树是按顺序构建的。   
3、GBM比RF更难调谐。通常有三个参数：树的数量、树的深度和学习率，并且每棵树的构建通常都是浅层的。  

criterion(分枝标准)

‘mse’：mean squared error   

‘mae’：mean squared error   

**‘friedman_mse’**   

$$p_{k} \in [0,1)$$   

$$w_{left}=\sum_{i\in R_{l}}w_{l}(x_{i})=\sum_{i\in R_{l}}p_{k}(x_{i})(1-p_{k}(x_{i}))$$  

每个$$x_{i}$$属于一个特定的类别 k-class  

Least-Squares Improvement Criterion：  

$$i^2(R_{l},R_{r})=\frac{w_{left}w_{right}}{w_{left}+w_{right}}(y_{lmean}-y_{rmean})$$




# LightGBM    

## histogram-based algorithms    

![_config.yml]({{ site.baseurl }}/images/86Boost/image5.png)  

LightGBM使用基于直方图的算法,该算法将连续特征（属性）值存储到离散的bin中。这样可以加快培训速度并减少内存使用量。基于直方图的算法的优点包括:    

1、降低了计算每个分割增益的成本,一旦构造了直方图，基于直方图的算法具有时间复杂度O(#bin)，比O(#data)小得多。   
2、使用直方图减法进一步加速,二叉树中获取子节点的直方图，只需要为一个子节点构造直方图， 然后可以使用父节点直方图减法刚构造的子节点直方图,获得另一个子节点的直方图   
3、减少内存使用，用离散的bin替换连续的值。 如果#bins较小，则可以使用较小的数据类型，例如 uint8_t，用于存储训练数据   
4、无需存储额外信息即可对特征值进行预排序    
5、降低并行学习的通信成本   

## GOSS: reduce data size by rows  

GOSS keeps all the instances with large gradients and performs random sampling on the instances
with small gradients.保留所有具有大梯度的实例，并对具有小梯度的实例执行随机采样。  

![_config.yml]({{ site.baseurl }}/images/86Boost/image6.png)  

流程：  

1、根据梯度绝对值以降序对样本进行排序   
2、选择排序前a* 100%的样本。  
3、从其余数据中随机抽样b * 100%个样本。 这将减少训练较好的样本的贡献。   
4、如果没有第3点，则具有较小梯度的样本数将为1-a（当前为b）。 为了保持原始分布，LightGBM通过恒定(1-a)/b放大具有小梯度的样本的贡献，从而将更多精力放在训练不足的实例上，而不会太大地改变数据分布。   


## EFB: reduce data size by columns  

The sparsity of the feature space provides us a possibility of designing a nearly lossless approach to reduce the number of features. Specifically, in a sparse feature space, many features are mutually exclusive, i.e., they never take nonzero values simultaneously.特征之间若存在某特征取非零值时，部分特征取值一定为零，可以将这些特征合并。  

![_config.yml]({{ site.baseurl }}/images/86Boost/image7.png)  

**Identifying features that could be bundled together**  

1、Construct a graph with weighted (measure of conflict between features) edges. Conflict is measure of the fraction of exclusive features which have overlapping non zero values. 特征非零值重叠程度     
2、Sort the features by count of non zero instances in descending order.  
3、Loop over the ordered list of features and assign the feature to an existing bundle (if conflict < threshold) or create a new bundle (if conflict > threshold).   

**Algorithm for merging features**  

![_config.yml]({{ site.baseurl }}/images/86Boost/image10.png)  


## Leaf-wise (Best-first) Tree Growth

大多数决策树学习算法都是按 level (depth)-wise来生长树，如下图所示：   

![_config.yml]({{ site.baseurl }}/images/86Boost/image8.png)  

LightGBM以 leaf-wise的方式生长树。它将选择具有最大增量损失的叶子来生长。 保持#leaf固定，leaf-wise算法往往比level-wise算法获得更低的损失。
当#data较小时，leaf-wise可能会导致过度拟合，因此LightGBM包含max_depth参数以限制树的深度。
![_config.yml]({{ site.baseurl }}/images/86Boost/image9.png)  
 
## Optimal Split for Categorical Features  

使用one-hot encoding来表示分类特征是很普遍的，但是这种方法对于树模型而言不是最理想的。 特别是对于高维度的分类特征，基于one-hot encoding表示分类特征的树倾向于不平衡，并且需要生长到非常深才能获得良好的精度。     

相比起one-hot encoding，最佳解决方案是将类别特征进行拆分为2个子集。 如果特征具有$$k$$个类别，则存在$$2^{(k-1 )}-1$$个可能的分区。 但是对于回归树有一个有效的解决方案。它需要大约$$O(k*log(k))$$来找到最佳分区。基本思想是根据训练目标对类别进行分类。 LightGBM根据其累积值（sum_gradient / sum_hessian）对直方图（用于分类特征）进行排序，然后在排序的直方图上找到最佳分割。

## Optimization in Parallel Learning

**Feature Parallel**   

特征并行旨在并行化决策树中的“查找最佳拆分”。 传统特征并行的过程是：  

1、Partition data vertically (different machines have different feature set).垂直分区：把特定的列划分到特定的分区，减少表的宽度，每个分区都保存了其中列所在的行。  
2、Workers find local best split point {feature, threshold} on local feature set.局部特征集上找到局部最佳分割点{特征，阈值}。  
3、Communicate local best splits with each other and get the best one.相互交流局部最佳分割点并获得全局最佳分割点。  
4、Worker with best split to perform split, then send the split result of data to other workers.根据最好分割点分割数据，并将分割数据结果(行索引分割结果)发送给其他工作程序。  
5、Other workers split data according to received data.根据接收到的分割数据结果进行下一次分割。  

传统功能并行的缺点：

1、Has computation overhead, since it cannot speed up “split”, whose time complexity is O(#data). Thus, feature parallel cannot speed up well when #data is large.因为它不能加速“拆分”，其时间复杂度为O（#data）。 因此，当#data很大时，特征并行不能很好地加速。   
2、Need communication of split result, which costs about O(#data / 8) (one bit for one data).  需要将分割结果的传递，其成本约为O（#data / 8）（一个数据一位）。

**Feature Parallel in LightGBM：**  

由于#data很大时，Feature Parallel无法很好地加速，LightGBM做了一些改动：不是垂直划分数据，而是每个Workers都保存了全部数据。LightGBM不需要就数据拆分结果进行交流，因为每个Workers都知道如何拆分数据。 而且#data不会更大，因此在每台计算机上保存完整数据是合理的。


流程： 

1、Workers find local best split point {feature, threshold} on local feature set.   
2、Communicate local best splits with each other and get the best one.   
3、Perform best split.   

这种特征并行算法在数据量大的情况下仍然存在“分割”的计算开销。

**Data Parallel**   

传统数据并行化旨在并行化整个决策学习。 数据并行的过程是：  

1、Partition data horizontally.水平分区：对表的行进行分区，不同分组中物理分隔的数据组合在一起，表中的所有列都可以在每个分区找到，维持了表的属性结构。  
2、Workers use local data to construct local histograms.使用局部数据，构建局部直方图
3、Merge global histograms from all local histograms.合并所有局部直方图获得全局直方图
4、Find best split from merged global histograms, then perform splits.从合并的全局直方图中找到最佳分割，然后执行分割。

**Data Parallel in LightGBM：**

LightGBM uses “Reduce Scatter” to merge histograms of different (non-overlapping) features for different workers.Then workers find the local best split on local merged histograms and sync up the global best split.    
As aforementioned, LightGBM uses histogram subtraction to speed up training. Based on this, we can communicate histograms only for one leaf, and get its neighbor’s histograms by subtraction as well.


**Missing Value Handle**  

1、LightGBM enables the missing value handle by default. Disable it by setting use_missing=false.   
2、LightGBM uses NA (NaN) to represent missing values by default. Change it to use zero by setting zero_as_missing=true.    
3、When zero_as_missing=false (default), the unshown values in sparse matrices (and LightSVM) are treated as zeros.   
4、When zero_as_missing=true, NA and zeros (including unshown values in sparse matrices (and LightSVM)) are treated as missing.   

参考：  
[ LightGBM Document](https://lightgbm.readthedocs.io/en/latest/Features.html#optimal-split-for-categorical-features)
[What makes LightGBM lightning fast?](https://medium.com/@abhisheksharma_57055/what-makes-lightgbm-lightning-fast-a27cf0d9785e)  
[Tree Series 2: GBDT, Lightgbm, XGBoost, Catboost](https://yanpuli.github.io/posts/2018/05/blog-post-13/)



# Catboost   

Prediction shift:预测靠近数据集中的数据远离真实值时，称为预测转移

**Handling Categorical Features.**

A categorical feature is one with a discrete set of values called categories that are not comparable to each other. One popular technique for dealing with categorical features in boosted trees is one-hot
encoding ,for each category, adding a new binary feature indicating it.  
However, in the case of high cardinality features (like, e.g., “user ID” feature), such technique leads to infeasibly large number of new features.   
To address this issue, one can group categories into a limited number of clusters and then apply one-hot encoding. A popular method is to group categories by target statistics (TS) that estimate expected target value in each category.
(对于高维度的分类特征，one-hot会产生很多新的稀疏特征，因此将分类变量转换为与目标变量相关的统计量)   

这种方式会导致过拟合的问题，假设将分类变量转换为对应目标变量的均值，如果一个特征的一个取值只有一个样本，则它的值会完全等于目标变量，这导致目标泄露，训练时导致过拟合。

Catboost使用ordered TS :   

The values of TS for each example rely only on the observed history. Catboost introduce an artificial “time”, a random permutation $$\sigma$$ of the training examples.  对样本进行随机排序  
Then, for each example, we use all the available “history” to compute its TS, i.e., take $$D_{k} = \{x_{j}:\sigma(j)<\sigma(k) \} $$in Equation:

![_config.yml]({{ site.baseurl }}/images/86Boost/image11.png)  

选择排在样本$$x_{j}$$前与其取值相等的样本，计算统计量。

if we use only one random permutation,then preceding examples have TS with much higher variance than subsequent ones. To this end, CatBoost uses different permutations for different steps of gradient boosting

**ordered boosting**   

![_config.yml]({{ site.baseurl }}/images/86Boost/image13.png)  
![_config.yml]({{ site.baseurl }}/images/86Boost/image12.png)  

Step 1: Calculate residuals for each datapoint using a model that has been trained on all the other data points at that time (For Example, to calculate residual for x5 datapoint, we train one model using x1, x2, x3 and x4 ). Hence we train different models for different data points . At the end we are calculating residuals for each datapoint that it’s corresponding model has never seen that datapoint before.  
Step 2: train the model using the residuals of each datapoint   
Step 3: Repeat Step 1 & Step 2 (for n iterations)   

这里有多少个样本就需要构建多少个M，为此对算法改进，构建的M个数为$$log_{2}^n$$.

For the above toy dataset, we should train 9 different models to get residuals for 9 data points. This is computationally expensive when we have more number of data points. Hence by default, instead of training different model for each datapoint, it trains only log(num_of_datapoints) models. Now if a model has been trained on n data points then that model is used to calculate residuals for the next n data points.
A model that has been trained on first data point is used for calculating residuals of second data point.第一个样本训练，计算第二个样本残差  
An another model that has been trained on the first two data points is used for calculating residuals of third and fourth data points。前两个样本训练，计算第三、四样本残差
and so on…   
In the above toy dataset, now we calculate residuals of x5,x6,x7 and x8 using a model that has been trained on x1, x2,x3 and x4.前四个样本训练，计算后四个样本残差
All this procedure that I have explained until now is known as ordered boosting.



[What’s so special about CatBoost?](https://medium.com/@hanishsidhu/whats-so-special-about-catboost-335d64d754ae)
 
