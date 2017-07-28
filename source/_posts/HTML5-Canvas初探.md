---
title: HTML5-Canvas初探（1）
date: 2016-12-18 17:50:33
tags: [html5, JavaScript]
---



---

canvas其实没有那么玄乎，它不外乎是一个H5的标签，跟其它HTML标签如出一辙：
```
<canvas></canvas>
```
canvas 元素用于在网页上绘制图形。

### 那么什么是 Canvas？
>HTML5 的 canvas 元素使用 JavaScript 在网页上绘制图像。
画布是一个矩形区域，您可以控制其每一像素。
canvas 拥有多种绘制路径、矩形、圆形、字符以及添加图像的方法。

* canvas本身没有任何的绘图能力，所有的绘图工作都是通过js来实现的。通常我们在js通过**getElementById**来获取要操作的canvas（这意味着咱得给canvas设个id）：
```
<canvas id="myCanvas"></canvas>

<script>
var c = document.getElementById("myCanvas"); //获取要操作的canvas
//操作canvas的代码...
</script>
```
注意最好在一开始的时候就给canvas设置好其宽高（若不设定宽高，浏览器会默认设置canvas大小为宽300、高100像素），而且不能使用css来设置（会被拉伸），建议直接写于canvas标签内部：

    <canvas id="myCanvas" width="200" height="200"></canvas>

也可以在js脚本中设置：

```
<canvas id="myCanvas"></canvas>

<script>
var c = document.getElementById("myCanvas");
c.width=200;
c.height=200;
</script>
```
### 为什么不能用css来设置呢？
这是因为 canvas 元素有元素本身大小与元素绘图表面大小两套尺寸。 设置 width 和 height 时，实际上是同时修改了该元素本身大小和元素绘图表面大小； 而设置 css，只会改变元素本身大小，并不会改变元素绘图表面大小。

>关于canvas大小需要知道的一点是，后续咱们对canvas所做的全部绘图操作，**超出此大小范围的部分是不可见的**。顾名思义，可以把canvas看成一块画布，其大小是咱设定好的宽高，那么无论你怎么画，画布外的地方自然是画不到的。


对于有些浏览器是不支持canvas功能的，我们可以直接在canvas标签中写一些替换内容，在浏览器不支持canvas时显示：
```
<canvas id="myCanvas" width="200" height="200" style="border:solid 1px #CCC;">
您的浏览器不支持canvas，建议使用最新版的Chrome
</canvas>
```

---
接着在聊如何在canvas上绘图前，咱得先说说.getContext("2d")这东西。
.getContext() 是canvas的绘图对象/方法，要让canvas执行绘图工作必须先获取canvas的.getContext()对象来执行。

.getContext()只接受一个参数，该参数用于获取canvas的绘图环境，例如.getContext("2d")表示该canvas的绘图环境为2D平面（可以绘制文本、直线、弧线、矩形、圆形等）。当前H5只支持2D环境，在不久的将来会开放3D绘图功能。（故咱可将“getContext”翻译为“获取绘图环境”）

接下来：主要是对canvas线段绘制功能的介绍
理论不多说，我们先来个小例子，从最简单的绘制直线开始：

```
<canvas id="myCanvas" width="200" height="200" style="border:solid 1px #CCC;">
您的浏览器不支持canvas，建议使用最新版的Chrome
</canvas>

<script>
var c = document.getElementById("myCanvas");
var ctx = c.getContext("2d"); //获取该canvas的2D绘图环境对象
ctx.moveTo(10,10);   //定义绘画开始的位置
ctx.lineTo(150,50);  //画一条直线，结束点坐标是x=150,y=50
ctx.stroke();  //描边
</script>
```
效果如下：
![一条直线][1]
在这里我们使用了3个getContext("2d")对象的绘图方法：

* .moveTo(x坐标 , y坐标)      可以理解为定位画笔在画布上的位置（注意所有绘图方法所定义的坐标是相对canvas而言的而不是浏览器窗口，对canvas来说，最左上角的点的坐标是(0,0)）

