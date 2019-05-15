---
layout: post
title: Chapter 3 N-gram Language Models
date:   2019-05-01
categories: 自然语言处理综述
---  

# N-gram

为了计算在history h 条件下word w的发生概率$$P(w\mid h)$$，假设h是its water is so transparent that，我们知道h后面单词是the的概率,h的出现次数，以及h后面但是是the的出现次数则：  

$$
P(the\mid its\ water \ is \ so \ transparent \ that )=\frac{C( its\ water \ is \ so \ transparent \ that \ the)}{C(its\ water \ is \ so \ transparent \ that)}
$$   
C表示出现频次 

这种估计联合概率方法非常的麻烦，因此可以根据概率的链规则(chain rule of probability)把这个概率加以分解.

把N个单词的序列$$(w_{1}...w_{n})$$记为$$w_{1}^{n}$$,序列联合概率$$P(X_{1}=w_{1},X_{2}=w_{2}....X_{3}=w_{n})$$记为$$P(w_{1}..w_{n})$$,则：  

$$
P(w_{1}^{n})=P(w_{1},w_{2}..w_{n})\\
=P(w_{1})P(w_{2}\mid w_{1})P(w_{3}\mid w_{1}^2)..P(w_{n}\mid w_{1}^{n-1})\\
=\prod_{k=1}^nP(w_{k}\mid w_{1}^{k-1})
$$

如果计算基于条件概率时，不是考虑全部的history h,而只是考虑最接近该单词的N个单词，从而近似逼近该history h，这就是N-gram模型。  

**N-gram是根据前面出现的N-1个单词估计下一个单词的模型。**一个N-gram模型是包含N个单词的序列，包含2个单词的序列称为biggram,包含3个单词的序列称为trigram。  

这种计算单词序列联合概率的模型又称为**语言模型(language model),简称LM**  

Example: 只通过前面一个单词的条件概率$$P(w_{n}\mid w_{n-1})$$来逼近$$P(w_{n}\ mid w_{1}^{n-1})$$,这是biggram model,。

$$
P(w_{n}\mid w_{1}^{n-1})\approx P(w_{n}\mid w_{n-1})  \\
P(the\mid its\ water \ is \ so \ transparent \ that )\approx  P(the\mid that ) 
$$

一个单词的概率只依赖于它前面的单词的概率这种假设称为马尔可夫假设(Markov assumption)

使用biggram计算单词序列的概率：  

$$
P(w_{1}^n)=\prod_{k=1}^n P(w_{k}\mid w_{k-1})
$$

估计$$P(w_{k}\mid w_{k-1})$$最简单最直观的方法称为最大似然估计(maximum likelihood estimate,MLE),biggram model的MLE参数估计为:   

$$
P(w_{k}\mid w_{k-1})=\frac{C(w_{n-1}w_{n})}{C(w_{n-1})}
$$

N-gram model的MLE参数估计为:  

$$P(w_{n}\mid w_{n-N+1}^{n-1})=\frac{C(w_{n-N+1}^{n-1}w_{n})}{C(w_{n-N+1}^{n-1})}$$  

这个比值称为相对频率relative frequency。

**Estimating the probability as the relative frequency is the maximum likelihood estimate (or MLE ), because this value makes the observed data maximally likely. **

术语：  

语料库：corpora,单数形式是corpus    
type:语料库中不同单数的数目,或者是词汇容量的大小V   
token:语料库全部单词数目，记为N    



N-gram模型依赖训练于训练语料库，训练模型的上下文越长(即N值越大)，句子的连贯性就越好。如果训练集合测试集语料库之间差异非常大，用统计模型预测是完全没有用的。  

由于V无法包括所有的单词，因此会出现unknown word(未知词)，词表以外的词，可以按下面方式处理未知词：  

1、选择词汇：这些词汇是事先确定好的词表  
2、转换:把训练集中没有出现在V词表的单词转换成<UNK>     
3、估计:像计算其他常规词一样计算<UNK>在训练集中的概率   
  
# Evaluating(评估) Language Models 

评估语言模型性能最好的办法是把语言模型嵌入到应用中取，并评估这个应用的总体性能。这种端对端的评估称为外在评估(extrinsic evaluation).  

内在评估(intrinsic evaluation)就是一种与任何应用无关的模型评估方法。

