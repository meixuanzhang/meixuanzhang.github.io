---
layout: post
title: Week 6 Relation Extraction and Question Answering
date:   2019-05-01
categories: ["From Languages to Information"]
---  

# 11.1 The Maximum Entropy Model Presentation

## Maximum Entropy Models  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image447.png)  

## Maxent Example  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image448.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image449.png)  

没有限制条件下$$-xlogx$$的最小值为$$\frac{1}{e}$$,对$$-xlogx$$求导$$logx=-1$$

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image450.png)  

the maximum entropy distribution is to say that each of those probabilities is 1/6 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image451.png)   

nouns are much more common than verbs in our data so we're going to add a feature the expected value of that feature is 32 over 36  

so if we add that constraint and then say what's the maximum Trippi distribution this constraint is satisfied the sum of these probabilities equals 32 over 36 but within that category probability mass is still going to be distributed uniformly because that that's the maximum entropy distribution   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image452.png)  

## Convexity   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image453.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image454.png)  