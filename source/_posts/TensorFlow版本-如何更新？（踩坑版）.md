---
title: TensorFlow版本-如何更新？（踩坑版）
date: 2017-10-25 17:50:33
tags: TensorFlow
---


2017/10/26,我的tensorflow是从0.12版本升级到最新版本（1.3）的，基于python3.5的


### 升级
升级很简单（在这里感谢一下为简化 TensorFlow 安装过程的工程师们），就是一行语句，这也是安装命令：
对于 GPU 版本：
`pip3 install --upgrade tensorflow-gpu`

对于 CPU 版本：
`pip3 install --upgrade tensorflow`
![版本更新前](http://upload-images.jianshu.io/upload_images/4340772-85596acfd641e49f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
<!-- more -->
![版本更新后](http://upload-images.jianshu.io/upload_images/4340772-ca31f64b6f27bf22.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


### 可能踩得坑！！

说到命令行，大家可能习惯性的就敲个cmd进去了。但是如果就这么简单的输入命令开始安装，会发现整个下载过程非常顺利，但是到了安装步骤的时候就出现异常了。

![image.png](http://upload-images.jianshu.io/upload_images/4340772-4c55433be4520df4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


**最关键的错误在最后两行：PermissionError: [WinError 5] 拒绝访问。 涉及到权限问题了。 **

暗红色的报错信息洋洋洒洒一整屏，最后还有一个换色的提示，说pip已经有9了建议升级，看到这个可能会被带到另外一个沟里，以为是pip版本太低导致的。实际上最关键的错误在最后两行：PermissionError: [WinError 5] 拒绝访问。 涉及到权限问题了。 
我们知道win7开始有严格的用户账户控制，大部分安装程序在安装的时候都会跳出对话框让你授权。这给系统安全带来了好处，但是也会带来一些莫名其妙的问题（之前写过一篇关于win7下装oracle10g，其中一个坑也是用户账户控制带来的）。出现这种情况一般两种情况：1、降低用户账户控制级别 2、用更高的权限来运行程序。我个人反对前者，**建议从开始菜单中找到Windows PowerShell，然后从右击菜单中选择以管理员身份运行**。


![打开power shell](http://upload-images.jianshu.io/upload_images/4340772-6105b576a50120a4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


![](http://upload-images.jianshu.io/upload_images/4340772-237e5b58eb81d3cf.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

好了，终于可以啦！！如果遇到其他问题，欢迎大家提问！

---
参考：
[【TensorFlow | 升级】TensorFlow 1.0 发布](http://blog.csdn.net/u010099080/article/details/55260055)
[Tensorflow升级1.0版本](http://blog.csdn.net/u010682375/article/details/72587962)
[win10安装TensorFlow填坑笔记](http://blog.csdn.net/chewinggum/article/details/70373098)
---
好看的人儿，点个喜欢❤ 你会更好看哦~~
