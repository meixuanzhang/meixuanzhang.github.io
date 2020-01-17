---
layout: post
title: Week 5 Relation Extraction and Question Answering
date:   2019-05-01
categories: From Languages to Information
---  

# 9.1 Information Extraction and Named Entity Recognition Introducing the tasks

## Information Extraction(IE信息提取)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image317.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image318.png)  

## Low-level information extraction 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image319.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image320.png)  

例子：google搜索答案，提取信息回答 

## Named Entity Recognition(NER)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image321.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image322.png)  

Entity Recognition用途之一：sentiment classifier中除了获得评价正负外，有时候还需要获得这是"谁"的评价，评价的"什么"。question answering中有时候回答的是命名实体。  

Entity Recognition simply pick out concrete(具体的) names of objects, people, organizations, et cetera, or quantities, dates, times, and things 

Information Extraction where the goal is to pick out particular relations from pieces of unstructured natural language text.  

# 9.2 What is Relation Extraction  

## Extracting Relations from text  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image323.png)   

每当我们需要某种类型的结构化知识并且该知识最初以文本形式出现时，应用程序更容易从结构化数据库中获取知识。 因此，我们希望将这些文本事实提取为结构化形式

##  Extracting Relation Triples(关系三元组) from Text  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image324.png)  

## Why Relation Extraction?  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image325.png)   

## Automated Content Extraction(ACE)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image326.png)   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image327.png)  

## UMLS:Unified Medical Languages System 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image328.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image329.png)  

## Databases of Wikipedia Relations

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image330.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image331.png) 

## Relation database that draw from Wikipedia  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image332.png)

## Ontological relations  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image333.png)

## How to build relation extractors 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image334.png)


# 9.3 Using Patterns to Extract Relations   

## Rules for extracting IS-A relation  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image335.png)  

## Hearst's Patterns for extracting IS-A relation  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image336.png)

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image337.png)  

## Extracting Richer Relations Using Rules  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image338.png)

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image339.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image340.png)  

## Extracting Richer Relations Using Rules and Named Entities   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image341.png)  

## Hand-built patterns for relation  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image342.png)  


# 9.4 Supervised Relation Extraction  

## Supervised machine learning for relations    

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image343.png)   

## How to do classfication in supervised relation extraction  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image344.png)  

## Relation Extraction  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image346.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image345.png)  

## Word Features for Relation Extraction  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image347.png)   

## Named Entity Type and Mention Level Features for Relation Extraction  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image348.png)  

## Parse Features for Relation Extraction  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image349.png)  

syntactic chunk sequence  句法块序列   
base chunk sequence 基本块序列   

## Gazeteer and trigger word features for relation extraction  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image350.png)  

gazetteer 地名词  
trigger 触发词  

**对句子提取出的特征**  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image351.png)  

## Classifiers for supervised methods  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image352.png)  

## Evaluation of Supervised Relation Extraction  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image353.png)   

## Summary:Supervised Relation Extraction  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image354.png)  


# 9.5 Semi Supervised and Unsupervised Relation Extraction   

## Seed-based or bootstrapping approaches to relation extraction  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image355.png)  

the extra intuition of snowball was the requirement that X and Y be named entities. So in the, in the Dipre algorithm, X and Y could beand string. 

the Snowball algorithm also computed a confidence value for each pattern, so that's kind of a new intuition.


Now from those huge number of seeds we have a
04:20
big database. We could have hundreds of thousands of examples. We create lots and
04:25
lots of features and now instead of iterating. We simply take all of those
04:29
features and build a big supervise classifier, supervised by all these facts
04:33
that we know are true in our large database


 For each relation. Let's see. We're trying to distract the born in
05:11
relation. We go to each tuple in some big database of the Bornin relations, we have
05:16
lots of Bornin relations. Edward Hubble, born in Marshfield, Albert Einstein, born
05:21
in Ulm. We find sentences in some large corpus, let's say we're using the web,
05:26
that have both entities, and here's a bunch of sentences we might find, Hubble
05:30
was born in Marshfield, Einstein born 1879, Ulm, Hubble's birthplace in
05:35
Marshfield, and so on. Lot's of sentences. And now from all of those sentences, for
05:39
all of those different entities we extract frequent features, so we might parse the
05:44
sentences, we might just use the words in between. We might have some [inaudible] entities,
05:48
we might have part of speech tags, all sort of things, we extract lots amounts of
05:53
features. And now, we take all those features and do exactly what we did for
05:57
supervised classification.

We extract our positive instances from what we've seen in the
06:15
database. So person, a particular person Albert Einstein born in Ulm is a
06:19
positive instance. So from our supervised classifier we can get a probability of the
06:24
born in relation for a particular data point and now what we can condition that
06:28
on all sorts of features we can extract from each sentence, so a huge number of
06:33
features.


They first used,
07:02
parsed data to train a classifier to decide if a particular relation [inaudible] or tuple is
07:06
trustworthy or not. And so they have a small amount of parse data where they can
07:10
use very expensive parse features to decide that a subject and a verb and an
07:14
object are in a, likely to be in a relation. Train a classifier that can do
07:18
that can do that for any relation. And now, they walk through the very large corpus,
07:22
let's say it's the web, in a single pass, and they just extract any relation between
07:27
NPs. And we keep them if the trustworthy classifier says this is likely to be a
07:31
relation between the two entities. And then we rank these relations based on
07:35
redundancy. If we. Relation occur and a lot of times between 2's and 3's in
07:39
different websites when we guess this is a real relation. extraction algorithm extracts relations like, FCI specializes in software
07:48
development or Tesla invented coil transformer, and so on, where we can
07:53
extract a virtually infinite number of possible relations between any entities.
07:58
All we have to do is see them often enough times on the web. 

## Evaluation of Semi-supervised and Unsupervised Relation Extraction  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image364.png)  
