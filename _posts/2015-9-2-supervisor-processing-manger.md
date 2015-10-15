--- 
title: supervisor方便的进程管理工具
layout: post
category: tools
---

## 序

一般我不喜欢电脑开机自动运行程序. 那么问题了, 开发的电脑需要运行各种服务, 如redis, mongo, mysql, es 等等. 以前我都是开几个终端去分别手动开启, 虽然我的电脑基本是不关机的, 但是有时候分别开启, 还是很麻烦, 特别是紧急的情况, 越是着急越慢.		
现在我发现了supervisor

## 安装supervisor

`sudo pip install supervisor` 就行了

然后 `sudo echo_supervisord_conf > /etc/supervisord.conf` 修改配置 `sudo supervisord`就好了
以后修改了配置文件`sudo supervisorctl reload`

## 管理

`sudo supervisorctl`进入了管理控制台

