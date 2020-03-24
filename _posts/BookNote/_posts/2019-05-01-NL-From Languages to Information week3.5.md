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

we build one model with some features we test it on some development data (not our final test data) and we see how it does. 

if it gets some performance level like it might be fifty seven percent and we'd like to do a bit better and then we're going to come up with a refine second model ,repeat it over and we'll commonly do this a number of times until we've tried to come up with the best model that we think we can and so the question is what do we do for this next model,in general you can look at the features and see which ones are useful

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image433.png)

derivative:导数   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image434.png)