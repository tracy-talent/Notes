<center><h1>docker tricks</h1></center>
## Command

* docker search ‘img’  ---搜索查找远程库中的镜像

*  docker pull ‘img:tag’   ---从远程库中下载镜像到本地，没有tag则默认为latest

* docker run –it [-d][--name container_name] [-p port1:port2] ‘img:tag’    ---建立运行镜像的容器，[]中的参数可选，-d指定容器在后台运行，--name指定容器名字否则docker会赋予它一个随机的名字，-p指定本机端口到容器端口的一个映射

* docker exec –it ‘container’ /bin/bash   ---运行容器，可以进入到在后台运行的容器，container可以使容器名也可以是容器ID

* docker start ‘container’  ---启动容器

* docker attach ‘container’  --进入到容器

* docker stop ‘container’  ---关闭容器

* docker logs ‘container’  --查看容器中程序执行输出

* docker inspect ‘container/img:tag’  ---查看容器或者镜像信息，可以用ID替代名字，以json格式输出

* docker ps [-a][-q]  ---查看正在运行的容器的基本信息，[]中参数可选，-a可查看所有容器包括未在运行的，-q指定输出容器信息为ID

* docker rm ‘container’  ---删除容器

* docker stop $(docker ps -aq)  ---关闭所有容器

* docker rm $(docker ps -aq)  --删除所有容器

* docker stop \$(docker ps -aq) & docker rm \$(docker ps -aq)  ---联合命令，关闭并删除所有容器

* docker commit ‘container’ img:tag  ---利用容器创建自定义的镜像

* docker tag ‘img:tag’ ‘newimg:newtag’  ---重命名镜像和标签，共用镜像ID

* docker rmi ‘img:tag’   ---删除镜像

* docker save –o ***.tar ‘img:tag’  ---将镜像打包，保留了各个历史版本的容器，可回滚，方便部署到其他机器

* docker load –i ***.tar  ---加载镜像到docker中

* docker export ‘container’ > ***.tar  ---将单个容器打包

* docker import < ***.tar   ---加载容器到docker中

* docker build [-f path_of_Dockfile] .  ---Dockfile以当前目录为本地上下文目录构建自定义镜像



## tensorflow image tutorial

* 下载镜像

```shell
docker pull tensorflow/tensorflow:nightly-py3
```

* 创建容器

<font color='green' size=3>参数说明:</font> -it参数关联终端terminal输入与容器输入并将容器输出到terminal,-d后台运行,-v映射本机目录到容器目录使得内容一致,-w指定容器工作目录,-p指定本机与容器的端口映射,--name指定容器名字,--rm使得关闭容器后删除容器

```shell
docker run -it -d -v $PWD:/tmp -w /tmp -p 13333:8888 --name tf tensorflow/tensorflow:nightly-py3  
```

* 进入容器终端

```
docker exec -it -u brooksj tf /bin/shell 进入指定用户的终端shell
```



