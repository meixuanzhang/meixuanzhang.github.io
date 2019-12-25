---
layout: post
title: week 2 Language Modeling and Spelling Correction
date:   2019-05-01
categories: From Languages to Information
---  

# 3.1 Introduction to N grams  

## Probabilistic Language Models  

计算句子的概率，对于多个句子，机器翻译选择概率更大句子作为翻译结果，拼写更正时选择句子更正后概率更大的更正方式，语音识别时选择概率更大的句子作为识别句子

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image46.png)  

计算句子概率或条件概率称为 language model 也可以称为 the grammar

## Compute the probability of a sentence by  Chain Rule 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image47.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image48.png)   


##  无法通过频数计算句子概率，句子组成形式过多  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image49.png)   

 
## Markov Assumption 


![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image50.png)   

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

## Example 

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

评估一个模型:使用训练集训练模型参数,使用测试集测试模型的表现   

## Extrinsic(外部) evaluation of N-gram models

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image62.png)  

## Intrinsic(内部) evaluation  

Extrinsic 评估需要花费大量时间 

Intrinsic 评估通常在可重现的实验室环境中根据已定义的标准来衡量NLP组件在已定义的子任务上的性能。这里常用的评估方法perplexity  

当测试集和训练集不是来自同一个分布时(不一样时)，perplexity不是很好的评估，所以通常仅在试验性实验中有用   

**perplexity**   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image63.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image64.png)   

减少perplexity意味增大句子概率

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image65.png)  

假设一个操作可以选择的分支因子(每个结点下的子结点数)，一个操作perplexity=分支因子，有一连串操作,每个操作有不同分支因子，perplexity=标准化长度后的"平均分支因子"(平均每个操作分支因子)？？

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image66.png)   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image67.png)  


# 3.4Generalization and Zeros  

**句子生成：**  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image68.png)   

已知w，计算x取不同值时概率P(w,x)，以P(w,x)最大值时x的取值作为下一个单词  

## The perils of overfitting过拟合  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image69.png)   

有部分词组合没有在训练集出现过概率为0，但测试集实际是存在这样组合概率不应该为0  

## Zero probability bigrams

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image70.png)  

在bigram模型中，在测试集中如果存在条件概率$$P(w_{1}\mid w_{2})$$为零，无法计算Perplexity   

# 3.5 Smoothing Add One   

## The intuition of smoothing(from Dan Klein)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image71.png)  

每个词都增加同样的频次    

## Add-one estimation  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image72.png) 

每个词都增加1个频次  

## Maximum Likelihood Estimate  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image73.png)  

最大似然估计的目的就是：利用已知的样本结果，反推最有可能（最大概率）导致这样结果的参数值

通过原本训练集估计的概率是最大似然估计如图中0.0004，修改频次后则不再是  

## Add-one estimation例子  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image74.png)   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image75.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image76.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image77.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image78.png)  

#3.6 Interpolation    

## Backoff and Interpolation 

计算语言模型两种方式Backoff和Interpolation： 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image79.png)  

**Linear Interpolation **  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image80.png) 

第二个式子$$\lambda$$会根据$$w_{n-1}w_{n-2}$$取值  

**How to set lambdas?**  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image81.png) 

将数据分成三份，训练集训练模型，Held-Out集确定$$\lambda$$取值？？  

## Unknown words:Open versus closed vocabulary tasks   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image82.png) 

词汇表确定后，有些词并不在表里，使用<UNK>代表   

## Huge web-scale n-grams   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image83.png) 

词汇表过大，可以进行修减，删去只出现一次的词或通过测试集计算entropy和perplexity，对概率贡献少的词删除

使用更有效的数据结构tries前缀树，Bloom filter等  

 
## Smoothing for Web-scale N-grams  

使用"backoff"方法计算语言模型  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image84.png) 

先用trigram计算，如果分母为0，使用加权bigram


## N-grams Smoothing Summary  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image85.png)   

## Advanced Language Modeling  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image86.png) 


# 3.7 Good-Turing Smoothing    

## More general formulations :Add-k(Smoothing) 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image87.png) 

**Unigram prior smoothing**  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image88.png)  

## Advanced smoothing algorithms  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image89.png)  

## Notation: $$N_{c}$$=Frequency of frequency c  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image90.png)   

$$N_{c}$$:文本资料中频数为$$c$$的词的个数  

## Good-Turing smoothing intuition  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image91.png) 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image92.png) 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image93.png)   

假设training set 有 c 个 word ，从training set中每次取一个word，直到所有word都被取了一遍，组成图中Held out set 共有c个word,从training set 取出一个W后计算剩下word中这个W的频数，如果为0，则在Held out set中归为$$N_{0}$$,如果为1归为$$N_{1}$$，以此类推。   

Held out set $$N_{0}$$实际为training set$$N_{1}$$,其占training set的$$(1)N_{1}/c$$,Held out set $$N_{k}$$实际为training set$$N_{k+1}$$,其占training set的$$(k+1)N_{k+1}/c$$,有$$N_{k+1}$$个不同的word，每个word频数是$$(k+1)$$,总数量为$$(k+1)N_{k+1}$$。  

则一个训练集中没有出现的word占比为$$(1)N_{1}/c$$，出现了k次的占比为$$(k+1)N_{k+1}/c$$，出现了k次的不同的word，每个word平均出现概率为$$(k+1)N_{k+1}/c/N_{k}$$。   







