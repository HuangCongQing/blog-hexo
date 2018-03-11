---
title: AngularJS浅谈-博客
date: 2016-11-28 17:50:33
tags: AngularJs
---


---


![AngularJs图片][1]
### AngularJS是啥？（一脸懵逼）

#### 简介：
>AngularJS诞生于2009年，由Misko Hevery 等人创建，后为Google所收购。是一款优秀的前端JS框架，已经被用于Google的多款产品当中。AngularJS有着诸多特性，最为核心的是：**MVC、模块化、自动化双向数据绑定、语义化标签、依赖注入**等等。
#### 具体点说：
1. AngularJS 是一个 JavaScript 框架
    * AngularJS 是以一个 JavaScript 文件形式发布的，**可通过 script 标签**添加到网页中： 
 `<script src="../libs/angular.js/1.4.6/angular.min.js"></script>`
 2. AngularJS 扩展了 HTML
>>AngularJS 通过 ng-directives 扩展了 HTML。
**ng-app** 指令定义一个 AngularJS 应用程序。
**ng-model** 指令把元素值（比如输入域的值）绑定到应用程序。
**ng-bind** 指令把应用程序数据绑定到 HTML 视图。
**ng-init** 指令初始化 AngularJS 应用程序变量

#### 那么，重点来了，AngularJs可以干啥啊？
AngularJS 使得开发现代的**单一页面应用程序**（SPAs：Single Page Applications）变得更加容易。

>>AngularJS 把应用程序数据绑定到 HTML 元素。
AngularJS 可以克隆和重复 HTML 元素。
AngularJS 可以隐藏和显示 HTML 元素。
AngularJS 可以在 HTML 元素"背后"添加代码。
AngularJS 支持输入验证。
<!-- more -->
* 举个荔枝（例子）吧！
```
<<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>例子</title>
	<script src="angular-1.0.1.min.js"></script>

</head>
<body>
<div ng-app="myApp" ng-controller="myCtrl">
	名：<input type="text" ng-model="lastName"><br>
	姓：<input type="text" ng-model="firstName"><br>
	<br>
	姓名：{{firstName+" "+ lastName}}
	<br>
	姓名：{{fullName()}}
</div>

<script>
	var app=angular.module('myApp',[]);
	app.controller('myCtrl',function($scope){
		$scope.firstName="重庆";
		$scope.lastName="黄";
		$scope.fullName = function() {
        return $scope.firstName + " " + $scope.lastName;
    }

	});
</script>	
</body>
</html>
```
 * 初始化加载流程
    * 统一过程： 
>1、浏览器载入HTML，然后把它解析成DOM。
2、浏览器载入angular.js脚本。
3、AngularJS等到DOMContentLoaded事件触发。
4、AngularJS寻找ng-app指令，这个指令指示了应用的边界。
5、使用ng-app中指定的模块来配置注入器(\$injector)。
6、注入器($injector)是用来创建“编译服务(\$compile service)”和“根作用域(\$rootScope)”的。
7、编译服务(\$compile service)是用来编译DOM并把它链接到根作用域(\$rootScope)的。

    * 具体过程：
>AngularJS 应用程序由 ng-app 定义。应用程序在 <div> 内运行。
ng-controller="myCtrl" 属性是一个 AngularJS 指令。用于定义一个控制器。
myCtrl 函数是一个 JavaScript 函数。
AngularJS 使用$scope 对象来调用控制器。
在 AngularJS 中， $scope 是一个应用象(属于应用变量和函数)。
控制器的 $scope （相当于作用域、控制范围）用来保存AngularJS Model(模型)的对象。
控制器在作用域中创建了两个属性 (firstName 和 lastName)。
ng-model 指令绑定输入域到控制器的属性（firstName 和 lastName）。
    * **记住一点：**在大型的应用程序中，通常是把控制器存储在外部文件中。
只需要把 `<script>` 标签中的代码复制到名为 `js文件.js` 的外部文件中即可，然后在script中引用js文件：

