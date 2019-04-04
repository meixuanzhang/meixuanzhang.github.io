---
layout: post
title: Chapter 2 Multi-armed Bandits 
date:   2019-03-23
categories: Reinforcement Learning:An Introduction
---

多臂老虎机(Multi-armed Bandits)是一种用零钱赌博的机器，因为上面有老虎图案的筹码而得名。老虎机有三个玻璃框，里面有不同的图案，投币之后拉下拉杆(游戏会提供k个杆，选择其中一个)，就会开始转，如果出现特定的图形（比如三个相同）就会吐钱出来，出现相同图型越多奖金则越高,我们希望通过数次拉杆后，获得最大期望奖金。通过n次action后(每次action是玩一场游戏，单一情境下行动)，获得最大期望total reward，这种类型问题称为"bandit problem"  
 
$$A_{t}:$$t时刻选的的action      

$$R_{t}:$$t时刻选action返回的reward   

$$q\ast (a):$$选择action a 期望reward   

$$Q_{t}(a):$$t时刻选action a,返回的value的估计   

$$q\ast (a)=E[R_{t}\mid A_{t}=a]$$    

我们希望$$Q_{t}(a)$$近似$$q\ast (a)$$    

**1、greedy action、exploiting、exploring**  

greedy action：在每个时间t,会有一个action使得估计$$Q_{t}(a)$$最大，这个action称为greedy action  

当我们选择greedy action这个行为称为，you are exploiting your current knowledge of the values of the actions.(你正在运用了你目前对行动价值的了解。)   

选择nongreedy action这个行为称为:you are exploring, because this enables you to improve your estimate of the nongreedy action's value.   

Exploitation 可以获得当前估计的最大化期望reward，Exploration 在短期看reward可能是较低的（可能是当前估计不准确造成的），但长远看可能可以获得更大的total reward，通过探索一旦发现更好的action,可以在以后exploit它们。 

因为选择action时不能同时实现Exploitation和Exploration，这里存在是一个矛盾，怎么均衡Exploitation和Exploration。  


**2、Action-value Methods**  

估计action的Q,并根据Q选择action。

sample -average method估计Q :

$$Q_{t}(a)=\frac{sum \ of \ rewards\ when \ a \ taken \ prior \ to \ t}{number \  of \ times \ a \ taken \ prior \ to \ t}=\frac{\sum_{i=1}^{t-1}R_{i}\mathbb{1}_{A_{i}=a}}{\sum_{i=1}^{t-1}\mathbb{1}_{A_{i}=a}}$$   

greedy action selection method选择a:  

$$A_{t}=\mathop{\arg\max}_{a}Q_{t}(a) $$ 

$$\varepsilon$$-greedy methods:每次选择action时，以$$1-\varepsilon$$概率选择greedy action，以$$\varepsilon$$概率随机选择action


**3、Example: the 10-armed Testbed**  

$$q\ast (a),a=1,.,10$$的值通过均值为0，方差为1的高斯分布产生  
$$R_{t}$$的值通过均值为$$q\ast (A_{t})$$,方差为1的高斯分布产生   
这个例子中$R_{t}$$概率分布是稳定的，不会随时间变化
结果如图： 
![_config.yml]({{ site.baseurl }}/images/12RL/image1.png)

使用sample -average估计Q，对比不同greedy method下，决策效果：   
$$\varepsilon=0$$，action的选择困在了局部最优action，，从长远看表现比较差    
$$\varepsilon=0.1$$，很快找到了最优action   
$$\varepsilon=0.01$$,找到最优action速度较慢    
reward方差越大，$$\varepsilon$$应越大，更多的取探索  

![_config.yml]({{ site.baseurl }}/images/12RL/image2.png)  

**4、Incremental Implementation**  

sample -average method估计Q :  

$$Q_{t}(a)\frac{\sum_{i=1}^{t-1}R_{i}\mathbb{1}_{A_{i}=a}}{\sum_{i=1}^{t-1}\mathbb{1}_{A_{i}=a}}$$   

现将$$R_{1},R_{2}..R_{n-1}$$定义t-1次游戏中有n-1次选择了action a 返回的reward,则$$Q_{t}(a)$$估计为：  

$$
Q_{n}(a)=\frac{R_{1}+R_{2}+..+R_{n-1}}{n-1}\\
Q_{t}(a) = Q_{n}(a)
$$


上面式子需要记录游戏所有action以及返回的reward，每场游戏后才能重新计算Q(a),为此提出incremental implementation(只需要记录每个action最新的Q及已经action次数):  

$$Q_{n+1}(a)=\frac{1}{n}\sum_{i=1}^nR_{i}\\
=\frac{1}{n}(R_{n} +\sum_{i=1}^{n-1}R_{i})\\
=\frac{1}{n}(R_{n} +(n-1) \frac{1}{n-1}\sum_{i=1}^{n-1}R_{i})\\
=\frac{1}{n}(R_{n} +(n-1)Q_{n}(a))\\
=\frac{1}{n}(R_{n} +(nQ_{n}(a)-Q_{n}(a))\\
=Q_{n}(a)+\frac{1}{n}[R_{n}-Q_{n}(a)]$$           (2.1)    

$$R_{n}$$是第n次选择action a 产生的reward    
对于任意的$$Q_{1},Q_{2}=R_{1}$$
式子(2,1)一般形式是：   
NewEstimate $$\gets$$ OldEstimate + StepSize[Target-OldEstimate]    

算法流程：  
![_config.yml]({{ site.baseurl }}/images/12RL/image3.png)

**5、Tracking a Nonstationary promble**  
前面提到bandit promble是stationary的，即reward分布不随时间变化，任何时候产生的reward都是一样重要的，强化学习中问题往往是Nonstationary，相比起过去rewards,recent rewards应有更大的权重，因为提出常数的步长参数(step-size parameter)$$\alpha$$。对(2.1)公式进行修改：  

$$Q_{n+1}=Q_{n}+\alpha[R_{n}-Q_{n}]\\
=\alpha R_{n}+(1-\alpha)Q_{n}\\
=\alpha R_{n}+(1-\alpha)[\alpha R_{n-1}+(1-\alpha)Q_{n-1}]\\
=\alpha R_{n}+(1-\alpha)\alpha R_{n-1}+(1-\alpha)^2 Q_{n-1}\\
=\alpha R_{n}+(1-\alpha)\alpha R_{n-1}+(1-\alpha)^2 \alpha R_{n-2}+..+(1-\alpha)^{n-1}\alpha R_{1}+(1-\alpha)^n Q_{1}\\
=(1-\alpha)^n Q_{1}+\sum_{i=1}^n \alpha(1-\alpha)^{n-i}R_{i}$$  

$$\alpha$$取值范围$$(0,1]$$  
