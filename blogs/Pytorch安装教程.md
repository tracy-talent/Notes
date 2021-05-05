# Linux下的Pytorch安装教程

## anaconda环境容器安装

anaconda是python的环境容器，可以根据需要创建不同的python环境

* [anaconda安装教程](https://blog.csdn.net/qq1483661204/article/details/78201451)
* [conda常用命令](https://zhuanlan.zhihu.com/p/67745160)

## pytorch安装

到[pytorch官网](https://pytorch.org/get-started/locally/)根据环境及需要选择相应的pytorch版本进行命令行安装，如下图所示

![image-20210425134344511](C:\Users\LiuJian\AppData\Roaming\Typora\typora-user-images\image-20210425134344511.png)

## nvidia driver, cuda，cudnn安装

为了支持gpu的使用，必须安装nvidia driver、cuda以及cudnn，详见[安装教程](https://brooksj.com/2019/09/18/linux%E4%B8%8B%E5%AE%89%E8%A3%85nvidia-driver-cuda10-cudnn7-tensorflow1-14/)。具体的nvidia driver版本由机器的系统、GPU型号、cuda版本决定，cudnn版本由cuda版本决定，在教程中有详细说明。

## 测试

一切安装好之后，进入python命令行。执行

```python
import torch
torch.cuda.is_available() # 返回True则表示上述nvidia driver、cuda、cudnn都已安装成功，否则失败
```

