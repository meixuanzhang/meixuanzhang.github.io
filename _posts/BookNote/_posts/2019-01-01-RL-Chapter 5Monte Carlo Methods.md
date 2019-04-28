---
layout: post
title: Chapter 5 Monte Carlo Methods
date:   2019-03-23
categories: ["Reinforcement Learning:An Introduction"]
---

Monte Carlo methods 只需要经验(sample sequences of states, actions, and rewards from actual or simulated interaction with an environment)，不需要环境动态的先验知识$$P(s',r\mid s,a)$$。  

Monte Carlo methods通过对returns求均值解决强化学习问题，只能适用于episodic tasks(即任务会有终止状态)。  

**1、Monte Carlo Prediction**   

使用MC估计在策略$$\pi$$下,状态s的value值$$V_{\pi}(s)$$,有两种方法估计,一种是first-visit MC method,另一种是every-visit MC method。 

在一个episode中s可能被访问很多次，如果只平均所有episode第一次访问s时的returns，使用方法是first-visit MC method，如果平均所有epsode所有访问s时的returns，使用方法是every-visit MC method  

图中unless=if not
