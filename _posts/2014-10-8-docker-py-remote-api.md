--- 
title: docker-py docker的remote API
layout: post
category: linux
---

## 安装docker
docker的安装很简单,在ubuntu下运行:

    curl -sSL https://get.docker.io/ubuntu/ | sudo sh 
即可安装最新的docker,详情见[官方说明][1]

[1]:https://docs.docker.com/installation/ubuntulinux/ "docker install on ubuntu"

## 配置docker
默认docker使用unix的sock进行通信,这样只能本机操作docker,要开启docker的tcp端口监听:

    sudo vi /etc/default/docker
把`DOCKER_OPTS=`这行注释去掉,改为:

    DOCKER_OPTS="-H unix:///var/run/docker.sock -H tcp://0.0.0.0:5001"
然后:

    sudo service docker restart
这样docker就在5001端口监听了.  
测试一下: 在浏览器输入 dockerhost:5001/info, 如果有输出docker info 则配置成功.

## 安装docker-py
首先安装pip或者easy_install等python包管理工具,一般系统自带easy_install.

    sudo pip install docker-py
## 使用docker-py
打开python

    import docker
    c = docker.Client(base_url="tcp:dockerhost:5001")
    c.info()
如果没有出错信息这说明一切ok,可以使用了.

## 
    