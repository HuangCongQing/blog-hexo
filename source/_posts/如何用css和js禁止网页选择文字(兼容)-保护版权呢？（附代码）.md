---
title: 如何用css和js禁止网页选择文字(兼容) 保护版权呢？（附代码）
date: 2017-11-14 17:50:33
tags: [html, css]
---


>现在有好多人为了省事直接复制他人的文章，从而损害到别人的利益，那么如何从技术上保护呢？

问： 前端开发css禁止选中文本如何禁止选中文字？？？

禁止选中的方法很简单，有两种方法：JS和CSS两种
<!-- more -->
### js方法（onselectstart="return false;）
直接干货
```
if(document.all){
    document.onselectstart= function(){return false;}; //for ie
}else{
    document.onmousedown= function(){return false;};
    document.onmouseup= function(){return true;};
}
document.onselectstart = new Function('event.returnValue=false;');
 
//劫持开始选择事件和（或）鼠标按下、抬起事件。
```





简单方法，可以直接在标签里添加
`
onselectstart="return false;
`
例子如下：
```
<div onselectstart="return false">  
    adasdasdasdasdasdasdad  
</div>  
```

### css方法（user-select）

**user-select**有两个值：
* none：用户不能选择文本
* text：用户可以选择文本
>需要注意的是：user-select并不是一个W3C的CSS标准属性，浏览器支持的不完整，需要对每种浏览器进行调整
```
body{
-moz-user-select: none; /*火狐*/
-webkit-user-select: none; /*webkit浏览器*/
-ms-user-select: none; /*IE10*/
-khtml-user-select: none; /*早期浏览器*/
user-select: none;
}
IE6-9还没发现相关的CSS属性
//IE6-9
document.body.onselectstart = document.body.ondrag = function(){
return false;
}
```
[附GitHub代码](https://github.com/HuangCongQing/useful-Demo/blob/master/%E7%A6%81%E6%AD%A2%E7%BD%91%E9%A1%B5%E9%80%89%E6%8B%A9%E6%96%87%E5%AD%97.html)

---
好看的人儿，点个喜欢❤ 你会更好看哦~~
