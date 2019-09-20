---
layout: post
title: Chapter 6 Temporal Difference Learning(TD)
date:   2019-03-23
categories: ["Reinforcement Learning:An Introduction"]
---

Temporal-Difference(TD) learning is a combination of Monte Carlo ideas and dynamic programming (DP) ideas. Like Monte Carlo methods, TD methods can learn directly from raw experience without a model of the environment's dynamics. Like DP, TD methods update estimates based in part on other learned estimates, without waiting for a final outcome (they bootstrap).

**1、TD Prediction**   

对于nonstationary environments 可以使用every-visit Monte Carlo method估计value:  

$$V(S_{t})\gets V(S_{t})+\alpha[G_{t}-V(S_{t})]$$     

$$G_{t}$$:t时刻的实际return   
$$\alpha$$:constant step-size parameter   

上述$$constant-\alpha MC$$方法,为了计算$$G_{t}$$需要等待episode结束,而TD方法只需要等待到下个时间点，即在t+1时刻通过$$R_{t+1}$$和$$V(S_{t+1})$$更新$$V(S_{t})$$:   

$$V(S_{t})\gets V(S_{t})+\alpha[R_{t+1}+\gammaV(S_{t+1}-V(S_{t})]$$     



![_config.yml]({{ site.baseurl }}/images/12RL/image23.png)  

**2、**   