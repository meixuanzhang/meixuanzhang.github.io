---
layout: post
title: week 2 Language Modeling and Spelling Correction
date:   2019-05-01
categories: From Languages to Information
---  

# 3.1 Introduction to N grams  

## Probabilistic Language Models  

计算句子的概率，对于多个句子，机器翻译选择概率更大句子作为翻译结果，拼写更正时选择更正后句子概率更大的更正方式，语音识别时选择概率更大句子作为识别句子

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image46.png)  

计算句子概率或条件概率称为 language model 也可以称为 the grammar

## Compute the probability of a sentence by  Chain Rule 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image47.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image48.png)   


##  无法通过频数计算句子概率，句子组成形式过多  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image49.png)   

 
## Markov Assumption 


![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image50png)   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image51.png)   

**Unigram model**  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image52.png)   

**Bigram model**
  
![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image53.png)   

**N-gram models** 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image54.png)  

一般不使用N很大的models,效率低，使用2,3,4-gram models基本能解决问题


# 3.2 Estimating N gram Probability  

## Estimating bigram probabilities  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image55.png)  

Example 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image56.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image57.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image58.png)   

"i"后面跟随"want" 次数为827

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image59.png)  

**使用Bigram 估计句子概率**  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image60.png)   

## Practical issues 实际应用问题  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image61.png)  

多个小数相乘接近0，会出现下溢问题  

# 3.3Evaluation and Perplexity   

##  如何评估一个模型？  
 
使用训练集训练模型参数  
使用测试集测试模型的表现  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image62.png)  

## Extrinsic(外部) and Intrinsic(内部) evaluation  

Extrinsic 评估需要花费大量时间 

Intrinsic 评估通常在可重现的实验室环境中根据已定义的标准来衡量NLP组件在已定义的子任务上的性能。这里常用的评估方法perplexity  

当测试集和训练集不是来自同一个分布时(不一样时)，perplexity不是很好的评估，所以通常仅在试验性实验中有用   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image63.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image64.png)   

减少perplexity意味增大句子概率

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image65.png)  

假设一个操作可以选择的分支因子(每个结点下的子结点数)，一个操作perplexity=分支因子，有一连串操作,每个操作有不同分支因子，perplexity=标准化长度后的"平均分支因子"(平均每个操作分支因子)？？

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image66.png)   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image67.png)  


# Generalization and Zeros  

生成句子：  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image68.png)   

已知w，计算x取不同值时概率P(w,x)，以P(w,x)最大值时x的取值作为下一个单词  

## The perils of overfitting过拟合  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image69.png)   

有部分词组合没有在训练集出现过概率为0，但测试集实际是存在这样组合概率不应该为0

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image70.png)  

在bigram模型中，在测试集中如果存在条件概率为零，无法计算Perplexity   

