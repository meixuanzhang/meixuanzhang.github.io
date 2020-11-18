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

给定一个近似值函数$$V$$，对于访问非终态的每个时间步长$$t$$计算由(6.1)或(6.2)指定的增量(increment)，但该值函数仅更改一次，即所有增量的总和 。 然后，使用新的值函数再次处理所有可用的数据(experience)，以产生新的总体增量(increment)，依此类推，直到值函数收敛为止。 之所以称为批量更新(batch updating)，是因为仅在处理完每批训练数据之后才进行更新。

在批处理更新中，只要将$$\alpha$$选为足够小，TD(0)就确定性地收敛到单个答案，而与步长参数$$\alpha$$无关。 $$constant- \alpha MC$$在相同条件下也可以确定地收敛，但是答案不同。


batch TD method was able to perform better according to the root mean-squared error measure shown in Figure 6.2. How is it that batch TD was able to perform better than this optimal method? The answer is that the Monte Carlo method is optimal only in a limited way, and that TD is optimal in a way that is more relevant to predicting returns.

Under batch training, $$constant-α MC$$ converges to values, V (s), that are sample averages of the actual returns experienced after visiting each state s. These are optimal estimates in the sense that they minimize the mean-squared error from the actual returns in the training set.

the batch TD method was able to perform better according to the root mean-squared error measure shown in Figure 6.2,Monte Carlo method is optimal only in a limited way, and that TD is optimal in a way that is more relevant to predicting returns   

例子：

![_config.yml]({{ site.baseurl }}/images/12RL/image24.png)  

Batch Monte Carlo总是在训练集上找到使均方误差(mean squared erroe)最小化的估计值，而batch TD(0)总是找到对于马尔可夫过程的最大似然模型来说正确的估计值。一般来说，参数的最大似然估计值(maximumlikelihood estimate)是使生成数据的概率最大的参数值。

在这种情况下，最大似然估计是通过观察到的事件(observed episodes)以明显的方式构建的马尔可夫过程的模型：从$$i$$到$$j$$的估计转移概率是观察到$$i$$到$$j$$的转移的比例，并且相关联奖励的期望是在这些过渡中观察到的奖励的平均值。 给定该模型，我们可以计算出值函数(value function)的估计值，如果模型完全正确，则该估计值将完全正确。 这被称为确定性等价估计(certainty-equivalence estimate)，因为它相当于假设基础过程的估计是确定的，而不是近似的。 通常batch TD(0) 收敛到确定性等价估计(certainty-equivalence estimate)。

在批处理形式(batch form)中，TD(0)比Monte Carlo法更快，因为它可以计算真实的certainty-equivalence estimate。尽管nonbatch方法既不能实现certainty-equivalence estimate也不能实现minimum squared-error estimates,，但可以将其理解为大致往这些方向上移动。 Nonbatch TD(0)可能比$$constant-\alpha MC$$快，因为它正在朝着更好的估计方向发展，即使它并没有一步到达。 目前，关于在线TD和Monte Carlo方法的相对效率尚无定论。

尽管certainty-equivalence estimate在某种意义上是一个最优解，但直接计算它几乎永远不可行。如果$$n=\mid S \mid $$ 是状态数，那么最大似然估计的过程可能需要$$n^2$$阶个存储器，而计算相应的值函数(value function)则需要$$n^3$$阶个计算步骤。在这些方面，TD方法确实可以使用不超过$$n$$阶的内存和在训练集上重复计算来近似相同的解。对于具有大状态空间的任务，TD方法可能是唯一可行的逼近确定性等价解的方法。

**4、Sarsa: On-policy TD Control**  

一个episode由states和state–action 对的交替序列组成：

![_config.yml]({{ site.baseurl }}/images/12RL/image25.png)  

在TD(0)下确保state values收敛的定理也适用于action values的相应算法：

$$Q(S_{t},A_{t})\gets Q(S_{t},A_{t})+\alpha[R_{t+1}+\gamma Q(S_{t+1},A_{t+1})-Q(S_{t},A_{t})]$$

此更新在每次从非终结状态$$S_{t}$$转换后完成,如果$$S_{t+1}$$是终结状态，则$$Q(S_{t+1},A_{t+1})$$定义为零。  

该规则使用由五部分构成的事件(quintuple)中的每个元素$$(S_{t},A_{t},R_{t+1}，S_{t+1},A_{t+1})$$，这些元素构成了从一个state–action对到下一个state–action对的过渡。

