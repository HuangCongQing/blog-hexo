---
title: TensorFlow版本更新后运行代码所遇到的error（持续更新）
date: 2017-10-25 17:50:33
tags: TensorFlow
---


本博客会**持续更新**，如果遇到新的问题，欢迎大家提问，大家一起进步！
##  AttributeError: module 'tensorflow' has no attribute 'mul'

![image.png](http://upload-images.jianshu.io/upload_images/4340772-1c99e17cc1b70071.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
<!-- more -->
* 原因：TensorFlow 发布的新版本的 API 修改了
**tf.mul, tf.sub and tf.neg are deprecated in favor of tf.multiply, tf.subtract and tf.negative.**
* 解决方法：使用时将 tf.mul 改成 tf.multiply 即可
其余的 tf.sub 和 tf.neg 也要相应修改为 tf.subtract 和 tf.negative。
---

相關學習：
[Tensorflow 1.3版本更新概览](http://www.infoq.com/cn/news/2017/08/changes-tensorflow-1-3)
[windows tensorflow 版本与升级](http://blog.csdn.net/lanchunhui/article/details/72892258)
---
好看的人儿，点个喜欢❤ 你会更好看哦~~
