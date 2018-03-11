---
title: Git 多分支管理亲手操作一波
date: 2018-01-21 17:50:33
tags: 域名
---

文 | 阿小庆  2018-01-21❤
![2018-01-21](http://upload-images.jianshu.io/upload_images/4340772-9fd73f39e9bd784a.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

快过年了，是时候对以前的知识总结一波了！

先问大家一个问题：
问：如果一个人想**针对项目不同阶段都有个备份**，在一台电脑上多分支管理一个项目，应该怎么搞呢？
答：我给你用电脑操作一下吧，哈哈，下面带大家实际操作一波。
<!-- more -->
1.   首先我建立一个仓库，clone到本地，建立了`README.md  主分支master.txt`
![](http://upload-images.jianshu.io/upload_images/4340772-57ab0ee0856fe943.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![](http://upload-images.jianshu.io/upload_images/4340772-09d55e06ba07e340.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

* 新建branch1分支，并切换到branch1分支（`git branch` 可以查看所有分支）
`git branch 分支名`
`git checkout 想要切换的分支名`
![](http://upload-images.jianshu.io/upload_images/4340772-3764314fa110f952.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


2.  新建次分支branch1.txt并提交
在此分支下提交可能会报错，报错后再执行下一句就可以
`git push -u origin dev`
表示本地分支将**建立对远程仓库目标分支的检测**，如果远程仓库**目标分支**不存在，将新建分支再push；如果存在，将进行push更新。
具体解决方法见下link:
[ git：fatal the current branch master has no upstream branch](http://blog.csdn.net/qqb123456/article/details/25319659)

3.  提交成功后 ，在github上查看，就能看到新建的branch1分支提交了`次分支branch1.txt`
![](http://upload-images.jianshu.io/upload_images/4340772-775ac31c872fe32e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](http://upload-images.jianshu.io/upload_images/4340772-c8b59f1808524d81.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
* 而主分支master内容没变
![](http://upload-images.jianshu.io/upload_images/4340772-18bb371d745e1335.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

好，这样就大功告成了，如果自己一个人开发，为了不容易乱，**我是把不同的分支放在不同的文件夹下**，如下图，当然，你也可以用你自己的方法
![](http://upload-images.jianshu.io/upload_images/4340772-56e3e2ff37437364.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
我把代码放在Github上了，供大家参考
https://github.com/HuangCongQing/branch

---

好看的人儿，点个喜欢❤ 你会更好看哦~~
