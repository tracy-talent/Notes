# Pytorch Tips

* 卷积conv
  
  深度学习中的卷积实际上是信号处理和图像处理中的互相关运算，它们二者之间有细微的差别。深度学习中的卷积（严格来说是互相关）是卷积核在原始图像上遍历，对应元素相乘再求和，得到的新图像在尺寸上会有减小。比如(channels, kH, KW)为(2,2,2)的图像输入input=[[[1,2],[3,4]],[[3,2],[1,3]]],卷积核weight=[[[3,4],[5,6]],[[1,2],[2,2]]]，二维卷积输出为65，对应通道卷积在求和
  
  1. torch.Conv2d(*in_channels*, *out_channels*,*kernel_size*, *stride=1*, *padding=0*, *dilation=1*, *groups=1*, *bias=True*, padding_mode='zeros')
  
     其中，padding用于控制外围pad的层数(默认用0作pad)，当padding_mode='zeros'时，(padding_left=padding[1], padding_right=padding[1], padding_top=padding[0], padding_bottom=padding[0])，当padding_mode='circular'时，(padding_left=(padding[1]+1)/2, padding_right=(padding[1]+1)/2, padding_top=(padding[0]+1)/2, padding_bottom=(padding[0]+1)/2)，若padding是int而不是tuple则默认每一维padding相同。
  
     dilation参数指卷积核相邻元素的步数距离，下图所示dilation=2时
  
     ![](/home/irving/github/pytorch-tutorials/images/dilation.png)
     
     <img src="https://raw.githubusercontent.com/tracy-talent/pytorch-tutorials/master/images/dilation.png?token=ADSCPHCOBKWL5QUPCLQH5CC6VPNUY" align="center">
     
  2. torch.nn.functional.conv2d(*input*, *weight*, *bias=None*, *stride=1*, *padding=0*, *dilation=1*, *groups=1*) → Tensor，**input** – input tensor of shape (minibatch, in\_channels, iH , iW)，**weight** – filters of shape (out_channels, $\frac{in_channels}{groups}$, kH, kW)，注意卷积核的第二维必须为$\frac{in_channels}{channels}$，因为groups参数用于控制卷积层输入输出之间的连接，输入通道划分为groups组，卷积核输出通道划分为为groups组，对应的进行卷积得到的结果再进行拼接。
  
* pytorch矩阵转置2中方式

  1. torch.transpose(input, dim0, dim1)，或者调用tensor内嵌的方法，tensor.transpose(dim0, dim1)或者tensor.transpose_(dim0, dim1)，后者是原地操作，transpose只能置换2维。
  2. 相比transpose，tensor内嵌的permute方法可以在多个维度上进行置换，接口tensor.permute(*dim)，但是permute没有原地操作方法permute_
  
* torch.Tensor.is_contiguous用于判断tensor is contiguous in memory in C order即tensor在内存中是否是按行排列的，torch.Tensor.contiguous方法先判断传入的tensor是否是contiguous的，如果不是则转换成contiguous的再返回，如果是则直接返回其本身。

* torch.Tensor()返回的tensor默认类型是torch.FoatTensor，而torch.tensor()返回的tensor默认类型是torch.LongTensor，但是torch.tensor可以通过dtype参数设定类型

