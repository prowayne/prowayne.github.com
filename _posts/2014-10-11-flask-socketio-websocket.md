--- 
title: 使用flask-socketio 进行websocket通信
layout: post
category: python
---

## flask-socketio
就是那个[socketio][1]的flask插件, 熟悉nodejs的可能了解socketIO的使用.

[1]:http://socket.io "socket.IO"

## 安装
在安装flask之后:

	sudo pip install flask-socketio
	
## 使用
在官方的github代码库中有[例子][2],运行example目录中的app.py即可看到演示.

1. 前台

	    # 包含库文件://cdnjs.cloudflare.com/ajax/libs/socket.io/0.9.16/socket.io.min.js
	    # 主要js
	    namespace = '/test';
	    var socket = io.connect('http://' + document.domain + ':' + location.port + namespace);
        socket.on('connect', function() {
           socket.emit('my event', {data: 'I\'m connected!'});
        });
2. 后端

		# from gevent import monkey
		# monkey.patch_all()
		@socketio.on('my event', namespace='/test')
		def test_message(message):
    		emit('my response',
         		{'data': message['data'],
         		'count': 1})


[2]:https://github.com/miguelgrinberg/Flask-SocketIO

## 相关
主要用到的就是on, 和emit方法:

1. on(监听)

		on('action', function)
其中'action'是指令, 前后台一样能通信.function(re){}参数接受websocket传过来的json数据.  
后台的namespace参数相当于flask的route(namespace)  

2. emit(发送)

		emit('action',data)
同样'action'是指令, data为json格式的数据

## 遇到的问题

1. uwsgi服务器的使用还有点问题, 好在有gunicorn可以使用.([flask-socketIO:0.4.0][3])

[3]:http://flask-socketio.readthedocs.org/en/latest/ 最新文档



















a
