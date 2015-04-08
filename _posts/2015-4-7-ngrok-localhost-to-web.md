--- 
title: ngrok-让localhost连到万维网上去
layout: post
category: tools
---

## 简介
[ngrok][1] 是一个能让外网访问本地环境的一个服务. 这样就能解决很多问题, 不用将代码部署到外网服务器即可测试. 还完美的解决了微信本地开发的问题, ngrok能将收到的请求和回复记录下来, 也方便了移动网页不能调试的问题. 甚至还能转发tcp.
## 使用
本来是可以使用ngrok.com提供的服务的, 但是我们的防火墙封锁了这个网站, 我也找到了这个国内开发者搭建的tunnel.mobi服务, 速度快很多. 但是总觉得使用别人的服务会有问题,说不定那天就被封了,毕竟这东西国内不允许.所以决定自己搭建一个服务, ngrok是一个开源的项目, 代码部署于github上.
## 搭建服务器
1. 首先当然要有一台服务器,或者vps. 还要有一个域名,将域名的A记录指向服务器.
2. 再我的本地环境是osx, 安装go1.1+, 用来编译服务器端和客户端程序.go可以很方便的交叉编译其他平台的程序, 我的服务器是linux的, 在mac上设置GOOS=linux/GOARCH=amd64环境变量,编译出来linux程序,清楚环境变量,编译出来的是mac程序.
3. 使用openssl生成自签名的证书, 当然购买正式的证书更好了.
4. 命令  

```
NGROK_DOMAIN="domain.com"
git clone https://github.com/inconshreveable/ngrok.git
cd ngrok

openssl genrsa -out rootCA.key 2048
openssl req -x509 -new -nodes -key rootCA.key -subj "/CN=$NGROK_DOMAIN" -days 5000 -out rootCA.pem
openssl genrsa -out device.key 2048
openssl req -new -key device.key -subj "/CN=$NGROK_DOMAIN" -out device.csr
openssl x509 -req -in device.csr -CA rootCA.pem -CAkey rootCA.key -CAcreateserial -out device.crt -days 5000

cp rootCA.pem assets/client/tls/ngrokroot.crt
make clean
make release-server release-client
```

+ 通过以上代码程序就编译好了,把编译好的ngrokd  device.key  device.crt 三个文件拷贝到服务器上运行

```
nohup ./ngrokd -tlsKey=device.key -tlsCrt=device.crt -domain="domain.com" -httpAddr=":80" -httpsAddr=":8081" > ngrok.log &
```

+ 这样服务器就可以工作了.

## 客户端
清除GOOS=linux/GOARCH=amd64环境变量,make release-client 编译一个mac用的客户端.

```
./ngrok -config ngrok.cfg -subdomain test 5000
```
test是子域名, 5000是监听的本地端口号, ngrok.cfg内容如下:

```
server_addr: "domain.com:4443"
trust_host_root_certs: false
```
如果是正式的ssl证书trust_host_root_certs:true    
客户端也能用了,现在访问test.domian.com试试吧.

## 遇到的问题
+ 交叉编译的问题

```
# 设置环境变量
export GOOS=linux
export GOARCH=amd64
# 去go的安装目录src/
./make.bash
# 然后再去编译环境
```

## 总结
记录一下使用过程, 这中间也遇到过各种问题.基本都能在作者的github上找到方法:

1. ngrok官网: https://ngrok.com (需要翻墙进入)


[1]:https://github.com/inconshreveable/ngrok "github代码"