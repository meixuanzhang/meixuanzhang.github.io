---
layout: post
title: 读《Word Embedding》相关论文(word2vec、Glove)
date:   2019-01-01
categories: 深度学习
---  

**涉及论文：**  

《Efficient Estimation of Word Representations in Vector Space》  
《Distributed Representations ofWords and Phrases and their Compositionality》  
《Distributed Representations of Sentences and Documents》  
《GloVe: Global Vectors forWord Representation》  

# word2vec模型

word2vec模型优点：训练后单向向量能捕获句法信息和单词语义间关系

word2vector总共有两种类型，分别是CBOW(Continuous Bag-of-Words)、Skip-gram,为了减少计算成本每种类型有两种算法策略,分别是Hierarchical Softmax、Negative Sampling。


CBOW是从窗口文本词推出中心词，如假设窗口大小为5，则“我喜欢吃梨”，“我喜吃梨” $$\to$$ “欢”  
Skip-gram是从中心词推出文本词,如“我喜欢吃梨”，“欢” $$\to$$ “我喜吃梨”  

## CBOW模型架构 

![_config.yml]({{ site.baseurl }}/images/15Word Embedding/image1.png)

Notation: 

V:词汇表  
$$W:$$Embedding matrix,维度$$N*V$$  
$$U:$$Embedding matrix,维度$$V*N$$   
$$k:$$是(窗口大小-1)/2   

假设给定一个训练序列$$w_{1},..w_{T}$$,$$w_{i}$$是onehot行向量，其目标函数为

$$L=\frac{1}{T}\sum_{t=k}^{T-k}logP(w_{t}\mid w_{t-k}...w_{t+k})$$

$$P(w_{t}\mid w_{t-k}...w_{t+k})=\frac{e^{y_{w_{t}}}}{\sum_{j}e^{y_{j}}}$$

$$y=b+Uh(w_{t-k}...w_{t+k};W)$$

y是行向量维度为V  

h输出是$$w_{t-k}...w_{t+k}$$在W Embedding matrix 对应vector的均值，是行向量。 

向量在W对应vector计算： 

![_config.yml]({{ site.baseurl }}/images/15Word Embedding/image5.png)


## Skip-gram模型架构   

Notation: 

V:词汇表  
$$W:$$Embedding matrix,维度$$N*V$$  
$$U:$$Context matrix,维度$$V*N$$   
$$c:$$是(窗口大小-1)/2 

![_config.yml]({{ site.baseurl }}/images/15Word Embedding/image3.png)  

![_config.yml]({{ site.baseurl }}/images/15Word Embedding/image2.png)  

假设给定一个训练序列$$w_{1},..w_{T}$$,$$w_{i}$$是onehot行向量，其目标函数为 

$$
L= \frac{1}{T}\sum_{t=1}^{T}\sum_{-c\le j\le c,j\ne 0}logP(w_{t+j}\mid w_{t})
$$

$$
P(w_{t+j}\mid w_{t})=\frac{e^{y_{w_{t+j}}}}{\sum_{j}e^{y_{j}}}
$$  

$$y=b+Uh(w_{t};W)$$  

y是行向量维度为V  

h输出是$$w_{t}$$在W Embedding matrix对应vector，是行向量。 

## 算法

### Hierarchical Softmax  

1、构建Huffman tree  

根据单词在词汇表出现的频率构建Huffman tree。树需要包含所有在词汇表中出现过的单词。例子(假设词汇表大小是8)： 

按频率高到低对单词进行排序  
{and:14,in:7,today:4,fat:3,potato:3,fridge:2,kangaroo:2,zebra:1}  

将频率最低的两个单词进行合并，并重新排序  
{and:14,in:7,today:4,fat:3,potato:3,(kangaroo,zebra):3,fridge:2} 

将频率最低的两个单词或合并词进行合并，并重新排序  
{and:14,in:7,(kangaroo,zebra,fridge):5,today:4,fat:3,potato:3} 

将频率最低的两个单词或合并词进行合并，并重新排序  
{and:14,in:7,(fat,potato):6,(kangaroo,zebra,fridge):5,today:4} 

以此类推就形成图中所示(单词频率越高，越靠近根部)：  

![_config.yml]({{ site.baseurl }}/images/15Word Embedding/image4.png)  

2、计算$$P(w\mid context(w))$$ 或  $$P(context(w)\mid w)$$  


