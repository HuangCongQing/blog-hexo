
---
title: Windows环境下msysgit下安装gitflow步骤
date: 2017-08-11 17:50:33
tags: git
---


![gitflow](http://upload-images.jianshu.io/upload_images/4340772-18d99fc9b9ca9dad.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
>在网上，查了好多资料，不过网上说法有好多坑，所有自己特意写了一篇，以便看此博文的人少踩坑！！
#一、Git相关配置（Windows）
##1.安装git和git flow
Windows下git客户端：Git-1.9.2-preview20140411.exe
参考文档，来自github的gitflow的wiki，链接：[https://github.com/nvie/gitflow/wiki/Windows](https://github.com/nvie/gitflow/wiki/Windows)  这里只介绍msysgit环境下的gitflow安装。
首先需要下载两个文件：`getopt.exe`和`libintl3.dll`
下载地址：（可以在浏览器下载就直接下载，如果不行（反正我是不行），复制网址到 迅雷直接下载）
[http://sourceforge.net/projects/gnuwin32/files/util-linux/2.14.1/util-linux-ng-2.14.1-bin.zip/download](http://sourceforge.net/projects/gnuwin32/files/util-linux/2.14.1/util-linux-ng-2.14.1-bin.zip/download)
[http://sourceforge.net/projects/gnuwin32/files/util-linux/2.14.1/util-linux-ng-2.14.1-dep.zip/download](http://sourceforge.net/projects/gnuwin32/files/util-linux/2.14.1/util-linux-ng-2.14.1-dep.zip/download)
<!-- more -->
上面两个链接，分别下载到两个文件：util-[Linux](http://lib.csdn.net/base/linux)-ng-2.14.1-bin.zip和util-[linux](http://lib.csdn.net/base/linux)-ng-2.14.1-dep.zip
我们需要的文件，getopt.exe文件在util-linux-ng-2.14.1-bin.zip文件中的bin目录下，
libintl3.dll也在util-linux-ng-2.14.1-dep.zip文件的bin目录下，将这两个文件
拷贝到msysgit安装目录的bin目录下。


然后打开“[git](http://lib.csdn.net/base/git) Bash”输入下面的命令：
```
$ git clone --recursive git://github.com/nvie/gitflow.git
```
![git clone --recursive git://github.com/nvie/gitflow.git](http://upload-images.jianshu.io/upload_images/4340772-562c68c7d5d2050d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


等下载完毕，打开windows下的命令行工具，进入到刚才下载的文件目录中，例如：如果刚才是在c盘下执行的git clone命令，则进入到F:\Front-End\gitflow目录，然后执行下面命令（可能需要管理员权限）
F:\Front-End\gitflow> contrib\msysgit-install.cmd
如下图：出现`MsysGit installation directory not found `不用管
![F:\Front-End\gitflow> contrib\msysgit-install.cmd](http://upload-images.jianshu.io/upload_images/4340772-54354d6831920395.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

执行完毕，打开“Git Bash”，输入命令 git flow，若安装成功，出现下图界面：
![gitflow](http://upload-images.jianshu.io/upload_images/4340772-c4f84e81127d7dad.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


如果你看到这，恭喜，你完成了，接下来，享受gitflow吧。



----------------------------------------
## 2 clone项目并初始化git flow
```Bash
    git clone https://github.com/Tours4Fun/yiifrontendtff.git
    cd yiifrontendtff
    git flow init
    #一路回车
```
#二、本地开发流程
##1. 切换到develop分支
```Bash
git checkout develop
```
##2. 更新develop分支
```Bash
git pull origin develop
```

##3. 基于develop新建分支
```Bash
git flow feature start proj{项目ID}_{项目简要描述}
        #假设项目2312:
        git flow feature start proj2312_update_sitemap
```
##4. 进行开发
```Bash
git status #提交前最好先查看修改了哪些文
        git add . #添加文件
        git commit -m "update sitemap.xml 注释" #提交日志
```
##5. 完成开发后把分支push到远程:
```Bash
git push origin feature/proj2312_update_sitemap
```
##6. 工单上线后可以定义删除本地无用分支(可选):
```Bash
git branch -d feature/proj2312_update_sitemap
        git branch -D feature/proj2312_update_sitemap #强制删除
```
##7. 常用命令
```Bash
git branch #查看本地分支
        git checkout branch-name #切换分支
        git remote update -p #远程分支拉到本地
        git branch -a | grep 关键字 #搜索分支
        git branch -m #重命名分支名
        git push origin :feature/feature/proj2312_update_sitemap #删除远端分支
```
###8. 更多命令
[更多命令](http://blog.csdn.net/dengsilinming/article/details/8000622)
