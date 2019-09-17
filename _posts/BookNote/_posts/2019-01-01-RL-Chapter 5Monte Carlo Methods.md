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

on-policy：由目标策略(target policy)$$\pi$$获得experience，同时使用experience更新$$\pi$$    
off-policy：由behavior policy 获得experience，更新target policy(后面解释)

The overall idea of on-policy Monte Carlo control is still that of GPI(第四章:GPI)

In on-policy control methods the policy is generally soft, meaning that $$\pi(a\mid s)>0$$($$\varepsilon$$-soft) for all $$s\in \widehat{S},a\in \widehat{A}(s)$$, but gradually shifted closer and closer to a deterministic optimal policy.  

下面展示采用$$\varepsilon$$-greedy策略的on-policy methods，即对于nongreedy action(解释在第二章)访问概率设置为$$\frac{\varepsilon}{\mid \widehat{A}(s)\mid}$$,对于greedy action访问概率设置为$$1-\varepsilon+\frac{\varepsilon}{\mid \widehat{A}(s)\mid}$$,   

可以看出$$\varepsilon$$-greedy是$$\varepsilon$$-soft的一个例子     

![_config.yml]({{ site.baseurl }}/images/12RL/image18.png)   

$$\pi ':\varepsilon$$-greedy 策略   
$$\pi: \varepsilon$$-soft 策略  

任何关于$$q_{\pi}$$的$$\varepsilon$$-greedy 策略都是对$$\varepsilon$$-soft策略的改进，这是由策略改进定理保证的。对于任何$$s\in \widehat{S}$$有：  

$$
q_{\pi}(s,\pi '(s))=\sum_{a}\pi '(a\mid s)q_{\pi}(s,a)\\
=\frac{\varepsilon}{ \mid \widehat{A}(s)\mid}\sum_{a}q_{\pi}(s,a)+(1-\varepsilon)\\
=\frac{\varepsilon}{\mid \widehat{A}(s)\mid} \sum_{a}q_{\pi}(s,a)+(1-\varepsilon)\mathop{max}_{a}q_{\pi}(s,a)\\
\ge \frac{\varepsilon}{\mid \widehat{A}(s)\mid} \sum_{a}q_{\pi}(s,a)+(1-\varepsilon)\sum_{a}\frac{\pi(a\mid s)-\frac{\varepsilon}{\mid \widehat{A}(s)\mid} }{1-\varepsilon}   \mathop{max}_{a}q_{\pi}(s,a)\\
=frac{\varepsilon}{\mid \widehat{A}(s)\mid} \sum_{a}q_{\pi}(s,a)-frac{\varepsilon}{\mid \widehat{A}(s)\mid} \sum_{a}q_{\pi}(s,a)+\sum_{a}\pi (a\mid s)q_{\pi}(s,a)\\
=V_{\pi}(s)
$$

(the sum is a weighted average with nonnegative weights summing to 1, and as such it must be lessthan or equal to the largest number averaged)    

根据策略改进定理,$$\pi '>\pi$$(即$$V_{\pi'}(s)>V_{\pi}(s)$$ for all $$s\in \widehat{S}$$)   

$$V_{*}(s)$$，$$q_{*}(s)$$:optimal value function  

考虑有两个environment，new environment规定每次选择action的策略是以$$1-\varepsilon$$概率选择greedy action，以$$\varepsilon$$概率在所有actions中随机选择一个action，通过experience估计state value，其optimal value function为：


$$
V_{*}(s)=\frac{\varepsilon}{\mid \widehat{A}(s)\mid} \sum_{a}q_{*}(s,a)+(1-\varepsilon)\mathop{max}_{a}q_{*}(s,a)\\
=\frac{\varepsilon}{\mid \widehat{A}(s)\mid} \sum_{a}\sum_{s',r}p(s',r\mid s,a)[r+\gamma V_{*}(s')]    +(1-\varepsilon)\mathop{max}_{a}\sum_{s',r}p(s',r\mid s,a)[r+\gamma V_{*}(s')]
$$

original environment 则是以上图中$$\varepsilon$$-soft策略不断更新$$\pi$$,通过experience不断更新state value，当$$V_{\pi}(s)=V_{*}(s)$$时，策略不再更新，此时是最优策略：   


$$
V_{\pi}(s)=\frac{\varepsilon}{\mid \widehat{A}(s)\mid} \sum_{a}q_{\pi}(s,a)+(1-\varepsilon)\mathop{max}_{a}q_{\pi}(s,a)\\
=\frac{\varepsilon}{\mid \widehat{A}(s)\mid} \sum_{a}\sum_{s',r}p(s',r\mid s,a)[r+\gamma V_{\pi}(s')]    +(1-\varepsilon)\mathop{max}_{a}\sum_{s',r}p(s',r\mid s,a)[r+\gamma V_{\pi}(s')]
$$

**5、off-policy Prediction via Importance Sampling**    

