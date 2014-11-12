--- 
title: windows server部署python web程序
layout: post
category: python
---

## 环境安装

安装完成python web环境之后. 安装iis 服务器. 然后安装[Helicon Zoo][1] , 连接里面是安装步骤.    
打开Helicon Zoo Manager 找到Python Hosting Package,并安装.



## 步骤

1. 打开web platform installer :
    ![step1][2]
   按照提示安装一个模版,现在不用管项目源码.
2. 打开helicon zoo manager(上一步安装完会自动打开,如果没有手动也可).点击左侧的项目, 修改右侧web.config 文件  
```
<add name="WSGI_APP" value="runserver.app" />
``` 
将里面的value值修改配合项目源码, 我的启动脚本是runserver.py, 里面定义了一个app 返回flask app.
3. ok, 这样一个python web就上线了.

## 问题
1. 使用记事本修改web.config 的时候提示出错(有另外的程序正在使用它), 用helicon zoo manager修改即可.

 
   
[1]:http://www.helicontech.com/zoo/install.html "Helicon Zoo"
[2]: ../img/2014-11-11/deploy-python-web-on-windows-1.png "step1"