--- 
title: 好用的图表模块 matplotlib
layout: post
category: python
---

## 简介matplotlib
广泛使用的python图表库, 提供类似matlab的绘图方式, 方便的将数据绘制成图表, [官网][1] 上面提供了详细的说明, gallery里面有很多例子,可以直接拿来使用,非常方便.

## 安装环境
使用pip 或源码安装都可, 我习惯pip安装  
`pip install matplotlib`
顺便把numpy也安装了`pip install numpy`

## 简单使用
```
import matplotlib.pyplot as plt
import numpy as np
x = np.arange(11)
y = x * x
fig = plt.figure(1)  # Create a `figure' instance
ax = fig.add_subplot(111)  # Create a `subplot' instance in the figure
ax.plot(x, y)  # Create a Line2D instance in the axes
plt.show()
```
就出现了:  
![figure1][2]
这是一个很简单的y=x^2 的曲线

## 另外
官网上有很多的很漂亮的图, 基本所有的图表都能画出来. pylab更是提供了,面向对象的额快速的画图方法.


[1]:http://matplotlib.org/ "matplotlib官网"
[2]:../img/2014-12-24/figure_1.png "figure1"

