## Dropout layer
	• Dropout
		○ 训练过程中，输入张量的一些元素按从伯努利分布中采样的概率p随机置零。在每个前向调用过程中每个通道都能被独立置零。
		○ Dropout方法证明被证明是正则化和防止神经元的互适应（co-adaptation）效应的有效技术，该技术最先在Improving neural networks by preventing co-adaptation of feature detectors中提出。
		○ 此外，再训练过程中输出被1/(1−p) 因此进行了缩放。这意味着在评估过程中，该单元只是简单的计算了一个恒等函数。
		○ 参数：
			§ p - 元素置零的概率，默认为0.5
			§ inplace - 如果设置为True，将会就地执行操作。默认为False
		○ 形状：
			§ 输入: 输入可以是任意形状
			§ 输出: 输出和输入同形状
			
	• Dropout2d
		○ 随机将整个通道置零（一个通道是一个二维的特征图，例如在一批输入的第i个样本的第j个通道是一个二维张量输入[i, j]）。在每个前向调用过程中每个通道会按照从伯努利分布中采样的概率p独立地置零。
		○ 通常Dropout2d的输入来自于nn.Conv2d模块。
		○ 如论文Efficient Object Localization Using Convolutional Networks中提到的，如果特征图中的相邻像素是强相关的（浅层的卷积层通常是这样的），那么Dropout将不会使激活函数正则化而是仅仅导致学习率的有效降低。这种情况下，使用nn.Dropout2d()可以有效地提升特征图之间的独立性。
		○ 参数
			§ p - 元素置零的概率，默认为0.5
			§ inplace - 如果设置为True，将会就地执行操作。默认为False
		○ 形状
			§ 输入：(N, C, H, W)
			§ 输出：(N, C, H, W)，和输入的形状一致
			
	• Dropout3d
		○ 随机将整个通道置零（一个通道是一个三维特征图，例如一个批次输入的第i个样本的第j个通道是一个三维的输入[i, j]）。每个通道在每个前向调用过程中将会以从伯努利分布中采样得到的概率p独立置零。
		○ 通常Dropout3d的输入来自于nn.Conv3d模块
		○ 如论文Efficient Object Localization Using Convolutional Networks中提到的，如果特征图中的相邻特征图之间是强相关的（浅层的卷积层通常是这样的），那么Dropout将不会使激活函数正则化而是仅仅导致学习率的有效降低。这种情况下，使用nn.Dropout2d()可以有效地提升特征图之间的独立性。
		○ 参数
			§ p - 元素被置零的概率
			§ inplace - 如果设置为True，将会就地执行该操作
		○ 形状
			§ 输入：(N, C, D, H, W)
			§ 输出：(N, C, D, H, W)，和输入的形状一致
			
	• AlphaDropout
		○ AlphaDropout是一种保持子规格属性的Dropout。对于一个0均值和单位标准差的输入，AphaDropout可以保持输入的均值和标准差。AlphaDropout往往伴随着SELU激活函数，以保证输入也是0均值和单位标准差。
		○ 训练过程中，AlphaDropout会以从伯努利分布中采样到的概率p使一些元素置零。每次前向调用过程中，保留的元素都是随机且会进行缩放和移位以保持0均值和单位标准差。
		○ 在评估过程中该模块都是仅仅计算一个恒等函数（评估过程中不进行Dropout）。
		○ 更多细节可在论文Self-Normalization Neural Networks中找到。
		○ 参数
			§ p - 元素被置零的概率，默认为0.5
			§ inplace - 如果设置为True，将会就地执行该操作
		○ 形状
			§ 输入：输入可以是任意形状
			§ 输出：输出和输入的形状相同
