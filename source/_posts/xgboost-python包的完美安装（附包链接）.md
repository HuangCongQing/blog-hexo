---
title: xgboost python包的完美安装（附包链接）
date: 2017-10-27 17:50:33
tags: python
---


* 在http://www.lfd.uci.edu/~gohlke/pythonlibs/#xgboost网站上找到xgboost现成的whl文件

![](http://upload-images.jianshu.io/upload_images/4340772-6f8312b56bff72ec.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
<!-- more -->
* 进入'C:\Users\hasee\AppData\Local\Programs\Python\Python35\Scripts'目录下执行

`pip install "C:\Users\hasee\AppData\Local\Programs\Python\Python35\Scripts"`

**注意：安装包要用英文状态下的双引号括住**

![](http://upload-images.jianshu.io/upload_images/4340772-f5e168e1b09127f5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

好了，这样就成功了！

---
运行`import xgboost`出现警告，不知怎么回事，望见过此错误的能回答一下呀？：
```
 DeprecationWarning: This module was deprecated in version 0.18 in favor of the model_selection module into which all the refactored classes and functions are moved. Also note that the interface of the new CV iterators are different from that of this module. This module will be removed in 0.20.
  "This module will be removed in 0.20.", DeprecationWarning)
```

![](http://upload-images.jianshu.io/upload_images/4340772-adc7cb06467f957f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

---
扩展阅读：
[xgboost入门与实战（原理篇）](http://blog.csdn.net/sb19931201/article/details/52557382)
[python xgboost 运行异常](https://bulvbuting.github.io/2017/02/23/xgboost.html)
[在windows 10环境下安装xgboost](http://blog.csdn.net/u010035907/article/details/70195429?locationNum=15&fps=1)
[python *xgboost* 运行异常 | ZL](https://bulvbuting.github.io/2017/02/23/xgboost.html)

---
好看的人儿，点个喜欢❤ 你会更好看哦~~
