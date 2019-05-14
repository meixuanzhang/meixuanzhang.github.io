---
layout: post
title: Chapter 3 N-gram Language Models
date:   2019-05-01
categories: 自然语言处理综述
---  

为了计算在history h 条件下word w的发生概率$$P(w\mid h)$$，假设h是its water is so transparent that，我们知道h后面单词是the的概率,h的出现次数，以及h后面但是是the的出现次数则：  

$$
P(the\mid its\ water \ is \ so \ transparent \ that )=\frac{C( its\ water \ is \ so \ transparent \ that \ the)}{C(its\ water \ is \ so \ transparent \ that)}
$$   
C表示出现频次




