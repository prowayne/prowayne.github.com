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
	sudo docker commit -m "add python2.7" -a "wayne" 590d769b2923 prowayne/ubuntu-py:1.0
	# 590d769b2923 是container id,使用sudo docker ps -a 查看
	sudo docker images
	# 列出了所有images,新建的prowayne/ubuntu-py就在其中
	
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
3. 查看运行日志

		sudo docekr logs container_name
		
## 将本地目录挂载到container上
container上的文件尽量不修改, 要把代码部署上去可以使用docker volume:

	sudo docker run -d -p 8080:5000 --name web -v /src/webapp:/opt/webapp:ro prowayne/wayne-dev python /opt/webapp/app.py
	# 将本地的/src/webapp挂在到了container的/opt/webapp上,设置只读
	# 注意目录必须为绝对路径
	
## 建立基于docker的sandbox运行环境
运行客户的代码可能产生安全问题,有必要为隔离每次运行的环境&限制运行使用的内存cpu,首先设置系统:

	sudo vi /etc/default/grub
	# 找到GRUB_CMDLINE_LINUX行,修改为
	>GRUB_CMDLINE_LINUX="cgroup_enable=memory swapaccount=1"
	sudo update-grub
	sudo reboot
这样之后:

	sudo docker run -d --name me -m 64m -c 512 -v /home/wayne/study:/opt/app prowayne/wayne-dev:1.0 python /opt/app/app.py
	
每次运行不安全的代码,就建立一个container,运行完销毁.基本确保了服务器不会被未知代码损害.




