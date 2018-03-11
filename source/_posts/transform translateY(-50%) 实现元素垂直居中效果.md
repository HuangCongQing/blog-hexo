
---
title: transform: translateY(-50%) 实现元素垂直居中效果
date: 2017-09-01 17:50:33
tags: css
---

>`ransform: translateY(-50%)`,向上移动自身高度的一半，结合`top:50%,`达到垂直居中的效果

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style>
        .center {
            height: 500px;
            background:#888;
        }
        .center p{
            background: #fafafa;
            position: relative;
            top: 50%;
            transform: translateY(-50%);
        }
    </style>
</head>
<body>
    <div class="center">
        <p>
            1、委托代理业务通过客户端发单律师在线报价机制，律师将获得更多案源机会；
            2、客户在线向平台支付律师服务费，并由平台对律师费进行托管；
            3、服务完成或确认线下达成交易后，平台向律师所在律师事务所支付律师费；
            4、律师事务所与律师自行结算律师费。
        </p>
    </div>
</body>
</html>
```
<!-- more -->
效果如下：

![垂直居中](http://upload-images.jianshu.io/upload_images/4340772-fcf240d916c52cc7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

参考：
[transform: translateY(-50%) 实现元素垂直居中效果](http://www.cnblogs.com/wx1993/p/5435254.html)