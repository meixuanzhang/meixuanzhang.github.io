---
layout: post
title: Week 7 Parsing
date:   2019-05-01
categories: ["From Languages to Information"]
---  

# 15.1 CFGs(Context-Free Grammars) and PCFGs(Probabilistic Context-Free Grammars)   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image506.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image507.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image508.png)  

categories,nouns verbs and so on are the preterminals   

terminals in other words as before  

non terminals really become our phrase or category   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image509.png)  

unary rules: one category rewrites as another category   

binary rules:   one category rewrites as another two category  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image510.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image511.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image512.png) 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image513.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image514.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image515.png)  

$$P(s)$$language model score  

## 15.2 Grammar Transforms   

Restricting the grammar form for efficient parsing 

乔姆斯基范式(CNF,Chomsky Normal Form)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image516.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image517.png)  

there have been a rule that has an NP on the right-hand side we're going to split it into two rules one just as before and one that then notes that the noun phrase can be empty and so just says it's can go to VP  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image518.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image519.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image520.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image521.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image522.png)  

@VP_V: the name of a non-terminal 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image523.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image524.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image525.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image526.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image527.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image528.png)  

 