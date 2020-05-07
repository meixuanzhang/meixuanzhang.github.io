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

# 15.2 Grammar Transforms   

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

# 15.3 CKY Parsing    

Exact polynomial time parsing of (P)CFGs   

成分句法分析(Constituency Parsing)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image529.png)  

we want to do is find a sentence structure that's licensed by the grammar and in the pcfg case we will do an exponential number of work but the CKY algorithm gives us a cubic time algorithm both in terms of the length of the sentence and the size of the grammar in terms of the number of non terminals 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image530.png)  

两个紫色正方形分别描述了 fish 和 people  

绿色正方形描述 fish people  

this is basically half a square the number of squares that we have is order N squared and so what we gonna show is that we can fill in each square in order in and so the resulting algorithm runs in cubic time   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image531.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image532.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image533.png)  

two ways of making an S and here their probabilities0.0189 versus 0.0007 so the S Coast where NP VP is the higher probability way of making an S and so I keep that one and I just don't store this one  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image534.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image535.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image536.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image537.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image538.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image539.png)  

# 15.4 CKY Example

here's the grammar that we're going to use :  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image540.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image541.png) 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image542.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image543.png)  

we also have to apply the unary rules and so the way we'll do that is for each cell will find unary rules that apply and if they create a category that isn't there before or one with higher probability than what was there before then we'll put it into our chart and in this case the relevant unary rules here

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image544.png)  

build a binary constituent:  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image545.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image546.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image547.png) 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image548.png) 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image549.png) 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image550.png) 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image551.png) 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image552.png) 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image553.png) 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image554.png) 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image555.png)  

# 15.5 Constituency Parser Evaluation   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image556.png)  

yesterday should be this kind of weird kind of temporal noun phrase in English hares where you have be a noun phrase like yes yesterday or next week to express a time and otherwise if it expresses a prepositional phrase like on Sunday in

the spring but the parser is wrongly just stuck it on as an extra noun at the end of the noun phrase great care and so that's an error so how are we going to go about measuring that well 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image557.png)   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image558.png)  
