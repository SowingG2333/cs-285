# MDP: Markov-Decision-Process

- handwrite-note: [[强化学习公式推导.pdf]]
- infinite-horizon-case: we try to maximize the average reward function when T -> infinite, because if $\mu \sim p_\theta(s, a)$, a stationary distribution, the average reward will be stationary
	![[Pasted image 20250417181236.png]]
- smooth-related
	![[Pasted image 20250417182159.png]]
	- Q: 强化学习中,我们将优化目标设置为期望是为了将离散化不可微的奖励变为平滑的期望，我举一个例子：在多分类任务中我们经常输出一个softmax的软标签，但是如果在强化学习中，奖励是根据硬标签来分配的；从软标签到硬标签直接有一道backward无法跨过的鸿沟，但是如果我们用期望，就相当于把软标签和reward联系起来了，从而可以进行backward，这样的理解正确吗？
	- A: 你的类比完全正确！​**强化学习通过策略的“软分布”生成动作，结合期望操作将硬奖励转化为可微目标，这与分类任务中通过Softmax将硬标签软化的逻辑一致**。图片中的平稳分布理论为此提供了数学基础——即使奖励函数本身非光滑，长期期望的光滑性使得基于梯度的优化成为可能。(DeepSeek)

---

# Algorithms
## general: 3 main parts

![[Pasted image 20250417233918.png]]
![[Pasted image 20250417234525.png]]
1. generate samples (trajectory): run current policy in environment
2. fit a model  / estimate the return
3. improve the policy

---

# Value Functions
## Q-Function

![[Pasted image 20250418000721.png]]
- 基于st，at的后续步骤预期奖励总和，即“在状态 s 下执行动作 a 有多好”
## Value-Function

![[Pasted image 20250418001117.png]]
- 基于st的后续步骤预期奖励总和，即“处于状态 s 有多好”
## idea: policy-improvement

- related：[[策略改进思想]]

![[Pasted image 20250418002310.png]]

---

# Different Algorithms

- select different algorithms according to the real situation
## sample-efficiency

![[Pasted image 20250418143934.png]]
- how many samples do we need to get a good policy?
- **off policy**: able to improve the policy without generating new samples
- **on policy**: each time the policy changed, need to generate new samples -- **policy-gradient algorithms**
- on policy 往往在采样上效率较低（用过即弃），但是挂钟时间wall clock time并不等于sample-efficiency，off policy在计算层面上可能消耗更大（处理distribution-draft，收敛更复杂）
## stability and ease of use

- converge problem
- **RL is often not gradient descent!**
### 几种常见的RL算法

![[Pasted image 20250418152423.png]]
- Q-Learning/Policy-Gradient/Model-based-RL
- related: [[常见RL-Algorithm基本思想]]
## assumptions

1. full observation
2. episodic-learning
3. continuity or smoothness