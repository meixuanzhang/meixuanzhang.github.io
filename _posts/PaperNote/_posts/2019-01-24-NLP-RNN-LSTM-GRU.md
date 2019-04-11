---
layout: post
title: RNN、LSTM、GRU
date:   2019-01-24
categories: 深度学习
---  

**来源论文**    
《A Critical Review of Recurrent Neural Networks for Sequence Learning》

# 概述
feedforward neural network假设输入样本间是独立同分布的，在处理完一个样本(数据点)之后，网络会丢失样本整个状态信息，然后再处理下一个样本，如果每个样本都是独立生成的，则没问题。 但如果样本在时间或空间上相关(样本之间不独立)，则不符合假设。   
feedforward neural network每次输入，输出长度是固定的。不能很好对输入，输出长度不固定情境建模。  

为了能对具有时间或序列结构的数据及输入和输出长度不固定的情境进行建模，产生了RNNs(Recurrent neural networks)。   
递归神经网络（RNN）具有选择性地跨序列传递信息的能力。 因此可以对输入或输出由不独立的元素序列组成的数据建模。    

#RNN

