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
=\prod_{k-1}^nP(W_{k}\mid w_{1}^{k-1})
$$

如果计算基于条件概率时，不是考虑全部的history h,而只是考虑最接近该单词的N个单词，从而近似逼近该history h，这就是N-gram模型。  

**N-gram是根据前面出现的N-1个单词估计下一个单词的模型。**一个N-gram模型是包含N个单词的序列，包含2个单词的序列称为biggram,包含3个单词的序列称为trigram。  

这种计算单词序列联合概率的模型又称为**语言模型(language model),简称LM**  

Example: 只通过前面一个单词的条件概率$$P(w_{n}\mid w_{n-1})$$来逼近$$P(w_{n}\ mid w_{1}^{n-1})$$,这是biggram model,。

$$
P(w_{n}\ mid w_{1}^{n-1})\approx P(w_{n}\mid w_{n-1})  \\
P(the\mid its\ water \ is \ so \ transparent \ that )\approx  P(the\mid that ) 
$$

一个单词的概率只依赖于它前面的单词的概率这种假设称为马尔可夫假设(Markov assumption)

使用biggram计算单词序列的概率：  

$$
P(w_{1}^n)=\prod_{k-1}^n P(w_{k}\mid w_{k-1})
$$

估计$$P(w_{k}\mid w_{k-1})$$最简单最直观的方法称为最大似然估计(maximum likelihood estimate,MLE),biggram model的MLE参数估计为:   

$$
P(w_{k}\mid w_{k-1})=\frac{C(w_{n-1}w_{n})}{C(w_{n-1})}
$$

N-gram model的MLE参数估计为:  

$$P(w_{n}\mid w_{n-N+1}^{n-1})=\frac{C(w_{n-N+1}^{n-1}w_{n})}{C(w_{n-N+1}^{n-1})}$$  

这个比值称为relative frequency。

**Estimating the probability as the relative frequency is the maximum likelihood estimate (or MLE ), because this value makes the observed data maximally likely. **

术语：  

语料库：corpora,单数形式是corpus   
词汇容量的大小：V，也可以用type或token  
