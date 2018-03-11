---
title: windows下mongodb的安装与配置（全）
date: 2017-08-25 17:50:33
tags: mongodb
---

![mongodb](http://upload-images.jianshu.io/upload_images/4340772-efb3b67cc9a34045.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

>由于学Python存数据，需要用到mongodb数据库，自己在网上搜了很多教程，也踩了许多坑，特记录下来，希望能够对一些朋友有用,也记录下自己学的东西。

## 下载与安装
1. 下载地址：[https://www.mongodb.com/download-center#community](https://www.mongodb.com/download-center#community)
2. 下载符合你系统的版本，然后安装。默认安装到`C:\Program Files\MongoDB`
,你也可以自定义安装目录。
我的目录是：·`D:\Program Files\Work\MongoDB\Server\3.4`

## 创建数据目录

MongoDB将数据目录存储在 db 目录下。但是这个数据目录**不会主动创建**，我们在安装完成后需要创建它。

请注意，数据目录应该放在**根目录**下（(如： C:\ 或者 D:\ 等 )。

这里我们新建`mongodb`文件夹在文件夹下新建各种东西
我们假设创建数据目录在`D:\mongodbData\data\db`

## 命令行运行mogondb服务

假设你的mongodb安装在
`D:\Program Files\Work\MongoDB\Server\3.4`
* 打开cmd命令框进入**安装目录**
`D:\Program Files\Work\MongoDB\Server\3.4\bin`

* 启动服务：
`mongod.exe --dbpath D:\mongodbData\data\db`

出现下图数据即算成功
![mongod.exe --dbpath D:\mongodbData\data\db](http://upload-images.jianshu.io/upload_images/4340772-501e44701d615a0e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 将MongoDB服务器作为Windows服务运行

先终止命令行，执行：
```
D:\Program Files\Work\MongoDB\Server\3.4\bin> mongod.exe --logpath "D:\mongodbDa
ta\data\log\mongodb.log" --logappend --dbpath "D:\mongodbData/data/db" --port 27017 --serviceName "MongoDB" --install
```
![D:\Program Files\Work\MongoDB\Server\3.4\bin> mongod.exe --logpath "D:\mongodbDa
ta\data\log\mongodb.log" --logappend --dbpath "D:\mongodbData/data/db" --port 27017 --serviceName "MongoDB" --install](http://upload-images.jianshu.io/upload_images/4340772-3792bfb384bf1f45.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


下表为mongodb启动的参数说明：**自己注意按照自己的路径进行修改**

```
--bind_ip	绑定服务IP，若绑定127.0.0.1，则只能本机访问，不指定默认本地所有IP
--logpath	定MongoDB日志文件，注意是指定文件不是目录
--logappend	使用追加的方式写日志
--dbpath	指定数据库路径
--port	    指定服务端口号，默认端口27017
--serviceName	指定服务名称
--serviceDisplayName	指定服务名称，有多个mongodb服务时执行。
--install	指定作为一个Windows服务安装。

```
终止命令行中的mongodb服务，打开刚才新建的mongodb服务：
`NET START MongoDB`
运行之后如下图
![NET START MongoDB](http://upload-images.jianshu.io/upload_images/4340772-36bec45f50247d71.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

如果出现服务器无法正常启动的问题，是因为mongod.lock这个文件，在服务器异常退出时，该文件会影响下一次启动mongod服务的,我们首先关闭命令行mongodb服务，然后只需要删除该文件就行了：

`mongod.exe --config e:\data\db\mongod.lock --remove`

>windows删除服务命令： sc delete MongoDB


## MongoDB后台管理 Shell

进入安装目录：
```
cd D:\Program Files\Work\MongoDB\Server\3.4\bin`

```
执行`mongo.exe`,如下图
![mongo.exe](http://upload-images.jianshu.io/upload_images/4340772-acbcb771d56f9e3f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


* 启动MongoDB服务
`net start MongoDB`
* 关闭MongoDB服务
`net stop MongoDB`
* 移除MongoDB服务
`D:\Program Files\Work\MongoDB\Server\3.4\bin\mongod.exe  --remove`

最后说一下：
* 由于mongodb数据看不到摸不着，可视化工具是必须的
推荐，推荐一个**MongoDB可视化工具RoboMongo**
[MongoDB可视化工具RoboMongo安装与连接教程](http://www.veryhuo.com/a/view/156974.html)
安装很简单，但是别忘了**配置环境变量**

* 再推荐一个mongodbd的操作教程：
http://wiki.jikexueyuan.com/project/mongodb/

好了接下来就可以好好玩数据了

参考文章：
http://www.jianshu.com/p/4bda3b7a9ea6
http://www.jianshu.com/p/bc088aa972e9
http://www.runoob.com/mongodb/mongodb-window-install.html
