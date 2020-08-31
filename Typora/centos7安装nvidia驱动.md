# Centos7安装nvidia驱动

step1: 检查是否存在/usr/bin/nvidia-uninstall，若有则可以直接卸载

step2: yum list installed|grep nvidia-\*查看nvidia驱动是否从yum安装，若有输出则执行yum remove nvidia-*卸载nvidia驱动

step3: 确认nouveau已禁用(/usr/lib/modprobe.d/blacklist-nouveau.conf添加`blacklist nouveau`)，执行init 3进入文字端，执行./NVIDIA-*.run --no-opengl-files

step4: reboot



## tensorlfow

1. tensorflow与cuda的适配版本参考[tf offcial](https://www.tensorflow.org/install/source#gpu_support_3)

