--- 
title: ipython & notebook
layout: post
category: python
---

## 安装
开始上网搜索怎么安装,看得我眼都花了,最后总结其实很简单,一句命令搞定

	sudo pip install 'ipython[notebook]'
这就行了.

## 启动
启动的时候也遇到了点问题,远程连接不到,只能本机使用,要这样启动才能:

	sudo ipython notebook --ip 0.0.0.0
	
好了, 默认监听的端口是8888,我的服务器地址是10.0.1.172,在浏览器输入10.0.1.172:8888, 这就能用了.

## 现在叫 jupyter
安装方式`sudo pip isntall jupyter`, 启动 `jupyter nootbook`

默认的配置

* `~/.ipython/profile_default/ipython_kernel_config.py`
* `~/.jupyter/jupyter_notebook_config.py`

## 其他问题
1. 导出html报错  
No module named pygments.formatters 遇到了500错误

		sudo pip install pygments


