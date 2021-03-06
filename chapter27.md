# docker基础

## 简介

Docker 使用客户端-服务器 \(C/S\) 架构模式，使用远程API来管理和创建Docker容器。Docker 容器通过 Docker 镜像来创建。容器与镜像的关系类似于面向对象编程中的对象与类。

Docker 镜像\(Images\)Docker 镜像是用于创建 Docker 容器的模板。  
Docker 容器\(Container\)容器是独立运行的一个或一组应用。  
Docker 客户端\(Client\)Docker 客户端通过命令行或者其他工具使用 Docker API \([https://docs.docker.com/reference/api/docker\_remote\_api](https://docs.docker.com/reference/api/docker_remote_api)\) 与 Docker 的守护进程通信。  
Docker 主机\(Host\)一个物理或者虚拟的机器用于执行 Docker 守护进程和容器。  
Docker 仓库\(Registry\)Docker 仓库用来保存镜像，可以理解为代码控制中的代码仓库。  
Docker Hub\([https://hub.docker.com](https://hub.docker.com)\) 提供了庞大的镜像集合供使用。  
Docker Machine：Docker Machine是一个简化Docker安装的命令行工具，通过一个简单的命令行即可在相应的平台上安装Docker，比如VirtualBox、 Digital Ocean、Microsoft Azure。

## 一.安装

## 二.命令及使用
### 1.容器生命周期管理

run  
start/stop/restart  
kill  
rm  
pause/unpause  
create  
exec

### 2.容器操作

ps  
inspect  
top  
attach  
events  
logs  
wait  
export  
port

### 容器rootfs命令

commit  
cp  
diff  
镜像仓库  
login  
pull  
push  
search

### 3.本地镜像管理

images  
rmi  
tag  
build  
history  
save  
import  
info\|version  
info  
version


## 三.dockerfile

Dockerfile是docker构建镜像的基础，也是docker区别于其他容器的重要特征，正是有了Dockerfile，docker的自动化和可移植性才成为可能。

FROM , 从一个基础镜像构建新的镜像  
MAINTAINER , 维护者信息  
ENV , 设置环境变量  
RUN , 非交互式运行shell命令  
ADD , 将外部文件拷贝到镜像里,src可以为url  
WORKDIR /path/to/workdir, 设置工作目录  
USER , 设置用户ID  
VULUME &lt;\#dir&gt;, 设置volume  
EXPOSE , 暴露哪些端口  
ENTRYPOINT \[‘executable’, ‘param1’,’param2’\]执行命令  
CMD \[“param1”,”param2”\]

# docker实例

# 优化



