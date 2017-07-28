---
title: JS-我待this如初见
date: 2016-08-18 17:50:33
tags: JavaScript
---


# 何为this？
this是对象，是在运行时基于`函数`的`执行环境`(和对象有关)绑定的，首先，当代码没执行前，或没执行到之前，this 是没有指向的,所以
切记：`在函数中this到底取何值，是在函数真正被调用执行的时候确定的，函数定义的时候确定不了`。因为this的取值是执行上下文环境的一部分，每次调用函数，都会产生一个新的执行上下文环境。
`this只要一出现，一定牵扯到函数和对象`
一般方法：`首先分析this所在的函数是被当做哪个对象的方法调用的，则该对象就是this所引用的对象。`


其实，this的取值，分五种情况。我们来挨个看一下。

> * 全局和调用普通函数
> * 构造函数
> * 函数作为对象的一个属性
> * 函数用call或apply或bind
> * 事件监听函数中的this





# 情况1：全局 & 调用普通函数

在全局环境下，this永远是window，这个应该没有非议。
```
console.log(this==window);//ture
this.a=20;
console.log(window.a);

```
 

普通函数在调用时，其中的this也都是window。


```
var home="中国";
var person=function(){
		var home="河南"
		console.log(this);  //window
		console.log(this.home);  //中国
  }
person();
```

但是严格模式下 this是undefined(竞然)：
```
function person1(){
	return this;        
}
person1()===window;   //true

function person2(){
	"use strict"  //严格模式
	return this;
}
person2()===undefined;        //true
```


 

# 情况2：构造函数

所谓构造函数就是用来new对象的函数。其实严格来说，所有的函数都可以new一个对象，但是有些函数的定义是为了new一个对象，而有些函数则不是。另外注意，构造函数的函数名第一个字母大写（规则约定）。例如：Object、Array、Function等。

`如果函数作为构造函数用，那么其中的this就代表它即将new出来的对象`

```
window.home="中国";
window.age="5000+";
function Person(){
	this.home="河南";
	this.age=20;

	console.log(this);   //Person {home: "河南", age: 20}
	console.log(this.home);//  河南
}
var chongqing = new Person();

console.log(chongqing.home);  //河南还是中国
console.log(chongqing.age);  //20还是5000+
console.log(age);  //5000+还是20
```

以上代码中，如果函数作为构造函数用，那么其中的this就代表它即将new出来的对象,即上文中的chongqing。

上个例子中构造函数没有返回值，默认返回this，但是若有返回语句，返回一个对象的话，会将return的对象作为返回值
```
function Myclass(){
	this.a=20;
}
var o=new Myclass();
console.log(o.a);   //20


function Person(){
	this.a=20;
	return {  a: 21};
}
var o=new Person();
console.log(o.a);   //21还是20
```
 

`注意，以上仅限new Person()的情况，即Person函数作为构造函数的情况。`如果直接调用Person函数，而不是new Person()，情况就大不一样了。相当于普通函数
```
window.home="中国";
window.age="5000+";
function Person(){
	this.home="河南";
	this.age=20;

	console.log(this);   //window 还是Person {home: "河南", age: 20}
	console.log(this.home);//???河南还是中国
	console.log(home);//???河南还是中国
}
Person();
```

这种情况下this是window，就是相当于普通函数中的this

构造函数还有一种情况，在构造函数的prototype中，this代表着什么？
`在整个原型链中，this代表的是当前对象的值`
```
window.home="中国";
window.age="5000+";
function Person(){
	this.home="河南";
	this.age=20;

	console.log(this);   //Person {home: "河南", age: 20}
}
Person.prototype.getHome=function(){
	console.log(this.home);  //河南
}

var chongqing= new Person();
chongqing.getHome();//
```


如上代码，在Person.prototype.getHome函数中，this指向的是chongqing对象。因此可以通过this.name获取chongqing.name的值。

其实，不仅仅是构造函数的prototype，即便是在整个原型链中，this代表的也都是当前对象的值。


 
# 情况3：函数作为对象的一个方法
在这又分两种情况：
1. 函数作为对象的方法`被调用`,此时函数中的`this指向该对象`
2. 函数`被赋值`到了另一个变量中，`this的值是window`


###1. 如果函数作为对象的一个方法时，`并且作为对象的一个方法被调用`时，函数中的`this指向该对象`。
```
window.home="中国";
window.age="5000+";
var obj={
	home:"河南",
	person: function(){
		console.log(this);  //Object {home: "河南"}
		console.log(this.home);  //河南

    }
};
obj.person();
```

以上代码中，person不仅作为一个对象的一个方法，`而且的确是作为对象的一个方法被调用。结果this就是obj对象`。

 

