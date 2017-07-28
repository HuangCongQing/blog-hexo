---
title: HTML5-Canvas之矩阵和多边形的绘制（2）
date: 2016-12-25 17:50:33
tags: [html5, JavaScript]
---



---

上篇文章我们了解了canvas的定义、获取和基础的绘图操作，其中的绘图功能我们讲解了线段绘制、上色、描边等方面知识点。

今天我们来讲讲矩形（Rectangle）和多边形的绘制。

矩形的绘制一共有两个口令，分别是 **ctx.fillRect(x, y, width, height) 和 ctx.strokeRect(x, y, width, height)** ，参数中的 x 和 y 依旧表示需绘制的矩形的起始点坐标（相对canvas原点），width 和 height表示需绘制的矩形宽高。

而 fillRect 表示绘制一个实心矩形，strokeRect 表示绘制一个描边矩形，我们来一个简单的例子：
```
<canvas id="myCanvas" width="200" height="200" style="border:solid 1px #CCC;">
您的浏览器不支持canvas，建议使用最新版的Chrome
</canvas>

<script>
var c = document.getElementById("myCanvas");
var ctx = c.getContext("2d"); //获取该canvas的2D绘图环境对象
ctx.fillRect(10,10,50,50);   //从画布上的(10,10)坐标点为起始点，绘制一个宽高均为50px的实心矩形
ctx.strokeRect(70,10,50,50);   //从画布上的(70,10)坐标点为起始点，绘制一个宽高均为50px的描边矩形
</script>
```
效果如下
![矩形**粗体文本**][1]

----
你也可以使用 `Rect( x, y, width, height )` 的方法创建矩形路径，之后再通过 .stroke() 或 .fill() 方法来给矩形上色：

```
var c = document.getElementById("myCanvas");
var ctx = c.getContext("2d"); //获取该canvas的2D绘图环境对象
ctx.rect(20,20,150,100);  //创建矩形路径
ctx.stroke();    //描边
ctx.beginPath();    //重置画笔，避免污染
ctx.rect(50,90,50,50);  //创建矩形路径
ctx.fill();    //填充
```
效果如下
![rect][2]

----
上方我们绘制了两个默认黑色的实心和描边矩形，相信你也联想到上一章我们绘制线段时，若没有定义strokeStyle，则线段也是默认为黑色的事情。那么我们要给这俩矩形上色，或许你也会联想到应当使用 *Style 来处理，而这想法也是正确的。

在canvas上，给实心对象上色可以用 fillStyle 来定义，给描边对象上色我们可以用 strokeStyle来定义，它们的赋值均为 color|gradient|pattern ，在上章我们已经细说过，这里不再赘述。

那么我们来给上方绘制了的实心矩形填充一个放射状渐变（黄-蓝-红），将描边矩形的描边设为绿色。我们可以这样做：

```
<canvas id="myCanvas" width="200" height="200" style="border:solid 1px #CCC;">
您的浏览器不支持canvas，建议使用最新版的Chrome
</canvas>

<script>
var c = document.getElementById("myCanvas");
var ctx = c.getContext("2d"); //获取该canvas的2D绘图环境对象

var grd = ctx.createRadialGradient(35,35,0,35,35,36);  //定义放射状渐变对象，设定渐变线起始点和结束点坐标，坐标格式为(起始点x,起始点y,结束点x,结束点y)
grd.addColorStop(0,"yellow");   //定义渐变线起点颜色
grd.addColorStop(0.5,"blue");   //定义渐变线中间点的颜色
grd.addColorStop(1,"red");  //定义渐变线结束点的颜色
ctx.fillStyle = grd;   //将放射状渐变对象赋值给fillStyle
ctx.fillRect(10,10,50,50);   //从画布上的(10,10)坐标点为起始点，绘制一个宽高均为50px的实心矩形

ctx.beginPath();  //重置画笔，这是个好习惯
ctx.strokeStyle = "green";   //定义描边颜色为绿色
ctx.strokeRect(70,10,50,50);   //从画布上的(70,10)坐标点为起始点，绘制一个宽高均为50px的描边矩形
</script>
```
效果如下
![此处输入图片的描述][3]

这里要提到的是上一次没有仔细介绍过的放射状渐变方法 `createRadialGradient` ，其语法为

    ctx.createRadialGradient( Xstart, Ystart, Radiusstart, Xend, Yend, Radiusend )

其中前三个参数表示渐变起始圆形的中心坐标和半径，后三个参数表示渐变结束圆形的中点坐标和半径。

或许你会被这里的“半径”迷惑，回顾我们上章学习的createLinearGradient，它的参数并没有“半径”的概念，如果你是一名平面设计师，你更可能觉得放射状渐变只需要起始点和结束点坐标就可以了（毕竟PS/AI中的径向渐变只需要这两个点）。

但canvas在这里加入的“半径”参数还是有一定作用的，可以创造出比PS中径向渐变稍微复杂一些的效果。