困惑度(perplexit，pp)是评估N-gram模型的一种常见的内在评估度量指标，信息越多(N越大)，困惑度越低。对于测试集$$W=(w_{1}..w_{N})$$,困惑度计算： 

$$
PP(W)=P(w_{1}w{2}...w{N})^{-\frac{1}{N}}\\
=\sqrt[N]{\frac{1}{P(w_{1}w{2}...w{N})}}\\
=\sqrt[N]{\prod_{i=1}^N \frac{1}{P(w_{i}\mid w{1}...w{i-1})}}\\
$$

计算biggram 模型中W的困惑度： 

$$PP(W) =\sqrt[N]{\prod_{i=1}^N \frac{1}{P(w_{i}\mid w{i-1})}}  $$   

在计算概率时，有必要把句子开头标记<s>和结尾标记</s>包括进来。但在词例token N计算总的计数中只包括结尾标记</s>.

# Smoothing(平滑)  

困惑度要求计算每一个测试句子的概率，但如果一个N-gram模型中测试集中有单词从未在训练集中出现过(这里指的不是unknown word)，则涉及这个单词的句子概率最大似然估计将为0.

因此需要修改最大似然估计以计算N-gram 模型中的概率。

##  Laplace Smoothing  

**Add-1 smoothing**  

计算单词$$w_{i}$$概率,$$c_{i}$$是单词计数：

$$
P_{Laplace}(w_{i})=\frac{c_{i}+1}{N+V}
$$

可以使用调整计数$$c*$$来描述平滑算法对分子的影响：  

$$
{c*}_{i}=(c_{i}+1)\frac{N}{N+V} 
$$

这个$$c*$$可以使用N归一化，然后转变为概率$${p*}_{i}$$

可以把平滑看成是打折(discounting),也就是把某个非零的计数降下来，使得到的概率量可指派给那些为零的计数。使用相对折扣$$d_{c}$$(discount)来描述平滑算法： 

$$
d_{c}=\frac{c*}{c}
$$

c*除以N就是平滑后的概率，$$d_{c}$$描述了因为平滑原来c的变化。

biggram 模型平滑概率计算： 

$$
P_{Laplace}(w_{n}\mid w_{n-1})=\frac{C(w_{n-1}w_{n})+1}{C(w_{n-1})+V}
$$

$$
c*(w_{n-1}w_{n})=[C(w_{n-1}w_{n})+1]\frac{C(w_{n-1})}{C(w_{n-1})+V} 
$$ 

对比以下图，单词计数和概率之所以发生这样大的变化，是因为很多的概率量被转移到为零的那些项目当中去了。如果我们不是加一而是加上一个分数，就能够使转移的概率量变小一些，但是这样的方法要求动态选项$$\delta$$,其结果是很多计数出现不恰当的折扣，得到的计数往往带有很糟糕的偏差。

![_config.yml]({{ site.baseurl }}/images/18SpeechAndLanguageProcessing/image1.png)  

![_config.yml]({{ site.baseurl }}/images/18SpeechAndLanguageProcessing/image2.png)   

![_config.yml]({{ site.baseurl }}/images/18SpeechAndLanguageProcessing/image3.png)  

**Add-k smoothing**  

$$
P_{Add-k}(w_{n}\mid w_{n-1})=\frac{C(w_{n-1}w_{n})+k}{C(w_{n-1})+kV}
$$


#and Interpolation插值法 

插值：将不同阶数的N-gram概率估计混合起来。

例如：线性插值法估计$$P(w_{n}\mid w_{n-2}w_{n-1})$$

$$
P(w_{n}\mid w_{n-2}w_{n-1})=\lambda_{1}P(w_{n}\mid w_{n-2}w_{n-1})+\lambda_{2}P(w_{n}\mid w_{n-1})+\lambda_{3}P(w_{n})\\
\sum_{i}\lambda_{i}=1
$$

如果trigram的计数时基于biggram计数的，biggram有精确计数，可以使trigram的$$\lambda$$值更高，插值时给trigram更高的权重：   

$$
P(w_{n}\mid w_{n-2}w_{n-1})=\lambda_{1}(w_{n-2}^{n-1})P(w_{n}\mid w_{n-2}w_{n-1})+\lambda_{2}(w_{n-2}^{n-1})P(w_{n}\mid w_{n-1})+\lambda_{3}(w_{n-2}^{n-1})P(w_{n})
$$

