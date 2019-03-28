---
layout: post
title: Chapter 1 Introduction 
date:   2019-03-23
categories: Reinforcement Learning:An Introduction
---

当我们思考学习的本质时，首先会想到学习的本质是通过与环境互动学习，通过互动进行学习是学习与智能理论的基本理念。   
本书探索了一种从互动中学习的计算方法。探索了理想化的学习情境和评估各种学习方法的有效性。探索了如何设计机器使其有效解决科学或经济方面学习问题，并通过数学分析和计算实验评估设计。     
本书探索的方法叫reinforcement learning，是通过互动实现以目标为导向的学习。   

**1 Reinforcement Learning**   

1、Reinforcement learning is learning what to do——how to map situations to actions——so as to maximize a numerical reward signal.  
action不仅影响immediate reward，也影响下一个情境，甚至所有subsequent rewards，trial-and-error search(反复搜索) and delayed reward(延迟奖励)是Reinforcement learning 两个最重要的不同特征   

2、理解问题和解决方法之间的区别在学习强化学习中非常重要;   

3、强化学习的挑战之一是，权衡exploration(探索) and exploitation(应用)，The agent has to exploit what it has already experienced in order to obtain reward, but it also has to explore in order to make better action selections in the future.只exploration(探索)或 exploitation(应用)都不能避免任务失败    

4、Reinforcement learning考虑的是以目标为导向的agent和不确定的环境之间互动的整个问题，这与一些只考虑子问题方法不同。  

5、All reinforcement learning agents have explicit goals, can sense aspects of their environments, and can choose actions to influence their environments    

**2、Examples**

