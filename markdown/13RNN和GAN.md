# 人工智能

## RNN和GAN等神经网络

### 循环神经网络

- 前馈网络(Feedforward Networks)

	- 示意图

	- 概念

		- 1）直接向前递送信息(不会再次接触已经经过的结点)，而循环网络则是通过循环传递信息。
		- 2）前馈网络中的样例，输入网络后被转换成输出；在监督学习中，输出将是一个标签，一个应用于输入的名称。
		- 3）一个训练好的前馈网络可以用在任何随机的照片数据集中，它识别的第一张照片，并不会影响它对第二张照片的预测。
		- 即前馈网络没有时间顺序的概念，它考虑的唯一输入就是它所接触到的当前输入样例。

	- 缺点

		- 1）每次网络的输出只依赖当前的输入，没有考虑不同时刻输入的相互影响。
		- 2）输入和输出的维度都是固定的，没有考虑到序列结构数据长度的不固定性。

- RNN

	- 示意图

		- 每个x是一个输入样例，w是过滤输入的权重，a是隐藏层的激活(加权输入和先前隐藏状态的和)，b是隐藏层使用修正线性或sigmoid单元转换或压缩后的输出。

	- 概念

		- 循环神经网络(Recurrent Neural Network)，是一类专门用于处理"时序数据"样本的神经网络。
		- 循环网络有两个输入源，现在和最近的过去，它们结合起来决定对新数据的反应，就像我们在现实生活中一样。
		- 循环网络是有记忆的。给神经网络增加记忆的目的在于：序列本身带有信息，循环网络用它来执行前馈网络不能执行的任务。
		- 这些连续的信息被保存在循环网络的隐藏状态中，这种隐藏状态管理跨越多个时间步，并一层一层地向前传递，影响网络对每一个新样例的处理。
		- 用数学的方式来描述记忆传递的过程：

			- t代表时间步，ht代表第t个时刻时间步的隐藏状态，是同一个时间步xt的输入函数。W是权重函数，用于修正xt。U是隐藏状态矩阵(转移矩阵)。ht-1代表第t-1个时间步的隐藏状态。
			- U权重矩阵，是决定当前输入和过去隐藏状态的重要程度的过滤器。它们产生的误差会通过反向传播返回，并用于调整相应的权重，直到误差不再降低。
			- 权重输入(Wxt)和隐藏状态(Uht-1)的总和被函数φ(Sigmoid或tanh)压缩。

	- 特点

		- 1）与前馈网络相比，循环网络的输入不仅包括当前的输入样例，还包括之前的输入信息。
		- 2）循环网络在t-1时刻的判定，会影响随后在t时刻的判定。因此RNN具有记忆功能。

- 时序反向传播算法(BPTT)

	- 循环网络的目的是准确地对序列输入进行分类。主要依靠误差的反向传播和梯度下降法来实现。
	- 前馈网络中的反向传播

		- 从最后的误差项开始，经过每个隐藏层的输出、权重和输入反向移动，将一定比例的误差分配给每个权重，计算它们的偏导数。随后，将这些偏导数应用到梯度下降法中，来调整权重减少误差。

	- 时序反向传播算法

		- 与前馈网络的反向传播不同，循环网络依赖于反向传播的一种扩展，称为时序反向传播算法(BPTT)。
		- 时间通过一系列定义明确、有序的计算来表达，这些计算将一个时间步与下一个时间步联系起来。
		- 神经网络，无论是循环的还是非循环的，都是简单的嵌套复合函数，如f(g(h(x)))。添加时间元素，只是扩展了我们用链式法则计算导数的函数序列。

- 截断式BPTT

	- 是完成BPTT的近似方法，是处理长序列的首选。
	- 在时间步较多的序列中，完成BPTT的每个参数更新的正/反向运算成本变得非常高。
	- 截断式BPTT的缺点：由于截断，梯度反向移动的距离有限，因此网络无法学习与完整BPTT一样长的依赖。

- 梯度消失和梯度爆炸

	- 循环网络中，深度神经网络的层和时间步是通过乘法相互关联，导致很容易出现梯度消失和梯度爆炸，类似蝴蝶效应。
	- 1）梯度爆炸解决起来相对容易，因为他们可以被截断或压缩。
	- 2）梯度消失正好相反，导数变得非常小，网络无法学习收敛。这是一个更难解决的问题。

