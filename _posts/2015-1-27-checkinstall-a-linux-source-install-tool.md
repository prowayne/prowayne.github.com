--- 
title: CheckInstall-更好的源码安装工具
layout: post
category: linux
---

## 简介
在linux上, 因为一些原因,我经常要从源码安装程序,但是当我想知道,我安装过什么程序或者需要将他们卸载的时候, 我有点不知所措. 相反我通过apt-get 还是dpkg安装的程序我能很方便的找到它们. 直到我发现了Felipe Eduardo 所写的 CheckInstall , 很完美的解决了我的问题. CheckInstall会在安装程序之前,先生成包, 然后使用包管理工具安装软件.

## 安装配置
从[官网][1] 下载源码,或安装包,安装  

```
tar xzf checkinstall-1.6.2.tgz  
cd checkinstall-1.6.2  
make  
make install
checkinstall
```
然后选择需要生成的包类型,有Slackware, RPM, Debian可以选择.

`/usr/local/lib/checkinstall/checkinstallrc`是配置文件,可配置INSTYPE(包的类型), PAK_DIR (包的路径), INSTALL(0只生成, 1生成完安装).

* 好了,现在可以使用
* 正常的从源码安装使用`./configure && make && make install`
* 现在只要使用`./configure && make && checkinstall`就行了, 如果配置里的INSTALL=1的话. 如果INSTALL=0的话,只是生成了对应的包, 
还要使用rpm 或者dpkg包管理工具安装包.
* 现在就可以使用包管理工具管理从源码安装的程序了.

## 总结
checkinstall应该被所有的人所使用.




[1]:http://asic-linux.com.mx/~izto/checkinstall/ "官网"