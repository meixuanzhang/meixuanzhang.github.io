---
layout: post
title: Week 4 Information Retrieval
date:   2019-05-01
categories: From Languages to Information
---  

# 7.1 Introduction to Information Retrieval 信息检索 

## Information Retrieval定义  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image231.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image232.png)  

## The classic search model  

检索过程： 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image233.png)   

## 检索评估  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image234.png)  

# 7.2 Term Document Incidence Matrices   

## Unstructured data in 1620  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image235.png)  

grep （缩写来自Globally search a Regular Expression and Print）一种强大的文本搜索工具，它能使用特定模式匹配（包括正则表达式）搜索文本，并默认输出匹配行。
 
grep搜索是匹配搜索，搜索出特定模式(词结构)的词，语料量大时速度慢，输入"Caesar"只能搜索出"Caesar",对于文档不包含"Calpurnia"词需要遍历文档所有词确定，同时无法进行更复杂的操作，如发现"Romans"与"countrymen"位置相近,对检索结果排序返回   

## Term-document incidence matrices   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image236.png) 

矩阵横轴是文档，纵轴是words，文档出现了word则标记1，否则0  

## Incidence vectors  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image237.png) 

将word转化成vector，每一维代表一个文档，通过and运算，可以找出同时含有"Brutus","Caesar","Calpurnia"词的文档   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image238.png) 

## big collections  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image239.png) 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image240.png) 

假设有大量文档，每个文档word都不同，矩阵中会存在大量0，这会浪费大量储存空间

# 7.3 The Inverted Index  

## Inverted index  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image241.png) 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image242.png)   

使用类似字典结构存储，“word”是键，"文档"是值  

## Inverted index  construction  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image243.png)   

将文档中句子进行分词(Tokenizer),对词进行处理(规范化)，构建索引   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image244.png)   

## Indexer steps   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image245.png) 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image246.png) 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image247.png) 

## Where do we play in storage?

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image248.png)   


# 7.4 Query Processing with the Inverted Index

## Query processing :AND  

查找同时含有单词"Brutus"和"Caesar"的文档  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image249.png)   

## The merge  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image250.png)   

NIL 是list结尾

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image251.png)   

# 7.5 The Boolean Retrieval Model  

## Boolean queries:Exact match   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image252.png)  

通过AND,OR ,NOT组织检索问题  

## Example：WestLaw  

使用Boolean queries检索的系统  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image253.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image254.png)  

## Boolean queries:More general "merges"   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image255.png)  
 
![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image256.png)  

## Query optimization  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image257.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image258.png)  

先从 document frequency 少的单词开始，"Calpurnia"和"Brutus"执行merge 算法，有相同文档id则与"Caesar"执行merge 算法,有相同则将同时有三个词的文档id保存，然后回到"Calpurnia"和"Brutus"执行merge 算法，不断循环   


7.6 Phrase Queries and Positional Indexes  

## Phrase queries 短语查询  

查找由两个或以上的单词组成的短语。

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image260.png)  

## A first attempt ：Biword indexes

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image261.png) 

句子所有单词，前后两两组成短语。 

## Longer phrase queries  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image262.png)   

Biword方式文档是否确定是否包含两个单词短语，对于是否包含多于两个词短语，短语需要重新组合成多个两词短语，然后查询文档是否包含这些两词短语。这种方式不够准确。 

## Solution 2:Positional indexes    

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image263.png)   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image264.png)   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image265.png)  

先判断哪些文档都含有这些词，然后文档内词实施"merge"算法

## Proximty queries 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image266.png)   

## Positional index size  


![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image267.png)   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image268.png)   

 考虑一个word出现在一篇文档频率是0.1%，1000字文档，word应该会出现一次，但100000字文档会出现100次，Positional index 会非常长 
 
## Rules of thumb   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image269.png)   

web page 的Positional index 长度大概是 non-ositional index 2到3倍
 
Positional index 长度几乎是原始文本长度的35%-50%

## Combination schemes  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image270.png)   

将Positional index和Biword indexes结合，对于有些两词短语不再是拆分成单个单词。

----------------------------------------------------------------------------------------------------------------   

# 8.1 Introducing Ranked Retrieval   

## Ranked retrieval  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image271.png)   

boolean queries 返回结果不是太多就是太少，不利于大部分用户使用   

## Promblem with Boolean search: feast or famine(过少或过多)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image272.png)   

## Ranked retrieval models  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image273.png)  

## Feast or famine: not a promblem in ranked retrieval  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image274.png)  

## Scoring as the basis of ranked retrieval  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image275.png) 

根据query对文档进行打分,分越高说明与query越匹配  

## Query-document matching scores  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image276.png) 

# 8.2 Scoring with the Jaccard Coefficient  

## Take 1: Jaccard coefficient  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image277.png) 

## Jaccard coefficient:Scoring example  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image278.png)  

## Issues with Jaccard for scoring  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image279.png)  

Jaccard coefficient没有考虑频次，频次少的词带有信息往往高于频次高的词    

计算时分母开根可以减少文档长度对Jaccard coefficient的影响  

# 8.3 Term Frequency Weighting 

## Term-document count matrices  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image281.png)  

## Bag of words model  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image282.png)  

## Term frequency tf  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image283.png)  

假设搜索词为"squirrels",出现10次"squirrels"的文档的评分应该高于出现1次"squirrels"的文档，但其评分并不是出现1次"squirrels"的文档的10倍  

## Log-frequency weighting  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image284.png)   

# 8.4 Inverse Document Frequency Weighting   

## Document frequency  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image285.png)   

希望检索词中，在文档中频次更低的词可以有更大的权重   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image286.png)  

## idf weight  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image287.png) 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image288.png)  

计算检索词的权重，根据文档中这些词出现与否计算每个文档的评分   

## Effect of idf on ranking  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image289.png)  

## Collection vs Document frequency  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image290.png)  

Collection frequency:计算词在所有文档中出现的频次  

Document frequency:计算包含词的文档数   

图中"insurance"可能在某个文档中高频率出现导致Collection frequency高于"try",但实际上"try"信息量少于"insurance"

# 8.5 TF IDF Weighting 

## tf-idf weighting  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image291.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image292.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image293.png)  

# 8.6 The Vector Space Model  

## Documents as vectors   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image294.png)   

## Queries as vectors   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image295.png) 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image296.png)  

欧式距离,q与d2距离(d2含有更多q不含有的词)大于q与d1或q与d3距离,但从信息检索看,q表示检索词(gossip,jealous)应该与d2距离更近,d1和d3只有其中一个词。 

## Use angle instead of distance  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image297.png)   

## From angle to cosines  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image298.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image299.png) 

## Length normalization  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image300.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image301.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image302.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image303.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image304.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image305.png)  

# 8.7 Calculating TF IDF Cosine Scores 

## tf-idf weighting has many variants  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image306.png)  

## Weighting may differ in queries vs document  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image307.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image308.png)  

wt(logarithmic scaling)  

## Computing cosine scores  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image309.png)  

length normalization of the query is actually unnecessary

## Summary-vector space ranking 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image310.png) 

# 8.8 Evaluating Search Engines  

## Measures for a search engine  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image311.png) 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image312.png)

## Evaluating an IR system  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image313.png)  

## Evaluating ranked results  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image314.png)  

## Recall/Precision 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image315.png)  

对一个检索问题，获得topN结果，计算Recall\Precision  

## Two current evaluation measures   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image316.png)  

AP:每一个检索问题，平均topN结果中计算预测为R(正)的文档的precision。
MAP:平均所有检索问题的AP


