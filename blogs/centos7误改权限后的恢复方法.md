今天由于权限问题zz一般把/usr/bin和/usr/lib两个目录用chmod -R 777执行了一遍，结果各种问题出现，su root就报su:鉴定故障的错误。然后上网找教程很多都要求在root权限下操作来修复，真是悔不当初，哭都哭不出来，只想剁手。幸好最好予以解决了，不然就真得重装系统了(那估计又是摸鱼几天来恢复系统)，在此把解决方案记录下来，希望能给踩到坑的朋友抢救一下。

## step1

新建一个.c文件，在这里我命名为chmodfix\.c，把如下内容写到这个\.c文件中

```c
#include <stdio.h>                                                                              #include <stdlib.h>
#include <string.h>
#include <sys/stat.h>
#include <ftw.h>
int list(const char *name, const struct stat *status, int type)
{
	if(type == FTW_NS)
		return 0;
	printf("%s 0%3o\n", name, status->st_mode & 07777);
	return 0;
}
int main(int argc, char *argv[])
{
	if(argc == 1)
		ftw(".", list, 1); 
	else
	ftw(argv[1], list, 2); 
	exit(0);
}
```

然后在终端命令行下使用gcc编译得到可执行文件chmodfix.com

```shell
gcc chmodfix.c -o chmodfix.com
```

## step2

新建一个.sh文件，在这里我命名为chmodfix.sh，把如下内容写到这个.sh文件中

```shell
#!/bin/sh                                                                                     if [ $# != 1 ] 
then
	echo Usage : $0 \<filename\>
	exit
fi
PERMFILE=$1
cat $PERMFILE | while read LINE
do
	FILE=`echo $LINE | awk '{print $1}'`
	PERM=`echo $LINE | awk '{print $2}'`	
	chmod $PERM $FILE
	#echo "chmod $PERM $FILE"
done
echo "change perm finished! "
```

## step3

找到另一台装有centos7并且系统权限正常的电脑，利用step1中得到的chmodfix.com从这台电脑上获取被你损坏的目录下所有文件的正常权限

```shell
# 假设原电脑上权限损坏的目录为/usr/bin
./chmodfix.com /usr/bin >> chmodfix.txt
```

输出文件chmodfix.txt的内容形式如下

> /usr/bin 0755                                                                                                                                                                                                      /usr/bin/cp 0755 
> /usr/bin/lua 0755 
> /usr/bin/captoinfo 0755 
> /usr/bin/csplit 0755 
> /usr/bin/clear 0755 
> /usr/bin/cut 0755 

将得到的权限文件chmodfix.txt复制到权限受损的电脑上

## step4

这时候由于电脑权限损坏无法切换到root用户从而无法直接修改根目录下被损坏文件的权限，需要切换到centos的**emergency mode**(ubuntu的用户对应进入到**recovery mode**)。那么如何进入到emergency mode呢？开机启动的grub界面处对对应系统按下**e**键，就进入到如下画面

<div align="center">
    <img src="https://raw.githubusercontent.com/tracy-talent/Notes/master/imgs/emergency mode.png">
</div>

然后将上图中红圈标示的**ro**替换成**rw init=/sysroot/bin/sh**，然后根据底下提示按下ctrl+x启动系统则进入到emergency mode，首先执行命令**chroot /sysroot**以获取直接访问真实系统文件的权限，然后进入到chmodfix.sh和chmodfix.txt所存放的文件夹下，执行chmodfix.sh以根据chmodfix.txt恢复受损文件的正确权限

```shell
bash chmodfix.sh chmodfix.txt
```

由于涉及的文件可能很多，这个过程可能比较长，耐心等待一下，执行结束后在命令行下输入以下命令来重启系统

```bash
exit
reboot
```

## 结束

重启之后在终端下执行su root若能成功切换到root用户而没有提示**su:鉴定故障**的错误则表明文件修复成功，也可以通过ls -l file来查看文件权限

```bash
>ls -l /usr/bin/python
lrwxrwxrwx. 1 root root 7 2月  22 11:25 /usr/bin/python -> python2
```



**血淋淋的教训(一怒之下险些要重装系统了)，通过这篇日志把此次重大事故记录下来，希望能帮助到同我一样踩到雷的朋友顺利解决。同时，吃一堑长一智以后可不能再随便使用chmod -R 777修改大批量系统文件的权限，也望各位引以为鉴。**

--------------------------------------------分隔线-----------------------------------------

emergency mode下也可以修改root密码，进入到emergency mode后输入下面的命令

```shell
chroot /sysroot
passwd root #接下来会要求输入密码以及确认密码
touch /.autorelabel  #如果系统启用了selinux，一定要加上这条命令以防无法正常开机
exit
reboot
```





