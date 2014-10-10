--- 
title: redis 做消息队列服务器(python)
layout: post
category: python
---

## 消息队列
就如同算法中的队列一般,消息队列就是把消息先进先出,类似生产者消费者的关系,这样就可以解决一些需要异步完成的一些事情.当我还是一个小孩子的时候,要找朋友出来玩,必须先找到他,后来我有了手机,就只需要群发个短信"今晚网吧通宵",收到并愿意来的人,晚上就会来到网吧.移动公司就像是个消息队列服务器.

## 生产者

	import redis
	import time
	
	def main():
		rc = redis.StrictRedis()
		while True:
			rc.publish('ch1', time.time())
			time.sleep(1)
			
	if __name__ == '__main__':
		main()
		
以上代码就完成了生产者的任务, 每隔1s像ch1频道发送一次当前时间戳.

## 消费者

	import redis
	
	def main():
		rc = redis.StrictRedis()
		sub = rc.pubsub()
		sub.subscribe('ch1')
		for m in sub.listen()
			print m
			
	if __name__ == '_main__':
		main()
	
简单的一个消息订阅者, 将收到的消息全打印出来.

## 一些问题
传说这个功能redis只用了150行代码, 所以他是很简单的,没有优先级,订阅者只能收到订阅之后产生的消息,

1. 阻塞还是非阻塞(be or no blocking?)  
这也是困扰我的一个问题,当我循环sub.listen()的时候,不管队列里面有没有值都会阻塞在那里,程序要往下执行,只能把它放到另一个线程里.

2. 如果能设置一个订阅期限真是极好的