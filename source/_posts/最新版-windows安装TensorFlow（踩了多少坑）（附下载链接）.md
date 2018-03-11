---
title: 最新版-windows安装TensorFlow（踩了多少坑）（附下载链接）
date: 2017-10-26 17:50:33
tags: TensorFlow
---


>摘要: 利用Anaconda安装python环境，并安装TensorFlow

网上有很多之类的文章，但是还是会很难安装成功,根据网上的及自己的经验，其间跳坑无数，摔得遍体鳞伤，曾一度怀疑自己廉颇老矣。最终吐血总结出来这篇博文，希望对大家有帮助！
先说下我的电脑是**win7,64位系统，支持**（tensorflow在windows下只支持python 3.5以上、amd64）
<!-- more -->
### 大致步骤
* 先安装Anaconda（**利用Anaconda创建python35的环境**）
* 安装CUDA,CUDNN（GPU运行要用到）
* 安装 TensorFlow

### 什么是 Anaconda？

>Anaconda is the leading open data science platform powered by Python.
Anaconda 是一个由 Python 语言编写领先的开放数据科学平台

### 神魔是cuDnn和CUDA

[CPU、GPU、CUDA，CuDNN 简介](http://blog.csdn.net/fangjin_kl/article/details/53906874)

### 什么是 TensorFlow？

>TensorFlow is an open source software library for numerical computation using data flow graphs.
TensorFlow是一个开源软件库，用于使用数据流图进行数值计算。


### 具体安装步骤

####1. 下载 Anaconda
**tensorflow在windows下只支持python 3.5以上、amd64**

Anaconda3-4.2.0-Windows-x86_64.exe
由于国外网站下载极慢，给下百度链接：http://pan.baidu.com/s/1jHNoIwu 密码：uvbg
Anaconda安装过程见下面教程（只需看到Anaconda这一步就行）
[【*Tensorflow*】Windows下基于*Anaconda*的*Tensorflow*环境..._CSDN博客](http://blog.csdn.net/ztf312/article/details/56018891)

###  2.1 安装CUDA（为了GPU）
cuda_8.0.61_windows.exe
链接：http://pan.baidu.com/s/1c2cZPNM 密码：o9x2
下面是安装步骤
[win7 CUDA8.0下tensorflow gpu版环境搭配(亲测）](http://blog.csdn.net/jiugeshao/article/details/76370137)
重新启动计算机。至此，cuda的安装就搞定了。

### 2.2 安装CUDNN（这里只有win10和win7安装包）（为了GPU）
cudnn-8.0-windows7-x64-v6.0.zip
win7链接：http://pan.baidu.com/s/1o8qmH7c 密码：l9zm
wn10链接：http://pan.baidu.com/s/1pLmhiqR 密码：puk1
安装步骤：
http://blog.csdn.net/jiugeshao/article/details/76370137
              [win7 CUDA8.0下tensorflow gpu版环境搭配(亲测）](http://blog.csdn.net/jiugeshao/article/details/76370137)




####3.安装 TensorFlow
目前Google的TensorFlow是增加了Windows版本的支持，以前是只有Linux和MacOs版本。好了，那么我们就按照官方文档来安装吧。

首先在安装上有2个区分，如果**你电脑支持GPU（一般都支持）**，那么你可以安装GPU版本，如果你的电脑不支持GPU，那么安装CPU版本。

先看看GPU版本需要多安装哪些。需要安装下面这2个驱动。

* CPU版本命令输入：(不建议)

`pip3 install --upgrade tensorflow  `

* GPU版本命令输入：（**用此方法安装，运行代码速度快的多**）


`pip3 install --upgrade tensorflow-gpu  `

如下图：
![如图：pip3 install --upgrade tensorflow-gpu ](http://upload-images.jianshu.io/upload_images/4340772-4e14fe375b52efae.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 测试
安装完后shell进入,输入`python`回车
输入`import tensorflow`试试，没报错，就证明可以

![](http://upload-images.jianshu.io/upload_images/4340772-cfe10cbf953edded.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

耶，可以好好玩tensorflow!
---
可参考：
[如何安装*支持GPU*运算的*TensorFlow* 1.0? - 知乎专栏](https://zhuanlan.zhihu.com/p/25340037)
[ubuntu16.04+cuda8.0+cudnn6+tensorflow安装](http://blog.csdn.net/roach_zfq/article/details/78121743)
[Tensorflow常见错误](http://blog.csdn.net/u010417185/article/details/51899364)
[安装tensorflow，那叫一个坑啊](http://www.cnblogs.com/shihuc/p/6593041.html)
[在Windows下直接安装Tensorflow的Windows版本](http://blog.csdn.net/jasonzzj/article/details/53490674)
[【*Tensorflow*】Windows下基于*Anaconda*的*Tensorflow*环境..._CSDN博客](http://blog.csdn.net/ztf312/article/details/56018891)
[Win10下用*Anaconda安装TensorFlow*- CSDN博客](http://blog.csdn.net/u010858605/article/details/64128466)

---
好看的人儿，点个喜欢❤ 你会更好看哦~~
