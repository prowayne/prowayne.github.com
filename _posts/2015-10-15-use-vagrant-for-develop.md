--- 
title: 使用vagrant搭建统一的开发环境
layout: post
category: tools
---

## 前言

有一个问题一直困扰我, 就是用一台新电脑, 或者用别人电脑的时候, 需要花很多的时间配置开发环境, 或者让别人开发的时候也是, 一样的需要花半天时间配置, 还有可能出现各种问题. 很可能就会出现在我的电脑上运行好好的程序, 别人不能运行. 或者自己的环境就与服务器的不同. 直到我发现了个好东西`vagrant` 其实也没什么特别的, 就是一个虚拟机管理工具, 但是它能把环境打包好自己维护, 或者发给别人都相当方便.

## 安装

vagrant 依赖virtualbox, 所以要先安装上.
然后去[boxs][1] 这里有很多打包好的镜像, 选一个需要的, 在此基础上配置, 当然有现成的就更好了.

## 配置vagrant

* 我下载的box存在~/ubuntu15_04.box, 所以我添加一个box

```
vagrant box add unbuntu15 ~/ubuntu15_04.box
```

* 然后到需要虚拟机运行的项目下面

```
vagrant init <machine_name>
vi Vagrantfile  # 修改成需要的配置
vagrant up
vagrant ssh
```

如果正常的话已经进入到新建的虚拟机下面了. 项目代码就挂载在 `/vagrant`, 如果挂载不成功的话, 需要google一下, 安装virtual的工具包.

## 配置虚拟机

现在已经在虚拟机里了, 就在这里将环境配置好吧, 退出

## 打包一个自己的box

```
vagrant halt
vagrant package --output my.box
```

现在把这个box存在网盘里吧, 给别人用自己用都不错的


[1]:http://www.vagrantbox.es "很多的box"