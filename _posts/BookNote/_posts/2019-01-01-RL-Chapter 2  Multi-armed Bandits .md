---
layout: post
title: Chapter 2 Multi-armed Bandits 
date:   2019-03-23
categories: ["Reinforcement Learning:An Introduction"]
---

多臂老虎机(Multi-armed Bandits)是一种用零钱赌博的机器，因为上面有老虎图案的筹码而得名。老虎机有三个玻璃框，里面有不同的图案，投币之后拉下拉杆(游戏会提供k个杆，选择其中一个)，就会开始转，如果出现特定的图形（比如三个相同）就会吐钱出来，出现相同图型越多奖金则越高,我们希望通过数次拉杆后，获得最大期望奖金。通过n次action后(每次action是玩一场游戏，单一情境下行动)，获得最大期望total reward，这种类型问题称为"bandit problem"  
 
$$A_{t}:$$t时刻选的的action      

$$R_{t}:$$t时刻选action返回的reward   

$$q\ast (a):$$选择action a 期望reward   

$$Q_{t}(a):$$t时刻选action a,返回的value的估计   

$$q\ast (a)=E[R_{t}\mid A_{t}=a]$$    

这里Multi-armed Bandits游戏目标是玩n场游戏，获得最大期望的total reward(Q)，对于这类情境单一，非序列决策的游戏即每次action获得最大的期望reward,我们希望$$Q_{t}(a)$$近似$$q\ast (a)$$，获得每个action的期望reward。

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

$$\varepsilon$$-greedy methods:每次选择action时，以$$1-\varepsilon$$概率选择greedy action，以$$\varepsilon$$概率在non-greedy actions随机选择一个action


**3、Example: the 10-armed Testbed**  

$$q\ast (a),a=1,.,10$$的值通过均值为0，方差为1的高斯分布产生  
$$R_{t}$$的值通过均值为$$q\ast (A_{t})$$,方差为1的高斯分布产生   
这个例子中$$R_{t}$$概率分布是稳定的，不会随时间变化
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
=Q_{n}(a)+\frac{1}{n}[R_{n}-Q_{n}(a)] \qquad \qquad\qquad (2.1) $$              

$$R_{n}$$是第n次选择action a 产生的reward    
对于任意的$$Q_{1},Q_{2}=R_{1}$$
式子(2,1)一般形式是：   
NewEstimate $$\gets$$ OldEstimate + StepSize[Target-OldEstimate]    

算法流程：  
![_config.yml]({{ site.baseurl }}/images/12RL/image3.png)

**5、Tracking a Nonstationary promble**  

前面提到bandit promble是stationary的，情境单一，reward分布不随时间变化，任何时候产生的reward都是一样重要的，强化学习中问题往往是Nonstationary，相比起过去rewards,recent rewards应有更大的权重，因为提出常数的步长参数(step-size parameter)$$\alpha$$。对(2.1)公式进行修改：  

$$Q_{n+1}=Q_{n}+\alpha[R_{n}-Q_{n}]\\
=\alpha R_{n}+(1-\alpha)Q_{n}\\
=\alpha R_{n}+(1-\alpha)[\alpha R_{n-1}+(1-\alpha)Q_{n-1}]\\
=\alpha R_{n}+(1-\alpha)\alpha R_{n-1}+(1-\alpha)^2 Q_{n-1}\\
=\alpha R_{n}+(1-\alpha)\alpha R_{n-1}+(1-\alpha)^2 \alpha R_{n-2}+..+(1-\alpha)^{n-1}\alpha R_{1}+(1-\alpha)^n Q_{1}\\
=(1-\alpha)^n Q_{1}+\sum_{i=1}^n \alpha(1-\alpha)^{n-i}R_{i} \qquad \qquad\qquad (2.2)$$  

$$\alpha$$取值范围$$(0,1]$$   
$$(1-\alpha)^n+\sum_{i=1}^n \alpha(1-\alpha)^{n-i}=1$$   
(2.2)式子称为：exponential recency-weighted average,$$R_{i}$$权重随着奖励次数增加而衰减  

将$$\alpha_{n}(a)$$定义为步长参数，在sample -average method中$$\alpha_{n}(a)=\frac{1}{n}$$，根据大数定律保证其能收敛于真实的action values。但不是所有{$$\alpha_{n}(a)$$}序列都能保证收敛的，根据stochastic approximation theory以概率1收敛条件是：  

$$\sum_{n=1}^{\infty}\alpha_{n}(a)=\infty $$ 和 $$\sum_{n=1}^{\infty}\alpha_{n}^2(a)<\infty$$   

第一个条件保证步伐足够大克服了任何初始状态(如任意$$Q_{1}$$)和随机波动影响，第二条保证最终步伐变得足够小确保收敛  
$$\alpha_{n}(a)=\frac{1}{n}$$满足这两个条件，设置为常数则不满足。  