`注意`，如果**`person函数不作为obj的一个方法被调用`**，会是什么结果呢？
### 2. `如果person函数被赋值到了另一个变量中，并没有作为obj的一个方法被调用，那么this的值就是window`

```
window.home="中国";
window.age="5000+";
var obj={
	home:"河南",
	person: function(){
		console.log(this);  //？？window还是object
		console.log(this.home);  //？？中国还是河南
    }
};
var person1=obj.person;
person1();
```

如上代码，如果person函数被赋值到了另一个变量中，并没有作为obj的一个属性被调用，那么this的值就是window,相当于全局了，this.home的值为中国

### 3.闭包中使用this对象（对象方法函数中又有一个匿名函数）-this用处（诡异）
 `在ES3中，此时使用this比较糟糕，因为this失去了方向，引用的是window对象，而不是定义函数所在的对象,欣慰的是，this在ES5中是固定的，我们应该清楚地了解这种情况`
注意： `在ES3中，当函数作为某个对象的方法调用时，this等于那个对象，不过在闭包中，匿名函数的执行环境具有全局性，此时通常this指向window`
```
var obj={
	home:"河南",
	person: function(){
		    function person1(){
			console.log(this);      //window
			console.log(this.home);    //undefined
        }
        person1();
}
};
obj.person();
```
总结**：当this值的宿主环境被封装在另一个函数内部或在另一个函数的上下文被调用时，this将永远是对window对象的引用（再次说明，this在ES5中是固定的）**

如何改变上述情况呢？
`可以在父函数中使用作用域链来保留对this的引用，以使this值不丢失`。如下代码演示了如何使用that变量及其作用域来有效跟踪函数上下文
```
var obj={
	home:"河南",
	person: function(){
	        var that=this;  //person作用域中，保存this引用对象obj（而不是window）
		    function person1(){
		      //输出通过作用域得到河南，因为that=this
			console.log(that);      //Object {home: "河南"}
			console.log(that.home);    //河南
        }
        person1();
}
};
obj.person();
```

 

# 情况4：函数用call或者apply或bind调用

> 先简单说一下call和apply和bind如何使用

### call(),apply()
* 关于call和apply，首先这两个方法的用途都是在`特定的作用域中调用函数`，，都有两个参数call/apply(`作用域`，`传递给函数的参数`)
* 它的作用是改变函数的调用对象，它的第一个参数就表示改变后的调用这个函数的对象。因此，`this指的就是这第一个参数`。 

    * apply的用法和call大致相同，只有一点区别，apply只接受两个参数，第一个参数和call相同，第二个参数必须是一个数组，数组中的元素对应的就是函数的形参。
注意不同的是接受参数的方式不同，call()传递给函数的参数必须逐个列举出来，而apply()则是参数数组

### bind()
* bind（）创造一个函数的实例，其this值会被绑定到传给bind（）函数的值。


牢记：**当一个函数被call或apply或bind调用时，this的值就取`传入的对象的值,即call（）或apply或bind（）括号里的对象`。**


call实例
```
window.home="中国";
window.age="5000+";
var obj={
	home:"河南"
};
var person=function(){
		console.log(this);  //Object {home: "河南"}
		console.log(this.home);  //河南
  }
person.call(obj);
```

> 还要注意：apply()的`参数`为空时，默认调用全局对象。

```

　　var x = 0; 
　　function test(){ 
　　　　alert(this.x); 
　　} 
　　var o={}; 
　　o.x = 1; 
　　o.m = test; 
　　o.m.apply(); //0 
　　
```

bind()实例
```
window.color="red";
var o={color:"blue"};

function sayColor(){
	alert(this.color);
}
var objectSayColor=sayColor.bind(o);
objectSayColor();    //blue还是red
```
sayColor()调用bind（）并传入对象o。创建了objectSaycolor（）函数，objectSaycolor（）函数中的this的值等于o，因此，即使是在全局作用域中调用这个函数也会看到“blue”。

#  情况5：事件监听函数中的this(大家应该熟悉)

```
var one = document.getElementByIdx( 'one' );

one.onclick = function(){

    alert( this.innerHTML );  //this指向的是one元素，
```


友情链接：
Javascript高级程序设计（第3版）-关于this对象-182页
JavaScript启示录-this部分
[博客-深入理解Js-this][1]
[博客-js中this][2]
[慕课网Javascript深入浅出-this部分][3]
[博客-this关键字详解][4]

# Ending（欲知后事如何，且听下回分解）



 


  [1]: http://www.cnblogs.com/wangfupeng1988/p/3988422.html
  [2]: http://blog.csdn.net/dfyong/article/details/7313028
  [3]: http://www.imooc.com/video/6430
  [4]: http://www.jb51.net/article/41656.htm