* .lineTo(x坐标 , y坐标)      顾名思义，就是画一条直线到某个点，很好理解。需要知道的是此方法仅仅做路径运动，而不存在任何视觉上的绘图效果（上色、描边）

* .stroke()     描边方法，有玩过AfterEffect的朋友会很清楚，不给运动路径加stroke特效的画是不存在描边效果的，canvas也一样，想要运动路径轨迹能有视觉效果，需要使用相应的上色/描边方法

---
自此我们很轻松地绘制了一条黑色的直线，但如果我们想要绘制一条红色的或者其它颜色的线段，该怎么做呢？

答案很简单，使用ctx.strokeStyle来设定描边的颜色即可。我们画三条红色的线段吧：

```
<canvas id="myCanvas" width="200" height="200" style="border:solid 1px #CCC; margin:30px;">
您的浏览器不支持canvas，建议使用最新版的Chrome
</canvas>

<script>
var c = document.getElementById("myCanvas");
var ctx = c.getContext("2d"); //获取该canvas的2D绘图环境对象
ctx.moveTo(0,0);   //咱把“画笔”移到坐标(0,0)
ctx.line
```
注释都说的很清楚了，故不再赘述实现原理，其效果如下：
![red line][2]
>注意在开始绘制路径的时候，一定要加上moveTo(x,y)，否则第一个lineTo()的运动轨迹将不计入绘图中（浏览器会认为没获取到该运动轨迹的起始点，故忽略此线段）。

---
另外有一个问题，如果上方我们会出来的两条线段（嗯，一条折线，一条直线），我们希望第一条折线是蓝色的，第二条直线是红色的，应当怎么做？

你会很自然地做如下处理：
```
<script>
  var c = document.getElementById("myCanvas");
  var ctx = c.getContext("2d"); 
  ctx.moveTo(0,0);   
  ctx.lineTo(150,50);  
  ctx.lineTo(20,100); 
  ctx.strokeStyle = "blue";    //设定描边颜色为蓝色
  ctx.stroke();  
   
  ctx.moveTo(90,90); 
  ctx.lineTo(80,150);  
  ctx.strokeStyle = "red";    //设定描边颜色为红色
  ctx.stroke();  
</script>
```
但运行脚本会发现，折线除了被描了一遍蓝色，也被描了一遍红色：
![line][3]
这是因为canvas在第二次给路径上色时，是把之前的所有路径轨迹合在一起来上色的，除非咱们让canvas知道那折线和直线应该是独立开来的俩路径。

我们可以使用.beginPath()来解决：

```
<script>
  var c = document.getElementById("myCanvas");
  var ctx = c.getContext("2d"); 
  ctx.moveTo(0,0);   
  ctx.lineTo(150,50);  
  ctx.lineTo(20,100); 
  ctx.strokeStyle = "blue";    //设定描边颜色为蓝色
  ctx.stroke();  
  
  ctx.beginPath();  //告诉canvas咱们要重新绘制一条全新的路径了，之前画的东西从此再无关系
  ctx.moveTo(90,90); 
  ctx.lineTo(80,150);  
  ctx.strokeStyle = "red";    //设定描边颜色为红色
  ctx.stroke();  
</script>
```
>有的朋友一开始会搞不清楚beginPath()的用途，觉得有moveTo()就可以了，其实beginPath()可以做到上述的隔离路径绘制效果的作用，防止之前的效果被污染。

----
接着唠嗑.strokeStyle的赋值方式，咱们上方是直接用了 ctx.strokeStyle="red" 来定义描边颜色为红色，不过ctx.strokeStyle可获值的形式有三种：

    ctx.strokeStyle=color|gradient|pattern;  //即支持 “颜色/渐变/图案笔刷” 的赋值
    
    
