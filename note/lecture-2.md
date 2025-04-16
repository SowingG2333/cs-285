# from traditional ML to RL

- input $x_t$ -> observation $o_t$
- output $y_t$ ->  action $a_t$
- predicting process with param $\theta$ -> policy $\pi_{\theta}(a_t|o_t)$ 
# from observation $o_t$ to state $s_t$
![[Pasted image 20250416094952.png]]

- an image's observation $o_t$ is a partial/noisy representation of current state $s_t$
- $o_t$ maybe can't determine the real $s_t$
- markov feature
- Q：**o能否真正表征s？这是否类似于传统ml中的特征提取？**
	1. o有时候能够直接表征s（围棋中的棋盘状态），有时候又无法完全表征
	2. ML中的特征提取和RL中o到s映射的构建，目标都是提取对任务有用的信息；但是s需要满足markov要求，特征提取则不受markov要求的限制，并且通常是静态数据
	3. o并不具备markov属性，只有s具有——我们尽可能使得o逼近s
# imitation learning

- like traditional supervised learning, we give the model observation and its action to train the RL model (behavior-clone)
- **it dosen't work**: when the model makes some **small mistakes**, it will be different from the training data, and it will don't know what to do (the current state is different from its training data), so it will make bigger mistakes
- NVIDIA-3-CAMERAS: 3 cameras are distributed in different angels to correct **small mistakes** above to reduce the mistake-accumulate
- **trick1**: let training-date show the mistakes and its correction (反馈控制器) -- let the model to learning correction policy —— 手动修正错误action进行训练，关注单个数据的纠正
- **trick2**: dataset-aggregation -- correct the dataset-distribution（类似于数据增强）-- need human to make decision/tags —— 将修正后的数据加入训练，关注整个数据分布的纠正
	![[Pasted image 20250416110312.png]]
	- Q：**drift和联邦学习中的skew区别在？RL中的分布偏移是否来源于自身的状态/上一个action会影响下一个action，而自身的状态与理想训练状态不可避免的会出现偏差，所以面对的真实输入与训练出现偏差？**
		1. drift是模型训练数据与应用场景数据分布不一致（协变量偏移、概念偏移）
		2. skew是指FL中clients的数据分布差异较大，导致global-model难以泛化
		3. RL的分布偏移确实某种程度上与agent的策略迭代/环境交互的耦合性相关
- reasons fail to fit the expert:
	1. non-markovian behaviour -- solution: combine with RNN/LSTM etc.
		- 因果混淆问题-causal confusion
			- Q1: **包含历史信息会不会加重因果混淆**
				- 如果因果关联不依赖于时序信息，可能加重；如果因果关联依赖于时序信息，可能缓解
			- Q2: **dagger会减弱因果混淆吗**
				- 某种程度上expert的介入可以减弱因果混淆，打断与无关特征的联系
			![[Pasted image 20250416113300.png]]
	2. multimodel-behavior：在无人机飞行决策中，如果对向左和向右的概率进行平均，会得到错误的直飞决策
		- details: [[多模态建模技术]]
		- solution: signal gaussian
			- mixture of gaussians
			- latent variable model
			- autoregressive discretization