off-policy 使用两个策略 The policy being learned about is called the **target policy**, the policy used to generate behavior is called the **behavior policy**,由于学习的数据不是从target policy获得，所以整个过程称为**off-policy learning**。  

off-policy methods are often of greater variance(方差) and are slower to converge(收敛).    
off-policy methods are more powerful and general. **They include on-policy methods as the special case in which the target and behavior policies are the same.**   

$$\pi:$$target policy，$$b$$:behavior policy    

使用off-policy methods估计$$V_{\pi},q_{\pi}$$，意味我们需要从策略b获得episodes(experience)来估计$$V_{\pi},q_{\pi}$$，同时$$\pi \ne b$$ 。  

In order to use episodes from b to estimate values for $$\pi$$, we require that every action taken under $$\pi$$ is also taken, at least occasionally, under b.(在$$\pi$$策略下发生的action,b策略下也应该发生) That is, we require that $$\pi(a\mid s)>0$$ implies $$b(a\mid s)>0$$.This is called the assumption of coverage. It follows from coverage that b must be stochastic in states where it is not identical to $$\pi$$(两个策略不同是b具有随机性,action是随机的在state下,但 $$\pi$$不一定). The target policy $$\pi$$, on the other hand, may be deterministic, and, in fact, this is a case of particular interest in control applications.  