$$\lambda$$值通过保留语料库学习。保留语料库是一个附加的训练语料库，用来设置参数的。


# Backoff回退法 

回退：当阶数较高的N-gram存在零计数时，需要回退到阶数较低的N-gram进行计数。

$$
P_{BO}(w_{n}\mid w_{n-N+1}^{n-1})=\left\{
 \begin{matrix}
  P*(w_{n}\mid w_{n-N+1}^{n-1}),if \ C(w_{n-N+1}^n)>0\\
  \alpha (w_{n-N+1}^{n-1})P_{BO}(w_{n}\mid w_{n-N+2}^{n-1}),otherwise\\
  \end{matrix}
  \right\} 
$$

$$
P*(w_{n}\mid w_{n-N+1}^{n-1})=\frac{c*(w_{n-N+1}^{n-1})}{c(w_{n-N+1}^{n-1})}
$$

# Kneser-Ney Smoothing 

Kneser-Ney 算法根源是一种称为绝对折扣(absolute discounting)的打折方法。

**Interpolated Kneser-Ney：** 

$$
P_{KN}(w_{i}\mid w_{i-n+1}^{i-1})=\frac{max(C(w_{i-n+1}^i)-d,0)}{C(w_{i-n+1}^{i-1})}+\lambda (w_{i-n+1}^{i-1})P_{KN}(w_{i}\mid w_{i-n+2}^{i-1})\\

P_{KN}(w_{i}\mid w_{i-1})=\frac{max(C(w_{i-1}w_{i})-d,0)}{C(w_{i-1})}+\lambda (w_{i-1})P_{CONTINUATION}(w_{i})
$$

$$
\lambda (w_{i-n+1}^{i-1})=\frac{d}{\sum_{w_{i}}C(w_{i-n+1}^{i-1}w_{i})}|\{w_{i}:C(w_{i-n+1}^{i-1}w_{i})>0\}|
$$

$$
P_{CONTINUATION}(w_{i})=\frac{|\{w_{i-1}:C(w_{i-1}w_{i})>0\}|}{\sum_{w_{i}}|\{w_{i-1}:C(w_{i-1}w_{i})>0\}|}
$$


# 熵  

给定随机变量X，及其概率函数P(X),随机变量的熵为：

$$
H(X)=-\sum_{x\in X}P(x)log_{2}P(x)
$$

对数可以使用任何底数，底数是2表示熵是用比特(bit)进行度量。

例子：假设有8匹马，我们想给Yonkers赛马场的赛马下注，但赛马场太远，所以只好通过短信告诉登记赌注的人，我们给哪匹马下注。号码为1的马的二进制代码是001，号码为1的马的二进制代码是010....号码为8的马二进制码是000，每一匹码都用比特编码，一天下来，平均起来每次比赛都要发3比特信息。

$$H(X)=-\sum_{i=1}^{8} \frac{1}{8}log \frac{1}{8}=-log\frac{1}{8}=3bit$$

如果我们根据赌注的实际分布来传送信息，假设每匹马的先验概率及随机变量X的熵如下：  

![_config.yml]({{ site.baseurl }}/images/18SpeechAndLanguageProcessing/image4.jpg)  

每次平均为2比特代码可以这样编码：用最短的代码来表示我们估计概率最大的马，估计概率越小的马，其代码越长，如使用0为估计概率最大的马编码，然后是10，,110,1110,111100,111101,111110,111111

**计算序列的熵:**  

语言L中长度为n的单词一切有限序列的随机变量的熵：  

$$
H(w_{1},w_{2}..w_{n})=-\sum_{W_{1}^n\in L}P(W_{1}^n)logP(W_{1}^n)
$$

熵率(entropy rate)[每个单词的熵]：

$$
\frac{1}{n}H(W_{1}^n)=-\frac{1}{n} \sum_{W_{1}^n\in L}P(W_{1}^n)logP(W_{1}^n)
$$


考虑无限长度的序列，如果把语言想象成产生单词序列的随机过程L，那么熵率H(L)可定义为：

$$
H(L)=-\mathop{lim}_{n\to \infty} \frac{1}{n} H(w_{1},w_{2}..w_{n})\\
=-\mathop{lim}_{n\to \infty} \frac{1}{n}\sum_{W \in L}P(w_{1},w_{2}..w_{n})logP(w_{1},w_{2}..w_{n})
$$
