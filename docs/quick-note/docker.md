# docker

# docker 基础

## docker 安装 (Arch)

```shell
sudo pacman -S docker
```

如果想以普通用户身份运行 docker 命令，将当前用户加入docker组中

```shell
sudo gpasswd -a ${USER} docker
```

## 基础命令

### 镜像命令

docker images

docker search

docker pull

docker system df 查看镜像/容器/数据卷所占的空间

docker rmi 某个XXX镜像名字ID

### 容器命令

docker run [OPTIONS] IMAGE [COMMAND] [ARG...] 新建+启动容器

docker ps [OPTIONS] 列出当前所有正在运行的容器

退出容器

exit run进去容器，exit退出，容器停止

ctrl+p+q run进去容器，ctrl+p+q退出，容器不停止



启动已停止运行的容器 docker start 容器ID或者容器名

重启容器 docker restart 容器ID或者容器名

停止容器 docker stop 容器ID或者容器名

 强制停止容器 docker kill 容器ID或容器名

删除已停止的容器 docker rm 容器ID

docker rm -f $(docker ps -a -q)

docker ps -a -q | xargs docker rm

启动守护式容器(后台服务器)

在大部分的场景下，我们希望 docker 的服务是在后台运行的，我们可以过 -d 指定容器的后台运行模式。

docker run -d 容器名

docker run -it redis:6.0.8



查看容器日志 docker logs 容器ID

查看容器内运行的进程 docker top 容器ID

查看容器内部细节 docker inspect 容器ID

进入正在运行的容器并以命令行交互

docker exec -it 容器ID bashShell

重新进入docker attach 容器ID

attach 直接进入容器启动命令的终端，不会启动新的进程
用exit退出，会导致容器的停止。

exec 是在容器中打开新的终端，并且可以启动新的进程
用exit退出，不会导致容器的停止。

推荐大家使用 docker exec 命令，因为退出容器终端，不会导致容器的停止。



从容器内拷贝文件到主机上

容器→主机

docker cp 容器ID:容器内路径 目的主机路径



导入和导出容器

export 导出容器的内容留作为一个tar归档文件[对应import命令]

import 从tar包中的内容创建一个新的文件系统再导入为镜像[对应export]

docker export 容器ID > 文件名.tar

cat 文件名.tar | docker import - 镜像用户/镜像名:镜像版本号









