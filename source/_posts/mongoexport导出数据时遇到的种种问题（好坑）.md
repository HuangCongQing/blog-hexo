---
title: mongoexport导出数据时遇到的种种问题（好坑）
date: 2017-08-26 17:50:33
tags: mongodb
---

>想导出mongodb数据库里的数据，结果，搞了一天，踩了无数的坑，才终于导出数据，真的，要哭了，赶紧记录下来（说实话，网上有些文章真的随着版本的更新，有些过时了，真的是助我踩坑耶）
我主要讲我踩得坑哈，顺便说下！

首先要开启服务，进入命令框
`NET START MongoDB`
然后进入安装目录（我的安装目录）：`cd D:\Program Files\Work\MongoDB\Server\3.4\bin`，执行
`mongo`

执行以上两步后，就可以输入有用的命令了
导出数据：
`mongoexport -h 127.0.0.1 -u root -p
 12345 -d taobao -c prodect --type=cvs  -o D:\data\prodect_cvs.dat`
不知上述意思的可以参见： [Mongo的导出工具mongoexport介绍](http://www.cnblogs.com/limingluzhu/p/4323146.html)
然后就报错
```
2017-08-26T15:48:30.940+0800    error connecting to db server: server returned e
rror on SASL authentication step: Authentication failed.
```
网上搜了一下，说**--authenticationDatabase admin   这是是必须的，否则会报上述错误：**
解决办法
再添加一串代码： `--authenticationDatabase admin`
但是添加了之后还是报相同的错，又搜了一下,看了下面一篇博文

[mongoDB authentication](http://blog.csdn.net/allen_jinjie/article/details/9235073)

>连接到admin数据库，在admin数据库上创建一个用户，这个用户保存在admin.system.users中，它的权限比在其它数据库中设置的用户权限更大。（当admin.system.users中一个用户都没有时，即使mongod启动时添加了--auth参数，如果没有在admin数据库中添加用户，此时不进行任何认证还是可以做任何操作，直到在admin.system.users中添加了一个用户。）

原来是我没**创建一个用户**，**但大家要注意创建用户的命令版本不同，命令也有可能不同**，我就遇到了这个问题，
![mark](http://upload-images.jianshu.io/upload_images/4340772-89217a2bec8657c5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
mongodb3.X用的方法： [mongoDB add user in v3.0 问题的解决（Property 'addUser' of object admin is not a func）](http://blog.csdn.net/unixpro/article/details/47302855)


我的版本是3.X的，所有我应该执行下面

```
use admin
db.createUser(
   {
     user: "appAdmin",
     pwd: "password",
     roles:
       [
         { role: "readWrite", db: "config" },
         "clusterAdmin"
       ]
   }
)
```
旧点的版本：
```
use admin
db.addUser('appAdmin', 'password') 
```
创建完成之后如下图：

![mark](http://upload-images.jianshu.io/upload_images/4340772-a20c1dedae69628b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


然后又遇到一个问题`csv mode requires a field list　　　　　　　　`
,原因是**第一次没有指明要导出的列，所以只是实现一个空的文件**

```
user@user-xubuntu:/usr/lib/mongodb/bin$ sudo ./mongoexport -d wx_connect -c template --csv -o template_csv.dat  
connected to: 127.0.0.1  
csv mode requires a field list　　　　　　　　　　　　　　　　　　　　　------第一次没有指明要导出的列，所以只是实现一个空的文件  
user@user-xubuntu:/usr/lib/mongodb/bin$ sudo ./mongoexport -d wx_connect -c template --csv -f msgId,templateId,status,toUser -o template_csv_new.dat  
connected to: 127.0.0.1  
exported 28 records　　　　　　　　　　　　　　　　　　　　　　　　　　　------导出成功  

```
所以在末尾再加上`-f 一列的名字`
`mongoexport -h 127.0.0.1 -u root -p
 12345 -d taobao -c prodect --type=cvs  -o D:\data\prodect_cvs.dat  --authenticationDatabase admin -f shop`

参考博客：  [mongoDB的基本操作以及数据的导入导出，备份和恢复](http://blog.csdn.net/a25115/article/details/40862293)
如下图
![mark](http://upload-images.jianshu.io/upload_images/4340772-c9b2aac5e519d019.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)




>哇。终于完成了，有点小激动啊！！