几乎所有的off-policy method利用[importance sampling](https://meixuanzhang.github.io/ML-Monte-Carlo-method/),a general technique for estimating expected values under one distribution given samples from another.   

We apply importance sampling to off-policy learning by weighting returns according to the relative probability of their trajectories occurring under the target and behavior policies, called the **importance-sampling ratio**     

在策略$$\pi$$下，给定初始状态$$S_{t}$$,后续的state-action轨迹为$$A_{t},S_{t+1},A_{t+1},...,S_{T}$$的概率为：  

$$
Pr\{A_{t},S_{t+1},A_{t+1},...,S_{T}\mid S_{t},A_{t:T-1}\sim \pi \}\\
=\pi(A_{t}\mid S_{t})p(S_{t+1}\mid S_{t},A_{t})\pi(A_{t+1}\mid S_{t+1})...p(S_{T}\mid S_{T-1},A_{T-1})\\
=\prod_{k=t}^{T-1}\pi(A_{k}\mid S_{k})p(S_{k+1}\mid S_{k},A_{k})
$$  

上述计算使用了MDP‘s(Markov Decision Processes)   

**importance-sampling ratio**：  

$$
\rho_{t:T-1}=\frac{\prod_{k=t}^{T-1}\pi(A_{k}\mid S_{k})p(S_{k+1}\mid S_{k},A_{k})}{\prod_{k=t}^{T-1}b(A_{k}\mid S_{k})p(S_{k+1}\mid S_{k},A_{k})}\\
=\prod_{k=t}^{T-1}\frac{\pi(A_{k}\mid S_{k})}{b(A_{k}\mid S_{k})}
$$

使用策略b得到的state value: 

$$
V_{b}(S_{t})=E_{b}[G_{t}\mid S_{t}]\\
=\frac{\sum_{n=1}^{N} \prod_{k=t}^{T-1}b_{n}(A_{k}\mid S_{t}) G_{n,t}}{\sum_{n=1}^{N} \prod_{k=t}^{T-1}b_{n}(A_{k}\mid S_{t})}
$$  

使用策略$$\pi$$得到的state value:  

$$
V_{\pi}(S_{t})=E_{\pi}[G_{t}\mid S_{t}]\\
=\frac{\sum_{n=1}^{N} \prod_{k=t}^{T-1}\pi_{n}(A_{k}\mid S_{t}) G_{n,t}}{\sum_{n=1}^{N} \prod_{k=t}^{T-1}\pi_{n}(A_{k}\mid S_{t})}
$$


两者关系：  

$$
V_{\pi}(S_{t})=\frac{\sum_{n=1}^{N} \prod_{k=t}^{T-1}b_{n}(A_{k}\mid S_{t})  \frac{\prod_{k=t}^{T-1}\pi_{n}(A_{k}\mid S_{t})}{\prod_{k=t}^{T-1}b_{n}(A_{k}\mid S_{t})} G_{n,t}}{\sum_{n=1}^{N} \prod_{k=t}^{T-1}b_{n}(A_{k}\mid S_{t})\rho_{n,t:T-1}}\\
=\frac{\sum_{n=1}^{N} \prod_{k=t}^{T-1}b_{n}(A_{k}\mid S_{t}) \rho_{n,t:T-1} G_{n,t}}{\sum_{n=1}^{N} \prod_{k=t}^{T-1}b_{n}(A_{k}\mid S_{t})\rho_{n,t:T-1}} \\

=
=E_{b}[\rho_{t:T-1}G_{t}\mid S_{t}]\\
$$

使用Monte Carlo方法估计$$V_{\pi}(s)$$：   

$$\jmath(s)$$:for every-visit method,it is the set of all time steps in which state s is visited,for first-visit method,would only include time steps that were first visits to s within their episodes   

$$T(t):$$the first time of termination following time t(表示时间t之后的首次终止的时间)

ordinary importance sampling:  

$$V_{\pi}(s)=\frac{\sum_{t\in \jmath(s)}\rho_{t:T(t)-1}G_{t}}{\mid \jmath(s) \mid}$$  


weighted importance sampling:   


$$V_{\pi}(s)=\frac{\sum_{t\in \jmath(s)}\rho_{t:T(t)-1}G_{t}}{\sum_{t\in \jmath(s)}\rho_{t:T(t)-1}}$$    

对于weighted importance sampling，如果signal return中(也就是s只出现了一次,其只有一个观测G)分子和分母的$$\rho_{t:T(t)-1}$$相互抵消，那么估计值会等于这个观测值，估计的state value更可能是$$V_{b}(s)$$而不是$$V_{\pi}(s)$$,而rdinary importance sampling则不存在这个问题.   
如果$$\rho_{t:T(t)-1}$$值为10，对于ordinary importance sampling 估计出的值将是观察值的10倍，也就是说，即使该轨迹被认为能一定代表目标策略的，它离观察到的回报仍有相当大的距离。 
(举例,假设s下有两个action,在b策略中action1和action2选择概率分别是99.9%,0.1%,$$\pi$$是99%,1%,两者概率分布相似,在b采样下观测值跟估计值应该是相似的,当观测为action2时,两个策略的比率相差非常大)

两种估计方法差异还体现在ordinary importance sampling是无偏的，weighted importance sampling是有偏的，前者的方差是无边界的，因为前者ratio是无边界的，后者在任何signal return 中ratio为1。   

In fact, assuming bounded returns, the variance of the weighted importance-sampling estimator converges to zero even if the variance of the ratios themselves is infinite.    
In practice, the weighted estimator usually has dramatically lower variance and is strongly preferred.  

书中例子：  

![_config.yml]({{ site.baseurl }}/images/12RL/image19.png)   

![_config.yml]({{ site.baseurl }}/images/12RL/image20.png)   

**6、Incremental Implementation**   

假设有一系列的return$$G_{1},G_{2},...G_{n-1}$$,它们起始状态是一样的以及每个return有对应的权重$$W_{i}=\rho_{t:T(t)-1}$$则：     

$$
V_{n+1}=\frac{\sum_{k=1}^{n}W_{k}G_{k}}{\sum_{k=1}^{n}W_{k}}\\
=\frac{1}{\sum_{k=1}^{n}W_{k}}  (W_{n}G_{n}+\sum_{k=1}^{n-1}W_{k}G_{k})\\
=\frac{1}{\sum_{k=1}^{n}W_{k}} (W_{n}G_{n}+\sum_{k=1}^{n-1}W_{k} (\frac{1}{\sum_{k=1}^{n-1}W_{k}}) \sum_{k=1}^{n-1}W_{k}G_{k})\\
=\frac{1}{\sum_{k=1}^{n}W_{k}} (W_{n}G_{n}+\sum_{k=1}^{n-1}W_{k}(V_{n}))\\
=\frac{1}{\sum_{k=1}^{n}W_{k}} (W_{n}G_{n}+V_{n}(\sum_{k=1}^{n}W_{k}-W_{n}))\\
=\frac{1}{C_{n}} (W_{n}G_{n}+V_{n}(C_{n}-W_{n}))\\
=V_{n}+\frac{W_{n}}{C_{n}}[G_{n}-V_{n}] \qquad \qquad n \ge 1\\
$$  
   

用同样方法估计$$Q$$:   

![_config.yml]({{ site.baseurl }}/images/12RL/image21.png)  

对比与第二章不同这里state是不断变化的，$$Q(S_{t},A_{t}),C(S_{t},A_{t})$$更新时需要根据对应$$S_{t},A_{t}$$进行更新.


 **7、Off-policy Monte Carlo Control**    
 
 
Off-policy Monte Carlo control methods follow the behavior policy while learning about and improving the target policy. (通过行为策略学习目标策略)  
These techniques require that the behavior policy has a nonzero probability of selecting all actions that might be selected by the target policy (coverage). To explore all possibilities, we require that the behavior policy be soft (i.e., that it select all actions in all states with nonzero probability). (行为策略所有action被选择概率应不为0,确保目标策略收敛于最优策略)     

off-policy Monte Carlo control method, based on **** and weighted importance sampling, for estimating $$\pi_{*}$$ and $$q_{*}$$. The target policy $$\pi \approx \pi_{*}$$ is the greedy policy with respect to $$Q$$, which is an estimate of $$q_{\pi}$$   
  
![_config.yml]({{ site.baseurl }}/images/12RL/image22.png)    

上图中$$W$$权重更新使用的是$$\frac{1}{b(A_{t}\mid S_{t})}$$,因为这里$$\pi$$是greedy policy,除了greedy action外,其他action被选概率为0。只有greedy action时更新$$W$$   





 


