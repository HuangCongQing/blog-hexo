---
title: 项目常用的less语法详解
date: 2016-12-10 17:50:33
tags: less
---



---

#### 什么是less？
>less是一种动态样式语言，属于css预处理语言的一种，类似于css的语法，为css赋予了动态语言的特性，如**变量、继承，运算，函数**等，更方便css的编写和维护

#### 编译工具
* Koala编译
    * 国人开发的less/sass编译工具、
    * 下载地址： http://koala-app.com/index-zh.html
        * 常用： 输出方式compress(进行压缩)
* Node.js库
* 浏览器端使用
#### Koala配置及使用
1. 新建后缀为.less文件：index.less
头部写上：@charset "utf-8"; 　　//设定字符集

2. 把文件夹拖到koala中，设置输出路径为style下的index.css
使用koala进行编译，然后就生成了一个index.css文件。

3. 之后我们只要编辑index.less文件即可。

#### 项目中常用的语言特性
#### 注释
* less有两种注释
    * `//*会在css中编译出来/*/ `
    * ` //不会在css中编译出来`
第一种的注释会在css中编译出来，第二种不会

#### 变量：
>变量允许我们单独定义一系列通用的样式，然后在需要的时候去调用。所以在做全局样式调整的时候我们可能只需要修改几行代码就可以了。

*  less中声明变量用@开头，例：@变量名：值；
less源码：
```
@margin-left:30px;
box{margin: margin-left;}
```
编译后的css
```
box{margin:30px;}

```

#### 混合模式（Mixins）
>混合可以将一个定义好的class A轻松的引入到另一个class B中，从而简单实现class B继承class A中的所有属性。我们还可以**带参数**地调用，就像使**用函数**一样。

```
//混合
.box{
	width: @text_width;
	height: 100px;
	background: green;
	.border;
}

.border{
	border:solid  1px pink;
}

//混合，可带参数
.border_02(@border_width){
	border:solid yellow @border_width;
}

.test_mix2{
	.border_02(30px); //注意：参数不初始化，括号里必须要有个值，
}
//混合默认带值
.border_03(@border_width:10px){
	border:solid yellow @border_width;
}

.test_mix3{
	.border_03();
}

//混合好例子（适用多个浏览器）

.border_radius(@radius:5px){
	-webkit-border-radius:@radius;
	-moz-border-radius:@radius;
	border-radius:@radius;
}
.radius_test{
	width: 100px;
	height: 100px;
	background: pink;
	.border_radius(30px);
}
```

#### 匹配模式：
>有点像switch或者if 判断
满足哪个条件就用哪一个。 其他的就是混合。
  >> @_ ： ,这个很强大：无论匹配到什么值，均会运行，类似于成全局了（函数名一致）
  
```
.float(left){ float:left; }
//调用匹配模式：那么就是：
 .setFloat{ .float(left); } 
//举个三角例子

//匹配模式(原始)

// .tri_test{  
	// width: 0;
	// height: 0
	// overflow: hidden;

// 	border-width: 150px;
// 	border-color: red transparent transparent transparent;
// 	border-style: solid dashed dashed dashed ;//dashed 虚线
// }

//匹配模式
.triangle(top, @w: 5px, @c:#ccc){        //朝上
	border-width: @w;
	border-color: transparent transparent #ccc transparent;
	border-style: dashed dashed solid dashed ;//dashed 虚线
}
.triangle(bottom, @w: 5px, @c:#ccc){    //朝下
	border-width: @w;
	border-color: @c transparent transparent transparent;
	border-style: solid dashed dashed  dashed ;//dashed 虚线
}
.triangle(left, @w: 5px, @c:#ccc){     //朝左
	border-width: @w;
	border-color: transparent @c transparent transparent;
	border-style: dashed solid dashed dashed ;//dashed 虚线
}
.triangle(right, @w: 5px, @c:#ccc){    //朝右
	border-width: @w;
	border-color: transparent transparent transparent @c ;
	border-style: dashed dashed dashed solid  ;//dashed 虚线
}
.triangle(@_, @w: 5px, @c:#ccc){      //@_   强大：无论匹配到什么值，均会运行这个函数
	width: 0;
	height: 0;
	overflow: hidden;
}
.tri_test{
	
	.triangle(top, 100px);
}

//好例子：：匹配：定位
.pos(r){
	position:relative;
}
.pos(a){
	position:absolute;
}
.pos(f){
	position:fixed;
}

.match{
	width: 100px;
	height: 150px;
	background-color: green;
	.pos(r);
}

```

#### 运算
>任何数字，颜色或者变量都可以参与运算，运算应该包裹在括号里

>>例如+ - *  /

```
@val:300px;
.box{
   width: @val + 20;/*less没有强制要求必须加单位，只要有一个有单位即可*/
   height: (@val - 20) * 5;
   color: #ccc - 10 ;/*less会把颜色转成 255 的数值，然后进行计算，输出颜色值对应的颜色，工作中很少用到*/
```
#### 嵌套规则
>& 代表上一层选择器
* 用处1：
```
a{
     &:hover{}
      }；
```
* 用处2：
```
    .content{
    	&_item1{  }
    	}        //&_item1就相当于。content_item1
```
```
//嵌套例子
/*
.list{}
.list li{}
.list a{}
.list span{}

*/下面所属关系，一层套一层，省去了重复的东西
.list{
	width: 600px;
	margin:30px auto;
	padding: 0;
	list-style: none;
	li{
		height: 30px;
		line-height: 30px;
		background-color: pink;
		margin-bottom: 5px;
	}
	a{
		float: left;
		//& 代表上一层选择器
		&:hover{
			color: red;

		}
	}
	span{
		float: right;
		
	}
}
```

* & 代表他的上一层选择器
```
//& 代表他的上一层选择器
a{
	float: left;
	//& 代表上一层选择器
	&:hover{
		color: red;
		}
	}
```
* &同样代表他的上一层选择器，起连接作用
```
//嵌套小例子
//HTML
<div class="content">
		<div class="content_item1"></div>
		<div class="content_item2"></div>
	</div>

//LESS
.content{
	width: 40px;
	height: 40px;
	background: #ccc;
	&_item1{          //&_item1就相当于。content_item1
		width: 20px;
		height: 20px;
		background: pink;
	}
}

```

* @arguments变量（用的不是很多）懒人必备
> @arguments包含了所有传递进来的参数。
```

 @border（@w：30px，@c：red，@s：solid）{
   border：@w @c @s
}
//如果你不想单独处理每一个参数的话就可以像这样写：
.border_arg(@w:30px,@c:red,@ww:solid){
border:@arguments;//这个@arguments就相当于@w,@c,@s 包含所有参数
}
//调用
.test_arguments{
.border_arg(40px);
}
```
#### 封装


>* 可以把封装的东西放到一个单独的 less里面，只需要在main.less主文件里面 @import 加文件名 xx 可以省略后缀名.
* 加载css需要  @import(less) "xxx.css"换汤不换药   其中“”前面有一个空格 还是css那一套加载方式，放到哪里就在哪里加载，样式表！
```
//引入a.less和a.css例子
@import "a.less";         //引入其他的less样式表,其中.less可写可不写
@import (less) "a.css"  //引入css样式表，注意（less）和“a.css”中间有个空格
```

#### less 也有作用域
```
.content1{
@w:100px;
width:@w;
}
.content2{
width:@w;//错误，这个@w引用不了，因为他在.content1中
}

```

欲知更多，请戳[less-中文官网][7]
可学习视频：[less即学即用-慕课][8]



  [7]: http://www.1024i.com/demo/less/
  [8]: http://www.imooc.com/learn/102