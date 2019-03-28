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

5、All reinforcement learning agents have explicit goals(明确目标), can sense aspects of their environments(感知环境), and can choose actions to influence their environments(通过行为影响环境)    

**2、Examples**  

书里举的例子包含以下方面：  

所有例子都包含目标，agent需要通过与不确定性环境互动去完成目标   

agent行动会影响环境未来状态，进而友影响后面agent决策，agent应具有预判和计划能力。  

行动造成的影响不能完全被预测，因此agent需要频繁监测环境做出相应的反应。   

agent可以通过经验提升表现   


**3、Elements of Reinforcement Learning**  

reinforcement learning 系统主要4个元素：a policy, a reward signal, a value function, and, a model of the environment(可选).  

1、A policy defines the learning agent's way of behaving at a given time. agent策略  

2、A reward signal defines the goal in a reinforcement learning problem. On each time step, the environment
sends to the reinforcement learning agent a single number called the reward .The agent's sole
objective is to maximize the total reward it receives over the long run. The reward signal thus defines
what are the good and bad events for the agent. 即时的奖励  

3、A value function specifies what is good in the long run.the value of a state is the total amount of reward an agent can expect to accumulate over the future, starting from that state.  长远的回报  

Whereas rewards determine the immediate, intrinsic desirability of environmental states, values indicate the long-term desirability
of states after taking into account the states that are likely to follow, and the rewards available in those
states.  

Action choices are made based on value judgments. 行动选择取决于对value判断

4、a model of the environment is something that mimics the behavior of the environment, that allows inferences
to be made about how the environment will behave.  如，基于情境和行动，预测环境返回reward以及下一个情境状态

5、Models are used for planning, by which we mean any way of deciding on a course of action by considering possible future situations before they are actually experienced. 

Methods for solving reinforcement learning problems that use models and planning are called model-based methods, as opposed to simpler model-free methods that are explicitly trial-anderror learners viewed as almost the opposite of planning.model-based就是对环境建模，描述环境是如何工作，使用规划算法找到最优策略 


**4、Limitations and Scope** 

1、Reinforcement learning relies heavily on the concept of state ——as input to the policy and value function(state是策略和回报函数的输入),
and as both input to and output from the model(state是环境模型的输入和输出).  

2、we can think of the state as a signal conveying to the agent some sense of "how the environment is" at a particular time.We do not address the issues of constructing, changing, or learning the state signal in this book.本书将状态认为是一种信号传送给agent，让agent感知现在环境怎样，没有说到如果构建、改变、学习状态信号   

In other words, our main concern is not with designing the state signal, but with deciding what action to take as a function of whatever state signal is available.主要关注设计任何状态下应采取什么行动的函数   

3、本书大部分强化学习方法围绕value function的估计。   

**5、An Extended Example: Tic-Tac-Toe三连棋游戏**   

使用value function 方法：  

1、将游戏中所有可能的状态列举    
2、假设我们使用$$X_{s}$$,所有$$X_{s}$$三连一线的state，赢的概率设为1，所有$$O_{s}$$三连一线的state，赢的概率设为0，其他state赢的概率设为0.5    
3、检查每个可能的动作会产生的状态,在表中找到它们当前Value。大多时候选择能达到赢的概率最大的状态的移动(贪婪移动)，有时会随机选择移动为了探索从没遇见的状态     
4、为了更准确估计状态赢的概率，将贪婪移动前的状态$$s$$的值更新为更接近移动后状态$$s'$$的值，即$$V(s) \gets V(s)+\alpha[V(s'-V(s))],\alpha$$是步长参数，影响学习率。这种更新方式是一种temporal-difference 学习方法。     


**Summary**   

强化学习是一种计算方法，能理解并自动有目标的学习和决策。 它通过代理人从与环境的直接互动中学习，而不依赖于模范监督或完整的环境模型。    
强化学习使用马尔可夫决策过程的框架来确定交互学习代理人与其环境之间的状态，行动和奖励。  