![_config.yml]({{ site.baseurl }}/images/15Word Embedding/image6.png) 

$$w:$$表示中心词  
$$context(w):$$表示窗口文本  

图中$$X$$是Huffman tree输入向量，当我们求解$$P(w\mid context(w))$$时$$X$$为context(w)在W对应vector的均值，求解$$P(context(w)\mid w)$$时$$X$$为中心词$$w$$ 在W对应vector  



$$l^w$$表示从树开始到达底端字 w 时经历的分叉次数，$$d_{j}^w$$表示在第 j 个分叉处选择，例如上图中足球,经历了4次分叉，$$l^w=4$$,每次选择分别是  
$$\{d_{1}^w:1,d_{2}^w:0,d_{3}^w:0,d_{4}^w:1\}$$ 

树每个节点都有一个$$\theta$$向量参数，$$\theta_{j}^{w}$$表示到达单词 w ,经历的第 j 个分叉处的$$\theta$$向量参数

$$P(w\mid context(w))=\prod_{j=1}^{l^w}P(d_{j}^w\mid X;\theta_{j}^{w})$$  

$$P(context(w) \mid w)=\prod_{u\in context(w)}\prod_{j=1}^{l^u}P(d_{j}^u\mid X;\theta_{j}^{w})$$   

$$P(d_{j}^w\mid X_{w};\theta_{j}^{w})=[\sigma(X^T \theta_{j}^{w})]^{1-d_{j}^w}[1-\sigma(X^T \theta_{j}^{w})]^{d_{j}^w}$$  

3、梯度更新参数$$W,\theta$$   

CBOW损失函数：  

$$
L=\frac{1}{T}\sum_{t=k}^{T-k}logP(w_{t}\mid context(w_{t}))
$$


Skip-gram损失函数：  

$$
L= \frac{1}{T}\sum_{t=1}^{T}logP(context(w) \mid w)
$$

CBOW更新了context(w) 在 W 矩阵对应的向量,以及计算过程中涉及的$$\theta$$   
Skip-gram只更新了中心词 w 在 W 矩阵对应的向量,以及计算过程中涉及的$$\theta$$      
最后求得的 W 矩阵就是单词的distributed representation    

### Negative Sampling(NEG)

基础：**Noise contrastive estimation (NCE)**  

假设二分类样本通过以下方式生成，根据$$p(c)$$分布采样，获得一个$$c$$,根据$$\tilde{p}(w \mid c)$$分布采样，获得一个$$w$$，把样本标记为$$D=1$$,根据$$q(w)$$“noise”分布采样，获得$$k$$个$$w$$,把样本标记为$$D=0$$,则：  

