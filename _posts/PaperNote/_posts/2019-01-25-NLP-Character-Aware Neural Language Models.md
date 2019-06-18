---
layout: post
title: 读《Character-Aware Neural Language Models》
date:   2019-01-25
categories: 深度学习
---  

# 概述

论文展示CNN-LSTM结构的神经语言模型，模型的输入是character-level,输出仍然是word-level，word的character是CNN的输入，CNN的输出是LSTM的输入。

# 模型结构  


# Character-level Convolutional Neural Network 

Notation:   
$$C:$$ the vocabulary of characters,词汇的所有字符(字母)   
$$d:$$ 字符embedding的维度    
$$Q\in R^{d*\mid C \mid}:$$matrix character embeddings,字符的embedding矩阵   

假设c