1. 先看看color赋值方式，和我们常规的css赋值是一样的，支持[css3颜色值标准][4]，如下例：
```
//下面四种形式都是一样的，表示描边颜色为“橙色”
ctx.strokeStyle = "orange";
ctx.strokeStyle = "#FFA500";    //#rrggbb形式
ctx.strokeStyle = "rgb(255,165,0)";   //RGB形式
ctx.strokeStyle = "rgba(255,165,0,1)";   //比上面的rgb多了个a（Alpha），即透明度
```
2 . 再看下渐变gradient，这个稍有复杂：

```
var c = document.getElementById("myCanvas");
var ctx = c.getContext("2d"); 
ctx.moveTo(0,0);   
ctx.lineTo(150,50); 
ctx.lineTo(20,100); 

var grd = ctx.createLinearGradient(0,0,170,0);  //定义线性渐变对象，设定渐变线起始点和结束点坐标，坐标格式为(起始点x,起始点y,结束点x,结束点y)
grd.addColorStop(0,"black");   //定义渐变线起点颜色
grd.addColorStop(0.5,"red");   //定义渐变线中间点的颜色
grd.addColorStop(1,"yellow");  //定义渐变线结束点的颜色

ctx.strokeStyle = grd;   //将渐变对象赋值给strokeStyle
ctx.stroke();  //描边
```
效果如下：
![line2][5]

这里我们提到了一个概念叫“渐变线”，没有玩过设计的朋友需要了解下渐变的知识点，我们可以把LinearGradient（线性渐变，另有放射状/圆形渐变RadialGradient）范围看成一个矩形（你可以通过Illustator、Photoshop等专业设计软件来辅助你理解这点）：
![line3color][6]
我们一开始定义线性渐变对象的代码 `var grd = ctx.createLinearGradient(0,0,170,0)` 不外乎就是设定了线性渐变线起始点为(0,0)，结束点为(170,0)。

紧接着我们通过 addColorStop( 渐变线位置<0~1>, 颜色 ) 来设定了渐变色值，分别在渐变线0、0.5、1的位置设置了黑色、红色、黄色，其渐变效果如下：
![color2][7]
通过 **`ctx.strokeStyle = grd`** 将渐变赋值给描边方法，最终描边得到了我们想要的渐变效果。

3 . 最后看看pattern描边方式，strokeStyle之所以不叫strokeColor是因为它除了支持颜色描边还支持图案描边（搞设计的朋友或许称作笔触描边会更有feel）。

线性渐变描边需要先createLinerGradient(xstart,ystart,xend,yend)，那么设置图案描边自然也要先新建一个canvasPattern对象：
```
createPattern(image, repetitionStyle)
```
其中参数 image 代表图案对象，一般通过 document.createElement('img') 或者 new Image() ，再定义其src值来创建该对象。
而repetitionStyle参数很好理解，即图案重复形式，其可选值有"repeat" 、"repeat-x"、"repeat-y" 和"no-repeat" （和css的background-repeat可选值一样，不赘述）。

我们这样写
```
<body>
<canvas id="myCanvas" width="200" height="200" style="border:solid 1px #CCC; margin:30px;">
您的浏览器不支持canvas，建议使用最新版的Chrome
</canvas>

<script>
    var c = document.getElementById("myCanvas");
    var ctx = c.getContext("2d"); 

    pic = new Image();   //创建图片对象，或者 pic = document.createElement('img')
    pic.src = "http://images.cnblogs.com/cnblogs_com/vajoy/558870/o_5.jpg";   //定义图片的映射地址
    var redTexture = ctx.createPattern(pic, "repeat");   //定义Pattern对象，设定填充图案为pic图片，填充形式为平铺
    ctx.strokeStyle = redTexture;     //定义描边样式为上一行设定的Pattern描边
    ctx.moveTo(80,10);
    ctx.lineTo(10,90);
    ctx.stroke();
</script>
```
效果如下：
![images][8]
注意这里我还加了个 ctx.lineWidth = 8 来设定线段的粗度。

自此我们学习了strokeStyle的三个赋值方式，也学习了上述的通过 ctx.lineWidth = lineWeight 的形式来给线段设定粗度。