$$
p(d,w\mid c)= \left\{ \begin{array}{rl}
& \frac{k}{1+k}*q(w) &if \ d=0\\
& \frac{1}{1+k}*\tilde{p}(w\mid c) &if \ d=1\\
\end{array} \right.
$$  

$$p(d=1,w,c)$$当 d=1 已经确定时，d 与 (w,c) 独立    

$$
p(d=1,w\mid c)=\frac{p(d=1,w,c)}{p(c)}\\
=\frac{p(d=1)p(w,c)}{p(c)}=\frac{p(d=1)p(w\mid c)p(c)}{p(c)}\\
=p(d=1)p(w\mid c)=p(d=1)\tilde{p}(w\mid c)
$$

$$p(w\mid c)$$当 d=0 已经确定时，w 和 c 相互独立   

$$
p(d=0,w\mid c)\\
=p(d=0)p(w\mid c)=p(d=0)q(w)
$$  


因此： 

$$
p(D\mid c,w)=\frac{p(D,w,c)}{p(w,c)}\\
=\frac{\frac{p(D,w,c)}{p(c)}}{\frac{p(w,c)}{p(c)}}\\
=\frac{p(D,w\mid c)}{p(w\mid c)}
$$

$$
p(D=0\mid c,w)=\frac{\frac{k}{1+k}*q(w)}{\frac{1}{1+k}*\tilde{p}(w\mid c)+\frac{k}{1+k}*q(w)}\\
=\frac{k*q(w)}{\tilde{p}(w\mid c)+k*q(w)}
$$


$$
p(D=1\mid c,w)=\frac{\tilde{p}(w\mid c)}{\tilde{p}(w\mid c)+k*q(w)}
$$

损失函数：

$$
L_{NCE_{k}}=\sum_{(w,c)\in D}(logp(D=1\mid c,w)+kE_{\bar{w}\sim q}logp(D=0\mid c,\bar{w}))
$$  

使用Monte Carlo approximation则：

$$
L_{NCE_{k}}^{MC}=\sum_{(w,c)\in D}(logp(D=1\mid c,w)+k*\sum_{i=1,\bar{w_{i}}\sim q}^k \frac{1}{k} logp(D=0\mid c,\bar{w_{i}}))\\
=\sum_{(w,c)\in D}(logp(D=1\mid c,w)+\sum_{i=1,\bar{w_{i}}\sim q}^k logp(D=0\mid c,\bar{w_{i}}))
$$

NCE可以近似为log probability of softmax则：

$$
p(D=1\mid c,w)=\frac{1}{1+e^{-v_{c}v_{w}}}=\sigma(v_{c}v_{w})\\
p(D=0\mid c,w)=\frac{1}{1+e^{v_{c}v_{w}}}=\sigma(-v_{c}v_{w})
$$

$$
L_{NCE_{k}}=\sum_{(v_{w},v_{c})\in D}(log\sigma(v_{c}v_{w})+\sum_{i=1}^kE_{\bar{w_{i}}\sim q}log\sigma(-v_{c}v_{\bar{w_{i}}}))\\
=\sum_{(v_{w},v_{c})\in D}(log\sigma(v_{c}v_{w})+kE_{\bar{w}\sim q}log\sigma(-v_{c}v_{\bar{w}}))\\
=\sum_{(v_{w},v_{c})\in D}(log\sigma(v_{c}v_{w})+\sum_{i=1,\bar{w_{i}}\sim q}^k log\sigma(-v_{c}v_{\bar{w_{i}}}))
$$

**CBOW**  

假设CBOW一组样本为(context(c),w),在Negative Sampling 方法中，$$v_{c}=context(c)$$的均值,$$v_{w}=w$$是中心词。需要对中心词进行负采样。

**Skip-gram**  

假设Skip-gram一组样本为(context(c),w),实际训练样本为$$(w,context(c_{1})),(w,context(c_{2}))...$$,在Negative Sampling 方法$$v_{w}=context(c_{i})$$,$$v_{c}=w$$,需要对$$context(c)$$每个单词进行负采样。

![_config.yml]({{ site.baseurl }}/images/15Word Embedding/image7.png) 

**采样方法**  


$$w_{i}\sim \frac{p(w_{i})^{3/4}}{Z}$$

$$Z=\sum_{i}^V p(w_{i})^{3/4}$$是标准化常数

为了对抗高频词和低频词之间的不平衡，使用简单的subsampling  

$$p(w_{i})=1-\sqrt{\frac{t}{f(w_{i})}}$$

$$f_(w_{i})$$是单词$$w_{i}$$的频率，t是选择阀值，取值围绕在$$10^{-5}$$左右  

对于如何按分布采样参考[MC直接采样](https://meixuanzhang.github.io/ML-Monte-Carlo-method/) 


# doc2vec模型  

通过doc2vec学习文档或段落representation，即Paragraph Vector。 模型结构与word2vector相似。模型使用的算法是Hierarchical Softmax。  

**使用与CBOW类似模型获得Paragraph Vector**  

![_config.yml]({{ site.baseurl }}/images/15Word Embedding/image8.png) 

与训练单词向量不同的是，输入中加入了Paragraph id(对训练文档进行编码1,2,3,...使用one-hot向量表示编码)，同时加入了一个新的矩阵$$D$$,作为，即Paragraph vector matrix,输出target是输入文字的下一个单词，不再是中心词。

$$L=\frac{1}{T}\sum_{t=k}^{T-k}logP(w_{t}\mid d,w_{t-1}..w_{t-k})$$

$$P(w_{t}\mid d,w_{t-1}..w_{t-k})=\frac{e^{y_{w_{t}}}}{\sum_{j}e^{y_{j}}}$$  

$$y=b+Uh(d,w_{t-1}...w_{t-k};D,W)$$  

h输出是$$w_{t-1}...w_{t-k}$$在W Embedding matrix 对应vector值,$$d$$在D Paragraph matrix对应vector值，相加取平均，是行向量。 


**使用与Skip-gram类似模型获得Paragraph Vector**  

![_config.yml]({{ site.baseurl }}/images/15Word Embedding/image9.png) 

输入是Paragraph id，输出是文档中文本。


$$
L= \frac{1}{T}\sum_{t=1}^{T}\sum_{1 \le j\le c,j\ne 0}logP(w_{t+j}\mid d)
$$

$$
P(w_{t+j}\mid d)=\frac{e^{y_{w_{t+j}}}}{\sum_{j}e^{y_{j}}}
$$  

$$y=b+Uh(d;D)$$  

相比起上面方法，这里参数只有$$U,b,D$$,没有$$W$$   

两种方法当有新的文档或段落需要训练时，按顺序接着编码，同时向下增加矩阵D长度，固定$$W,U,b$$，然后更新$$D$$直到收敛，即可获得新文档的Paragraph Vector  
 
# Glove模型  

学习词汇向量空间representation的一些向量算法已经成功捕获了精细化(fine-grained:细粒度）语义和句法规律，但规律起源仍是模糊的。构建word representation主要两类模型结构为：global matrix factorization,local context windows

![_config.yml]({{ site.baseurl }}/images/15Word Embedding/image10.png)  

论文提出的模型结合了两类模型结构的优点，同时为了让词汇向量蕴含某些规律，分析和明确了模型应具有哪些属性。

语料库word occurrences统计是非监督学习word representation的主要信息来源，现在已经存在很多方法利用统计信息构建word representation的方法，它们解决的问题是统计蕴含了什么意义，word vector是怎样代表了这些意义。论文提出了GloVe模型，模型直接捕获了语料库统计信息  

**模型构建**  

Notation:   
$$X_{ij}$$:word j 出现在word i context的频数。单词 i context 指的是在整个语料中以 i 为中心词的窗口范围内在出现的所有文本    
$$X_{i}=\sum_{k}X_{ik}$$: i context 的所有文本量  
$$P_{ij}=P(j\mid i)=X_{ij}/X_{i}$$: word j 出现在 i context里的概率   

下图为词汇 ice 和 steam 的共现概率矩阵，k代表是context。  
从图中观察发现，当k=water或k=fashion时，$$P(k\mid ice)$$和$$P(k\mid steam)$$概率大小相等，意味这两个词汇出现在ice,steam context的概率是相等的，k 与 i,j要么都相关，要么都不相关，此时$$P(k\mid ice)/P(k\mid steam)$$接近1。    
当k=solid时，k与ice相关，但与steam不太相关，此时ratio较大。   
当k=gas时，k与steam相关，但与ice不太相关，此时ratio就比较小。  
通过ratio可以区分出与i或 j相关的词，以及与i,j都相关或都不相关的词。此外ratio一定程度区分了相关词差异如(solid,gas)。   



![_config.yml]({{ site.baseurl }}/images/15Word Embedding/image11.png)    

我们希望构建模型通过词汇向量空间捕获词汇间(i,j,k)ratio信息：  

$$F(w_{i},w_{j},\bar{w_{k}})=\frac{P_{ik}}{P_{jk}}$$  

注意这里$$w_{i},w_{j}$$与$$w_{k}$$是来自不同的向量空间

由于向量空间是线性结构，又希望通过F编码能在词汇向量空间中呈现ratio的信息,所以(这个理由有点跳跃..可能ratio信息呈现出了i，j词汇差异在 k 上表现)：  

$$F(w_{i}-w_{j},\bar{w_{k}})=\frac{P_{ik}}{P_{jk}}$$

ratio是常量，我们希望F输出结果是常量，F可能是非常复杂的结构如神经网络，但是上式F输入会模糊了想要捕获的线性信息(如：king-queen=man-woman),混合了向量维度(向量每个维度代表信息类型不一致,如所有向量维度1都应该代表同一类信息如：积极或消极)，所以：

$$F((w_{i}-w_{j})^T \bar{w_{k}})=\frac{P_{ik}}{P_{jk}}$$

这样向量维度之间计算一一对应(个人理解)，由于共现矩阵，context和中心词互换是不会改变两个词汇间共现频率的，就是 i 是 j 的context,j是中心词，共现频率是n,反过来 j 是 i 的cotext ，i,j共现频率依然是n。 

![_config.yml]({{ site.baseurl }}/images/15Word Embedding/image12.png) 

上一个式子没有体现出这种对称的信息,因为交换位置后ratio就不同了,如：

$$F(\bar{w_{k}}^T w_{i}-w_{j}^T\bar{w_{k}})=\frac{P_{ki}}{P_{jk}}$$

对称性通过两步实现，首先需要F是homomorphism，所以 ：

$$F((w_{i}-w_{j})^T \bar{w_{k}})=\frac{F(w_{i}^T \bar{w_{k}})}{F(w_{j}^T \bar{w_{k}})}\\
F(w_{i}^T \bar{w_{k}})=P_{ik}=\frac{X_{ik}}{X_{i}}\\
F=exp\\
w_{i}^T \bar{w_{k}}=log(P_{ik})=log(X_{ik})-log(X_{i})\\
$$


![_config.yml]({{ site.baseurl }}/images/15Word Embedding/image13.png)      
![_config.yml]({{ site.baseurl }}/images/15Word Embedding/image14.png)     

假设去掉末尾项$$log(X_{i})$$,式子就具有对称性，$$w_{i}$$和$$\bar{w_{k}}$$对换,不会改变ratio,由于$$log(X_{i})$$与k是独立的，所以可以将这项信息吸收到$$w_{i}$$偏差$$b_{i}$$里，同时加入$$\bar{w_{k}}$$偏差$$\bar{b_{k}}$$，这样就保持了对称性：

$$w_{i}^T\bar{w_{k}}+b_{i}+\bar{b_{k}}=log(X_{ik})$$   

上式存在一个问题，当$$X_{ik}=0$$时结果是发散的，无穷小，同时对于共现频数大和频数小词汇权重是一样的，但共现频数大的词汇信息高于共现频数小的，所以提出加入weight function $$f(X_{ik})$$

$$
J=\sum_{i,k=1}^V f(X_{ij})(w_{i}^T \bar{w_{k}}+b_{i}+\bar{b_{k}}-logX_{ik})^2
$$

weight function 需要满足三个条件：

当$$X_{ik}=0$$时，$$f(0)=0$$   

$$f(X_{ik})$$应该是非递减的，这样小共现词汇的权重不会过大(递减意味越小的$$X_{ik}$$权重越大)   

$$f(X_{ik})$$对于大共现词汇，权重不应该过大。后面这两个条件体现对于大共现词汇权重应高于小共现词汇，但差距不应该过大。    

V是词汇量数  

所以,当$$X_{ik}$$不为零时：

$$
f(x)= \left\{ \begin{array}{rl}
& (x/x_{max})^{\alpha} &\qquad if \ x < x_{max}\\
& 1 &\qquad otherwise\\
\end{array} \right.
$$

图中j是式子k: 

![_config.yml]({{ site.baseurl }}/images/15Word Embedding/image15.png)

论文中$$x_{max}=100$$  

# 评估word representation好坏

总的来说有两类方法：Intrinsic Evaluation 和 Extrinsic Evaluation

**Extrinsic Evaluation**  

借助任务对word representation进行评估，将word representation应用到任务中(如情绪分类)，评估任务的好坏作为word representation表现评估。

**Intrinsic Evaluation**

不借助任务进行评估，通常评估方法有 Word Analogies、Word Correlation

**向量类比（word vector analogies）**: 它评估了一组词向量在语义和句法上表现出来的线性关系

![_config.yml]({{ site.baseurl }}/images/15Word Embedding/image17.png)

$$\vec{OB}-\vec{{OA}=\vec{AB}\\
\vec{OC}+\vec{AB}=\vec{OX'}$$

根据线性关系$$\vec{OX'}$$应该与$$\vec{OX}$$相似，两个向量相似性作为word representation评估 

**Word Correlation** : 将词向量相似性与人打分进行对比。

![_config.yml]({{ site.baseurl }}/images/15Word Embedding/image16.png)

参考：  
[Learning Word Embedding](https://lilianweng.github.io/lil-log/2017/10/15/learning-word-embedding.html)   
[Hierarchical Softmax](http://building-babylon.net/2017/08/01/hierarchical-softmax/)  
[Notes on Noise Contrastive Estimation and Negative Sampling](http://demo.clab.cs.cmu.edu/cdyer/nce_notes.pdf)  
[Noise-contrastive estimation: A new estimation principle for unnormalized statistical models](http://proceedings.mlr.press/v9/gutmann10a/gutmann10a.pdf) 
[Understanding GloVe](https://www.slideshare.net/JiHyunPark18/understanding-glove)



