--- 
title: docker 使用笔记
layout: post
category: linux
---

## docker 获得images

	sudo docker run -t -i ubuntu:14.04 /bin/echo "ubuntu:14.04 images"
运行命令ubuntu的images 会下载下来

## 在别人的基础上打造自己的镜像
别人的镜像毕竟不会很适合自己, 下载的ubuntu:14.04作为基础镜像,修改成自己需要的:

	sudo docker run -t -i ubuntu:14.04 /bin/bash
	# 下面的操作是已经进入到container中的
	apt-get update
	apt-get upgrade
	apt-get install python
	exit
	# 下面实在主机上进行的
	sudo docker commit -m "add python2.7" -a "wayne" 590d769b2923 wayne/ubuntu-py:1.0
	# 590d769b2923 是container id,使用sudo docker ps -a 查看
	sudo docker images
	# 列出了所有images,新建的wayne/ubuntu-py就在其中
	
## 从头开始建立自己的images
使用`Dockerfile` 来建立images,这样就可以很容易的分享建立的image

	mkdir prowayne
	cd prowayne
	vi Dockerfile
输入

	# this will create a image form ubuntu:14.04 and 	install python
	FROM ubuntu:14.04
	MAINTAINER Wayne <prosmarter@163.com>
	RUN apt-get update && apt-get -y upgrade
	RUN apt-get -y install python
然后使用docker build建立

	sudo docker build -t="prowayne/wayne-dev:1.0" .
	# 注意最后有个点, 表示当前目录
	
正常的话一个wayne/wayne-dev:1.0 image就建立好了, 要分享你的image只需把Dockerfile分享出去,别人就可以建立同样的image.

## 相关操作
1. 删除 image 
  
		sudo docker rmi [image id]
但是如果存在这个image建立的container则不能删除成功,需要先删除container

		sudo docker ps -a
		sudo docker rm container_name
2. 删除所有container  

		sudo docker ps -a -q|xargs sudo docker rm
		
## 