---
咱们再学习两个很简单的线段属性 lineCap 和 lineJoin。

⑴ lineCap是设定线段端点的形状（线帽），其值可以是

>butt    默认，即线条端点为平直的边缘
round   线条端点为圆角线帽
square  为线条端点添加正方形线帽




```
<canvas id="myCanvas" width="250" height="120" style="border:1px solid #DDD;">
</canvas>

<script>
var c=document.getElementById("myCanvas");
var ctx=c.getContext("2d");
ctx.lineWidth=10;

ctx.beginPath();
ctx.lineCap="butt";
ctx.moveTo(20,10);
ctx.lineTo(200,60);
ctx.strokeStyle="red";
ctx.stroke();

ctx.beginPath();
ctx.lineCap="round";
ctx.moveTo(30,90);
ctx.lineTo(200,40);
ctx.strokeStyle="blue";
ctx.stroke();

ctx.beginPath();
ctx.lineCap="square";
ctx.moveTo(10,30);
ctx.lineTo(200,80);
ctx.strokeStyle="green";
ctx.stroke();
</script>
```
 效果如下：
 ![3lin][9]
 光看此图可能看不太出“butt”和"square"的区别，但懂得使用AI绘制矢量的同学们应该比较了解：
![AI][10]


⑵ lineJoin则是设定折线的交接处的外角类型，其值可为：

 
miter    默认，折线交接处为尖角
round   折线交接处为圆角
bevel   折线交接处为斜角
 
```
<canvas id="myCanvas" width="200" height="220" style="border:1px solid #DDD;">
</canvas>

<script>
var c=document.getElementById("myCanvas");
var ctx=c.getContext("2d");

ctx.lineWidth=13;
ctx.lineJoin="bevel";
ctx.moveTo(20,20);
ctx.lineTo(100,50);
ctx.lineTo(20,80);
ctx.strokeStyle="red";
ctx.stroke();

ctx.beginPath();
ctx.lineJoin="round";
ctx.moveTo(20,60);
ctx.lineTo(100,90);
ctx.lineTo(20,150);
ctx.strokeStyle="green";
ctx.stroke();

ctx.beginPath();
ctx.lineJoin="miter";
ctx.moveTo(20,90);
ctx.lineTo(100,150);
ctx.lineTo(20,200);
ctx.strokeStyle="blue";
ctx.stroke();
</script>
```
效果如下
![picture][11]

需要了解的是，miter还受到了属性miterLimit的影响（[点此查看详细][12]），但个人觉得它跟bevel实现的效果是一致的，故在此不做介绍。
这次就到这里了，下次再见了啦！


---
下面推荐一下其他很好的博文
[HTML5- Canvas入门（一）][13]
[玩转html5`<canvas>`画图][14]


  [1]: http://images.cnitblog.com/i/561179/201408/031159061807376.jpg
  [2]: http://images.cnitblog.com/i/561179/201408/031221589157297.jpg
  [3]: http://images.cnitblog.com/i/561179/201408/031526223371748.jpg
  [4]: https://www.w3.org/TR/2003/CR-css3-color-20030514/#numerical
  [5]: http://images.cnitblog.com/i/561179/201408/031244376968316.jpg
  [6]: http://images.cnitblog.com/i/561179/201408/031253445712410.jpg
  [7]: http://images.cnitblog.com/i/561179/201408/031305418375947.jpg
  [8]: http://images.cnitblog.com/i/561179/201408/031517138374311.jpg
  [9]: http://images.cnitblog.com/i/561179/201408/031600162431918.jpg
  [10]: http://images.cnitblog.com/i/561179/201408/031605129308023.jpg
  [11]: http://images.cnitblog.com/i/561179/201408/031620285551919.jpg
  [12]: http://www.w3school.com.cn/tags/canvas_miterlimit.asp
  [13]: http://www.cnblogs.com/vajoy/p/3887608.html
  [14]: http://www.cnblogs.com/tim-li/archive/2012/08/06/2580252.html1