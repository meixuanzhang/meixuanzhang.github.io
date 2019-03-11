---
layout: post
title: MCMC采样方法：MH、GibbSample
date:   2019-01-01
categories: 
---

# MCMC方法(Markov Chain Monte Carlo)
马尔可夫链蒙特卡罗（MCMC）方法包括一类用于从概率分布中采样的算法。通过构建一条马尔可夫链，它的平稳分布是所需分布(要采样的概率分布)，通过观察马尔可夫链随机过程，从而获得所需分布的样本。    
这条马尔可夫链的平稳分布是$$\pi_{x}$$，平稳分布对应的转移概率为P，任意初始状态分布x经过n次迭代后会收敛于$$\pi_{x}$$,我们可以通过P进行采样，但是P未知,我们需要找打合适的P。  
目前常用MCMC采样方法有Metropolis-Hastings、Gibb Sample。   

# Metropolis-Hastings  
**Notation:**    
$$P(x)=\pi_{x}$$：所需分布(要采样的概率分布)、马尔可夫链平稳分布  
$$P(y \mid x)$$：$$P(x)$$作为平稳分布的马尔可夫链的转移概率分布  
$$g(y \mid x)$$：候选的转移概率分布(proposal distribution)  
$$A$$：接受移动率(acceptance ratio)  

目前已知马尔可夫链平稳分布$$\pi_{x}=P(x)$$,希望通过$$P(y \mid x)$$转移概率分布进行采样，因$$P(y \mid x)$$未知，所以提出$$g(y \mid x)$$作为候选的转移概率分布。通过候选分布进行采样。

真实转移概率分布应满足：  

$$P(y \mid x)P(x)=P(x|y)P(y)$$   

左边表示从 x 移动到 y 的非条件概率,x是从$$\pi$$生成的,右边表示从y 移动到 x的非条件概率（y是从$$\pi$$生成的），两个概率相等   

候选分布未必满足$$g(y\mid x)P(x)=g(x\mid y)P(y)$$，即x 移动到 y的频率与y 移动到 x频率不相等，因此引入A接受移动率。$$A \le 1$$。通过调节使两边相等：  

$$A(x,y)g(y \mid x)P(x)=A(y,x)g(x|y)P(y)$$

A(x,y):x移动到y的接受率    
A(y,x):y移动到x的接受率   

当$$g(y \mid x)P(x)>g(x\mid y)P(y)$$,意味使A(y,x)尽量大，A最大值是1，所以：   

$$A(y,x)=1,A(x,y)=\frac{P(y)g(x \mid y)}{P(x)g(y \mid x)}$$  

当$$g(y \mid x)P(x)<g(x\mid y)P(y)$$,意味使A(x,y)尽量大，A最大值是1，所以：   

$$A(x,y)=1,A(y,x)=\frac{P(x)g(y \mid x)}{P(y)g(x \mid y)}$$  

因此：  

$$A(x,y)=min(1,\frac{P(y)g(x \mid y)}{P(x)g(y \mid x)})$$    


流程：  
1、Generate：从$$g(y\mid x)$$分布中生成一个候选样本$$y$$    
2、Calculate:计算接受率$$A(x,y)=min(1,\frac{P(y)g(x \mid y)}{P(x)g(y \mid x) })$$  
3、Accept or Reject：是否接受从x移动到y     
+ 从[0,1]均匀分布中生成样本u
+ 如果$$u \le A(x,y)$$,则接受$$x_{t+1}=y$$
+ 如果$$u > A(x,y)$$,则拒绝，$$x_{t+1}=x$$

4,Increment：设t=t+1

参考：    
[Understanding the Metropolis-Hastings Algorithm](https://eml.berkeley.edu/reprints/misc/understanding.pdf)  

# Gibbs Sample    
Gibbs Sample 是从多元概率分布采样。 假设我们想从多元概率分布$$P(x_{1}..x_{n})$$抽取k个$$X=(x_{1}...,x_{n})$$样本。将$$X_{(i)}=(x_{1}^{(i)}....x_{n}^{(i)})$$设为抽取第i个样本。     
流程：  
1、随机初始化样本$$X^{(i)}$$   
2、想获得下一个样本$$X^{(i+1)}$$。由于$$X^{(i+1)}=(x_{1}^{(i+1)},x_{2}^{(i+1)},...x_{n}^{(i+1)})$$是一个向量，需要对每个元素$$x_{j}^{(i+1)}$$ 进行抽样。$$x_{j}^{(i+1)}$$ 基于$$X_{(i+1)}$$和$$X_{i}$$元素条件概率分布$$P(x_{j}^{(i+1)} \mid x_{1}^{(i+1)},...,x_{j-1}^{(i+1)},x_{j+1}^{(i)}..x_{n}^{(i)})$$。    
3、重复上述步骤k次    

**证明**    

$$P(X)$$：所需分布(要采样的概率分布)、马尔可夫链平稳分布$$X=(x_{1}...,x_{n}),X \in \theta$$    
$$P_{XY}$$：$$P(X)$$作为平稳分布的马尔可夫链的转移概率分布  

$$P(x_{j} \mid x_{1},..,x_{j-1},x_{j+1},..x_{n})=\frac{P(x_{1},...x_{n})}{P(x_{1},..,x_{j-1},x_{j+1},..x_{n})}\\
=\frac{P(x_{1},...x_{n})}{\sum_{x_{j}}P(x_{1},..,x_{j-1},x_{j},x_{j+1},..x_{n})}\propto P(x_{1},...x_{n})$$

分母与$$x_{j}$$取值无关相当于一个常量

1、随机选取index,$$1 \le j \le n$$   
2、根据$$P(x_{1},..x_{j-1},\cdot ,x_{j+1},..x_{n})$$,为$$x_{j}$$选择一个新的值,这里相当于根据转移概率分布选择新值

这两步定义了可逆的马尔科夫链，平稳分布是P(X)。证明：  

假设有两个变量$$X,Y,X \in \theta ,Y \in \theta , X \sim_{j}Y$$(X,Y向量里除了第j个元素不确定外，两个向量其他元素一定相等)，从X转移到Y有：

$$
P_{XY}= \left\{ \begin{array}{rl}
\frac{1}{d}\frac{P(Y)}{\sum_{Z \in \theta:Z \sim_{j}X}P( Z)} & X \sim_{j}Y\\
0 &\mbox{ otherwise}
\end{array} \right.
$$

$$
P(X)P_{XY}=\frac{1}{d}\frac{P(X)P(Y)}{\sum_{Z \in \theta:Z \sim_{j}X}P( Z)}\\
=\frac{1}{d}\frac{P(Y)P(X)}{\sum_{Z \in \theta:Z \sim_{j}Y}P( Z)}\\
=P(Y)P_{YX}
$$

In practice, the index j. is not chosen at random, and the chain cycles through the indexes in order. In general this gives a non-stationary Markov process, but each individual step will still be reversible, and the overall process will still have the desired stationary distribution (as long as the chain can access all states under the fixed ordering).


参考：  
[Gibbs sampling-wiki](https://en.wikipedia.org/wiki/Gibbs_sampling#Variations_and_extensions)
