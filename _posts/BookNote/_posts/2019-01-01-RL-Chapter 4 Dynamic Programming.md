---
layout: post
title: Chapter 4 Dynamic Programming
date:   2019-03-23
categories: ["Reinforcement Learning:An Introduction"]
---

动态规划：解决决策过程中最优化的数学方法，把多阶段过程转换为一系列单阶段问题，利用各阶段之间的关系，逐个求解，解决这类过程优化问题的方法。  

线性规划：研究线性约束条件下线性目标函数的极值问题的数学理论和方法。  
+ 数学模型：  
列出约束条件及目标函数   
画出约束条件所表示的可行域   
在可行域内求目标函数的最优解及最优值  

The term dynamic programming (DP) refers to a collection of algorithms that can be used to compute optimal policies given a perfect model of the environment as a Markov decision process (MDP).

这里假设environment是有限MDP，state,action,rewards集合($$\widehat{S},\widehat{A},\widehat{R}$$)也是有限的,它的动态由$$P(s',r\mid s,a)$$给出，$$s\in \widehat{S},a\in \widehat{A},r\in \widehat{R},s'\in \widehat{S^+}$$($$\widehat{S^+}=\widehat{S}+$$terminal state)。尽管DP可以用于连续的state和action空间，更普遍的方式是将state和action离散化，然后使用finite-state DP 方法。

这章将展示如何通过DP求解value function,通过optimal value function获得最优策略,optimal value function公式：  

$$
V_{\ast} (s)=\mathop{max}_{a}E_{\pi_{\ast}}[R_{t+1}+\gamma V_{\ast}(S_{t+1})\mid S_{t}=s,A_{t}=a]\\
=\mathop{max}_{a} \sum_{s',r}P(s',r\mid s,a)[r+\gamma V_{\ast}(s')]
$$  

$$q_{\ast} (a,s)=E[R_{t+1}+\gamma \mathop{max}_{a'} q_{\ast}(S_{t+1},a') \mid S_{t}=s,A_{t}=a]\\
= \sum_{s',r}P(s',r\mid s,a)[r+\gamma \mathop{max}_{a'}  q_{\ast}(s',a')]$$


**1、Policy Evaluation(Prediction)策略评估**  

Policy Evaluation：对任意$$\pi$$,计算state-value fuction $$V_{\pi}$$,这是一个prediction problem  

$$V_{\pi}(s)=E_{\pi}[G_{t}\mid S_{t}=s]\\
=E_{\pi}[R_{t+1}+\gamma G_{t+1} \mid S_{t}=s]\\
=E_{\pi}[R_{t+1}+\gamma V_{\pi}(S_{t+1}) \mid S_{t}=s]\\
=\sum_{a}\pi(a\mid s)\sum_{s',r}P(s',r\mid s,a)[r+\gamma V_{\pi}(s')],for\ all \ s\in  \widehat{S}  \qquad  \qquad (4.1)$$   


$$\pi(a\mid s)$$表示在策略$$\pi$$下，处于状态s时采取行动a的概率，$$E_{\pi}$$采取策略$$\pi$$下的期望  

假设环境动态是已知的即$$P(s',r\mid s,a)$$已知，固定策略$$\pi$$，考虑近似value function 序列{$$V_{0},V_{1},V_{2}...$$}将$$\widehat{S^+}$$映射到实数，初始值$$V_{0}$$对任意状态是任意取值(除了terminal state,它的值应被设为0)，通过Bellman equation式子更新：

$$
V_{k+1}(s)=E_{\pi}[R_{t+1}+\gamma V_{k}(S_{t+1}) \mid S_{t}=s]\\
=\sum_{a}\pi(a\mid s)\sum_{s',r}P(s',r\mid s,a)[r+\gamma V_{k}(s')],for\ all \ s\in  \widehat{S}
$$  

当$$k \to \infty$$,序列$${V_{k}}$$收敛于$$V_{\pi}$$
