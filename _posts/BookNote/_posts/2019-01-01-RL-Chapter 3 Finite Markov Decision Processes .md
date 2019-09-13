---
layout: post
title: Chapter 3 Finite Markov Decision Processes
date:   2019-03-23
categories: ["Reinforcement Learning:An Introduction"]
---
这章主要介绍是finite Markov decision processes 类型问题，这类问题不仅涉及evaluative feedback，还涉及根据不同的situations,选择不同的action。  

MDPs是序列决策的经典模型，actions不仅会影响immediate reward ,还会影响后面的situations或state,甚至是future reward。MDPs 需要平衡 immediate 和delayed reward。  

bandit promble 是估计$$q\ast (a)$$   
MDPs 是估计$$q_{\ast} (s,a)$$或$$V_{\ast} (s)$$(s情境，最优action下value）  


**1、The Agent-Environment Interface**  

agent:leaner and decision maker(决策者)   
environment:与agent 互动的对象   
互动过程是连续的，agent根据situation选择action,environment 对选择action作出响应并向agent呈现新的situation。   

马尔可夫决策过程中agent和environment互动过程：




agent和environment在离散时间序列(t=0,1,2..)每个时刻进行互动，在每个时刻t，agent收到environment's state($$S_{t}\in \widehat{S}$$)并据此选择action($$A_{t}\in \widehat{A}(s)$$),作为action结果，agent获得对应的reward($$R_{t+1}\in \widehat{R} \subset R$$实数)和新的state ($$S_{t+1}$$)  

MDP和agent结合会生成下列序列：  

$$S_{0},A_{0},R_{1},S_{1},A_{1},R_{2},S_{2},A_{2},R_{3}...$$  

finite MDP 下，states,actions,rewards($$\widehat{S},\widehat{A},\widehat{R}$$)的集合都是有限的，$$R_{t},S_{t}$$离散概率分布只跟前一时刻的state和action有关即：  

$$P(s',r\mid s,a)=Pr\{S_{t}=s',R_{t}=r\mid S_{t-1}=s,A_{t-1}=a\}\qquad s',s \in\widehat{S},r \in \widehat{R},a\in\widehat{A} $$   

$$\sum_{s'\in \widehat{S}}\sum_{r\in\widehat{R}}=1,for\ all \ s \in\widehat{S},a\in\widehat{A}(s)$$

$$P(s'\mid s,a)=Pr\{S_{t}=s'\mid S_{t-1}=s,A_{t-1}=a\}=\sum_{r \in \widehat{R}}P(s',r\mid s,a)$$

$$r(s,a)=E[R_{t}\mid S_{t-1}=a,A_{t-1}=a]=\sum_{r \in \widehat{R}}r\sum_{s'\in\widehat{S}}P(s',r\mid s,a)$$  

$$r(s,a,s')=E[R_{t}\mid S_{t-1}=a,A_{t-1}=a,S_{t}=s']=\sum_{r \in \widehat{R}}r\frac{P(s',r\mid s,a)}{P(s'\mid s,a)}$$  


**2、Goals and Rewards**  

agent 的目标是最大化the total amount of reward,意味并不是最大化imemediate reward而是长远的 cumulative reward。   

选择提供reward方式时,应考虑agent获得最大化rewards同时应该完成目标，我们希望它完成的目标是什么。

**3、Returns and Episodes**  

我们希望最大化expected return($$G_{t}$$),$$G_{t}$$被定义为function of the reward sequence(从时间t+1到T累计reward):    

$$G_{t}=R_{t+1}+R_{t+2}+R_{t+3}+...+R_{T}  \qquad  T \ is \ the \ final \ time \ step$$  

将agent-enviroment 互动分解为一个个子序列，称为episodes，一个子序列是一个episode，每个episode的末尾状态称为terminal state。(会在有限步骤下终止的强化学习问题)    
每个episode会以terminal state为结束，并返回不同rewards(子序列reward)。    
下一个episode开始跟前一个episode的结束是独立的    

将nonterminal states 记为$$\widehat{S}$$，terminal states 记为$$\widehat{S^+}$$，time of termination(终止时间)记为T，T是一个随机变量，每个episode的T取值往往不一样。   
这种涉及episodes任务称为episodic tasks   

在很多情况下，并不能将agent-enviroment 互动分解成一个个子序列,因为互动是无限制继续下的(强化学习的问题有无限步骤)，$$T=\infty$$，return也是无限的   

discounted return:    

$$G_{t}=R_{t+1}+\gamma R_{t+2}+\gamma^2 R_{t+3}+\gamma^3 R_{t+4}...=\sum_{k=0}^{\infty}\gamma^kR_{t+k+1} \\
=R_{t+1}+\gamma(R_{t+2}+\gamma R_{t+3}+\gamma^2 R_{t+4}...)\\
=R_{t+1}+\gamma G_{t+1}  \qquad  \qquad  0\le \gamma \le 1$$   

式子中$$t<T$$,$$G_{T}=0$$

$$ \gamma$$是disounting rate,如果$$ \gamma <1$$,只要序列$${R_{k}}$$是有界的，则$$G_{t}$$不是无限的。   
假设reward是非零常数,$$\gamma <1$$则：   

$$G_{t}=constant \cdot \sum_{k=0}^{\infty}\gamma^k=constant \cdot \frac{1}{1-\gamma} $$    

如果$$ \gamma =0$$，相当于只关注immediate rewards,当$$ \gamma$$越接近1说明越考虑未来的rewards,agent是有远见的    

统一Episodic and Continuing Task标记：   

$$G_{t}=\sum_{k=t+1}^{T}\gamma^{k-t-1}R_{k} $$  

$$T$$可以等于$$\infty$$，$$\gamma$$可以等于1,但两个不能同时出现。

**4、Policies and Value Function**

value function 分为state-value function($$V_{\pi}(s)$$)和 action-value function($$q_{\pi}(s,a)$$)。
policy($$\pi$$) 是将状态映射到actions被选择概率分布，如果在t时刻，agent的policy是$$\pi$$,则$$\pi(a\mid s)$$表示当$$S_{t}=s$$时$$A_{t}=a$$的概率     

$$V_{\pi}(s)$$：the value of a state under a policy $$\pi$$     
$$V_{\pi}$$:the state-value function for policy $$\pi$$   
$$q_{\pi}(s,a)$$: the value of taking action s under a policy $$\pi$$     
$$q_{\pi}$$:the action-value function for policy $$\pi$$  
$$E_{\pi}[\cdot]$$agent 使用策略$$\pi$$下，随机变量的期望值  

$$V_{\pi}(s)=E_{\pi}[G_{t}\mid S_{t}=s]=E_{\pi}[\sum_{k=0}^{\infty}\gamma^{k}R_{t+k+1}\mid S_{t}=s],for\ all \ s \in \widehat{S}$$  

$$q_{\pi}(s,a)=E_{\pi}[G_{t}\mid S_{t}=s,A_{t}=a]=E_{\pi}[\sum_{k=0}^{\infty}\gamma^{k}R_{t+k+1}\mid S_{t}=s,A_{t}=a]$$   


$$V_{\pi}(s)=E_{\pi}[G_{t}\mid S_{t}=s]\\
=E_{\pi}[R_{t+1}+\gamma G_{t+1} \mid S_{t}=s]\\
=\sum_{a}\pi(a\mid s)[R_{t+1}+\gamma G_{t+1} \mid S_{t}=s,A_{t}=a]\\
=\sum_{a}\pi(a\mid s)E_{(R_{t+1},S_{t+1})}[R_{t+1}+(\gamma G_{t+1}\mid S_{t+1}=s') \mid S_{t}=s,A_{t}=a]\\ 

=\sum_{a}\pi(a\mid s)E_{(R_{t+1},S_{t+1})}[R_{t+1}+\gamma E_{\pi}[G_{t+1}\mid S_{t+1}=s']\mid S_{t}=s,A_{t}=a]\\ 


=\sum_{a}\pi(a\mid s)\sum_{s',r}P(s',r\mid s,a)[r+\gamma V_{\pi}(s')],for\ all \ s\in  \widehat{S}  \qquad  \qquad (3.1)$$   

$$s'$$:是next states   

式子(3.1)是Bellman equation for $$V_{\pi}$$,它描述了当前state value和下一个state value 关系，并平均了所有的可能性。

从图可知，agent处于状态s时，根据$$\pi$$有actions被选择的概率分布，根据概率分布随机选择action获得不同的$$G_{t}$$,因此$$V_{\pi}(s)=E_{\pi}[G_{t}\mid S_{t}=s]$$，描述agent在状态s下，采取策略$$\pi$$下value估计值等于处于状态$$s$$时采取策略$$\pi$$下(actions 被选择概率分布下)value期望值。

$$G_{t}=R_{t+1}+\gamma G_{t+1}$$,当agent确定$$S_{t},A_{t}$$后$$R_{t+1},S_{t+1}$$是随机变量，因为确定action后，根据函数p,会以不同的概率返回$$r,s'$$,所以$$R_{t+1}+\gamma G_{t+1}$$估计值为$$E_{(R_{t+1},S_{t+1})}[R_{t+1}+[\gamma G_{t+1} \mid S_{t+1}=s']]$$,同样在确定$$S_{t+1}=s'$$后，$$G_{t+1}$$仍是随机变量，$$G_{t+1}$$估计为$$E_{\pi}[G_{t+1} \mid S_{t+1}=s']=V_{\pi}(s')$$        


对比$$q_{\pi}(s,a)$$和$$V_{\pi}(s)$$，$$q_{\pi}(s,a)$$已经确定了$$A_{t}=a$$,因此并不存在根据概率分布选择action这一步。  

$$V_{\pi}(s)=\sum_{a}\pi(a\mid s)\sum_{s',r}P(s',r\mid s,a)[r+\gamma V_{\pi}(s')]$$  

$$q_{\pi}(s,a)=\sum_{s',r}P(s',r\mid s,a)[r+\gamma V_{\pi}(s')]$$   

![_config.yml]({{ site.baseurl }}/images/12RL/image8.png)  ![_config.yml]({{ site.baseurl }}/images/12RL/image9.png)

**5、Optimal Policies and Optimal Value Function**  

如果一个策略$$\pi$$的期望return大于另一个策略$$\pi^{'}$$，我们认为策略$$\pi$$优于策略$$\pi^{'}$$($$\pi \ge \pi^{'}$$ if and only if $$V_{\pi}(s)\ge V_{\pi_{'}}(s)$$)   

$$\pi_{\ast}$$:optimal policy(表现优于或等于其他所有策略) 

$$V_{\ast} (s)$$:optimal state-value function   

$$q_{\ast} (s,a)$$:optimal action-value function    

$$V_{\ast} (s)=\mathop{max}_{\pi} V_{\pi}(s),for\ all \ s\in \widehat{S}$$   

$$q_{\ast} (a,s)=\mathop{max}_{\pi} q_{\pi}(s,a),for\ all \ s\in \widehat{S},a \in \widehat{A}(s)$$  

$$q_{\ast} (a,s)=E[R_{t+1}+\gamma V_{\ast}(S_{t+1})\mid S_{t}=s,A_{t}=a]$$  

$$q_{\ast} (a,s)$$和$$V_{\ast} (s)$$之间的关系：  

$$
V_{\ast} (s)=\mathop{max}_{a \in \widehat{A}(s)} q_{\pi_{\ast}}(s,a)\\
=\mathop{max}_{a}E_{\pi_{\ast}}[G_{t}\mid S_{t}=s,A_{t}=a]\\
=\mathop{max}_{a}E_{\pi_{\ast}}[R_{t+1}+\gamma G_{t+1}\mid S_{t}=s,A_{t}=a]\\
=\mathop{max}_{a}E_{\pi_{\ast}}[R_{t+1}+\gamma V_{\ast}(S_{t+1})\mid S_{t}=s,A_{t}=a]\\
=\mathop{max}_{a} \sum_{s',r}P(s',r\mid s,a)[r+\gamma V_{\ast}(s')]
$$  


$$q_{\ast} (a,s)=E[R_{t+1}+\gamma \mathop{max}_{a'} q_{\ast}(S_{t+1},a') \mid S_{t}=s,A_{t}=a]\\
= \sum_{s',r}P(s',r\mid s,a)[r+\gamma \mathop{max}_{a'}  q_{\ast}(s',a')]$$  

![_config.yml]({{ site.baseurl }}/images/12RL/image10.png)




