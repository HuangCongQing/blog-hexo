---
title: python35下的NLTK工具的安装和配置
date: 2017-08-17 17:50:33
tags: python
---

>首先要说明的是我的安装环境是win7 64位，安装了python35


* 官网下载NLTK
https://pypi.python.org/pypi/nltk
我安装的是nltk-3.2.4.tar.gz
安装上述软件，我的安装目录是
D:\Program Files\Computer-learning
解压缩nltk-3.2.4.tar.gz，在 **cmd** 中进入到`D:\Program Files\Computer-learning\nltk-3.2.4`目录，执行
* ` python setup.py install`

![python setup.py install](http://upload-images.jianshu.io/upload_images/4340772-8ba2cc3afcd51f17.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
<!-- more -->
成功标志：
```
Installed c:\users\hasee\appdata\local\programs\python\python35\lib\site-package
s\six-1.10.0-py3.5.egg
Finished processing dependencies for nltk==3.2.4
```

安装完成后，在IDLE中运行：执行下面两行

```
import nltk
nltk.download()
```
出现一个NLTK Downloader对话框，修改Download Diretory（E盘或其他盘符下），我放在了C:\Users\hasee\AppData\Roaming\nltk_data。点击`all`开始下载，如下
![mark](http://upload-images.jianshu.io/upload_images/4340772-add2072ff4e4636b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

下载完成后
![mark](http://upload-images.jianshu.io/upload_images/4340772-d53a863c565b0757.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

下载慢还可以到**NLTK Corpora** [http://nltk.org/nltk_data/](http://nltk.org/nltk_data/)手工下载缺失的，然后放到Download Diretory，zip别删。重装系统后nltk_data文件夹可以保留，避免重复下载。
