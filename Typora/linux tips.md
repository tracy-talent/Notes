<center><h1>Linux Tips</h1></center>

## vim

* vim打开文件中文乱码问题解决方法

```bash
vim ~/.vimrc
添加以下内容：
#打开文件的时候依次尝试这几种编码
set fileencodings=utf-8,gb18030,utf-16,big5  
```

* vim编辑时撤销和回退撤销快捷键

```shell
撤销上一步操作：u
恢复上一步被撤销的操作：ctrl+r
```

* vim比对两个文件方法

```shell
1、vimdiff file1 file2
2、vim -d file1 file2
3、编辑状态下竖向打开并比对另一个文件：vert diffsplit file2
4、对编辑状态下的两个文件进行比对：diffthis
5、若编辑状态下对文件更新后的对比差异没有及时显现：diffupdate

caution:给文件对比选择一个合适养眼的主题很重要，在~/.vimrc中添加如下代码：
if &diff
    colors blue
endif
```

* vim窗口分割

```shell
1、vs竖向分割
2、sv横向分割
```

* vim退格键失效

```shell
在~/.vimrc中添加：
set backspace=indent,eol,start
```

* vim的home、end键失效

```shell
在~/.bashrc中配置：
export TERM=xterm
```

* vim快捷键映射查询

```
比如查询F5映射到的快捷键
verbose map <F5>
```

* shell执行出现换行'\r'错误

```shell
一般是由windows编辑默认换行\r\n而linux换行\n不一致导致，可在vim中执行如下命令解决
set ff=unix
```



## iconv命令

* iconv转换文件编码

```bash
#从编码gb18030转换为utf-8并且输出文件保存为file2 
iconv -f gb18030 -t utf-8 file1 > file2
iconv -f gb18030 -t utf-8 file1 -o file2
```

* 批量转换

```shell
# 将src目录下所有.txt后缀的文件编码从gb18030转为utf-8并输出在原目录下
find src -name *.txt -exec iconv -f gb18030 -t utf-8 {} -o {} \;
```

* 转换ISO-8859编码文件

```shell
# file命令查看文件编码为ISO-8859,vim打开ISO-8859编码中文乱码,使用iconv转换
iconv -cs -f iso-8859-1 -t utf-8 file1 > file2
```



## 解压&压缩

* 7z

```shell
#解压.7z的压缩文件需要先安装p7zip
yum -y install p7zip
#解压命令
7za x *.7z
```

* zip

```shell
#解压,参数[-o:未提示直接覆盖],[-d:指明解压到的目录]
unzip -o -d ./zipdir *.zip
#压缩，参数[-r:递归压缩]，[-d:指明压缩到的目录]
zip -d myfile.zip data.txt
zip -r -d myfile.zip ./data
```

* tgz，tar.gz，gz

```shell
#解压tgz和tar.gz，参数[-C:指明解压到的目录]
tar zxf *.tgz -C /home/brooksj/workarea
#压缩tgz和tar.gz
tar zcf FileName.tar.gz DirName
#解压gz，参数[-d:解压后删除原文件]
gzip -d FileName.gz 
#压缩gz
gzip FileName 
```

* tar.xz

```shell
#解压,参数[-d:解压后删除原文件]
xz -d *.tar.xz
#进一步解压.tar
tar -zxf *.tar
```

* tar.bz2，bz2

```shell
#解压tar.bz2
tar jxvf FileName.tar.bz2
#解压bz2，参数[-d:解压后删除原文件]
bzip2 -d FileName.bz2 
#压缩tar.bz2
tar jcvf FileName.tar.bz2 DirName 
#压缩bz2
bzip2 -z FileName
```

* rar

```shell
# 解压(解压后文件分散出来)
unrar e FileName.rar
```



## aria2c命令

* 启动aria2c

  ```
  aria2c --conf-path=/home/brooksj/.aria2/aria2.conf
  ```



## dpkg命令

* dpkg参数说明

  ```bash
  dpkg -r # 删除但是配置文件不删
  dpkg -P/--purge # 包括配置文件都删除
  ```

* 批量删除

  ```bash
  # 删除deepin开头的软件
  dpkg -l |grep deepin|awk '{print $2}'|xargs sudo dpkg -P
  ```

  

## head/tail命令

* 提取文件指定行数到另一个文件

  ```
  head -10000 a.txt > b.txt  提取a.txt文件前10000行到文件b.txt
  ```

* 复制前100个文件到文件夹tmp中

  ```
  ls |head -n 100|xargs -i cp {} /tmp
  ```

* 复制后100个文件到文件夹tmp中

  ```
  ls |tail -n 100|xargs -i cp {} /tmp
  ```

  

## 快捷键

* shell窗口命令

```shell
ctrl+shift+n   打开一个新的终端窗口
ctrl+shift+t    在当前终端窗口中增加一个终端页签
ctrl+shift+w   关闭一个终端页签
ctrl+shift+q    关闭所有终端页签
```

* terminal下粘贴复制

```shell
CTRL+SHIFT+C  复制
CTRL+SHIFT+V  粘贴
```

* terminal下的Tab窗口切换

```shell
Alt+1  切换到1窗口
Alt+2  切换到2窗口
ctrl+PaUp  切换到上一个窗口
ctrl+PaDn  切换到下一个窗口
```



## 测试端口

* 测试某台机器上的某端口是否开启

  ```shell
  curl ip:port
  wget ip:port
  ssh -v -p port username@ip
  telnet ip port
  ```

  

## socat代理设置

* 先安装socat，然后使用nohup执行以下命令

  ```shell
  nohup socat tcp-listen:8888,reuseaddr,fork tcp:114.212.85.95:8888 2>&1 &
  ```
  
  [socat命令详解](https://www.hi-linux.com/posts/61543.html)



## squid代理服务

* 配置文件/etc/squid/squid.conf中添加

  ```shell
  acl all src all # or acl all src 0.0.0.0/0.0.0.0，允许所有ip访问
  http_access allow all # 允许所有人使用代理
  ```

  [squid使用及配置详解](https://www.cnblogs.com/he-ding/p/10038264.html)



## group管理

* 查询用户所在group

```
groups $USER
```

* 创建group

```
sudo groupadd docker 创建一个docker用户组
```

* 添加用户到group中

```
sudo usermod -aG docker brooksj 添加brooksj用户到docker中
sudo gpasswd -a brooksj docker 添加brooksj用户到docker中
```

* 从group中删除一个用户

```
sudo gpasswd -d brookj docker 从docker这个group中删除brooksj这个用户
```

* 删除group

```
sudo groupdel docker  删除docker这个group
```

* 切换group

```
newgrp docker 将当前用户从切换到docker这个group,前提是用户在这个group下
```



## user管理

* 创建用户

```
创建用户brooksj,-s指定使用的shell,指定/sbin/nologin的不允许登录,-d指定用户主目录,配合-m使用则当用户主目录不存在时创建主目录,-g指定用户组
sudo useradd -s /bin/bash -d /home/brooksj -g users -m brooksj 
```



## alias常用命令

```shell
alias dataset='cd ~/github/AIPolicy/input/benchmark/entity'
alias labs='cd ~/github/AIPolicy/labs/entity; conda activate py37'
alias nv='nvidia-smi'
alias cd='func() { cd $1; ls; }; func'
alias k9='func() { ps -ef|grep $1|grep -v grep|cut -c 9-15|xargs kill -9; }; func'
alias tat='tmux a -t'
alias tns='tmux new -s'
```

