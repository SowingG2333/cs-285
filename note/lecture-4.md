# MDP: Markov-Decision-Process

- handwrite-note: [[强化学习公式推导.pdf]]
- infinite-horizon-case: we try to maximize the average reward function when T -> infinite, because if $\mu \sim p_\theta(s, a)$, a stationary distribution, the average reward will be stationary
	![[Pasted image 20250417181236.png]]
- smooth-related
	![[Pasted image 20250417182159.png]]
	- Q: 强化学习中,我们将优化目标设置为期望是为了将离散化不可微的奖励变为平滑的期望，我举一个例子：在多分类任务中我们经常输出一个softmax的软标签，但是如果在强化学习中，奖励是根据硬标签来分配的；从软标签到硬标签直接有一道backward无法跨过的鸿沟，但是如果我们用期望，就相当于把软标签和reward联系起来了，从而可以进行backward，这样的理解正确吗？
	- A: 你的类比完全正确！​**强化学习通过策略的“软分布”生成动作，结合期望操作将硬奖励转化为可微目标，这与分类任务中通过Softmax将硬标签软化的逻辑一致**。图片中的平稳分布理论为此提供了数学基础——即使奖励函数本身非光滑，长期期望的光滑性使得基于梯度的优化成为可能。(DeepSeek)