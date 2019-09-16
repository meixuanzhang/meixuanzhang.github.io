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

在一个episode中s可能被访问很多次，如果只平均所有episode第一次访问s时的returns，使用方法是first-visit MC method，如果平均所有episode所有访问s时的returns，使用方法是every-visit MC method  

图中unless=if not(算法episode迭代顺序是逆序从结束T到开始0)

![_config.yml]({{ site.baseurl }}/images/12RL/image16.png)  

**2、Monte Carlo Estimation of Action Values**   

The Monte Carlo methods for this are essentially the same as just presented for state values, except now we talk about visits to a state-action pair rather than to a state. A state-action pair s,a is said to be visited in an episode if ever the state s is visited and action a is taken in it.    
The every-visit MC method estimates the value of a state-action pair as the average of the returns that have followed all the visits to it. The first-visitMC method averages the returns following the first time in each episode that the state was visited and the action was selected.   

使用Monte Carlo估计state-action value 方法与估计state value方法相似，区别是估计state-action value，考虑的是(s,a),算法中需要把s替换为(s,a)  

The only complication is that many state-action pairs may never be visited. If $$\pi$$ is a deterministic policy, then in following $$\pi$$ one will observe returns only for one of the actions from each state.With no returns to average, the Monte Carlo estimates of the other actions will not improve with experience.  
This is the general problem of **maintaining exploration.**  

在确定性策略下(解释在第四章)，有一些state-action pairs将不会被访问,则没有办法估计它们的state-action value,可能会错过更好的决策   

一种解决的办法是： every pair has a nonzero probability of being selected as the start.(exploring starts)   


**3、Monte Carlo Control**   

根据第四章提到的GPI(Generalized Policy Iteration),使用Monte Carlo估计value，再根据value确定$$\pi$$(确定性策略)

![_config.yml]({{ site.baseurl }}/images/12RL/image17.png)  


**4、Monte Carlo Control without Exploring Starts**   

在不使用exploring starts假设下，为了确保所有的action能经常被访问，可以使用on-policy 和 off-policy方法。   

on-policy：   
off-policy：  

In on-policy control methods the policy is generally soft, meaning that $$\pi(a\mid s)>0$$($$\varepsilon$$-soft) for all $$s\in \widehat{S},a\in \widehat{A}(s)$$, but gradually shifted closer and closer to a deterministic optimal policy.  

下面展示采用$$\varepsilon$$-greedy策略的on-policy methods，即对于nongreedy action(解释在第二章)访问概率设置为$$\frac{\varepsilon}{\mid \widehat{A}(s)\mid}$$,对于greedy action访问概率设置为$$1-\varepsilon+\frac{\varepsilon}{\mid \widehat{A}(s)\mid}$$,   

可以看出$$\varepsilon$$-greedy是$$\varepsilon$$-soft的一个例子     

![_config.yml]({{ site.baseurl }}/images/12RL/image18.png)   

$$\pi ':\varepsilon$$-greedy 策略   
$$\pi: \varepsilon$$-soft 策略  

任何关于$$q_{\pi}$$的$$\varepsilon$$-greedy 策略都是对$$\varepsilon$$-soft策略的改进，这是由策略改进定理保证的。对于任何$$s\in \widehat{S}$$有：  

$$
q_{\pi}(s,\pi(s))=\sum_{a}\pi '(a\mid s)q_{\pi}(s,a)\\
=\frac{\varepsilon}{ \mid \widehat{A}(s)\mid}\sum_{a}q_{\pi}(s,a)+(1-\varepsilon)\\
=\frac{\varepsilon}{\mid \widehat{A}(s)\mid} \sum_{a}q_{\pi}(s,a)+(1-\varepsilon)\mathop{max}_{a}q_{\pi}(s,a)\\
\ge \frac{\varepsilon}{\mid \widehat{A}(s)\mid} \sum_{a}q_{\pi}(s,a)+(1-\varepsilon)\sum_{a}\frac{\pi(a\mid s)-\frac{\varepsilon}{\mid \widehat{A}(s)\mid} }{1-\varepsilon}   \mathop{max}_{a}q_{\pi}(s,a)\\
=frac{\varepsilon}{\mid \widehat{A}(s)\mid} \sum_{a}q_{\pi}(s,a)-frac{\varepsilon}{\mid \widehat{A}(s)\mid} \sum_{a}q_{\pi}(s,a)+\sum_{a}\pi (a\mid s)q_{\pi}(s,a)\\
=V_{\pi}(s)
$$

(the sum is a weighted average with nonnegative weights summing to 1, and as such it must be lessthan or equal to the largest number averaged)    

根据策略改进定理,$$\pi '>\pi$$(即$$V_{\pi'}(s)>V_{\pi}(s)$$ for all $$s\in \widehat{S}$$)   

$$V_{*}(s)$$，$$q_{*}(s)$$:optimal value function
