--- 
title: elasticsearch-开源搜索引擎
layout: post
category: programme
---

## elasticsearch简介
简介就引用百度百科上的吧 [elasticsearch][1]
>ElasticSearch是一个基于Lucene构建的开源，分布式，RESTful搜索引擎。设计用于云计算中，能够达到实时搜索，稳定，可靠，快速，安装使用方便。  
我们建立一个网站或应用程序，并要添加搜索功能，令我们受打击的是：搜索工作是很难的。我们希望我们的搜索解决方案要快，我们希望有一个零配置和一个完全免费的搜索模式，我们希望能够简单地使用JSON通过HTTP的索引数据，我们希望我们的搜索服务器始终可用，我们希望能够一台开始并扩展到数百，我们要实时搜索，我们要简单的多租户，我们希望建立一个云的解决方案。Elasticsearch旨在解决所有这些问题和更多的。

好吧,百科简介貌似是翻译的, 我想要为网站建立一个强大的搜索功能,可以使用阿里的,或者google的站内搜索, 我要在程序内部使用一个搜素功能,就比较麻烦了,因为我不想花费很多的时间去研究它, 我了解了一些比如数据库的全文检索,Sphinx等等一些东西,还是不能满意,知道我听说了elasticsearch(简称es).


[1]:http://baike.baidu.com/view/8005387.htm?fr=aladdin "百科elasticsearch"

## 下载安装启动
[官网在此][2],下载即可, 不用编译,也不用安装.  
在mac(osx10.9)默认的jdk是1.6版本的,而es需要1.7以上,先安装jdk然后

```
# 我下载的是tar包
tar -vzxf elasticsearch-1.3.4.tar.gz
cd elasticsearch-1.3.4
./bin/elasticsearch
# 至此安装启动完毕
curl -X GET http://localhost:9200/
如果有数据输出,status是200,那么,es正常运行了
```


[2]:http://www.elasticsearch.org/ "es官网"

## 给es安装一个管理工具
有一个插件[elasticsearch-head][3]挺好用,纯html写的,方便管理es,github上介绍了两种安装方式:

1. 以插件的方式

        sudo ./bin/plugin -install mobz/elasticsearch-head
        open http://localhost:9200/_plugin/head/
2. 将文件下载下来直接打开就行

        git clone git://github.com/mobz/elasticsearch-head.git
        cd elasticsearch-head
        open index.html
        # 在最上面那个输入框里填上es的地址就行了
    
[3]:https://github.com/mobz/elasticsearch-head "elasticsearch-head"

not end