后面的案例中，通常不满足第二个条件，意味估计值不会收敛，往往会根据最近的reward不断变化，这对于Nonstationary情境是非常有用的，我们遇见的问题往往是Nonstationary，现实中很少要求{$$\alpha_{n}(a)$$}要符合收敛条件，更多在理论中使用，同时即使符合收敛过程也是非常慢的。  

**5、Optimistic Initial Values**  

 (2.2)更新方法估计的Q是永远存在bias的，因为会一直受到初始Q影响，(2.1)方法当所有action都被选过一次后，估计的Q则不再受初始Q的影响。初始状态Q作为参数需要人为确定，对初始Q设定可以根据人的先验知识。  
 
 初始Q可以作为一种方法鼓励exploration,上面案例中，若将所有action初始Q设为常数(如+5)，无论选择哪个action,reward很大可能会小于初始Q($$q\ast (a)$$是服从均值为0，方差为1的分布),意味被选取的action的Q更新后，会小于其他action的Q，根据learner会倾向于选择其他的action,所以最终在估计值Q收敛前所有的action可能都会被选择几次。尽管每次都是选择greedy actions,这种设置会使action有大量公平机会被选取。把这种方法称为：optimistic initial values  

optimistic initial values对于stationary问题是非常有效的，但对于nonstationary问题没有效果，因为探索只发生在刚开始一段时间。如果任务发生变化，应该需要加入新的探索，这种方法没办法处理。

Any method that focuses on the initial conditions in any special way is unlikely to help with the general nonstationary case.Because
the beginning of time occurs only once.

两种策略对比：   
$$Q_{1}=5,\varepsilon=0$$开始时候表现差些，因为开始更偏向探索，随着时间推移，探索不断减少，表现不断变好    

![_config.yml]({{ site.baseurl }}/images/12RL/image4.png)  

**6、Upper-Confidence-Bound Action Selection**  

$$\varepsilon-greedy$$对于non-greedy actions没有选择偏好的随机选择，没有考虑这些actions的好坏和不确定性，为此提出UCB(upper confidence bound),根据下面公式选择action:  

$$A_{t}=\mathop{\arg\max}_{a}[Q_{t}(a)+c\sqrt{\frac{lnt}{N_{t}(a)}}]$$   

$$N_{t}(a):$$是action a在时间t以前被选择的次数    
$$c>0:$$控制exploration程度   

如果$$N_{t}(a)=0$$,action a 会被认为是获得式子最大值的action,根号里式子是对action value不确定性及方差的衡量    

公式使每个action最终都会被选择到，对于value低或已经被频繁选择的action，会随着时间增加，减少被选择的频率，同时如果随着时间t增加，$$N_{t}(a)$$没有增长的action,其被估计的value会被认为不确定性会增加，被选择频率会增加  

对比UCB和$$\varepsilon-greedy$$：  

![_config.yml]({{ site.baseurl }}/images/12RL/image5.png)  


UCB相比$$\varepsilon-greedy$$更难推拓展到其他的强化学习问题上，对上述例子虽然有很好的表现，但比较难处理nonstationary及state空间大类型的强化学习。（state空间大，UCB在每个情境下都需要探索所有action）  

**7、Gradient Bandit Algorithms**  

对每个action设置数值偏好(numerial preference)$$H_{t}(a)$$,偏好值越大的action，被选择次数更高，通过soft-max计算行动a在时间t被选概率$$\pi_{t}(a)$$为：  

$$Pr\{A_{t}=a\}=\frac{e^{H_{t}(a)}}{\sum_{b=1}^k e^{H_{t}(b)}}=\pi_{t}(a)$$  

设$$H_{1}(a)=0$$，开始时候每个action被选的概率相同  

偏好值更新方法：  

$$H_{t+1}(A_{t})=H_{t}(A_{t})+\alpha (R_{t}-\bar{R_{t}})(1-\pi_{t}(A_{t}))\\
H_{t+1}(a)=H_{t}(a)-\alpha(R_{t}-\bar{R_{t}})\pi_{t}(a),for all \  a\ne A_{t}$$ 

这里$$R_{t}$$是t时刻选择$$A_{t}$$返回的reward,$$\bar{R_{t}}$$则是估计的$$Q_{t}(A_{t})$$，估计方法参考前面。$$\bar{R_{t}}$$相当于基准(baseline),当$$R_{t}>\bar{R_{t}}$$,选择$$A_{t}$$的概率提升，当$$R_{t}<\bar{R_{t}}$$选择$$A_{t}$$的概率下降，在t时刻没有被选择的action则往相反方向更新。

下图展示了游戏过程中有baseline和没有baseline，以不同$$\alpha$$下，选中最优action的比例：  

![_config.yml]({{ site.baseurl }}/images/12RL/image6.png)  

 

**8、Associative Search(Contextual Bandits)**  

reinforcement learning 任务普遍不是单一情境的，需要学习的policy是根据不同情境(situations)选择对应最好的action。  

nonassociative task: 情境(task)固定，选择最好的action   

associative search task(Contextual Bandits)：情境(task)会变化，根据情境(task)，选择对应最好action  

full reinforcement learning问题：action会影响next situations 和reward  




 
 
 

