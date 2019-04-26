深度学习是机器学习的一个分支。深度学习通过深层神经网络自行寻找特征来解决问题，不同于传统方法需要告诉算法找什么样的特征。为获取数据的本质特征深度神经网络需要处理大量信息，一般有两种处理方式：CPU和GPU

先抛出三个问题：

1. 为什么深度学习需要使用GPU？

2. GPU的哪些性能指标最重要？

3. 如何选购GPU？


#### CPU or GPU:

CPU是基于延迟优化，更擅长快速获取少量的内存（5×3×7），GPU基于带宽优化，更擅长获取大量的内存（矩阵乘法A×B×C）。所以GPU的处理速度快得益于它可以高效的处理矩阵乘法和卷积，背后的原因是由高带宽的内存、多线程并行下的内存访问隐藏延迟、数量多且速度快的可调整的寄存器和L1缓存三大因素支撑。

当采用深度学习进行网络训练需要对大数据做同样的事情时，GPU更合适，能够专注于大量并发的浮点数计算。


#### 深度学习相关的GPU性能指标如下：

++内存带宽++：GPU处理大量数据的能力，是最重要的性能指标，指单位时间内数据的吞吐量。

处理能力：表示GPU处理数据的速度，可以量化为CUDA核数量和每一个核的频率的乘积。

显存大小：一次性加载到显卡上的数据量，运行计算机视觉模型显存越大越好。

#### Single GPU or Multi GPU：

多GPU一般用于并行训练多个模型或者分布式训练单个模型。分布式训练或在多个显卡上训练单个模型的效率较低，但是此方法越来越受欢迎。主流的深度学习框架Tensorflow、Keras、PyTorch等都开放了分布式训练接口，分布式训练几乎可以随着GPU数量成线性的性能提升，比如两个GPU可以获得1.8倍的训练速度。
总而言之，GPU越多需要越快的处理器并需要更快的数据读取能力的硬盘
 
#### 主流GPU的性能比较：


##### Tesla K80的技术规格：

CUDA核心数: 2 x 2496

核心频率: 562MHz (875 MHz boost)

显存时钟: 5 GHz GDDR5

显存位宽: 2 x 384 bit

显存带宽: 240.6 GB/s x2

显存大小: 2 x 12GB(采用双芯设计，所以内存也有两个)

单精度浮点性能: **++8.74 TFLOPS(双卡并行)、5.6 TFLOPS(单卡)++**

功率: 2 x 150W

制程: TSMC 28nm

发布时间：2013年底

官方价格：$1699(参考亚马逊定价)

评价：Tesla K80架构很老了，是Kepler GK210。K80作为HPC用卡相比游戏卡有着么几大优点：集成两个GK210核心，但如果不特别设计程序只能使用其中一个。1/3倍速双精度（GM204只有1/32），Cache/显存ECC，为可靠性服务的。

Tesla K80是双芯设计，它的性能指标看起来比K40高得多，不过实际上不一定总是超过K40，因为单个GPU的规格比K40低，而且它的基础频率更低，不过K80主要的应用环境显然都是对多路GPU优化较好的，所以Tesla K80总性能还是要比K40快得多，但是作为一个发行时间超过5年，架构陈旧，Nvidia官方停产的GPU，==++完全不推荐购买++==。而且Tesla K80支持的cuda版本最高为8.0，而Nvidia放出的最新版本为10.1，tensorflow 1.6之后的版本就放弃了对8.0的支持，所以在Tesla  K80上只能使用较低版本的Tensorflow。

##### Tesla P100的技术规格：

CUDA核心数: 3584

显存带宽: 732 GB/s

显存大小: 16GB

单精度浮点性能: **++10.6 TFLOPS++**

功率: 300W

发布时间：2016年

官方价格：$4998(参考亚马逊定价)

##### P100与K80的性能对比在Nvidia官网和Tensorflow官网都能找到，如下所示

