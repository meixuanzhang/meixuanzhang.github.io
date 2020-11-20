---
layout: post
title: Chapter 7 n-step Bootstrapping
date:   2020-11-20
categories: ["Reinforcement Learning:An Introduction"]
---



**1、n-step TD Prediction**   

Bootstrapping算法，指的就是利用有限的样本资料经由多次重复抽样，重新建立起足以代表母体样本分布的新样本

Monte Carlo methods perform an update for each state based on the entire sequence of observed rewards from that state until the end of the episode.

The update of one-step TD methods  is based on just the one next reward, bootstrapping from the value of the state one step later as a proxy for the remaining rewards.

One kind of intermediate method, then, would perform an update based on an intermediate number of rewards: more than one, but less than all of them until termination.(two-step update,three-step update,four-step update)

![_config.yml]({{ site.baseurl }}/images/12RL/image34.png)  

使用n-step update方法仍然是TD方法，因为它们仍然根据其与later estimate的差异来更新earlier estimate。 只是later estimate的估计不是一步，而是n步。

Methods in which the temporal diﬀerence extends over n steps are called n-step TD methods. 

$$G_{t}$$:return (cumulative discounted reward) following time t  

Monte Carlo updates the estimate of $$v_{\pi}(S_{t})$$ is updated in the direction of the complete return:  

$$G_{t} = R_{t+1} + \gamma R_{t+2} + \gamma^2 R_{t+3} + ....+\gamma^{T-t-1} R_{T}$$

where $$T$$ is the last time step of the episode.Let us call this quantity the target of the update.(把这个数量称为更新的目标)   

Monte Carlo updates the target is the return, in one-step updates the target is the ﬁrst reward plus the discounted estimated value of the next state, which we call the one-step return:

$$G_{t:t+1} = R_{t+1} + \gamma V_{t}(S_{t+1})$$

where $$V_{t}:S \to R$$ here is the estimate at time t of $$v_{\pi}$$.  

$$G_{t:t+1}$$:it is a truncated return for time t using rewards up until time t+1, with the discounted estimate$$\gamma V_{t}(S_{t+1}) $$taking the place of the other terms $$\gamma R_{t+2} + \gamma^2 R_{t+3} + ....+\gamma^{T-t-1} R_{T}$$of the full return.   

**two-step return:**   

$$G_{t:t+2} = R_{t+1} + \gamma R_{t+2} + \gamma^2 V_{t+1}(S_{t+2})$$

where now $$\gamma^2 V_{t+1}(S_{t+2})$$ corrects for the absence of the terms $$ \gamma^2 R_{t+3} + \gamma^3 R_{t+4}+....+\gamma^{T-t-1} R_{T}$$ Similarly, 

**n-step return:**

$$G_{t:t+n} = R_{t+1} + \gamma R_{t+2} + ....+\gamma^{n-1}R_{t+n} + \gamma^{n}V_{t+n-1}(S_{t+n})$$

for all $$n$$, $$t$$ such that $$ n \ge 1$$and $$0 \le t < T −n$$.

If $$t+n \ge T $$(if the n-step return extends to or beyond termination), then all the missing terms are taken . as zero, and the n-step return deﬁned to be equal to the ordinary full return $$(Gt:t+n = G_{t} if t+n \ge T)$$. 

The natural state-value learning algorithm for using n-step returns is thus：  

$$V_{t+n}(S_{t}) = V_{t+n-1}(S_{t})+ \alpha[G_{t:t+n-V_{t+n-1}(S_{t})}], \ 0 \le t < T$$

![_config.yml]({{ site.baseurl }}/images/12RL/image35.png)  

计算当前state的value需要涉及到后面的n步的R，value更新需要等待   