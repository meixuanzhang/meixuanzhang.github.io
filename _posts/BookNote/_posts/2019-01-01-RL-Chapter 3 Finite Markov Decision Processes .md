---
layout: post
title: Chapter 3 Finite Markov Decision Processes
date:   2019-03-23
categories: Reinforcement Learning:An Introduction
---
这章主要介绍是finite Markov decision processes 类型问题，这类问题不仅涉及evaluative feedback，还涉及根据不同的situations,选择不同的action。    
MDPs是序列决策的经典模型，actions不仅会影响immediate reward ,还会影响后面的situations或state,甚至是future reward。MDPs 需要平衡 immediate 和delayed reward。  
bandit promble 是估计$$q\ast (a)$$   
MDPs 是估计$$q\ast (s,a)$$或$$v\ast (s)$$(s情境，最优action下value）  


**1、The Agent-Environment Interface**  

agent:leaner and decision maker(决策者)
environment:与agent 互动的对象 
互动过程是连续的，agent选择action,environment 对选择action作出响应并向agent呈现新的situations。   

agent和environment在离散时间序列(t=0,1,2..)每个时刻进行互动，在每个时刻t，agent收到environment's state($$S_{t}\in \widehat{S}$$)并据此选择action(A_{t}\in \widehat{A(s)}),作为action结果，agent获得对应的reward($$R_{t+1}\in \widehat{R} \subset R$$实数),并获得新的state $$S_{t+1}$$  

MDP和agent一起产生了下列序列：  

$$S_{0},A_{0},R_{1},S_{1},A_{1},R_{2},S_{2},A_{2},R_{3}...$$


