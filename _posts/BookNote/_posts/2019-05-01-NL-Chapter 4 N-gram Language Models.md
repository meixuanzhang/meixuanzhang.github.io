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

这种估计联合概率方法非常的麻烦，因此可以根据概率的链规则(chain rule of probability)把这个概率加以分解，把N个单词的序列$$(w_{1}...w_{n})$$记为$$w_{1}^{n}$$,序列联合概率$$P(X_{1}=w_{1},X_{2}=w_{2}....X_{3}=w_{n})$$记为$$P(w_{1}..w_{n})$$,则：

$$
P(w_{1}^{n})=P(w_{1},w_{2}..w_{n})\\
=P(w_{1})P(w_{2}\mid w_{1})P(w_{3}\mid w_{1}^2)..P(w_{n}\mid w_{1}^{n-1})\\
=\prod_{k-1}^nP(W_{k}\mid w_{1}^{k-1})
$$




