powerline是一款比较炫酷的状态栏工具，多用于vim和终端命令行。先上两张效果图，然后介绍一下具体的安装教程。

<div align="center">
    <img src="https://raw.githubusercontent.com/tracy-talent/Notes/master/imgs/powerline_bash.png">
</div>

<center>图 1  powerline在shell下的效果图</center>

<div align="center">
    <img src="https://raw.githubusercontent.com/tracy-talent/Notes/master/imgs/powerline_vim.png">
</div>

<center>图 2 powerline在vim下的效果图</center>

## step1

确保当前系统中已有可用的git和python-pip，这两个常用工具相信大家电脑上基本都有安装，没装的网上教程也很多，这里就不再赘述这两个工具的安装方法。有了这两个工具之后就可以执行下面这条命令来安装powerline

```bash
pip install git+git://github.com/powerline/powerline
```

## step2

安装完成后powerline就是我们电脑上可用的python包了，为了支持powerline的着色效果，还需要下载powerline的字体及其配置文件

```bash
wget https://github.com/powerline/powerline/raw/develop/font/PowerlineSymbols.otf
wget https://github.com/powerline/powerline/raw/develop/font/10-powerline-symbols.conf
```

下载好之后需要将上面两个文件分别移植到/usr/share/fonts和/etc/fonts/conf.d下

```bash
mv PowerlineSymbols.otf /usr/share/fonts
fc-cache -vf /usr/share/fonts/  #更新系统的字体缓存
mv 10-powerline-symbols.conf /etc/fonts/conf.d 
```

## step3

下面就是对系统环境变量进行修改，在/etc/bashrc文件末尾添加以下内容，且注意**最后一行的.与/usr之间必须加一个空格**

```bash
# powerline
powerline-daemon -q
POWERLINE_BASH_CONTINUATION=1
POWERLINE_BASH_SELECT=1
. /usr/lib/python2.7/site-packages/powerline/bindings/bash/powerline.sh 
```

如果只想作用于某一个用户，则只需对用户环境变量进行修改，在~/.bashrc的文件末尾添加上面一致的配置内容，这是再打开一个新的终端应该就可以看到powerline的渲染效果了，如果还是没有则重启一下电脑试试看，如果还是没有则在上面配置的基础上加一行export TERM="screen-256color"试试。对于powerline在vim中的安装在我的另一篇博客[vim配置python编程环境及YouCompleteMe安装教程](https://www.cnblogs.com/brooksj/p/10428722.html)中有提到，可以参考一下。