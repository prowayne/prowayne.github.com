---
title: 使用 Github Pages
layout: post
category: git
---
## 什么是github pages
github众所周知,当你注册github账号的时候,你已经获得了一个自己主页,就像QQ与QQ空间一样.不同之处在于你还可以为你的每一个项目建立一个主页,这就是你的pithub pages,以下简称gh-pages. 每个人的主页地址是username.github.io(username 换成你的帐号),项目主页的地址是username.github.io/repository(repository换成你的项目名),需要把主页文件放在在gh-pages分支里.github会使用jekyll自动构建一个静态的网站.

## 为什么使用gh-pages
为什么使用呢,这个问题向来不好回答.   
问银行劫匪为什么抢银行,他回答:"因为钱在那里!"   
问探险家为什么冒险登峰,他回答:"因为它在那!"   
那为什么用gh-pages,因为他在哪儿,github提供了这样一个功能   
其实使用gh-pages还是需要一些技术,大概知道git,html,markdown是什么就能上手了.
## 怎么使用gh-pages
详细的直接看官方怎么说吧[官网][1]   
简单几步就能搞定:  

1. 得有的个github帐号吧,username(用户名)也得记住了.
2. 创建一个代码库(add new repository)这个代码库名字必须是:`username.github.com` .
3. 建好代码库clone下来,在里面新建index.html文件,填上任意内容,push上去等十分钟.
4. 正常的话,打开浏览器,键入username.github.com
5. 好了

为已有项目添加主页就更简单了,新建一个空的名叫gh-pages分支,把静态页面放进,等十分钟就好了.  

[1]:https://pages.github.com/ "gh-pages"


## 高级点的用法
只能放html文件未免有些不变,当然有更高级的用法.[jekyll][2]是一个很易用的一个静态页面生成器,使用它可以生成很漂亮的页面.最重要的是这是gh官方支持默认使用的.  
如果不喜欢自带的域名,还可以使用自己的域名,具体参考[官网][1].


[2]:https://github.com/jekyll/jekyll "jekyll"