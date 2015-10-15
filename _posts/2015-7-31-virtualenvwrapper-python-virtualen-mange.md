--- 
title: zsh 可以代替bash了
layout: post
category: tools
---

## 前言

对系统默认bash一直用起来也不错, 有一天看到网上有人推荐zsh, 我也就试了一下, 果然好用, 当然是配合了oh-my-zsh之后. 

## 安装

`apt-get insall zsh` 也有很多系统已经内置了, `vi /etc/passwd` 改掉默认登录的bash		

再安装上 oh-my-zsh `sh -c "$(wget https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"`

好了重新登录试试, 是不是漂亮了一点呢, 

## 配置

配置文件在 `~/.zshrc` 修改主题, 或者 插件, 默认的主题我就觉得很好. 插件默认只加载了git,  我还很喜欢用autojump 加上去好了

## 可以使用了

