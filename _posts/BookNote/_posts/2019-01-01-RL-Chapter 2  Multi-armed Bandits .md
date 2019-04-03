---
layout: post
title: Chapter 2 Multi-armed Bandits 
date:   2019-03-23
categories: Reinforcement Learning:An Introduction
---

多臂老虎机(Multi-armed Bandits)是一种用零钱赌博的机器，因为上面有老虎图案的筹码而得名。老虎机有三个玻璃框，里面有不同的图案，投币之后拉下拉杆(游戏会提供k个杆，选择其中一个)，就会开始转，如果出现特定的图形（比如三个相同）就会吐钱出来，出现相同图型越多奖金则越高,我们希望通过数次拉杆后，获得最大期望奖金。通过n次action后，获得最大期望total reward，这种类型问题称为"bandit problem"  
 
$$A_{t}:$$t时刻选的的action      

$$R_{t}:$$t时刻选action返回的reward   

$$q\ast (a):$$选择action a 期望reward   

$$Q_{t}(a):$$t时刻选action a,返回的value的估计   

$$q\ast (a)=E[R_{t}\mid A_{t}=a]$$    

我们希望$$Q_{t}(a)$$近似$$q\ast (a)$$    

**1、greedy action、exploiting、exploring**  

greedy action：在每个时间t,会有一个action使得估计$$Q_{t}(a)$$最大，这个action称为greedy action   n

当我们选择greedy action这个行为称为，you are exploiting your current knowledge of the values of the actions.(你正在运用了你目前对行动价值的了解。)   

选择nongreedy action这个行为称为:you are exploring, because this enables you to improve your estimate of the nongreedy action's value.   

Exploitation 可以获得当前估计的最大化期望reward，Exploration 在短期看reward可能是较低的，但长远看可能可以获得更大的total reward，通过探索一旦发现更好的action,可以在以后exploit它们。  

因为选择action时不能同时实现Exploitation和Exploration，这里存在是一个矛盾，怎么均衡Exploitation和Exploration。  


**2、Action-value Methods**  

估计action的Q,并根据Q选择action。

sample -average method估计Q :

$$Q_{t}(a)=\frac{sum \ of \ rewards\ when \ a \ taken \ prior \ to \ t}{number \  of \ times \ a \ taken \ prior \ to \ t}=\frac{\sum_{i=1}^{t-1}R_{i}\mathbb{1}_{A_{i}=a}}{\sum_{i=1}^{t-1}\mathbb{1}_{A_{i}=a}}$$   

greedy action selection method选择a:  

$$A_{t}=\mathop{\arg\max}{a}Q_{t}(a) $$ 

$$\varepsilon$$-greedy methods:每次选择action时，以$$1-\varepsilon$$概率选择greedy action，以$$\varepsilon$$概率随机选择action

