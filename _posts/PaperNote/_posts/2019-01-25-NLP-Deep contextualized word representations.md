---
layout: post
title: 读《ELMo Deep contextualized word representations》
date:   2019-01-25
categories: 深度学习
---  

# 概述  

论文提出了deep contextualizedd(基于上下文/语境) word repesentation，它既模拟了(1)词语使用的复杂特征（如句法和语义）,又模拟了(2)这些用法在不同语言环境中的变化（即，对一词多义进行建模）。word vectors是深层双向语言模型（bilm）内部状态的学习函数，该模型对大文本语料库进行了预训练。  

word repesentation通过双向LSTM在大文本语料库上使用coupled language model目标训练获得，因此把这个过程称为ELMo(Embedding from Language Models),ELMo repesentations是深层的，从某种意义上说它是biLM所有内部层的函数，学习了每一个结束任务的输入字上方的向量的线性组合，这比仅使用顶级LSTM层显著提高了性能。

以这种方式组合内部状态获得非常丰富的word repesentation。论文通过内部评估(intrinsic evaluations)表明，较高级别的LSTM状态捕获了与上下文相关的词义方面（例如，它们可以在不修改的情况下使用以在监督的词义消歧任务上有好的表现），而较低级别的状态模拟语法的方面（例如， 它们可用于进行词性标注）。同时暴露所有这些信号是非常有益的，允许学习的模型选择对每个最终任务最有用的半监督类型。
