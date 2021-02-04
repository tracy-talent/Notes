# Pytorch Tips

* 卷积conv
  1. torch.Conv2d(*in_channels*, *out_channels*, *kernel_size*, *stride=1*, *padding=0*, *dilation=1*, *groups=1*, *bias=True*, padding_mode='zeros')
  
     其中，padding用于控制外围pad的层数(默认用0作pad)，当padding_mode='zeros'时，(padding_left=padding[1], padding_right=padding[1], padding_top=padding[0], padding_bottom=padding[0])，当padding_mode='circular'时，(padding_left=(padding[1]+1)/2, padding_right=(padding[1]+1)/2, padding_top=(padding[0]+1)/2, padding_bottom=(padding[0]+1)/2)，若padding是int而不是tuple则默认每一维padding相同。
  
     dilation参数指卷积核相邻元素的步数距离，下图所示dilation=2时
  
     <img src="https://raw.githubusercontent.com/tracy-talent/pytorch-tutorials/master/images/dilation.png?token=ADSCPHALO3BOYFIQXBOBCC26N573O" align="center">
     
  2. torch.nn.functional.conv2d(*input*, *weight*, *bias=None*, *stride=1*, *padding=0*, *dilation=1*, *groups=1*) → Tensor，**input** – input tensor of shape (minibatch, in\_channels, iH , iW)，**weight** – filters of shape (out_channels, $\frac{in_channels}{groups}$, kH, kW)，注意卷积核的第二维必须为$\frac{in_channels}{channels}$，因为groups参数用于控制卷积层输入输出之间的连接，输入通道划分为groups组，卷积核输出通道划分为为groups组，对应的进行卷积得到的结果再进行拼接。
  
* pytorch矩阵转置2中方式

  1. torch.transpose(input, dim0, dim1)，或者调用tensor内嵌的方法，tensor.transpose(dim0, dim1)或者tensor.transpose_(dim0, dim1)，后者是原地操作，transpose只能置换2维。
  2. 相比transpose，tensor内嵌的permute方法可以在多个维度上进行置换，接口tensor.permute(*dim)，但是permute没有原地操作方法permute_
  
* torch.Tensor.is_contiguous用于判断tensor is contiguous in memory in C order即tensor在内存中是否是按行排列的，torch.Tensor.contiguous方法先判断传入的tensor是否是contiguous的，如果不是则转换成contiguous的再返回，如果是则直接返回其本身。

* torch.Tensor()返回的tensor默认类型是torch.FoatTensor，而torch.tensor()返回的tensor默认类型是torch.LongTensor，但是torch.tensor可以通过dtype参数设定类型

* pytorch normalization方式

  1. torch.nn.BatchNorm2d(num_features, eps=1e-05, momentum=0.1, affine=True, track_running_stats=True)，其中num_features对应输入大小(N,C,H,W)中的C(channel)，eps对应公式$y=\frac{x-E[x]}{\sqrt{Var[x]+\epsilon}}*\gamma+\beta$中$\epsilon$平滑参数，初始$\gamma$全为1，$\beta$全为0，$E[x]$和$Var[x]$是除channel维度外的均值和有偏方差，每个channel共用一个参数，一共有C个可学习的$\gamma$和$\beta$，因此公式等价于$y=\frac{x-x.mean(dim=(0, 2, 3), keepdim=True)}{torch.sqrt(x.var(dim=(0, 2, 3), keepdim=True, unbiased=False) + \epsilon)}*\gamma+\beta$. affine为True则表示模型拥有可学习的再缩放参数$\gamma$和再平移参数$\beta$，momentum按公式$\hat{x}_{new}=(1-momentum)\times\hat{x}+momentum\times{x_t}$计算统计值$E[x]和Var[x]$，$x_t$为当前这一个batch计算的统计值。track_running_stats为True表示保存训练阶段最终的均值和方差用于测试阶段，为False则表示测试阶段与训练阶段一样计算每个batch的均值和方差。

  2. torch.nn.LayerNorm(normalized_shape, eps=1e-5, elementwise_affine=True)，其中normalized_shape对应input.shape[1:]，eps对应公式$y=\frac{x-E[x]}{\sqrt{Var[x]+\epsilon}}*\gamma+\beta$中$\epsilon$平滑参数，初始$\gamma$全为1，$\beta$全为0，$E[x]$和$Var[x]$是batch中每个样本的均值和有偏方差，样本中每个元素都有可学习的再缩放参数$\gamma$和再平移参数$\beta$，各个样本中对应元素共用参数，所以$\gamma$和$\beta$的size为input.shape[1:]，公式等价于$y=\frac{x-x.mean(dim=tuple(range(1, x.ndim)), keepdim=True)}{torch.sqrt(x.var(dim=tuple(range(1,x.ndim)), keepdim=True, unbiased=False) + \epsilon)} * \gamma + \beta$. elementwise_affine为True则表示模型拥有可学习的参数$\gamma$和$\beta$.
  3. BatchNorm与LayerNorm对比：LayerNorm测试阶段独立计算均值和方差，而BatchNorm测试阶段可采用训练阶段的累积均值和方差，因此BatchNorm需要缓存Channel个均值和方差，内存消耗更大。LayerNorm的均值和方差是针对单个样本计算的，与batch大小无关，不受batch分布影响，适用于小batch或者动态网络比如RNN(RNN由于batch中各个样本序列长度不一致，因此后面的step计算时的batch可能比前面的小，因此BatchNorm不适用)
