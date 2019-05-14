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

**add-1 smoothing**  

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



add-1 smoothing,
add-k smoothing, stupid backoff, and Kneser-Ney smoothing.


