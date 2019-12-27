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

则一个训练集中没有出现的word占比为$$(1)N_{1}/c$$，出现了k次的占比为$$(k+1)N_{k+1}/c$$，则训练集中出现了k次的不同的word，每个word平均出现概率为$$(k+1)N_{k+1}/c/N_{k}$$。   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image94.png)   

上述方法有可能出现中间某些频次$N_{k}$$$不存在问题导致无法计算，为此提出Simple Good-Turing   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image95.png)   

# 3.8 Kneser-Ney Smoothing   

在实践中通常原始的count和经过Good-Turing计算的count，它们之间的间隔$$d$$是一个固定的很小的数，如上图间隔约是0.75  

## Absolute Discounting Information  

使用Absolute Discounting Information 计算语言模型，式子$$d$$表示间隔

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image96.png)

## Kneser-Ney Smoothing   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image97.png)

上图 Shannon game 估计句子下一个单词时，往往先使用bigrams(有部分词的组合没有在训练集中出现$$P(w_{i}\mid w_{i-1})$$=0),无法计算时使用unigram代替$$P(w_{i})=P(w_{i}\mid w_{i-1})$$,这样估计不准确，如下图例子"Francisco"出现概率往往比"glasses"高，但其通常搭配"San",当前面没有"San"时，"glasses"出现概率应该更高，为此提出了$$P_{continuation}(w)$$   

首先计算文本$$(w_{i-1},w_{i})$$类别组合数(有多少中组合)作为分母,其中$$w_{i}=w$$的组合的个数，即：$$\mid\{w_{i-1}:c(w_{i-1},w)\}\mid$$ 作为分子

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image98.png)

也可以计算$$(w_{i-1},w)$$类别组合中，$$w_{i-1}$$有哪些取值，每个取值有多少种类别组合$$(w_{i-1},w_{i})$$,将每个取值类别组合数求和作为分母   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image99.png)  

bigram formulation for Kneser-Ney：     

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image100.png)   

the general recursive formulation for n grams：  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image101.png)   

---------------------------------------------------------------------------------------- 

# 4.1 The Spelling Correction Task  错误拼写更正

## Spelling Tasks  

$$\bullet$$ 拼写错误检测(检测出错误的拼写)
$$\bullet$$ 拼写错误更正: 
自动更正($$hte \to the$$)
提供一个更正建议
提供多个更正(Suggestions lists) 

## Types of spelling errors  

$$\bullet$$ Non-word Errors(错误单词不存在)

$$graffe \to giraffe$$  

$$\bullet$$ Real-word Errors(错误单词存在)  

Typographical Errors排字错误:$$three \to there$$  

Cognitive Errors认知错误(homophones同音字):$$piece \to peace , too \to two $$ 

## Rate of spelling errors 


![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image102.png)   

## Non-word spelling Errors

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image103.png)   

## Real word spelling Errors  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image104.png)   


# 4.2The Noisy Channel Model of Spelling   

## Noisy Channel Intuition  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image105.png) 

词可能拼写成不同错误的词，反过来通过错误词可以推出其原本最可能是什么词  

## Noisy Channel Model 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image106.png) 

通过贝叶斯找到拼写错误的词最大可能是什么词 

### History:Noisy channel for spelling proposed around 1990  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image107.png)  

### 生成更正候选词  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image108.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image111.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image109.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image110.png)  


### 根据语言模型计算$$P(w)$$  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image112.png)   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image113.png)  

使用Unigram语言模型，直接选择候选词中在语料库出现频率高的词  

### 计算Channel model概率$$P(x\mid w)$$  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image114.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image115.png)  

对错误词更正为正确词需要操作进行统计，如acrss更正为across,进行了插入，则在矩阵表中，横轴找到r(表示插入字母前面字母)，纵轴找到o，频次加1,下图是替换操作统计矩阵：  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image116.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image117.png)  

上图$$w_{i}$$表示一个字母，错误词通过某个操作更正为正确的词，计算操作对应概率作为$$P(x \mid w)$$  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image118.png)  

根据noisy channel probability 应该选择across，实际上actress才是正确选择，应结合bigram语言模型，分别计算两个词与其前后位置两个词搭配概率，选择概率更大的词作为更正词

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image119.png)   
 
## Evaluation  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image120.png)  

# 4.3Real-Word Spelling Correction  

大概有25-40%拼写错误属于Real-Word类型  

## Solving real-world spelling errors   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image121.png)  

产生候选词方法：输入的词本身，与输入词有单位编辑距离正确的词，同音词  

## Noisy channel for real-world spell correction  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image122.png)   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image123.png)  

输入句子的每个词都产生候选词，候选词相互组合产生句子中选择概率最大的句子作为结果 

## Simplification: One error per sentence 

实际情况中，句子中只有一个词是输入错误的，只需对这个词产生候选词，然后计算不同候选词下句子概率，选择能使句子概率最大的候选词作为替换  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image124.png)  

## 使用Noisy Channel Model对候选进行选择  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image125.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image126.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image127.png)  

$$P(thew \mid the)$$表示语料中the被错误输入为thew的概率，$$P(thew \mid thew)$$表示语料中thew被正确输入为thew的概率   

# 4.4State of the Art Systems  

## HCI issues in spelling  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image128.png) 

Unconfident 对于有错但系统不知道如何解决的错误，只是标记一个错误  

## State of the art noisy channel  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image129.png) 

## Phonetic error model  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image130.png)   

将发音相似的单词作为候选   

## Improvements to channel model

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image131.png)  

## 影响计算channel model $$P(x \mid w)$$   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image132.png)  

## Classifier-based methods for real-world spelling correction  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image133.png) 