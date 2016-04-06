--- 
title: jupyterhub add python2 kernel
layout: post
category: python
---

## 背景

jupyter notebook(ipython notebook) 是一个很有意思的工具, 
但是默认的python解析器可能并不适合我们使用, 这里我要给他加一个kernal, 我自己的virtaulenv 环境

## 准备

首先我们准备一个virtualenv 环境

```shell
virtualenv .venv
source .venv/bin/activate
pip install jupyter

cd /var/www/jupyterhub
mkdir -p kernels/python2_way
jupyter kernelspec list
# jupyter kernelspec remove python2_way
```

## 添加一个kernel

```shell
vi kernels/python2_way/kernel.json
```

具体

```
{
 "display_name": "Python2(way)",
 "language": "python",
 "argv": [
  "/home/wayne/.venv/bin/python",
  "-m",
  "ipykernel",
  "-f",
  "{connection_file}"
 ]
}
```

然后 

```
jupyter kernelspec install kernels/python2_way
```