⑴ 我们先来一个最简单最好理解的例子：
```
var c = document.getElementById("myCanvas");
var ctx = c.getContext("2d"); //获取该canvas的2D绘图环境对象

var grd = ctx.createRadialGradient(70,70,0,70,70,100);  //定义放射状渐变对象，设定起始圆和结束圆中点重叠，且起始圆半径为0
grd.addColorStop(0,"yellow");   //定义渐变线起点颜色
grd.addColorStop(0.5,"blue");   //定义渐变线中间点的颜色
grd.addColorStop(1,"rgba(255,0,0,0)");  //定义渐变线结束点的颜色，其中颜色透明度为0
ctx.fillStyle = grd;   //将放射状渐变对象赋值给fillStyle
ctx.fillRect(0,0,c.width,c.height);   //绘制一个跟画布大小一样的实心矩形
```
我们设置起始圆和结束圆中点相同，且起始圆半径为0，那么它的渐变线就是从两圆的中点开始到结束圆的边缘结束。我们设置渐变线结束点颜色透明度为0是为了方便查看结束圆的边界。效果如下：
![渐变线][4]

⑵ 我们在⑴的基础上将起始圆的半径设为20，代码和效果图如下：
```
var c = document.getElementById("myCanvas");
var ctx = c.getContext("2d"); //获取该canvas的2D绘图环境对象

var grd = ctx.createRadialGradient(70,70,20,70,70,100);  //定义放射状渐变对象，设定起始圆和结束圆中点重叠，且起始圆半径为20
grd.addColorStop(0,"yellow");   
grd.addColorStop(0.5,"blue");  
grd.addColorStop(1,"rgba(255,0,0,0)");  
ctx.fillStyle = grd;   
ctx.fillRect(0,0,c.width,c.height);  
```
![radial][5]

⑶ 我们在⑵的基础上挪动起始圆的中点，不要让它跟结束圆的中点重叠，代码和效果图如下：

```
var c = document.getElementById("myCanvas");
var ctx = c.getContext("2d"); //获取该canvas的2D绘图环境对象

var grd = ctx.createRadialGradient(60,40,20,70,70,100);  //起始圆不仅有半径，而且中点跟结束圆中点不相同
grd.addColorStop(0,"yellow");   
grd.addColorStop(0.5,"blue");  
grd.addColorStop(1,"rgba(255,0,0,0)");  
ctx.fillStyle = grd;   
ctx.fillRect(0,0,c.width,c.height);  
```
![此处输入图片的描述][6]

注意我们在定义RadialGradient时，要尽量避免起始圆的范围超出结束圆的范围（起始圆最好是结束圆内部的一个真子集），否则绘制出来的效果会出现无法预知的错误，例如下面的代码：
```
var c = document.getElementById("myCanvas");
var ctx = c.getContext("2d"); //获取该canvas的2D绘图环境对象

var grd = ctx.createRadialGradient(60,60,50,70,70,50);  //起始圆的左边超出了结束圆内部区域
grd.addColorStop(0,"yellow");   
grd.addColorStop(0.5,"blue");  
grd.addColorStop(1,"rgba(255,0,0,0)");  
ctx.fillStyle = grd;   
ctx.fillRect(0,0,c.width,c.height);  
```
![此处输入图片的描述][7]

不过如果你掌握了RadialGradient上色原理，倒是可以随意定位起始圆和结束圆的方位和大小。我从TimeLangoliers的博客（[点击查看出处][8]）看到这张原理图：
![此处输入图片的描述][9]
他还依照此原理图写了一个例子：
```
     var canvas = document.getElementById(id);
            if (canvas == null)
            return false;
            var context = canvas.getContext('2d');
            var g1 = context.createRadialGradient(100, 150, 10, 300, 150, 50);
            g1.addColorStop(0.1, 'rgb(255,0,0)');
            g1.addColorStop(0.5, 'rgb(0,255,0)');
            g1.addColorStop(1, 'rgb(0,0,255)');
            context.fillStyle = g1;
            context.fillRect(0, 0, 400, 300);
```

至此我们学习了通过 fillRect 和 strokeRect 来绘制矩形，下面再讲一个Rect相关的功能——clearRect。

clearRect类似PS中的方块橡皮擦，可以擦除画布上任意一块矩形区域的内容，其语法如下：

    ctx.clearRect( x, y, width, height );

其中 x 和 y 表示起始点坐标，width 和 height 表示这块“橡皮擦”的宽高。举个例子：
```
var c = document.getElementById("myCanvas");
var ctx = c.getContext("2d"); //获取该canvas的2D绘图环境对象

ctx.fillStyle = "red";   
ctx.fillRect(0,0,c.width,c.height);  
ctx.beginPath();
ctx.fillStyle = "blue";   
ctx.fillRect(10,20,60,60);  
ctx.clearRect(20,20,80,50);  //擦除以（20,20）坐标为起点，宽高为80*50的区域
```
![此处输入图片的描述][10]


