---
layout: post
title: week 3.5 Generative vs Discriminative Models
date:   2019-05-01
categories: ["From Languages to Information"]
---  

# 8.1Generative vs Discriminative Models

## Introduction   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image411.png)  

## Joint vs.Conditional Model   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image412.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image413.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image414.png)  

## Conditional vs.Joint Likelihood  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image415.png) 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image416.png) 

# 8.2 Making features from text for discriminative NLP models  

## Features  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image417.png)
 
## Example features   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image418.png)   

## Feature Expectations      

$$P$$: distribution

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image419.png) 

## Features  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image420.png) 

## Feature-Based Models  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image421.png) 

## Example:Text Categorization   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image422.png)   

## Other Maxent Classifier Examples  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image423.png) 

# 8.3 Feature Based Linear Classifiers  

## Feature-Based Linear Classifiers   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image423.png) 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image424.png) 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image425.png) 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image426.png) 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image427.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image429.png)  

## Aside:logistic regression 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image428.png)   


# 8.4 Building a Maxent Model The Nuts and Bolts   

datum:数据   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image430.png) 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image431.png) 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image432.png) 

we build one model with some features we test it on some development data (not our final test data),if it gets some performance level like it might be fifty seven percent and we'd like to do a bit better and then we're going to come up with a refine second model ,repeat it over and we'll commonly do this a number of times until we've tried to come up with the best model that we think we can and so the question is what do we do for this next model,in general you can look at the features and see which ones are useful

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image433.png)

derivative:导数   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image434.png)   

# 8.5 Generative vs Discriminative models   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image435.png) 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image436.png) 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image437.png)  

we should say that this document is equally likely to be a document about Europe or Asia but again we don't get that effect because the two tokens(Hong Kong) here are wrongly being treated as independent sources of  evidence and so therefore we think we still have a three to one odds ratio in favor of the document being about Asia     

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image438.png)  

# 8.6 Maximizing the Likelihood   

## The Likelihood Value  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image439.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image440.png)  

## Derivative   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image441.png) 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image442.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image443.png)  

## Finding the optimal parameters  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image444.png)   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image445.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image446.png)   
 