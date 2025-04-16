# from traditional ML to RL

- input $x_t$ -> observation $o_t$
- output $y_t$ ->  action $a_t$
- predicting process with param $\theta$ -> policy $\pi_{\theta}(a_t|o_t)$ 
# from observation $o_t$ to state $s_t$
![[Pasted image 20250416094952.png]]

- an image's observation $o_t$ is a partial/noisy representation of current state $s_t$
- $o_t$ maybe can't determine the real $s_t$
- markov feature
- Q：o能否真正表征s？这是否类似于传统ml中的特征提取？o并不具有markov属性，但是s具有。
# imitation learning

- like traditional supervised learning, we give the model observation and its action to train the RL model (behavior-clone)
- **it dosen't work**: when the model makes some *small mistakes*, it will be different from the training data, and it will don't know what to do (the current state is different from its training data), so it will make bigger mistakes
- NVIDIA-3-CAMERA-EXP：by 3 camera distributed in different angels to correct *small mistakes* above to reduce the mistake-accumulate
- **trick1**: let training-date show the mistakes and its correction (反馈控制器) -- let the model to learning correction policy
- **trick2**: dataset-aggregation -- correct the dataset-distribution（类似于数据增强的idea？）-- need human to make decision/tags
	![[Pasted image 20250416110312.png]]
	- 关于分布偏移（drift）的思考：和联邦学习中的skew区别在？RL中的分布偏移是否来源于自身的状态/上一个action会影响下一个action，而自身的状态与理想训练状态不可避免的会出现偏差，所以面对的真实输入与训练出现偏差？
- reasons fail to fit the expert:
	1. non-markovian behaviour -- solution: combine with RNN etc.
		- 因果混淆问题-causal confusion
			- Q1: **包含历史信息会不会加重因果混淆**
			- Q2: **dagger会减弱因果混淆吗**
			![[Pasted image 20250416113300.png]]
	2. multimodel-behavior：在无人机飞行决策中，如果对向左和向右的概率进行平均，会得到错误的直飞决策（为什么这个叫做多模态？）
		- solution: signal gaussian
			- mixture of gaussians：**为什么由单变多有效？**
			- latent variable models：**变分自编码器为什么有效？**
			- autoregressive discretization：**不懂**

