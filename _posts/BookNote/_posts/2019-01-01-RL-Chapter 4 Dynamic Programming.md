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

![_config.yml]({{ site.baseurl }}/images/12RL/image11.png)  

**2、Policy Improvement**   

已知$$\pi$$是deterministic policy(确定性策略：选择概率为1的动作，其他动作概率为0，？)，在s状态下value值为$$V_{\pi}$$,根据策略$$\pi$$,在s状态下选择a的value值为：

$$q_{\pi}(s,a)\\
=E[R_{t+1}+\gamma V(S_{t+1}) \mid S_{t}=s,A_{t}=a]\\
= \sum_{s',r}P(s',r\mid s,a)[r+\gamma V{\pi}(s')]$$

**policy improvement theorem**:

对于确定性策略$$\pi'$$和$$\pi$$,如果$$q_{\pi}(s,\pi'(s)) \ge V_{\pi}(s)$$,for all $$s \in \widehat{S}$$,则$$V_{\pi'}(s)\ge V_{\pi}(s)$$,for all $$s \in \widehat{S}$$,策略$$\pi'$$优于或和$$\pi$$一样好。     

如果$$q_{\pi}(s,\pi'(s)) > V_{\pi}(s)$$，for all $$s \in \widehat{S}$$，策略$$\pi'$$优于$$\pi$$。  

如果存在一个状态s使$$q_{\pi}(s,\pi'(s)) > V_{\pi}(s)$$,则至少有一个状态使$$V_{\pi'}(s) > V_{\pi}(s)$$。    

$$
V_{\pi}(s)\le q_{\pi}(s,\pi'(s))\\
=E[R_{t+1}+\gamma V_{\pi}(S_{t+1})\mid S_{t}=s,A_{t}=\pi'(s)]  \qquad only \ A_{t}=\pi'(s),A_{t+1}...is\ not \\
=E_{\pi'}[R_{t+1}+\gamma V_{\pi}(S_{t+1})\mid S_{t}=s]\\
\le E_{\pi'}[R_{t+1}+\gamma q_{\pi}(S_{t+1},\pi'(S_{t+1}))\mid S_{t}=s]\\
=E_{\pi'}[R_{t+1}+\gamma E_{\pi'}[R_{t+2}+V_{\pi}(S_{t+2})]\mid S_{t}=s]\\
=E_{\pi'}[R_{t+1}+\gamma R_{t+2}+\gamma^2 V_{\pi}(S_{t+2})\mid S_{t}=s]\\
\le E_{\pi'}[R_{t+1}+\gamma R_{t+2}+\gamma^2 R_{t+3}+\gamma^3V_{\pi}(S_{t+3})\mid S_{t}=s]\\
.\\
.\\
\le E_{\pi'}[R_{t+1}+\gamma R_{t+2}+\gamma^2 R_{t+3}+\gamma^3R_{t+4}...\mid S_{t}=s]\\
=V_{\pi'}(s)
$$

对每一个state选择能使$$q_{\pi}(s,a)$$最大的action,这种策略称为**greedy policy $$\pi'$$**:   

$$
\pi'(s)=\mathop{argmax}_{a}q_{\pi}(s,a)\\
=\mathop{argmax}_{a}[R_{t+1}+\gamma V_{\pi}(S_{t+1})\mid S_{t}=s,A_{t}=a]\\
=\mathop{argmax}_{a} \sum_{s',r}q(s',r\mid s,a)[r+\gamma V{\pi}(s')] \qquad \qquad (4.2)
$$ 

greedy policy 根据$$V_{\pi}$$选择了看起来短期最好的action,这个策略满足了policy improvement theorem,因为$$\pi'$$会优于或等于$$\pi$$。  

The process of making a new policy that improves on an original policy, by making it greedy with respect to the value function of the original policy, is called **policy improvement.**   

假设new greedy policy $$\pi'$$= old policy $$\pi$$则：   

$$
V_{\pi'}(s)=\mathop{max}_{a}E[R_{t+1}+\gamma V_{\pi'}(S_{t+1})\mid S_{t}=s,A_{t}=a]\\
=\mathop{max}_{a} \sum_{s',r}q(s',r\mid s,a)[r+\gamma V{\pi}(s')]
$$

根据optimal value function公式，$$V_{\pi'}=V_{\ast}$$,$$\pi,\pi'$$是最优策略。

这里我们只考虑了deterministic policies。stochastic policy $$\pi$$ 表示每个s状态下，选择每个行动a的具体概率$$\pi(s\mid s)$$，一般情况能将这里提到想法扩展到stochastic policy情况下。此外如果尝试使用 policy improvement step(4.2)，对于几个action都能使Value达到同样最大值，在stochastic case中不会从其中选择单一一个action(即不会单一给一个action概率为1),会平分被选择概率给这些action。

**3、Policy Iteration**    

policy $$\pi$$,通过Policy Evaluation估计$$V_{\pi}$$,通过Policy Improvement获得更好的policy $$\pi'$$,然后估计$$V_{\pi'}$$.获得更好的policy$$\pi''$$。 这样可以获得单调提升的policies和value function序列：  

$$\pi_{0}\mathop{\longrightarrow}^{E} V_{\pi_{0}}\mathop{\longrightarrow}^{I}\pi_{1}\mathop{\longrightarrow}^{E}  V_{\pi_{1}}\mathop{\longrightarrow}^{I} \pi_{2} \mathop{\longrightarrow}^{E}...\mathop{\longrightarrow}^{I}\pi_{\ast}\mathop{\longrightarrow}^{E}V_{\ast}$$ 

$$\mathop{\longrightarrow}^{E}$$:policy evaluation  
$$\mathop{\longrightarrow}^{I}$$:policy improvement  

因为finite MDP policies是有限的，因此在有限迭代中，过程最终会向最优策略和最优value function收敛。这种寻找最优策略的方式称为**policy iteration**

![_config.yml]({{ site.baseurl }}/images/12RL/image12.png)


**4、Value Iteration**  

policy iteration 缺点是每次迭代都需要更新一次Policy Evaluation step，Policy Evaluation的更新是延后的(需要更新完策略再更新)，更新需要多次扫过state set，在Policy Evaluation过程中有限次迭代策略value会收敛于真实$$V_{\pi}$$,事实上Policy Evaluation这一步可以通过一些方法进行缩短，同样保证policy iteration的收敛。如只进行一次policy evaluation 这一步的更新。**vlaue iteration**将policy improvement 和 缩减 policy evaluation联合,只需要进行一次policy improvement和policy evaluation更新：  

$$
V_{k+1}(s)=\mathop{max}_{a}E_[R_{t+1}+\gamma V_{\ast}(S_{t+1})\mid S_{t}=s,A_{t}=a]\\
=\mathop{max}_{a} \sum_{s',r}P(s',r\mid s,a)[r+\gamma V_{\ast}(s')]
$$  

![_config.yml]({{ site.baseurl }}/images/12RL/image13.png)


**5、Asynchronous Dynamic Programming**  

**Generalized Policy Iteration**  

**Efficiency of Dynamic Programming**
