<center><h1>centos下docker安装教程</h1></center>

目前最新版本的docker19.03支持nvidia显卡与容器的无缝对接，从而摆脱了对[nvidia-docker](https://github.com/NVIDIA/nvidia-docker)的依赖。因此毫不犹豫安装19.03版本的docker，安装教程可参考官方教程[Get Docker Engine - Community for CentOS](https://docs.docker.com/install/linux/docker-ce/centos/)，安装好之后还要解决一个问题就是如何才能使非root用户拥有docker使用权。

用户其实是通过/var/run/docker.sock与docker容器进行交互，因此要获得docker使用权则必须拥有对/var/run/docker.sock这个文件的读写权，使用stat命令查看/var/run/docker.sock这个文件的基本信息

<div align="center">
	<img src="https://raw.githubusercontent.com/tracy-talent/Notes/master/imgs/docker-sock-stat.png">
</div>

可以看到root和docker group对docker.sock拥有读写权，那么非root用户只要成为docker group中的一员即可拥有对docker.sock的读写权，下面给出具体步骤:

1. 创建docker用户组，其实docker安装时会自动创建一个名为docker的用户组，可以通过查看/etc/group确认docker用户组的存在，如若不存在则手动创建docker用户组

   ```bash
   sudo groupadd docker
   ```

2. 添加当前非root用户到docker用户组中

   ```bash
   sudo gpasswd -aG docker $USER
   ```

3. 将当前非root用户的group切换到docker用户组

   ```bash
   newgrp docker
   ```

4. 执行docker image ls验证当前的非root用户是否获得了docker使用权，被授权了则会打印本地镜像，否则显示禁止访问/var/run/docker.sock

   ```bash
   docker image ls
   ```



参考链接:

1. https://docs.docker.com/install/linux/linux-postinstall/
2. https://coderleaf.wordpress.com/2017/02/10/run-docker-as-user-on-centos7/
