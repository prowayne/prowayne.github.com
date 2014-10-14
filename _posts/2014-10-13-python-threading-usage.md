--- 
title: python的多线程模块threading
layout: post
category: python
---

## 简单使用

1. threading模块是thread的扩展,使用很方便:

		import threading
		
		def handler():
			print "im in thread"
		
		def main():
			t = threading.Thread(target=handler)
			t.start()
			
		if __name__ == "main":
			main()
			
2. 也可以继承threading.Thread

		import threading
		
		class Listener(threading.Thread):
			def __init__(self):
				threading.Thread().__init__(self)
			
			def run():
				print "im in listener now"
				
		if __name__ == "main":
			l = Listener().start()
			
## threading.local
这个模块的主要功能是为每个现成创建了一个变量,变量的值只在自己的线程里有效:
	
	import threading
	
	local = threading.local()
	local.name = 'main'
	
	def handler():
		local.name = 'child'
		print local.name
	
	def main():
		print local.name
		threading.Thread(target=handler).start()
		print local.name
		
	if __name__ == "main":
		main()

以上运行结果是:
	
	main
	child
	main
	
是的,虽然这个变量在各个线程中, 但它们的值却是不一样的.  
我把这用在一个数据库连接模块中,当作一个全局变量来用的.







	