>注意clearRect不会清除掉之前定义过的样式、画笔位置等绘制信息，打个比方，有时候我们需要清空整个画布，我们可以这样做：
```
var c = document.getElementById("myCanvas");
var ctx = c.getContext("2d"); //获取该canvas的2D绘图环境对象

ctx.fillStyle = "blue";   
ctx.fillRect(10,20,60,60);  
//下面重置画布大小，从而清空画布
c.width = c.width;  //在jQ中可以写为 c.attr("width", c.width());  
c.height = c.height;  //在jQ中可以写为 c.attr("height", c.height());  
//重新绘制一个矩形
ctx.fillRect(10,20,60,60);  

```
这个方法是通过重置画布大小，从而触发清空画布事件，但前面定义的 fillStyle="blue" 也被清空掉了，从而绘制了一个黑色的矩形：
![此处输入图片的描述][11]

如果不想清除掉之前定义的样式，我们可以通过clearRect来实现：
```
var c = document.getElementById("myCanvas");
var ctx = c.getContext("2d"); //获取该canvas的2D绘图环境对象

ctx.fillStyle = "blue";   
ctx.fillRect(10,20,60,60);  
//下面通过clearRect来擦除画布
ctx.clearRect(0,0,c.width,c.height);
//重新绘制一个矩形
ctx.fillRect(10,20,60,60);  
```
执行结果如下：
![此处输入图片的描述][12]

----
最后聊一下多边形的绘制，其实现非常简单，先来个例子：
```
var c = document.getElementById("myCanvas");
var ctx = c.getContext("2d"); //获取该canvas的2D绘图环境对象

//定义样式
ctx.fillStyle = "blue";   
ctx.strokeStyle = "red";
ctx.lineWidth = "8";
ctx.lineJoin = "round";

//绘制多边形
ctx.moveTo(10,10);
ctx.lineTo(100,30);
ctx.lineTo(120,80);
ctx.lineTo(60,60);
ctx.lineTo(10,10);

ctx.stroke();  //描边
ctx.fill();    //填充
```
可见我们这里通过lineTo绘制了多边形的每条边（注意起点跟终点是同一个坐标），然后通过 stroke() 来描边、fill() 来填充，其执行效果如下：
![此处输入图片的描述][13]

眼尖的朋友会发现该多边形左上角的俩条描边没有接在一起，这是因为我们没有把这个多边形路径闭合起来，我们可以通过 ctx.closePath() 来解决这个问题：

眼尖的朋友会发现该多边形左上角的俩条描边没有接在一起，这是因为我们没有把这个多边形路径闭合起来，我们可以通过 ctx.closePath() 来解决这个问题：
```
var c = document.getElementById("myCanvas");
var ctx = c.getContext("2d"); //获取该canvas的2D绘图环境对象

//定义样式
ctx.fillStyle = "blue";   
ctx.strokeStyle = "red";
ctx.lineWidth = "8";
ctx.lineJoin = "round";

//绘制多边形
ctx.moveTo(10,10);
ctx.lineTo(100,30);
ctx.lineTo(120,80);
ctx.lineTo(60,60);
ctx.lineTo(10,10);
ctx.closePath();  //闭合多边形路径
ctx.stroke();  //描边
ctx.fill();    //填充
```
![此处输入图片的描述][14]
这次就到这里，下次再见了！、

学习链接

[canvas学习笔记][15]
[HTML5- Canvas入门（二）][16]
[玩转html5画图][17]


  [1]: http://images.cnitblog.com/i/561179/201408/151020443271689.jpg
  [2]: http://images.cnitblog.com/i/561179/201408/211453376748143.jpg
  [3]: http://images.cnitblog.com/i/561179/201408/151103301082183.jpg
  [4]: http://images.cnitblog.com/i/561179/201408/151343581391102.jpg
  [5]: http://images.cnitblog.com/i/561179/201408/151350137176009.jpg
  [6]: http://images.cnitblog.com/i/561179/201408/151353320459899.jpg
  [7]: http://images.cnitblog.com/i/561179/201408/151358364838839.jpg
  [8]: http://www.cnblogs.com/tim-li/archive/2012/08/06/2580252.html
  [9]: http://images.cnitblog.com/i/561179/201408/211100086741182.png
  [10]: http://images.cnitblog.com/i/561179/201408/151532598736138.jpg
  [11]: http://images.cnitblog.com/i/561179/201408/151542360457595.jpg
  [12]: http://images.cnitblog.com/i/561179/201408/151545433421349.jpg
  [13]: http://images.cnitblog.com/i/561179/201408/151555187176162.jpg
  [14]: http://images.cnitblog.com/i/561179/201408/151559585928099.jpg
  [15]: http://www.cnblogs.com/charmingyj/p/5527223.html
  [16]: http://www.cnblogs.com/vajoy/p/3914131.html
  [17]: http://www.cnblogs.com/tim-li/archive/2012/08/06/2580252.html