- 长短期记忆(LSTM)

	- 长短期记忆网络LSTM——循环网络的变体，作为梯度消失问题的解决方案。
	- 核心：引入门控单元和线性连接。
	- 原理

		- 门控单元通过打开和关闭的门来决定存储什么，以及何时允许读取、写入和忘记。
		- LSTM将信息存放在循环网络正常信息流之外的门控单元中。信息可以像计算机内存中的数据一样存储、写入单元、从单元读取。
		- 与计算机上的数字存储器不同，这些门是模拟的，通过范围在0~1之间的Sigmoid函数的逐元素相乘来实现。与数字信号相比，模拟信号的优势是可微分，因此适用于反向传播。
		- 这些门类似于神经网络的节点，会根据它们接受到的信号决定开关，它们根据信息的强度和重要性来阻止或传递信息，然后用它们自己的权重过滤这些信息。
		- 这些权重，就像调整输入和隐藏状态的权重一样，可以在循环网络学习过程中进行调整。
		- 也就是说，记忆单元学习会通过猜测、反向传播误差和梯度下降法调整权重的迭代过程，来决定何时允许数据进入、离开或删除。

	- LSTM的重要概念

		- 三个门

			- 遗忘门

			- 输入门

			- 输出门

		- 两种记忆

			- 长记忆

			- 短记忆

	- 工作流程

		- 1）首先，将t时刻的输入xt和隐藏层输出ht-1复制四份，并为它们随机初始化不同的权重，计算出遗忘门、输入门、输出门、变换后的新信息。

		- 2）其次，使用遗忘门和输入门来控制忘记多少历史信息和保存多少新信息，从而更新内部记忆细胞状态。
		- 3）最后，使用输出门控制输出多少内部记忆单元的信息到隐状态。

	- 应用：适合于处理和预测时间序列中间隔和延迟非常长的重要事件。

- 门控循环单元(Gated Recurrent Unit，GRU)

	- 是LSTM最流行的一个变体，比LSTM模型要简单。
	- 结构

	- 工作流程

		- 1）首先，通过上一个状态ht-1和当前输入xt来获取两个门控状态(重置门和更新门)。

		- 2）通过重置门控得到"重置"之后的数据，再与输入xt进行拼接，然后通过一个tanh激活将数据缩放到-1~1范围内。

		- 3）更新记忆：使用一个门控同时进行遗忘和记忆两个步骤。

	- 为何一般选择GRU而不是LSTM？

		- GRU的输入输出的结构和普通的RNN相似，其中的内部思想和LSTM相似。与LSTM相比，GRU内部少了一个"门控"，参数比LSTM少，但是却也能达到与LSTM相当的功能。考虑到硬件的计算能力和时间成本，因而很多时候我们选择更加实用的GRU。

### Seq2seq

- 编解码结构，利用两个RNN，一个作为encoder，另一个作为decoder。
- encoder负责将输入序列压缩成指定长度的向量(语义向量)。
- decoder负责将语义向量生成指定的序列。

	- 1）语义向量只作初始化参数参与运算。

	- 2）语义向量参与解码的每一个过程。

### 生成模型

- 1）VAE

	- 自编码器(AutoEncoder，AE)

		- 编码器：将输入压缩成潜在空间表征。
		- 解码器：重构来自潜在空间表征的输入。
		- 主要用途：去噪、降维、特征学习、信息补全等。

	- 变分自编码器(Variational auto-encoder，VAE)

		- 问题描述

			- 我们有一批数据样本X1,X2,...,Xn,其整体用X来描述。我们想通过这些数据样本得到X的分布p(X)，如果能得到的话，那么我们就可以直接根据p(X)来采样，得到所有可能的X，这是一个终极理想的生成模型。然而直接通过这些样本点来得到分布是不现实的，因为我们不知道它符合什么分布。
			- VAE和GAN生成模型，对这个问题的解决思路：引入一个中间隐变量Z，然后构建一个从隐变量Z生成数据X的模型。
			- 它们假设Z服从某些常见的分布(如正太分布或均匀分布)，然后训练一个模型X=g(Z)，进行分布之间的变换。
			- 这种生成模型的难题：判断生成分布和真实分布的相似度。

				- 只有样本本身，没有分布表达式，无法计算KL散度。

			- GAN的思路：既然没有合适的度量，干脆把这个度量也用神经网络训练出来——WGAN。

		- VAE的思路

			- 1）使用两个Encoder，一个用来计算均值，一个用来计算方差。这样对于每个样本Xk，都得到一个对应的专属正太分布，有多少个X就有多少个正太分布。
			- 2）然后我们从专属的正太分布中进行采样，最小化D(Xk´,Xk)^2即可重构X。
			- 3）同时添加一个KL loss来让所有的p(Z|X)都向标准正太分布看齐。

				- 若p(Z|X)是或接近标准正太分布，则p(Z)也是标准正太分布。

		- VAE的本质

			- 1）计算均值的Encoder，加上了"高斯噪声"，使得Decoder对噪声具有鲁棒性。
			- 2）KL loss目的是让均值为0,方差为1，实际上就是相当于对Encoder的一个正则项，希望Encoder出来的东西均有零均值。
			- 3）计算方差的Encoder，用来动态调整噪声的强度。

				- 当decoder还没训练好时(重构误差远大于KL loss)，就会适当降低噪声(KL loss权重增加)，使得拟合起来容易一些(重构误差开始下降)；反之，如果decoder训练得还不错时(重构误差小于KL loss)，这时候噪声就会增加(KL loss权重减小)，使得拟合更加困难了(重构误差又开始增加)，这时候decoder就要想办法提高它的生成能力了。

