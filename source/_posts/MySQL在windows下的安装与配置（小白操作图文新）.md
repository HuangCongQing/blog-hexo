---
title: HTML5-Canvas之矩阵和多边形的绘制（2）
date: 2016-12-25 17:50:33
tags: [html5, JavaScript]
---

![MySWQL](http://upload-images.jianshu.io/upload_images/4340772-f5c160b5d4379261.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


### MySQL安装

官网版本：   https://dev.mysql.com/downloads/mysql/5.6.html#downloads

有msi和zip两种下载形式，**推荐下载msi这种形式**，安装简单
我下载的是[mysql-5.5.44-winx64.msi](https://dev.mysql.com/downloads/file/?id=457403)

* 如下图，自己可随意选择对应版本
![MySQL下载](http://upload-images.jianshu.io/upload_images/4340772-c90622057d64e8cd.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![点击下载](http://upload-images.jianshu.io/upload_images/4340772-907d0e08078d6e1e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


安装过程注意几点：
* 安装类型选择Typical-典型安装

![Typicle安装](http://upload-images.jianshu.io/upload_images/4340772-5a7a3eb916e46eae.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

* 安装最后，会有个复选框，询问是否进行MySQL配置操作，可以先不配置，因为等额下我们自己可以进行额外的配置。结果和它是一样的，只需单击finish按钮，如下图
![无需勾选](http://upload-images.jianshu.io/upload_images/4340772-807057d7af4e9055.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### MySQL配置
接下来，我们就要进行配置，那么我们要到那个地方进行配置呢？
* 首先，我们要找到，配置向导文件，然后点击进入
一般情况下，典型安装都是讲文件安装在`C:\Program Files\MySQL\MySQL Server 5.5\bin`，


![配置向导文件](http://upload-images.jianshu.io/upload_images/4340772-808a183b9b4493ec.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

* 选择配置类型
详细配置对于初学者配置特别多，难以掌握，最好选择标准配置，点击Next按钮

![标准配置.png](http://upload-images.jianshu.io/upload_images/4340772-e473b48abcc3f915.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

* 是否安装windows服务
之后询问是否安装windows服务和配置环境变量，一般情况下是都要勾选的
![windows服务.png](http://upload-images.jianshu.io/upload_images/4340772-582fc321e14f7492.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

* 设置root用户和密码

![密码](http://upload-images.jianshu.io/upload_images/4340772-55f3fcddd4afff54.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

* 准备执行设置选项
觉得哪一步需要修改，可以back回去修改，各方面确认好之后，就可以点击Execute按钮

![Execute](http://upload-images.jianshu.io/upload_images/4340772-a171b6c9604093cc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

* 配置完成

![配置完成](http://upload-images.jianshu.io/upload_images/4340772-5e96284852b18828.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

上图中，第二个选项Write configuration file，写入配置文件，存储在安装目录下my.ini
第三个选项，Start Service，当前启动你的服务，因为刚才已经设置为windows的一个服务

* 下面验证一下
  * 配置文件my.ini存不存在,
  * windows服务中是否存在MySQL的一个服务

右键点击“我的电脑”，在弹出的快捷菜单中选择“管理”，打开“计算机管理”

![我的电脑右击.png](http://upload-images.jianshu.io/upload_images/4340772-c1598d76d4ca5a3c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


![找到服务](http://upload-images.jianshu.io/upload_images/4340772-5a0996627976fda6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
可以看到MySQL服务已启动
![查看MySQL](http://upload-images.jianshu.io/upload_images/4340772-546bded12e9547d6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

>到此为止，我们已经完成了最简单的配置,如果要进行其他的配置，我们就需要了解MySQL目录结构了， 

下图就很好地表示各目录的功能：

![目录结构](http://upload-images.jianshu.io/upload_images/4340772-de94f6c56f841e3e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


除了通过配置向导的图形化界面来配置，我们还可以来**修改配置文件来实现**

标准配置当中没有的编码方式
配置文件在哪呢？
* 就是我们刚才提到的bin文件夹下的`my.ini`

![my.ini](http://upload-images.jianshu.io/upload_images/4340772-62dc4f9eccdcee9d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


在my.ini文件中，我们发现有几个选项比较重要：
* client--指的MySQL客户端
* port--指的MySQL的端口号（默认3306）
* default-character-set默认编码方式（默认的是latin1，**要修改为utf8，不是utf-8哈**）
* mysqld主要是进行MySQL服务器端的配置


![相关配置](http://upload-images.jianshu.io/upload_images/4340772-59e5404a6e22b332.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


**注意修改了MLSQL的配置，要进行重新启动才行**

### 启动关闭MySQL服务  
* 运行cmd，输入`net  stop mysql`(其实在服务列表中，所有的服务都可以通过`net stop XX`来停止)
* 运行cmd，输入`net  start mysql`(其实在服务列表中，所有的服务都可以通过`net start XX`来启动)
如下图

![服务启动与停止](http://upload-images.jianshu.io/upload_images/4340772-880d2d2c733453a3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

关于cmd界面无法启动mysql：

1. 必须要使用管理员身份运行cmd程序

2. 如果下载MySQL5.7版本的，在windows服务上Mysql的名字默认是MySQL57，因此在cmd运行 net start/stop mysql 是无效的，必须改成 net start/stop mysql57才行

或者

在dos下运行net  start mysql 不能启动mysql！提示发生系统错误 5；拒绝访问！切换到管理员模式就可以启动了。所以我们要以管理员身份来运行cmd程序来启动mysql。

那么如何用管理员身份来运行cmd程序呢？

1.在开始菜单的搜索框张收入cmd，然后右键单击，并选择以管理员身份运行！

如果每天都要启动mysql服务，这样不很麻烦？所以：

2.右键单击cmd选择“附到【开始】菜单(U)”;这是就可以到开始菜单上找到cmd了，

3.右击选择属性，选择快捷方式，选择高级，选择以管理员身份运行，单击确定

这样再输入net start mysql就不会出错了！




这样修改配置就成功了
