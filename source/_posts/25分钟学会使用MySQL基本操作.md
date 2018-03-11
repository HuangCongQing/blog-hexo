---
title: 25分钟学会使用MySQL基本操作
date: 2017-09-17 17:50:33
tags: MySQL
---


###1 MySQL登录与退出
* MySQL登陆
`MySQL 参数`(在cmd命令框中输入)

* 登陆MySql
`mysql -uroot -p -P3306 -h127.0.0.1 `

![mysql -uroot -p -P3306 -h127.0.0.1](http://upload-images.jianshu.io/upload_images/4340772-7c1ec9cb6fcb9921.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
<!-- more -->
![mysql 参数](http://upload-images.jianshu.io/upload_images/4340772-6b56090b52efc767.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

* MySql退出
![退出](http://upload-images.jianshu.io/upload_images/4340772-5a2dd466d42f95ee.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
* MySQL修改root密码

[MySQL修改root密码链接
](http://www.jb51.net/article/39454.htm)

### 2  修改MySQL提示符及语法规范
先说一个小技巧，cmd命令框清屏用`cls`

![cls清屏](http://upload-images.jianshu.io/upload_images/4340772-ea34478e4f1030e5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

首先说一下神魔是MySql提示符？看下面图就懂了

![MySQL提示符](http://upload-images.jianshu.io/upload_images/4340772-fa496e99df25a6a2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



![修改MySql提示符](http://upload-images.jianshu.io/upload_images/4340772-13cf08b40ca40733.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
* 连接客户端即登录时通过参数指定
`mysql -uroot -proot --prompt 提示符`

![mysql -uroot -p -P3306 -h127.0.0.1 --prompt 提示符](http://upload-images.jianshu.io/upload_images/4340772-86199cda8dac41ab.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


 * 连接上客户端后，通过prompt命令修改
`prompt  提示符`

![prompt](http://upload-images.jianshu.io/upload_images/4340772-577a3f68f16f5150.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

下面是MySql具体可更更改的操作

![\D\d\h\u](http://upload-images.jianshu.io/upload_images/4340772-64b55a857963e5c2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
`PROMPT \u@\h \d`  修改为用户名@主机名 数据库名称

![](http://upload-images.jianshu.io/upload_images/4340772-798f09b8a1438de4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 3 MySQL常用命令


![常用命令](http://upload-images.jianshu.io/upload_images/4340772-936a9fabf9a0af5b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![实例](http://upload-images.jianshu.io/upload_images/4340772-bc08f795b85880b6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 4 MySQL语句规范

![语句规范](http://upload-images.jianshu.io/upload_images/4340772-c25a2befce1ae7dc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
特别注意分号，因为不加分号，这段语句不执行，如下图

![;](http://upload-images.jianshu.io/upload_images/4340772-e9ab52531a4419b2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 5 数据库操作
{}必选项，[]可选项

![image.png](http://upload-images.jianshu.io/upload_images/4340772-59cae233ede058c7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


![CREATE DATABASE 数据库名](http://upload-images.jianshu.io/upload_images/4340772-e1ca842ee156e56f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

数据库怎么看呢？
当前服务器下到底有多少数据库(正确安装之后，默认有四个数据库)
`show DATABASES`
![Database lists](http://upload-images.jianshu.io/upload_images/4340772-56c467cc0a19e478.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![show DATABASES](http://upload-images.jianshu.io/upload_images/4340772-4d2fda01dbf809ac.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

* 创建数据库编码方式是什么？不加，默认是配置文件设置的编码方式


![utf8](http://upload-images.jianshu.io/upload_images/4340772-c8a8ebaca6a6c4d3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
* 如果想创建一个GBK的编码方式的数据库怎么来？
`CREATE DATABASE IF NOT EXISTS Hello2 CHARACTER SET gbk`
![](http://upload-images.jianshu.io/upload_images/4340772-01ba35bd92c4e8df.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



* 修改数据库
  * 修改编码方式
`ALTER DATABASE Hello2 CHARACTER  SET utf8`

![](http://upload-images.jianshu.io/upload_images/4340772-8c9da553a5117bca.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


![](http://upload-images.jianshu.io/upload_images/4340772-7933a1ab59c861d8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

* 删除数据库
DROP DATABASE 数据库名


![drop DATABASE](http://upload-images.jianshu.io/upload_images/4340772-987b749ee414e464.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

基本操作就这样了！
回顾下重点：
![重点](http://upload-images.jianshu.io/upload_images/4340772-71ef9c3830a0f69f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
对了，还要说下，写SQL每句语句的后面，一定要加**分号 ;**哦！！
---
* 可参考的常用命令链接：

[MYSQL常用命令](http://www.cnblogs.com/hateislove214/archive/2010/11/05/1869889.html)
[*Mysql命令*大全 - 宁静.致远 - 博客园](https://www.baidu.com/link?url=OasvgcmO7JPV5_IhO4prskNhbV7VpGAggdekFmJdt95uBgezFkZcocFE3x5tK4xdL8-WjXhp9qBvsWoivigkLGPF_hgwGkBB5B4U1fIhVcW&wd=&eqid=a07b6514000420a70000000559bdc633)
