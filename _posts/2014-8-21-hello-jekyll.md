--- 
title: 使用 jekyll
layout: post
category: git
---

## 什么是jekyll?
简单的讲就是静态网页生成器,项目地址:[jekyll][1]  
 
[1]:https://github.com/jekyll/jekyll "jekyll"

## 为什么使用jekyll
还是有很多理由...   
有那么多类似的项目,我用它是因为他是github默认使用的生成器.本着一切从简的原则,就不换成别的了,而且也很好用的.

## 怎么使用jekyll
这里[jekyll][1]讲的很详细了,但是e文水平有限,看的不是特别明白,在浏览了一下前人的站点和源码之后,调理渐渐清晰起来

### 目录结构
我的主页的目录

    CNAME    _drafts/    _posts/    css/    index.html
    README.md    _includes/    _site/    fonts/    js/
    _config.yml/    _layouts/    categories.html    img/
    
基本这样就足够了:

* CNAME 文件里面只有一行`blog.prowayne.com`(自己的域名),在域名提供商哪里添加一条CNAME解析,记录值是username.github.io.如果不使用自己的域名这个文件是可选的.
* _drafts/ 文件夹里面放草稿,不用草稿的话这个文件夹也用不着.
* _post/ 文件夹里存放的是自己写的文章命名规则`年-月-日-标题.md`,文章文件这样就会被自动识别.
* css,js,fonts,img这几个文件夹放对应的静态文件.
* index.html 主页
* _includes/ 文件夹放需要重复使用的代码块.
* _layout/ 文件夹放模版文件.
* _config.yml 这是个配置文件.

具体的可以看一下[我的源码][2],这里[有更多][3]的项目可以参考. 

### 总结 
开始的时候可能觉得麻烦点,但是架子搭建好以后就可以流畅的写博客了.使用markdown写好文章,git push上去,如同写代码,对于我们这群程序员来说简直愉快.

[2]:https://github.com/prowayne/prowayne.github.com "我的"
[3]:https://github.com/jekyll/jekyll/wiki/Sites "更多"