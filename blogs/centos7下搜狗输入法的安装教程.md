&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;相信用过centos自带的输入法的朋友都会感叹这也实在是太难用了吧,使用拼音打出来的词总是不能在前几个匹配到,即使是一些常用词也是如此,简直无法忍受跟个zz似的.吐槽完了,这里给出centos7下搜狗输入法的安装方法,帮助施主早日脱离苦海,皆大欢喜.

1. 首先配置epel源以获取后续需要安装的包

   ```bash
   wget   /etc/yum.repos.d/epel.repo http://mirrors.aliyun.com/repo/epel-7.repo
   ```

   这是通过阿里云镜像站下载的，根据你自己的喜好从各镜像站或官方下载，也可以使用下面的命令安装epel源

   ```bash
   yum -y install epel-release.noarch
   ```

   然后更新源

   ```bash
   yum -y update
   ```

2. 检测系统中是否已安装ibus

   ```bash
   rpm -qa ibus
   ```

   如果结果输出了ibus版本,那么需要卸载ibus

   ```bash
   yum -y remove ibus
   ```

3. 接着安装搜狗输入法所依赖的一些包

   ```bash
   yum -y install qtwebkit alien dpkg opencc
   yum -y install fcitx fcitx-pinyin fcitx-configtool
   ```

4. 确保上面的包都已安装成功后,到搜狗输入法官网上下载[搜狗输入法for linux版本的deb安装包](https://blog.csdn.net/ys19940521/article/details/82084171)

5. 我这里下载得到sogoupinyin_2.2.0.0108_amd64.deb,然后复制到你要安装的目录下,这里我是安装在/usr/local/sogou这个目录下

   ```bash
   mkdir /usr/local/sogou
   cp sogoupinyin_2.2.0.0108_amd64.deb /usr/local/sogou
   ar -vx sogoupinyin_2.2.0.0108_amd64.deb  #解压deb包
   tar -xf data.tar.xz /  #将data.tar.xz解压到根目录下
   cp /usr/lib/x86_64-linux-gnu/fcitx/fcitx-sogoupinyin.so  /usr/lib64/fcitx  #复制搜狗拼音模块到相应目录下
   ```

6. 首先关闭gnome-shell 对键盘的监听，然后切换输入法为fcitx: （启用键盘键盘监听后，依然可以用键盘默认的ibus输入法,但是应该没有人会这么做吧）

   ```bash
   gsettings set org.gnome.settings-daemon.plugins.keyboard active false 
   imsettings-switch fcitx
   ```

7. 最后最好再重启一下系统，用shift就可以切换出搜狗输入法了

   ```bash
   reboot
   ```


参考:

https://blog.csdn.net/ys19940521/article/details/82084171

http://blog.sina.com.cn/s/blog_98df9a260102wc2z.html