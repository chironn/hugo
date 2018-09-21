---
title: "Docker"
author: "Chiron"
tags: ["Theme", "Hugo"]
categories: ["Uncategorized"]
date: 2018-09-20T20:10:09+08:00
draft: false
---
## Introduction

目前.net core已经支持Linux系统，所以可以直接在安装.net core sdk后运行发布后的.net core应用（https://www.microsoft.com/net/learn/get-started-with-dotnet-tutorial#install）

## Operation
从Ubuntu存储库安装Docker

```
##如果您想从Ubuntu存储库安装docker版本，则可以运行下面的apt命令。
$ sudo apt install docker.io
##等到安装完成后，您可以启动Docker并使用systemctl命令将其添加到引导时间：
$ systemctl start docker
$ systemctl enable docker
##检查docker版本：
$ docker --version
```

从Docker存储库安装Docker

```
##在从Docker存储库安装docker-ce之前，使用apt命令安装一些依赖项，如下所示。
$ sudo apt install \
$ apt-transport-https \
$ ca-certificates \
$ curl \
$ software-properties-common
##安装完成后，添加docker密钥和docker'nightly'存储库。
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-    key add -
$ echo "deb [arch=amd64] https://download.docker.com/linux/ubuntu     bionic nightly" > /etc/apt/sources.list.d/docker-nightly.list
##并更新存储库。
$ sudo apt update
##现在docker仓库已经添加到系统中。
##使用apt-cache命令检查docker仓库提供的所有docker软件包。
$ sudo apt search docker-ce
$ sudo apt-cache policy docker-ce
##使用下面的apt命令安装它。
$ sudo apt install docker-ce
##安装完成后，启动Docker服务并使其每次在系统启动时启动。
$ systemctl start docker
$ systemctl enable docker
##现在检查系统上安装的码头版本。
$ docker --version
```

在ubuntu上配置Docker

```
##拉取dotnet-sdk的最新镜像，速度慢的话请使用daocloud docker hub加速。
$ sudo docker pull microsoft/dotnet:latest
##将发布之后的文件夹publish上传到服务器上
##创建Dockerfile文件，内容配置如下：
$ FROM microsoft/dotnet //该命令指定了基础镜像启动构建流程
$ WORKDIR /app //WORKDIR命令用于设置CMD指明的命令的运行目录
$ COPY ./app  //从构建上下文目录中 <源路径> 的文件/目录复制到新的一层的镜像内的 <目标路径> 位置
$ ENTRYPOINT ["dotnet", "Intest.dll"] //配置容器启动后执行的命令，并且不可被 docker run 提供的参数覆盖
##切换到Dockerfile所在的目录下，并执行构建命令，成功之后会有下图的提示
$ sudo docker build -t lightweb .　　//注意后边还有一个点
##运行刚才构建成功的容器
$ sudo dokcer run -it Intest.dll
##备注（run命令参数介绍）：http://www.runoob.com/docker/docker-run-command.html
```
