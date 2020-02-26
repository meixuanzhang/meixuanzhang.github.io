---
layout: post
title: Week 5 Relation Extraction and Question Answering
date:   2019-05-01
categories: ["From Languages to Information"]
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

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image356.png) 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image357.png) 

## Dipre:Extract<author,book>pairs  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image358.png)

## Snowball   

Dipre算法和Snowball算法区别

The extra intuition of snowball was the requirement that X and Y be named entities. So in the Dipre algorithm, X and Y could be any string. 
the Snowball algorithm also computed a confidence value for each pattern

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image359.png)   

## Distant supervision  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image360.png)   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image361.png)   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image362.png)   

We extract our positive instances from what we've seen in the database. So a particular person Albert Einstein born in Ulm is a positive instance.   

So from our supervised classifier we can get a probability of the born in relation for a particular data point and now what we can condition that on all sorts of features we can extract from each sentence

需要先判断两个主体是否存在某种关系？   

## Unsupervised relation extraction  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image363.png)   

They first used  parsed data to train a classifier to decide if a particular relation or tuple is trustworthy(值得信赖) or not.   

And so they have a small amount of parse data where they can use very expensive parse features to decide that a subject and a verb and an object are likely to be in a relation.    

Train a classifier that can do that for any relation. And now, they walk through the very large corpus,let's say it's the web, in a single pass, and they just extract any relation between NPs. And we keep them if the trustworthy classifier says this is likely to be a relation between the two entities.   

we rank these relations based on redundancy. If Relation occur and a lot of times between 2's and 3's in different websites when we guess this is a real relation. extraction algorithm extracts relations like, FCI specializes in software development or Tesla invented coil transformer(特斯拉发明了线圈变压器), and so on, where we can extract a virtually infinite(几乎无限) number of possible relations between any entities.   


## Evaluation of Semi-supervised and Unsupervised Relation Extraction  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image364.png)  

----------------------------------------------------------------------------------------------------------   

# 10.1 What is Question Answering  

## Question Answering  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image365.png)  

worms：蠕虫    
  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image366.png)    

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image367.png)    

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image368.png)   

## Types of Questions in Modern Systems  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image369.png)  

Complex questions are generally answered more in research systems.  

Factoid question(事实问题) answering is a widely used commercial application.    

## Commerical systems:mainly factoid question  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image370.png)  

## Paradigms for QA   

paradigms：范式  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image371.png)    

The IR based approach is go find the answer in some string on the web.    

The knowledge based approach is build an answer from understanding a parse of the question.     

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image372.png)   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image373.png)    

## IR-based Factoid QA  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image374.png)     

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image375.png)    

 
The general algorithm for IR-based factoid question answering starts with a question, and begins by extracting information from the question itself.  

And the two most important and common things to extract from the question are a **query** that's going to be sent to an IR engine, and the type of the **answer** that tells us what kind of named entity we're looking for   

we take a whole lot of documents, we index them, so that when we have a query we can return a whole lot of  documents. From those documents we extract passages, so parts of those documents.   

And then, those passages are then processed, in answer processing, looking for the type of the answer that we know we're looking for. And then returning an actual answer.

## Knowledge-based approaches(Siri)   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image376.png)   

builds a pure semantic representation of the query, and this is true of Siri or Wolfram Alpha, where they're gonna come up with a semantic representation language for questions that they understand.   

And you might pick some sub-domain that you're able to build a perfect semantic representation for: times, dates, locations, scientific questions, mathematical questions.   

And from this semantics, we can then map to structured databases or structured resources, geospatial databases, or ontologies, or restaurant review systems;these things where we can build up pure semantics of the approach.   

Hybrid approaches, and IBM Watson is a good example of this  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image377.png)   

# 10.2 Answer Types and Query Formulation  



## Factoid Q/A  

The first thing we're going to do in question processing is understand what's being asked here.   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image378.png)  

## Question Processing Thing to extract from the question  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image379.png)   

## Question Processing  

Here's an example of the kind of things we might extract from a question.   

border: 边境  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image380.png)   

## Answer Type Detection:Named Entities  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image381.png)    

## Answer Type Taxonomy

taxonomy:分类法    

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image382.png)    

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image383.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image384.png)     

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image385.png)   

The Jeopardy system also used a lot of answer types and they did a nice analysis   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image386.png)   

## Answer Type Detection  

How do we do answer type detection?   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image387.png)  

if we see who, and then a form of to be a named entity person  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image388.png)   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image389.png)  

机器学习使用的特征   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image390.png)   

##  Keyword Selection Algorithm 

The next step is query formulation. How do we decide what words to send to the IR engine to return documents and then passages. (Query Formulation)    

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image378.png)   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image391.png)   

## Choosing keywords from the query  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image392.png) 

We could try just sending the things of rank one.Or we could send, go until we have enough query words to make a long query, or we can send the things that rank one, see how many queries we get back, and if there's not enough, add in more query terms and so on.    

what we do with these ranking of queries depends on exactly what database were querying, whether it's the web or a smaller database and so on



