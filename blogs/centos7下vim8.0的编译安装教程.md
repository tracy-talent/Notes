之前安装YouCompleteMe的时候遇到vim版本不兼容的问题，看网上说是需要将vim版本提升到8.0及以上，然后就开始安装最新版本的vim，安装过程中的遇到了不少问题主要集中在配置方面和缺少插件，在这里把最终的安装方法贴出来，希望能帮到需要的朋友，也是考虑到自己以后可能还要用到。

## <div align="center">
    <img src="">
</div>

为了使vim支持ruby、lua、perl、python2、python3编写的插件，在正式编译安装vim之前需要在系统中安装好相关插件，否则编译vim会出错。

```shell
sudo yum install ruby ruby-devel lua lua-devel luajit \
luajit-devel ctags git python python-devel \
python36 python36-devel tcl-devel \
perl perl-devel perl-Extutils-ParseXS \
perl-ExtUtils-XSpp perl-ExtUtils-CBuilder \
perl-ExtUtils-Embed libX* ncurses-devel gtk2-devel
```

如果系统中有可用的python2.7或者python3.6则将上面安装项中的python和python36去除。

## step2

卸载已有的vim

```shell
yum -y remove vim
```

下载vim的项目源码

```shell
git clone https://github.com/vim/vim.git
```

下载好后进入到vim目录下进行**配置、编译、安装**

* 配置
  ```shell
  ./configure --with-features=huge \
  --enable-gui=gtk2 \
  --with-x \
  --enable-fontset \
  --enable-cscope \
  --enable-multibyte \
  --enable-pythoninterp \
  --with-python-config-dir=/usr/lib64/python2.7/config \
  --enable-python3interp \
  --with-python3-config-dir=/usr/lib64/python3.6/config \
  --enable-luainterp \
  --enable-rubyinterp \
  --enable-perlinterp \
  --enable-multibyte \
  --prefix=/usr/local/vim \
  --with-compiledby="brooksj"
  ```

  参数说明如下：

  –with-features=huge：支持最大特性 

  –enable-rubyinterp：启用Vim对ruby编写的插件的支持 

  –enable-pythoninterp：启用Vim对python编写的插件的支持 

  -enable-python3interp：启用对python3编写的插件的支持

  –enable-luainterp：启用Vim对lua编写的插件的支持 

  –enable-perlinterp：启用Vim对perl编写的插件的支持 

  –enable-multibyte：多字节支持 可以在Vim中输入中文 

  --enable-fontset：支持字体设置

  –enable-cscope：Vim对cscope支持 ，cscope是一款优秀的代码浏览工具

  –enable-gui=gtk2：gtk2支持,也可以使用gnome，表示生成gvim 

  -–with-python-config-dir 指定 python配置 路径 

  --with-python3-config-dir 指定python3配置路径

  –-prefix：编译安装路径 

  --with-compiledby：编译者

  配置很关键，这直接关系到你以后vim的功能使用，这里建议最好按照上面我所给出的的配置方案来配置，以免后续出现问题。

* 编译

  ```shell
  make
  ```

  如果编译错误则可能是缺少相关插件，回过头去查看上面那些插件是否都已安装上。

* 安装

  ```shell
  make install
  ```
## step3

设置系统环境变量，把vim的bin目录添加到path中，在/etc/bashrc末尾添加

```shell
# 注意/usr/local换成你的vim安装路径
export PATH=/usr/local/vim/bin:$PATH 
```

source /etc/bashrc或者重新打开一个终端就可以使用vim和gvim来打开文件了。下图是我安装好之后执行vim --version的输出截图

<div align="center">
    <img src="https://raw.githubusercontent.com/tracy-talent/Notes/master/imgs/vim_version.png">
</div>

