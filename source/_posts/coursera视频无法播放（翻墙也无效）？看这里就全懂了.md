---
title: coursera视频无法播放（翻墙也无效）？看这里就全懂了
date: 2017-09-17 17:50:33
tags: [技术杂谈, coursera]
---

![Coursera](http://upload-images.jianshu.io/upload_images/4340772-b5cbc22de794143d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

>Coursera是国外的一款非常有名的公开课网站，值得大家一起学习,但有时候要在coursera上看个课程，发现看不了，爬墙各种方法都试了，特意在网上搜集了解决方案，亲测有效，现在特意记录下来，希望能帮到你。好好学习，天天向上。

该方法针对Windows用户(**win7，win8，win10**)，亲测有效。**Mac电脑**的可参考我最后发的链接
<!-- more -->
1. 用管理员权限记事本打开host文件，地址如下: `C:\Windows\System32\drivers\etc`，（以文本格式打开hosts就好）

![hosts](http://upload-images.jianshu.io/upload_images/4340772-35d38c5130f91d51.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

2. 将如下内容复制到文件末尾
```
52.84.246.90    d3c33hcgiwev3.cloudfront.net
52.84.246.252    d3c33hcgiwev3.cloudfront.net
52.84.246.144    d3c33hcgiwev3.cloudfront.net
52.84.246.72    d3c33hcgiwev3.cloudfront.net
52.84.246.106    d3c33hcgiwev3.cloudfront.net
52.84.246.135    d3c33hcgiwev3.cloudfront.net
52.84.246.114    d3c33hcgiwev3.cloudfront.net
52.84.246.90    d3c33hcgiwev3.cloudfront.net
52.84.246.227    d3c33hcgiwev3.cloudfront.net
```
如下图：
![解决DNS污染](http://upload-images.jianshu.io/upload_images/4340772-a389baea939beb8f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

3. 打开cmd命令行，输入如下命令
`ipconfig/flushdns`

![ipconfig/flushdns](http://upload-images.jianshu.io/upload_images/4340772-36fdba9a9a223084.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

4. 刷新页面即可，终于可以看视频啦


![看看看](http://upload-images.jianshu.io/upload_images/4340772-0310da00d6088fa3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

参考链接：
[*coursera 视频*总是缓冲或者*无法观看*,有什么方法解决? - 知乎](http://www.baidu.com/link?url=f9TFhOk7zUavTew3dtbGN0XmdvRtgX6RQAcSG58fWFvWdJb0FjDbEX1pr1PQWGibzLMTrLmodUcwSRqDzAUjt_)
[coursera无法观看视频解决方法](http://blog.csdn.net/sinat_15443203/article/details/71694554)
[Coursera无法观看课程解决方案-百度经验](https://jingyan.baidu.com/article/6f2f55a14059eeb5b93e6cab.html)
[Mac和windows国内coursera官网看不了视频怎么办](http://jingyan.baidu.com/article/e6c8503c5ea596e54f1a18a8.html)**
---
好看的人儿，点个喜欢❤ 你会更好看哦~~
