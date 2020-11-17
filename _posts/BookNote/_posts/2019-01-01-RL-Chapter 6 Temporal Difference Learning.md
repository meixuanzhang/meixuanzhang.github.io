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

$$V(S_{t})\gets V(S_{t})+\alpha[R_{t+1}+\gamma V(S_{t+1})-V(S_{t})]$$     

Monte Carlo method 更新的是$$G_{t}$$,TD更新的是$$R_{t+1}+\gamma V(S_{t+1})$$,这个TD方法称为$$TD(0)$$,或者one-step TD,它是$$TD(\lambda)$$即n-step TD的特例   


![_config.yml]({{ site.baseurl }}/images/12RL/image23.png)  

$$TD(0)$$方法更新是基于现有的估算，称之为**bootstrapping**  

粗略地说，Monte Carlo 方法以(6.1)的估计作为目标，而DP方法以(6.2)的估计作为目标。

$$V_{\pi}(s)=E_{\pi}[G_{t}\mid S_{t}=s] \qquad \qquad 6.1\\
=E_{\pi}[R_{t+1}+\gamma G_{t}\mid S_{t}=s]\\
=E_{\pi}[R_{t+1}+\gamma V_{\pi}(S_{t+1})\mid S_{t}=s]  \qquad \qquad 6.2
$$  

Monte Carlo 目标是一个估计，因为式子6.1期望值未知,用return($$G_{t}$$)样本估计实际的$$G_{t}$$期望值。 DP目标是一个估计，但不是因为$$G_{t}$$期望值，是因为$$V_{\pi}(S_{t+1})$$未知,使用当前$$V(S_{t+1})$$替代。  

TD methods combine the sampling of Monte Carlo with the bootstrapping of DP.it samples the expected values in 6.2 and it uses the current estimate $$V$$ instead of the true $$V_{\pi}$$

我们将TD和Monte Carlo更新称为Sample updates，因为它们涉及到预测样本后续状态（或状态-操作对），使用后续状态的值和沿途的奖励来计算备份值，然后相应地更新original state（or state-action pair）的值。样本更新不同于DP方法的预期更新，因为它们基于单个样本后继，而不是基于所有可能后续样本的完整分布。


TD error(measuring the diﬀerence between the estimated value of $$S_{t}$$ tand the better estimate $$R_{t+1} + \gamma V(S_{t+1})$$:   

$$\delta_{t}=R_{t+1}+\gamma V(S_{t+1})-V(S_{t})$$   

The TD error depends on the next state and next reward, it is not actually available until one time step later.

if the array $$V$$ does not change during the episode (as it does not in Monte Carlo methods),Monte Carlo error can be written as a sum of TD errors:  

[为什么需要$$V$$不改变？](https://amreis.github.io/ml/reinf-learn/2019/10/14/reinforcement-learning-an-introduction-exercise-6-1.html)

$$
G_{t}-V(S_{t})=R_{t+1}+\gamma G_{t+1}-V(S_{t})+\gamma V(S_{t+1})-\gamma V(S_{t+1})\\
=\delta_{t}+\gamma (G_{t+1}-V(S_{t+1}))\\
=\delta_{t}+\gamma \delta_{t+1} +\gamma^2(G_{t+2}-V(S_{t+2}))\\
=\delta_{t}+\gamma \delta_{t+1} +\gamma^2 \delta_{t+2}+...+\gamma^{T-t-1} \delta_{T-1} + \gamma^{T-t}(G_{T}-V(S_{T})) \\
= \delta_{t}+\gamma \delta_{t+1} +\gamma^2 \delta_{t+2}+...+\gamma^{T-t-1} \delta_{T-1} + \gamma^{T-t}(0-0)\\
=\sum_{k=t}^{T-1}\gamma^{k-t}\delta_{k}
$$


This identity is not exact if $$V$$ is updated during the episode (as it is in TD(0)), but if the step size is small then it may still hold approximately

**2、Advantages of TD Prediction Methods**   

TD methods have an advantage over DP methods in that they do not require a model of the environment, of its reward and next-state probability distributions.(他们不需要关于环境，奖励和下一状态概率分布的模型。)  

The next most obvious advantage of TD methods over Monte Carlo methods is that they are naturally implemented in an on-line, fully incremental fashion.With Monte Carlo methods one must wait until the end of an episode, because only then is the return known, whereas with TD methods one need wait only one time step.(使用Monte Carlo方法，必须等到情节结束，因为只有这样才能知道收益， 而使用TD方法时，只需等待一个时间步。)   
 
Some Monte Carlo methods must ignore or discount episodes on which experimental actions are taken, which can greatly slow learning. TD methods are much less susceptible to these problems because they learn from each transition regardless of what subsequent actions are taken.   

For any fixed policy $$\pi$$, TD(0) has been proved to converge to $$V_{\pi}$$, in the mean for a constant step-size parameter if it is sufficiently small, and with probability 1 if the step-size parameter decreases according to the usual stochastic approximation conditions(书 2.7). Most convergence proofs apply only to the table-based case of the algorithm presented above, but some also apply to the case of general linear function approximation.   

**3、Optimality of TD(0)**   

**4、Sarsa: On-policy TD Control**  
