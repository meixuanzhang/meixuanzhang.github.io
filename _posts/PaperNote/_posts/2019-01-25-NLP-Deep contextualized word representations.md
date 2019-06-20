---
layout: post
title: 读《ELMo Deep contextualized word representations》
date:   2019-01-25
categories: 深度学习
---  

# 概述  

论文提出了deep contextualizedd(基于上下文/语境) word repesentation，它既模拟了(1)词语使用的复杂特征（如句法和语义）,又模拟了(2)这些用法在不同语言环境中的变化（即，对一词多义进行建模）。   

传统的repesentation是每个词语对应一个固定repesentation，论文repesentations通过双向LSTM模型使用coupled language model目标在大文本语料库上训练获得，因此称为ELMo(Embedding from Language Models) repesentations。ELMo repesentations从某种意义上说它是biLM所有内部层的函数，学习每个结束任务输入词语上方的向量的线性组合，这比仅使用LSTM顶层显著提高了性能。   

以这种方式组合内部状态获得非常丰富的word repesentation。论文通过内部评估(intrinsic evaluations)表明，较高级别的LSTM状态捕获了与上下文相关的词义方面（例如,它们可以在不修改的情况下使用以在监督的词义消歧任务上有好的表现），而较低级别的状态模拟语法的方面(例如,它们可用于进行词性标注)

# 模型结构  

## Bidirectional LSTM language models 

Notation:    
$$(t_{1}..t_{N}):$$长度为N的语料序列      
$$k:$$表示在序列中的位置    
$$L:$$表示LSTM隐藏层数    
$$j:$$表示LSTM的第j层，$$j=1,..L$$    
$$\overrightarrow{h}_{k,j}^{LM}$$:表示 forward 语言模型第 j 层的第 k 位置的隐藏状态     
$$\overleftarrow{h}_{k,j}^{LM}$$:表示 backward 语言模型第 j 层的第 k 位置的隐藏状态     
$$\overrightarrow{\theta}_{LSTM}:$$forward 语言模型所有参数    
$$\overleftarrow{\theta}_{LSTM}:$$backward 语言模型所有参数    
$$\theta_{x} :$$token(语料) representation(第一层token layer) ,类似embedding matrix,第k个位置token representation用$$h_{k,0}^{LM}$$或$$X_{k}^{LM}$$表示，(forward和backward是同一个参数)   
$$\theta_{s}：$$最后softmax层的参数(forward和backward是同一个参数)   

forward language model:   

$$
p(t_{1},t_{2},...t_{N})=\prod_{k=1}^N p(t_{k}\mid t_{1},t_{2}...t_{k-1})
$$

backward language model:   

$$
p(t_{1},t_{2},...t_{N})=\prod_{k=1}^N p(t_{k}\mid t_{k+1},t_{k+2}...t_{N})
$$  

目标函数：  

$$
\sum_{k=1}^N(logp(t_{k}\mid t_{1},..,t_{k-1};\theta_{x},\overrightarrow{\theta}_{LSTM},\theta_{s})+logp(t_{k}\mid t_{k+1},..,t_{N};\theta_{x},\overleftarrow{\theta}_{LSTM},\theta_{s}))

$$

## ELMo  

ELMo是组合biLM中间层的一项任务

对于每一个语料$$t_{k}$$,通过L-layer biLM计算一组representations:  

$$
R_{k}=\{X_{k}^{LM},\overrightarrow{h}_{k,j}^{LM},\overleftarrow{h}_{k,j}^{LM}\mid j=1,..,L\}\\
=\{h_{k,j}^{LM}\mid j=0,..,L\}\\
h_{k,j}^{LM}=[\overrightarrow{h}_{k,j}^{LM};\overleftarrow{h}_{k,j}^{LM}]\\
h_{k,0}^{LM}=X_{k}^{LM}
$$

对于下游的任务，ELMo需要将所有层折叠成单个向量$$EMLo_{k}=E(R_{k}\theta_{e})$$,最简单的例子是只取最顶层作为最后的repesentation$$E(R_{k})=h_{k,L}^{LM}$$.

更一般的是计算权重对biLM的layer进行组合：   

$$
ELMo_{k}^{task}=E(R_{k}\theta^{task})=\gamma^{task}\sum_{j=0}^L s_{j}^{task}h_{k,j}^{LM}
$$

$$s_{j}^{task}:$$softmax-normalized weights   
$$\gamma^{task}:$$scalar parameter allows the task model to scale the entire ELMo vector   

the activations of each biLM layer have a different distribution, in some cases it also helped to apply layer normalization (Ba et al., 2016) to each biLM layer before weighting.




