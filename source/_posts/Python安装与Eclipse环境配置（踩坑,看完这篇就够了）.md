
---
title: Python安装与Eclipse环境配置（踩坑,看完这篇就够了）
date: 2017-08-12 17:50:33
tags: python
---


### 安装python（配置环境变量）
http://www.runoob.com/python/python-tutorial.html
### 配置Eclipse（路径）
http://www.runoob.com/python/python-ide.html
### 配置PyDev
* 点击help按钮-->Install New Software

![mark](http://upload-images.jianshu.io/upload_images/4340772-f1554c0413db063c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
Name:取PyDev
Location：http://www.pydev.org/updates
![mark](http://upload-images.jianshu.io/upload_images/4340772-1e188cb6b039d5e1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
进去之后只需选择第一个包，点击next，之后一直点击下一步即可（有任何弹框，选择accept）
![mark](http://upload-images.jianshu.io/upload_images/4340772-ac84019523237109.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
完成，点击Yes重新启动Eclipse
![mark](http://upload-images.jianshu.io/upload_images/4340772-89470378e26cab82.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
<!-- more -->

### 新建python项目流程
点击new Project，会出现Pydev文件夹，选择PyDev Project，点击Next
![mark](http://upload-images.jianshu.io/upload_images/4340772-fddf5233928133c9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![mark](http://upload-images.jianshu.io/upload_images/4340772-a97bc67d839709e0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![mark](http://upload-images.jianshu.io/upload_images/4340772-62a0922c50f3adc7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![mark](http://upload-images.jianshu.io/upload_images/4340772-5db6e45ce76d99d7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
点击OK
![mark](http://upload-images.jianshu.io/upload_images/4340772-5261b186d991bd80.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
点击apply应用
![mark](http://upload-images.jianshu.io/upload_images/4340772-b1e1bbe63cb685d2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
点击next
![mark](http://upload-images.jianshu.io/upload_images/4340772-ee2b49c6b67b264f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
点击finish
![mark](http://upload-images.jianshu.io/upload_images/4340772-66319da28569cccd.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
然后在新建的Project（python35）右击，new一个PyDev Module
![mark](http://upload-images.jianshu.io/upload_images/4340772-8d5892f51b04bfe8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
这样基本就完成了
![mark](http://upload-images.jianshu.io/upload_images/4340772-80028a852af151ec.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
下面写一行代码测试一下
选直接运行就行，目前不需要单元测试
![mark](http://upload-images.jianshu.io/upload_images/4340772-96367501041bfe8e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
运行之后报错
```
Python脚本语法错误：SyntaxError: (unicode error) 'utf8' codec can't decode byte 0xc0 in position 0: invalid start byte  
![mark](http://upload-images.jianshu.io/upload_images/4340772-e7845b15c4257aa3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
```
这是因为编码格式出现问题
具体了解可参考下面这个文章
http://againinput4.blog.163.com/blog/static/1727994912011112224749861/
要加两行代码
```
#!/usr/bin/python  
# -*- coding: UTF-8 -*-
```
![mark](http://upload-images.jianshu.io/upload_images/4340772-4e3566b0a63c3d90.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
有个尴尬的问题：我加上那两行代码，还是出错，删除那两行代码，又可以运行了,可能之前我安装了python27,这次安装了python35，第一次运行没反应过来，哈哈。
![mark](http://upload-images.jianshu.io/upload_images/4340772-8c3c5f5d803b858e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
总结一下：
>python2.X版本需要加下面这两行代码，python3.X则不需要
```
#!/usr/bin/python  
# -*- coding: UTF-8 -*-
```
接下来就可以好好玩Python（蛇）了