- 2）GAN及其变种

	- 1.GAN概述

		- 什么是GAN？

			- Generative Adversarial Networks(GANs)

				- Generative 学习一个生成式模型
				- Adversarial 使用对抗的方法训练
				- Networks 使用神经网络

			- 特点：使用对抗的方法去学习数据分布的生成式模型。
			- 核心思想：通过生成网络G(Generator)和判别网络D(Discriminator)不断博弈，来达到生成类真数据的目的。

		- 为什么要学习GAN？(GAN的优势)

			- 1）无监督学习。训练深度学习模型需要大量的数据，标注数据费时费力，GAN提供更便捷的方法训练模型。
			- 2）图像风格迁移。马变斑马，桔子变苹果，春天变冬天等。
			- 3）可以输入文本生成图像。
			- 4）GAN的1+1>2。GAN结合迁移学习，可以生成超分辨率图像。

	- 2.原理与改进

		- 1）GAN的基本原理

			- GAN的发展脉络

			- GAN的原理

				- 相关概念

					- 负和博弈、零和博弈统称为非合作博弈；正和博弈称为合作博弈。
					- 零和博弈/游戏理论/零和游戏：它是指参与博弈的各方，不存在合作的可能，在严格竞争下，一方的收益必然意味着另一方的损失，博弈各方的收益和损失总和永远为零。
					- 纳什均衡：又称非合作博弈均衡，博弈各方不互相沟通(存在信息不对称的情况下)，每个人都从利己的目的出发。

						- 典型的囚徒困境，纳什均衡点就是A、B都认罪。从A角度分析：1）若B认罪，不认罪服刑10年，认罪服刑5年，认罪更有利；2）若B不认罪，不认罪服刑1年，认罪立刻释放，认罪更有利。
					- 最大似然估计(Maximum Likelihood Estimation, MLE)：利用已知的样本结果信息，反推最具有可能(最大概率)导致这些样本结果出现的模型参数值。

			- GAN的目标函数

		- 2）GAN的训练方法：锁定一个，训练另一个。
		- 3）GAN存在的问题

			- 1.Non-Convergence（不收敛）。VAE比GAN更稳定。
			- 2.Mode-Collapse（模式坍塌）。给定了一个z，当z发生变化的时候，对应的G(z)没有变化，那么在这个局部，GAN就发生了mode collapse，也就是不能产生连续变化的样本，从而导致生成的样本多样性不足。

		- 4）GAN的改进

			- 1.DCGAN

				- 核心思想

					- 1）使用卷积层代替全连接层。
					- 2）使用Batch Normalization(除生成器的最后一层和判别器的第一层)，将特征归一化，加速训练。
					- 3）G的隐藏层使用ReLU，G的输出层使用Tanh；D使用Leaky ReLU而不是ReLU，防止梯度稀疏。

			- 2.层级结构

				- 层级结构的GAN 通过逐层次，分阶段生成，一步步提生图像的分辨率。
				- 典型的使用多对GAN 的模型有StackGAN，GoGAN。使用单一GAN，分阶段生成的有ProgressiveGAN。
			- 3.自编码结构

				- 典型的自编码器结构的GAN 有：BEGAN，EBGAN，MAGAN 等。

			- 4.Mode Collapse的解决方案

				- 1）Multi agent diverse GAN (MAD-GAN) 采用多个生成器+1个判别器以保证样本生成的多样性。
				- 2）Wasserstein GAN

					- 原始GAN的问题：模型难以训练、模式坍塌。

						- 1）判别器越好，生成器梯度消失越严重。

						- 2）判别器不好，无法给出准确的指示，生成器效果也不好。

					- 相比原始GAN，做了四点改进：

						- 1）判别器最后一层去掉Sigmoid。
						- 2）生成器和判别器的loss不取log。
						- 3）每次更新判别器的参数之后把它们的绝对值截断到不超过一个固定常数C。
						- 4）不用基于动量的优化算法(包括Adam、momentum)，推荐RMSProp、SGD。

					- WGAN的优点：

						- 1）彻底解决GAN训练不稳定的问题，不再需要小心平衡生成器和判别器的训练程度。
						- 2）基本解决了mode collapse问题，确保生成样本的多样性。
						- 3）训练过程中终于有一个像交叉熵、准确率这样的数值来指示训练的进程，这个数值越小代表GAN训练的越好，代表生成器产生的图像质量越高。
						- 4）以上一切好处不需要精心设计的网络结构，最简单的多层全连接网络就可以做到。

					- Wasserstein距离相比KL散度、JS散度的优越性在于，即便两个分布没有重叠，Wasserstein距离仍然能够反映它们的远近。

	- 3.应用场景

		- 1）图像风格迁移、超分辨率图像生成、序列生成、文本风格迁移、Video视频生成等。
		- 2）GAN潜力巨大，可学习模仿任何数据分布，因此可以被应用于多种领域，比如图像、音乐、演讲、散文。

