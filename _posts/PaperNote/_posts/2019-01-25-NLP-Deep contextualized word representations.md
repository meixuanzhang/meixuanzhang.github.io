---
layout: post
title: 读《ELMo Deep contextualized word representations》
date:   2019-01-25
categories: 深度学习
---  

# 概述  

论文提出了deep contextualizedd(基于上下文/语境) word repesentation，它既模拟了(1)词语使用的复杂特征（如句法和语义）,又模拟了(2)这些用法在不同语言环境中的变化（即，对一词多义进行建模）。论文word vectors是学习深层双向语言模型（bilm）内部状态的函数，该模型对大文本语料库进行了预训练。  

传统的repesentation是每个单词对应一个特定repesentation，论文中repesentation是学习整个输入句子的函数，根据输入句子输出单词repesentation。     
word repesentation通过双向LSTM在大文本语料库上使用coupled language model目标训练获得，因此把这个过程称为ELMo(Embedding from Language Models),ELMo repesentations是深层的，从某种意义上说它是biLM所有内部层的函数，学习了每一个结束任务的输入字上方的向量的线性组合，这比仅使用顶级LSTM层显著提高了性能。   

以这种方式组合内部状态获得非常丰富的word repesentation。论文通过内部评估(intrinsic evaluations)表明，较高级别的LSTM状态捕获了与上下文相关的词义方面（例如，它们可以在不修改的情况下使用以在监督的词义消歧任务上有好的表现），而较低级别的状态模拟语法的方面（例如， 它们可用于进行词性标注）。同时暴露所有这些信息是非常有益的，允许学习的模型选择对每个最终任务最有用的半监督特征。

# 模型结构  

## Bidirectional language models 

Notation:
$$(t_{1}..t_{N}):$$长度为N的单词序列  
$$k:$$表示在序列中的位置  
$$L:$$表示LSTM隐藏层数
$$j:$$表示LSTM的第j层，$$j=1,..L$$
$$\vec{h}_{k,j}^{LM}$$:表示 forwardLM 模型第 j 层的第 k 位置的隐藏状态 
$$\cev{h}_{k,j}^{LM}$$:表示 backwardLM 模型第 j 层的第 k 位置的隐藏状态 

forward language model:   

$$
p(t_{1},t_{2},...t_{N})=\prod_{k=1}^N p(t_{k}\mid t_{1},t_{2}...t_{k-1})
$$

backward language model:   

$$
p(t_{1},t_{2},...t_{N})=\prod_{k=1}^N p(t_{k}\mid t_{k+1},t_{k+2}...t_{N})
$$



