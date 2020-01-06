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

entity recognition-- of simply picking out concrete(具体的) names of objects, people, organizations, et cetera, or quantities, dates, times, and things 

information extraction where the goal is to pick out particular relations, rows in a database table, from pieces of unstructured, natural language text.  

# 9.2 What is Relation Extraction  

## Extracting relations from text  

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

## Databases of Wikipedia RelationS

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image330.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image331.png) 

## Relation database that draw from Wikipedia  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image332.png)

## Ontological relations  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image333.png)

## How to build relation extractors 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image334.png)




