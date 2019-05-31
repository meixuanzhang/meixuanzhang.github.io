---
layout: post
title: 读《Learned in Translation ContextualizedWord Vectors》
date:   2019-01-25
categories: 深度学习
---  

# 概述  

在计算机视觉中，convolutional neural networks (CNNs)通过在ImageNet(数据集)进行预训练，然后迁移到其他计算机视觉任务中，获得了非常好的效果。

论文使用deep LSTM encoder(编码器)，获得带有语境的词向量(contextualize word vectors)，编码器是通过训练机器翻译任务attentional sequence-to-sequence model中获得。论文主要关注通过大型NLP任务训练编码器，将编码器迁移到其他任务中(迁移学习)。  


