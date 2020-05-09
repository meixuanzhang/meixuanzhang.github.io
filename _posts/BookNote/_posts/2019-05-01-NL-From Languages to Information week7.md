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

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image559.png)  

------------------------------------------------------------------------------------------------

# 16.1 Lexicalization of PCFGs

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image560.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image561.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image562.png) 

if we want to work out for a prepositional phrase(for january) whether it is modifying announce of precedes or modifying a verb that perceives 

we can capture quite a lot of that inside a pcfg once we lexicalize ,now we'll have a rule where an NP-rates is taking on its right-hand side a PP-for and we can ask whether that is a likely thing to happen or not or we can say we have a VP-announce is taking expanding on its right-hand side to a PP-in is that a reasonable thing to happen or not

# 16.2 Charniak's Model

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image563.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image564.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image565.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image566.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image567.png)   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image568.png)  

# 16.3 PCFG Independence Assumptions   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image569.png)  

you can work out the probabilities of things inside here(图中绿色)  knowing only that this is a noun phrase(NP)   

you can work out the probabilities of things up here(图中红色) knowing only this is a noun phrase(NP) that's a very strong independence assumption   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image570.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image571.png)  

右边两个结构上半部分是一样的，根据独立假设，第二NP下内容只需要根据第二NP预测，第二NP下内容应该一样，明显独立假设过强   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image572.png)  

we can relax independence assumptions of a pcfg by encoding more information into the non terminals cymbals the process that's often referred to as state splitting：  

you can improve a probabilistic context-free grammar quite a lot by encoding as part of each non-terminal also what was the parent category 

we're going to split out noun phrases that are possessive and pull them an NP-pos and then that information will also be captured in the grammar   

# 16.4 The Return of Unlexicalized PCFGs  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image573.png) 

we have a couple of statistics one is our performance level which will be our usual if one of label precision recall and then the other one is the size of our grammar that as we make more state splits the grammar will be bigger in terms of its number of non-terminals and if this number gets too big that's both dangerous for two reasons it'll both slow down the parser and we'll start to get problems with sparseness 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image574.png) 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image575.png) 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image576.png) 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image577.png) 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image578.png)   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image579.png) 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image580.png) 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image581.png) 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image582.png) 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image583.png) 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image584.png) 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image585.png) 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image586.png)  

# 16.5 Latent Variable PCFGs  