这个quintuple为该算法起名为Sarsa。 Sarsa的backup diagram 如下

![_config.yml]({{ site.baseurl }}/images/12RL/image26.png)  

基于 on-policy ,我们会对行为策略(behavior policy)$$\pi$$连续估算$$q_{\pi}$$,同时将$$\pi$$变成关于$$q_{\pi}$$的贪婪策略   

Sarsa control algorithm 的一般形式在下面的框中给出:  

![_config.yml]({{ site.baseurl }}/images/12RL/image27.png)  

Sarsa算法的收敛性取决于策略对$$Q$$的依赖性。例如，可以使用$$\varepsilon-greedy$$或$$\varepsilon-soft$$策略。 只要无限次访问所有state–action对，并且策略收敛于贪婪策略的极限，Sarsa就会以概率1收敛到optimal policy 和 action-value function（例如，可以通过设置$$\varepsilon = 1/t$$来实现$$\varepsilon-greedy$$）。

**5、 Q-learning: Oﬀ-policy TD Control**  

强化学习的早期突破之一是开发一种称为$$Q-learning$$的off-policy TD控制算法（Watkins，1989），定义如下：   

$$Q(S_{t},A_{t})\gets Q(S_{t},A_{t})+\alpha[R_{t+1}+\gamma \mathop{max}_{a}  Q(S_{t+1},a)-Q(S_{t},A_{t})]$$

在这种情况下，学习到的action-value function $$Q$$,直接近似于optimal action-value function $$q_{∗}$$，而与遵循的策略无关。 这极大地简化了算法的分析，并使用了早期收敛证明。 该策略仍然具有效果，因为它可以确定访问和更新了哪些状态操作对。

然而，正确收敛所需的全部条件是所有state–action pairs都要持续更新。正如我们在第5章中所观察到的，这是一个最低限度的要求，任何保证在一般情况下找到最佳行为的方法都必须要求它。在这一假设下，在步长参数序列常用的随机逼近条件下，已证明Q以概率1收敛于$$q_{*}$$。

![_config.yml]({{ site.baseurl }}/images/12RL/image28.png)  

![_config.yml]({{ site.baseurl }}/images/12RL/image29.png)  

**6、 Expected Sarsa**  

比起最大化下一state–action 对的$$Q$$，Expected Sarsa 使用 value的期望。考虑每一个action在当前策略下发生的可能性，这是考虑了update rule的算法  

$$
Q(S_{t},A_{t})\gets Q(S_{t},A_{t})+\alpha[R_{t+1}+\gamma E[Q(S_{t+1},A_{t+1}\mid S_{t+1})]-Q(S_{t},A_{t})]\\
\gets Q(S_{t},A_{t})+\alpha[R_{t+1}+\gamma \sum_{a}\pi(a\mid S_{t+1})Q(S_{t},a)-Q(S_{t},A_{t})]
$$

但这也遵循了$$Q-learning$$的模式。该算法与Sarsa在期望中的运动方向一致,它的backup diagram 在Figure 6.5   

算法消除了由于随机选择$$A_{t+1}$$带来的方差，如果有相同的样本，我们可能会期望它的性能比Sarsa好一些，并且确实如此。  

下图显示了与Sarsa和$$Q-learning$$相比，使用Expected Sarsa进行的cli-walking任务的摘要结果。

![_config.yml]({{ site.baseurl }}/images/12RL/image30.png)  

Expected Sarsa can safely set $$\alpha = 1 $$ without suﬀering any degradation of asymptotic performance, whereas Sarsa can only perform well in the long run at a small value of $$\alpha$$ at which short-term performance is poor.

在cliﬀ walking中，Expected Sarsa使用了on-policy，但通常它可以使用与目标策略$$\pi$$不同的策略来生成action，在这种情况下，它成为 oﬀ-policy 算法。例如，假设$$\pi$$是贪婪策略，而行为则更具探索性。那么Expected Sarsa正是$$Q-learning$$。 从这个意义上说，Expected Sarsa包含并推广了$$Q-learning$$，同时可靠地对Sarsa进行了改进。 除了少量的额外计算成本外，Expects Sarsa可能会完全主导其他两个更为著名的TD control algorithms。

**7、 Maximization Bias and Double Learning**

**8、Games, Afterstates, and Other Special Cases**