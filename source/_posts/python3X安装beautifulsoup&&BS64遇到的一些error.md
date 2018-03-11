---
title: python3X安装beautifulsoup&&BS64遇到的一些error
date: 2017-08-19 17:50:33
tags: python
---

![beautifulsoup&&BS64](https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1503121701573&di=6299ff4b6aefe2b11141cae630eb6da1&imgtype=0&src=http%3A%2F%2Fimage.lxway.com%2Fupload%2Fa%2F1b%2Fa1bc79d237bf05535330b1af1dc28afc_thumb.jpg)
[用beautifulsoup写的没错的小爬虫地址：](https://github.com/HuangCongQing/python-NLP/blob/master/%E7%BD%91%E7%BB%9C%E6%95%B0%E6%8D%AE%E7%88%AC%E5%8F%96.py)
![](http://upload-images.jianshu.io/upload_images/4340772-4cd3cf67dceb2a50.gif?imageMogr2/auto-orient/strip)
>前言: Beautiful Soup 3 目前已经停止开发，推荐在现在的项目中使用Beautiful Soup 4，不过它已经被移植到BS4了，也就是说导入时我们需要 import bs4 。所以这里我们用的版本是 Beautiful Soup 4.3.2 (简称BS4)，另外据说 BS4 对 Python3 的支持不够好，虽然我用的Python35，如果有小伙伴用的是 Python3 版本，可以考虑下载 BS3 版本。
 >自己搞网页数据爬取时，需要 `from bs4 import BeautifulSoup`,所以在py程序运行中遇到了一系列错误.......
<!-- more -->

## 错误一：`ImportError: No module named 'bs4'`

错误如下：

![ImportError: No module named 'bs4](http://upload-images.jianshu.io/upload_images/4340772-b364e751ce6cbd53.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

* 解决方法如下

Python如何安装模块：

1.下载BS4模块：

http://www.crummy.com/software/BeautifulSoup/bs4/download/4.3/beautifulsoup4-4.3.2.tar.gz

2.解压到Python安装目录下的根目录中：
![根目录](http://upload-images.jianshu.io/upload_images/4340772-7210e5b25ea26561.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

3.运行cmd，进入解压缩后的目录（如果Python默认安装在C盘下，打开cmd之后可以使用cd ...语句先返回根目录，再进入Python27\beautifulsoup4-4.3.2）
![mark](http://upload-images.jianshu.io/upload_images/4340772-40d18bbfcd7bffb1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
4.进入Python27\beautifulsoup4-4.3.2之后安装BS4模块：
执行：`python setup.py install`

![python setup.py install](http://upload-images.jianshu.io/upload_images/4340772-ebac366f3a3386b7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

可参考链接：http://www.cnblogs.com/victor5230/p/6397449.html

----
然而又出现错误：
## 错误二： `ImportError: cannot import name 'HTMLParseError'`


解决bs4在Python 3.5下出现“ImportError: cannot import name 'HTMLParseError'”错误

* 解决方法如下：
直接在cmd命令框中执行`pip --upgrade beautifulsoup4`

![pip --upgrade beautifulsoup4](http://upload-images.jianshu.io/upload_images/4340772-5f48c2ff74be1dcd.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

可参考链接：http://blog.csdn.net/sinat_26599509/article/details/50609646

----
## 错误三：`bs4.FeatureNotFound`
又出现错误:如下
  `bs4.FeatureNotFound: Couldn't find a tree builder with the features you requested: lxml. Do you need to install a parser library?`
![bs4.FeatureNotFound](http://upload-images.jianshu.io/upload_images/4340772-0824f13ed3aa237d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

* 解决方法：
首先安装'pip install wheel'
https://www.zhihu.com/question/49221958/answer/115712155
![pip install wheel](http://upload-images.jianshu.io/upload_images/4340772-c64102d6ece6724a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)




安装`pip install lxml`
![pip install lxml](http://upload-images.jianshu.io/upload_images/4340772-e7ada87d9ee63707.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
可参考链接1：https://www.zhihu.com/question/49221958/answer/115712155
可参考链接2：http://study.163.com/forum/detail/1002230039.htm

竟然就好了！！！！！！！
