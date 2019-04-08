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

马尔可夫决策过程中agent和environment互动过程：




agent和environment在离散时间序列(t=0,1,2..)每个时刻进行互动，在每个时刻t，agent收到environment's state($$S_{t}\in \widehat{S}$$)并据此选择action($$A_{t}\in \widehat{A}(s)$$),作为action结果，agent获得对应的reward($$R_{t+1}\in \widehat{R} \subset R$$实数)和新的state $$S_{t+1}$$  

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

我们希望最大化expected return($$G_{t}$$),$$G_{t}$$被定义为function of the reward sequence 

$$G_{t}=R_{t+1}+R_{t+2}+R_{t+3}...R_{T}  \qquad  T \ is \ the \ final \ time \ step$$  

将agent-enviroment 互动分解为一个个子序列，称为episodes，一个子序列是一个episode，每个episode的末尾状态称为terminal state。(会在有限步骤下终止的强化学习问题)    
每个episode会以terminal state为结束，并返回不同rewards(子序列reward)。    
下一个episode开始跟前一个episode的结束是独立的    

将nonterminal states 记为$$S$$，terminal states 记为$$S^+$$，time of termination(终止时间)记为T，T是一个随机变量，每个episode的T取值往往不一样。   
这种涉及episodes任务称为episodic tasks   

在很多情况下，并不能将agent-enviroment 互动分解成一个个子序列,因为互动是无限制继续下的(强化学习的问题有无限步骤)，$$T=\infty$$，return也是无限的   

discounted return:    

$$G_{t}=R_{t+1}+\gamma R_{t+2}+\gamma^2 R_{t+3}...=\sum_{k=0}^{\infty}\gamma^kR_{t+k+1} \ 0\le \gamma \le 1$$

$$ \gamma$$是disounting rate,如果$$ \gamma <1$$,只要序列$${R_{k}}$$是有界的，则$$G_{t}$$不是无限的，如果$$ \gamma =0$$，相当于值关注immediate rewards,当$$ \gamma$$越接近1说明越考虑未来的rewards,agent是有远见的




