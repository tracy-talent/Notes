&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;前面写过一篇[centos7下搜狗输入法的安装教程](https://www.cnblogs.com/brooksj/p/10458641.html),现在把搜狗输入法在Ubuntu下的安装方法也记录一下,相比之下Ubuntu下安装搜狗输入法要简便得多

1. 安装fcitx以支持搜狗输入法

   ```bash
   sudo add-apt-repository ppa:fcitx-team/nightly  #添加fcitx安装源
   sudo apt-get update
   ```

   如果是Ubuntu18.04以下 的版本,使用下面的命令安装

   ```bash
   sudo apt-get install fcitx
   sudo apt-get install fcitx-config-gtk
   sudo apt-get install fcitx-table-all
   sudo apt-get install im-switch
   ```

   如果是Ubuntu18.04则使用下面的命令安装

   ```bash
   sudo apt-get install fcitx
   # 安装报错则使用下面这条命令来安装
   sudo apt-get --fix-broken install fcitx
   ```

2. 安装好fcitx之后就可以安装搜狗输入法了,到搜狗输入法官网上下载[搜狗输入法for linux版本的deb安装包](https://blog.csdn.net/ys19940521/article/details/82084171),然后使用如下命令安装

   ```bash
   sudo dpkg -i sogoupinyin_2.2.0.0108_amd64.deb
   ```

3. 安装好之后如果左上方没有出现搜狗输入法的logo,则到系统设置->语言支持下将**键盘输入法系统**设置为fcitx,然后重启或者注销使其生效.再次打开电脑若此时右上角没有搜狗输入法的logo则在命令行下执行fcitx-config-gtk3或者在右上角输入法上右击选择设置来配置输入法,添加搜狗输入法即可使用了.



参考:

https://blog.csdn.net/ljheee/article/details/52966456