### 接下来说一下AngularJs中核心的集中特性吧！！
* 先来个图！
![mark](http://ojmcn9nlw.qnssl.com/blog/20170112/160712894.png)
>MVC
模块化
自动化双向数据绑定

#### MVC（Model模型 View视图 Controller控制器）
>首先要知道为什么要MVC？
![MVC][2]


* AngularJs程序分为3部分：模板，表现层逻辑，数据（model）。

     >模板：我们用html，css写的ui视图代码，其中包含AngularJs的指令，表达式，并最终会被AngularJs编译机制编译为附加在dom树上。AngularJs的指令（directive）可以由我们自由扩展。

    >表现层逻辑：包括应用程序逻辑和行为。用javascript定义作为视图控制器逻辑。在AngularJs作为MVC框架，在控制器中我们无需添加对于dom级的事件监听，这些在AngularJs中已经内置了。在ui节点dom事件发生后AngularJs会自动转到scope上的某个行为（Action）逻辑。

    > 数据：视图对象（viewobject）需要被AngularJs Scope（1.0中作为service出现）引用，可以使任何类型的javascript对象，数组，基本类型，对象。并且AngularJs会自动异步更新模型，即在ui发生改变的时他会自动刷新模型（mode），反之在模型发生改变的时候也会自动刷新ui。在这里我们不需要定义形如getter，setter的一些列方法。
    
* MVC之间的关系，下面这张图看一下MVC中都包含些什么东西
![MVC][3]
* 再看下面这张图-其中**service是共用的的东西抽象出来的服务**
![此处输入图片的描述][4]

#### 模块化
* AngularJs的模块（module):它是一个集合，相当于一个框子，由模型，视图，过滤器，服务等等组成
* 我们都知道JavaScript很容易就写出全局函数，所以无论是用jQuery还是纯JavaScript，我们都会使用模块化的策略避免写出来的函数污染全局。




```
HTML代码:
<!doctype html>
<html ng-app="HelloAngular">
    <head>
        <meta charset="utf-8">
    </head>
    <body>
        <div ng-controller="helloNgCtrl">
            <p>{{greeting.text}},Angular</p>
        </div>
    </body>
    <script src="js/angular-1.3.0.js"></script>
    <script src="NgModule1.js"></script>
</html>

```
```
//JS代码1:
var modelName = angular.module('modelName',[]);
modelName .controller('contollerName',['$scope',function($scope){
   $scope.greeting = {$scope.greeting={text:'hello'};}
}]);

//JS代码2
function HelloAngular($scope){
    $scope.greeting={
        text:'hello'
        };
}

```
很明显JS1代码函数污染了全局，而Js2代码通过一个模块进行封装，从而避免污染了全局。
>在前面我们看到ng-app指令。它的作用是自动启动一个AngularJS应用，ng-app指令一般指派在应用的根元素上，比如，body或者html标签。在每一个HTML文档中，只能有一个AngularJS应用可以被自动启动，在HTML文档中第一个被找到定义在根元素上的ng-app指令将会作为自动启动的应用。
那我们在js代码中定义的模块和ng-app有什么关系呢？很明显，它是告诉AngularJS应用在启动时加载指定的模块，假设这里ng-app只是放一个纯标签，而不给它赋值。那么它就不知道这里该加载什么模块，于是，它也不认识在模块中定义的textController控制器。

* 但是，赋值与否和启动一个AngularJS的应用无关：
```
<body ng-app>
        <div ng-controller="helloNgCtrl">
            <p>{{greeting.text}},Angular</p>
        </div>
    </body>
```
这样也是可以启动AngularJS应用，并实现name模型的绑定。
* 看一下ng官方的模块切分方式
![模块切分方式][6]

* 最后看一下模块化的完整项目结构，有利于大家对项目的整体认知
![完整的项目结构][5]

#### 双向数据绑定
* 先来个官方例子：
```
<!doctype html>
 2 <html ng-app>
 3 
 4 <head>
 5 
 6 <script src="http://code.angularjs.org/angular-1.0.1.min.js"></script>
 7 
 8 </head>
 9 
10 <body>
11 
12 Your name: <input type="text" ng-model="yourname" placeholder="World">//一个输入框，默认内容为World
13 
14 <hr>
15 
16 Hello {{yourname || 'World'}}!
18 </body>
20 </html>
```
>注:在输入框中输入任何字符都会立即绑定更新到页面.
>>这里采用ng-model指令（directive）绑定是模型scope属性yourname。
并采用表达式将yourname绑定到文本信息中。
这里只需要任何的dom时间监听，因为AngularJs内置了。





友情链接：
[MVC框架-破浪博客][7]
[AngularJs实战视频][8]
[AngularJs中文][9]
[铁锚的CSDN博客][10]
[模块化][11]


  [1]: http://ojmcn9nlw.qnssl.com/blog/20170112/160435655.jpg
  [2]: http://img.mukewang.com/58353e680001545712800720.jpg
  [3]: https://docs.angularjs.org/img/angular_parts.png
  [4]: http://img.mukewang.com/582042680001380a12800720.jpg
  [5]: http://img.mukewang.com/582d1de30001d20d11520720.jpg
  [6]: http://img.mukewang.com/582e9f2a0001220a11520720.jpg
  [7]: http://www.cnblogs.com/whitewolf/archive/2012/08/12/2635586.html
  [8]: http://www.imooc.com/video/4285
  [9]: http://www.ngnice.com/
  [10]: http://blog.csdn.net/renfufei/article/details/19038123
  [11]: http://ju.outofmemory.cn/entry/155946