![image](http://note.youdao.com/yws/res/1130/7DAAC322641B4D33A746DFC1B433EA86)
![image](http://note.youdao.com/yws/res/1201/757B6895932D4A008E3FBD831692C010)
![image](http://note.youdao.com/yws/res/1199/A59C95145576456680C4D992B551A75E)

可以看到P100在深度学习各项任务中的性能几乎都在K80的两倍或以上，而P100的性能不过是与1080Ti相差不多而已。

##### GTX 1080 Ti
英伟达产品线里的高端显卡，拥有大容量显存和高吞吐量，GTX 1080 Ti 可以让你完成计算机视觉任务，并在 Kaggle 竞赛中保持强势。参数：

显存（VRAM）：11GB

内存带宽：484GB/s

处理器：3584个CUDA核心@1582MHz

单精度浮点性能：**++10.6-11.4TFLOPS++**

功率: 250W

官方价格：$1199(参考亚马逊定价)

##### Titan XP 参数：

显存（VRAM）：12GB

内存带宽：547.7GB/s

处理器：3840个CUDA核心@1480MHz

单精度浮点性能：**++12.3-13.2TFLOPS++**

功率: 280W

官方价格：￥9999(参考京东定价)



#### Nivda面向专业市场的Tesla
Tesla显卡的显存数量超过游戏用显卡，同时Tesla显卡的双精度浮点运算能力大大强于普通的GTX显卡，**++Tesla作为专用计算显卡，包括了如ECC memory等增强稳定性的措施，使得计算结果更不容易出错。++**
专业计算卡是++为科学运算设计的，科学运算需要很高的精度，因此成本会增加很多++，包括配套的ECC校验和专门驱动，都会提高成本。所以科学计算卡比普通消费级显卡贵很多。但但**++大多数情况都是用不到它的这些特性，例如深度学习主要包含的是 单精度计算，也不需要ECC纠错，普通显卡的极低错误率完全在接受范围内。++**

GPU产品型号包括K40、K80、P100等，经过前人针对 GTX 1080 Ti 和 K40 在深度学习方面的一些基准测试。1080Ti 的速度是 K40 的 5 倍，是 K80 的 2.5 倍。K40 有 12 GB 显存，K80 有 24 GB 的显存。P100 和 GTX 1080 Ti 性能相差不多。但是性价比落后于桌面级 GPU故不推荐。

综合考虑性能和计算专业性，***++最为推荐的深度学习用GPU是Nvidia的Titan系列++***，例如Titan xp、Titan RTX、Titan V，Titan系列有高于Geforce系列的性能，比Geforce系列更大的内存(其中Titan RTX的内存更是多达24GB)，同时特别优化了双精度计算(Titan V甚至优化了半精度计算)，却与Tesla的价格相差甚远。

PS：Tesla的最新款为Tesla T4，性能卓越，单精度浮点性能达到了8.1 TFLOPS，价格为19000rmb左右，是Tesla系列中唯一在性价比方面有竞争力的GPU
[官网链接](https://www.nvidia.cn/data-center/tesla-t4/)
##### Tesla T4的技术规格：

CUDA核心数: 2560

图灵Tensor核心数: 320

核心频率: 585MHz (1590 MHz boost)

显存时钟: 5 GHz GDDR6

显存位宽: 256 bit

显存带宽: 320 GB/s

显存大小: 16GB

单精度浮点性能: **++8.74 TFLOPS++**

功率: 70W

官方价格：19000 RMB(参考京东定价)


#### 当前市面上常用的显卡指标如下：

![image](http://note.youdao.com/yws/res/822/F35065E3123E4E6F8B4B17675A6DBA9C)

![image](http://note.youdao.com/yws/res/1175/41211CF067044ED18CEE5D98A108153F)


## 参考网址
1. [tensorflow基准测试：tesla k80 vs tesla p100](https://tensorflow.google.cn/guide/performance/benchmarks)

    https://tensorflow.google.cn/guide/performance/benchmarks
    
    原链接无法访问可以尝试[tensorflow基准测试：tesla k80 vs tesla p100](https://cloud.tencent.com/developer/section/1475712)
    
    https://cloud.tencent.com/developer/section/1475712

2. [高性能显卡对比测试](https://mp.weixin.qq.com/s/EuEJYOm09iZpIr_xG_lPTw)
    
    https://mp.weixin.qq.com/s/EuEJYOm09iZpIr_xG_lPTw

    [英文版](https://lambdalabs.com/blog/best-gpu-tensorflow-2080-ti-vs-v100-vs-titan-v-vs-1080-ti-benchmark/)
    
    https://lambdalabs.com/blog/best-gpu-tensorflow-2080-ti-vs-v100-vs-titan-v-vs-1080-ti-benchmark/
    
3. [最新云端&单机GPU横评](https://www.jiqizhixin.com/articles/Benchmarking-Tensorflow-Performance-on-volta-gpus)
    
    https://www.jiqizhixin.com/articles/Benchmarking-Tensorflow-Performance-on-volta-gpus
