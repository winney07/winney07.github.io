---
title: JavaScript-笔记
date: 2019-10-28 20:28:51
tags:
- JavaScript
categories: 
- 工作笔记
- JavaScript
---





- JavaScript基础编程
- 内置类使用、面向对象编程
- 作用域链、原型链
- 内存原理、函数高级运用
- BOM模型、DOM模型
- JSON结构及交互
- Ajax技术及跨域技术
- 错误处理及调试等

#### 实用技术

##### JavaScript模块化

- Seajs的应用
- RequireJS的应用

##### JavaScript数据推送

- Comet-基于 HTTP 长连接的服务器推送技术
- 基于WebSocket 的推送方案
- SSE(Server-Send Event)-服务器推送数据的新方式

##### JavaScript高级函数

- 函数柯里化
- JavaScript惰性函数
- JavaScript级联函数

##### JavaScript高级技巧

- this的使用
- 作用域和闭包
- 按值传递和按引用传递

##### JavaScript面向切面编程

##### JavaScript多线程

- WebWork
- Concurrent.Thread.js

#### 书籍

《JavaScript高级程序设计》

#### JavaScript组成

- 核心（ECMAScript）
- 文档对象模型（DOM）
- 浏览器对象模型（BOM）

#### [underscorejs中文网](https://www.underscore-js.com/)

```
// 常量 使用 全部字母大写，单词间下划线分隔 的命名方式。
var HTML_ENTITY = {};
// 类 使用 Pascal命名法。 类名 使用 名词。
function TextNode(options) {
    //
}
// 函数名 使用 动宾短语。
function getStyle(element) {
}
```

#### 闭包

```
//1
function foo () {
    var n = "hello";
}

// console.log(n);
//2
var m = 0;
function mFun () {
    console.log(m);
}
mFun();
//3
function foo () {
    var a = 2;
    function bar () {
        console.log(a);
    }
    bar();
}
foo();

// 第一题
var a = 1;
function fn() {
  console.log('1:' + a);

  var a = 2;
  bar()
  console.log('2:' + a)
}

function bar() {
  console.log('3:' + a)
}

fn();

// 第二题
var a = 1;
function fn() {
  console.log('1:' + a);
  a = 2
}

a = 3;
function bar() {
  console.log('2:' + a);
}

fn();
bar();

// 第一题
var a = 1;
function fn(f) {
  var a = 2;
  return f;
}
function bar() {
  console.log(a)
}
var f1 = fn(bar);
f1();

// 第二题
var a = 1;
function fn(f) {
  var a = 2;
  return function () {
    console.log(a)
  }
}

var f1 = fn();
f1();
```

```
var jsonObj = {
    "title":"javascript",
    "group":{
        "name":"jia",
        "tel":12345
    }
};
var json = JSON.stringify(jsonObj);
console.log(json);
console.log(typeof jsonObj);
console.log(typeof json);

var jsonParse = JSON.parse(json);
console.log('jsonParse');
console.log(jsonParse);

console.log(JSON.stringify(Math));

var json2 = JSON.stringify({a:1,b:2}, function(key, value) {
    if(typeof value === "number"){
        value = 2*value;
    }

    return value;
})

console.log('json2');
console.log(json2);

var json3 = JSON.stringify({a: {b: 1}},function (key, value){
    console.log(key + value);

    return value;
})
console.log('json3');
console.log(json3);

var o = {
    foo: 'foo',
    toJSON: function(){
        return 'bar';
    }
}

console.log(JSON.stringify({x: o}));



var objectFoo = {same:'same'};
var objectBar = {same:'same'};
console.log(objectFoo == objectBar);//false

var objectA = {foo: 'bar'};
var objectB = objectA;

console.log(objectA == objectB);//true

console.log(a);
var a = 1;

// console.log(b);
// b = 2;

switch(a){
case  1 :
    console.log("正确的");
    break;
case  2 :
    console.log('错误的');
    break;
default :
    console.log("没关系");
}

// var even = (n % 2 === 0) ? true : false;

var x = 3;
var i = 0;

do{
    console.log(i);
    i++;
} while(i < x);


console.log(typeof window);
console.log(typeof {});
console.log(typeof []);
console.log(typeof null);
console.log(typeof undefined);


console.log( Number(null));  //null相当于0
console.log( Number(undefined)); //undefined相当于NaN

console.log(0.1 + 0.2 === 0.3);
console.log(0.3 / 0.1);

console.log("Did you greet \'hello\' yesterday?");

var s = '\uD834\uDF06';
console.log(s);

function b64Encode(str) {
    return btoa(encodeURIComponent(str));
}

function b64Decode(str) {
    return decodeURIComponent(atob(str));
}

console.log(b64Encode("感恩节快乐！"));
console.log(b64Decode(""));


var o = {
    name : 'Alice'
};

var p = [];

with (o) {
    p.push('Hello', name, '!');
};

// p.join('');

console.log(p.join(' '));
```

```
function employee(name,job,born)
{
    this.name=name;
    this.job=job;
    this.born=born;
}
if(!window.console){  
    window.console = {};  
}  
if(!window.console.log){  
    window.console.log = function(msg){};  
}
var bill=new employee("Bill Gates","Engineer",1985);
var yang=new employee("Bill Gates","Engineer",1985);

employee.prototype.salary=3000;
bill.salary=20000;

document.write("bill的薪资：" + bill.salary + "<br/>");
document.write("yang的薪资：" + yang.salary);
console.log("yang");
console.log(yang);
console.log("bill");
console.log(bill);

console.log(employee.prototype);
console.log(bill.__proto__);

var date = new Date();
console.log(date);
console.log(date.constructor);
console.log(date.prototype);
console.log(date.__proto__);
console.log(Date.prototype);
console.log(date.__proto__ === Date.prototype);

function extendFun(){

}
var p = new Date();
extendFun.prototype = p;

console.log(extendFun.__proto__);
console.log(extendFun.prototype);
console.log(Date.prototype);

p.setMonth(0);
console.log(p);

console.log(Math.max(2,10));  
console.log(Math.min(2,10));  
console.log(Math.abs(-100));  
console.log(Math.random().toFixed(1));  
console.log(Math.round(2.90833));  
console.log(Math.round(2.0210));

var num = new Number();
console.log(num.constructor);//Number()
console.log(num.__proto__);
console.log(Number.constructor);//Function()
console.log(Number.prototype);

var num1 = new Number("2990909");
var num2 = new Number("dsdfdfd");
num1.len = 7;
console.log(num1);
console.log(num1.len);
console.log(num2);
console.log(typeof(num1));
//num1 和 num2是对象(object)，num3 和 num4是变量（number类型）
var num3 = Number("2990909");
var num4 = Number("dsdfdfd");
console.log(num3);
console.log(num4);
console.log(typeof(num3));
//判断一个值是不是数字，使用isNaN()
if(isNaN(num4)){
    console.log("这个值不是数字");
}

console.log(Number.NaN);

console.log(num5.toString(2));
console.log(num5.toString(3));
console.log(num5.toString(4));
console.log(num5.toString(5));
console.log(num5.toString(6));
console.log(num5.toString(7));
console.log(num5.toString(8));
console.log(num5.toString(9));
console.log(num5.toString(11));

var num5 = new Number("520");
console.log(num5.toString(13));
console.log(num5.toString(14));
console.log(num5.toLocaleString());
console.log(num5.toFixed());
console.log(num5.toExponential(20));
console.log(num5.toPrecision(20));

var str = new String();
var str1 = String("90909090");
var str2 = Number("90909090");
console.log(str.__proto__);
console.log(String.prototype);
console.log(str1.length);//字符串有长度。输出8
console.log(str2.length);//number没有长度，输出值为undefined
var txt="Hello world!"

// document.write(txt.anchor("myanchor"));
// document.write(txt.big());
document.write("<br/>" + txt.charCodeAt(8));
var txt1 = "hhjhkhkhjkhssdkhs";
var txt2 = "jkdkdksd";
var txt3 = "hjkhksdhsksh";
console.log(txt1.concat(txt2,txt3));

var str = new String("yangyanyi");
var str2 = String("yangyanyi");
console.log(str);
console.log(str.__proto__);
document.write(str2.big());
console.log(str2);

document.write(str.fontcolor("pink"));
document.write(str.fontsize("16"));
document.write(str.italics());

console.log(str.lastIndexOf("i"));
console.log(str.match("yi"));
var index = str.match("yi").index;//字符串出现的位置
console.log(index);
var str3="1 plus 2 equal 3";
console.log(str3.match(/\d+/g));

var str4 = "w3c学习";
document.write(str4.link("http://www.w3school.com.cn"));
var str5 = "2017-09-11";
console.log(str5.replace(/-/g,"/"));
console.log(str5.replace(/-/g," "));

var arr1 = ["yi", 7,"yangyanyi"];
var arr2 = {
    name:"yangyanyi",
    age:25,
    hobby:["read","play","liste"]
};
console.log($.isArray(arr1));
console.log($.isArray(arr2));
console.log($.isArray(arr2.hobby));

var str6 = "yangYanyi";
console.log(str6.search(/yany/));
console.log(str6.search(/yany/i));
console.log(str6.slice(0,5));
console.log(str6.slice(-1));

var str7 = "How are you doing today?";
console.log(str7.split(" "));
console.log(str7.split(""));
console.log(str7.split(" ",3));

var arr = new Array(3);
arr[0] = "How";
arr[1] = "are";
arr[2] = "you";
var strJoin =  arr.join(" ");
console.log(strJoin + "!");
document.write(strJoin.strike());
console.log(strJoin.substr(0,10));

var reg = new RegExp();
console.log(reg.__proto__);
console.log(isFinite("2558558"));
console.log(isFinite("hello"));
console.log(isFinite("2017/09/13"));
console.log(window);
console.log(window.prototype);
console.log(window.__proto__);
console.log(window.constructor);
console.log(window.innerHeight);
console.log(window.innerWidth);
console.log(window.navigator);
console.log(window.outerHeight);
console.log(window.outerWidth);
console.log(window.pageXOffset);
console.log(window.pageYOffset);
console.log(window.screenX);
console.log(window.screenY);
console.log(window.screenLeft);
console.log(window.screenTop);

//  随机生成6个数
function sixNum(e){
  var str ='';
  for(var i=0;i<e;i++){

      str += Math.floor(Math.random()*10);
  }
  return str;
}
console.log(sixNum(4));
console.log(Math.random()*10);

var  aa = 123;(function(){console.log(aa)})();
var  bb = 123;(function(){console.log(bb);var  bb  =  456;})();
var  cc = 123;(function(){var cc;console.log(cc);cc = 456;})();
var str1 = '{"name":"yangyanyi","age":"25"}';//JSON字符串
var str2 = {"name":"yangyanyi","age":"25"}//JSON对象
var str3 = eval('(' + str1 + ')');//JSON字符串转换为JSON对象
console.log(str3);
console.log(str1.parseJSON);
console.log(JSON.parse(str1));//JSON字符串转换为JSON对象
console.log(JSON.stringify(str2));//JSON对象转换为JSON字符串

function user(n, a)
{
  this.name = n;
  this.age = a;
  this.toString = function() {
      return "Name:" + this.name + ", Age:" + this.age;
  }
}

var u = new user("tom", 18);
for (var k in u) {
    alert('key: ' + k + ', value:' + u[k]);
}

console.log(this);


function Person(){};

Person.prototype.name = '杨伊冰';
Person.prototype.age = 25 ;
Person.prototype.say = function(){
    console.log("name:" + this.name + "age:" + this.age);
}

//通过prototype创建的属性和方法，会存放在该函数对象中的__proto__属性中   __proto__是一个对象
//
//通过prototype创建的属性和方法，也会存放在该函数对象的__proto__属性中的constructor（构造函数是Person)  中的prototype中
var person2 = new Person();

console.log(person2);
person2.say();

person2.name = "yangyanyi";
person2.say();

Person.prototype = {
    name : 'yangyanyi',
    age : 26,
    say : function(){
        console.log(name + age);
    }
}
//修改后的prototype会放置在新建的对象中的__proto__原型对象中，但不会放到它的构造函数中的prototype中
var person3 = new Person();
console.log(person3);


var obj = new Object();
console.log(obj);
obj.prototype.name = "杨演绎";

console.log(window);

var data = function(){

}

console.log(typeof data);

var obj = []

console.log(typeof obj);

var aa;
var bb = null;

console.log(aa);
console.log(bb);


var cat = new Object();
console.log(cat);

console.log(window);
```

#### 基本数据类型(值类型)

- number

- string

- boolean

- null

- undefined

#### 引用数据类型

- 对象

  - 普通对象
- 数组
  - /^$/正则
- Math对象数据类型的
  - ....

- 函数

  - function普通函数
  - 类
  - .....

#### 变量提升（预解释）

- 基础概念（变量提升和作用域链)
- 定义变量带var和不带var的区别
- 只对等号左边的进行变量提升
- 不管条件是否成立都要进行预解释
- 重名的处理

#### 打印当前时间

```
<a href="javascript:new Date().toLocaleTimeString();">
  What time is it?
</a>
```

#### window

变量提升

```
var num;
fn = aaafff111

function aaafff111() {
	console.log(a);
    var a = 10;
    console.log(a);
}
```

代码执行：

```
num => undefined
fn => 函数本身

num= 13: //->提升阶段已经完成声明了，此处不需要再var，但是没有定义过，所以此处还需要重新的赋值
//->遇到创建fn的代码直接跳过∶在提升阶段声明和定义都做过了

fn()
num => 13
```

#### fn()

```
变量提升: var a; //->在私有作用域中声明的变量都是私有变量代码执行
a => undefined
a = 10;
a => 10;
```

#### window全局作用域

```
var a = 12;
var b = a; ->b = 12
b = 13;
a=>12
```

```
var o = xxxfff000
var p = o; ->p = xxxfff000 
p.name ="周啸天"

xxxfff000是地址
```

xxxfff000

> name :“~~珠峰培训~~“
> 				"周啸天”

```
var m = aaafff111
var n =m; ->n = aaafff111
n = aaafff222
fn = aaafff333
```

aaafff111

> name :“珠峰培训“

aaafff222

> name :“中国最权威...“

aaafff333

> "var
> ary=Array.prototype.slice.call(arguments);
> return
> evalary.join(" + ):"

fn(..)私有的（作用域）

```
var ary =
Array.prototype...
...
```

#### jq里面用this和用$(this)有什么区别

this表示的是javascript提供的当前对象
$(this)表示的是用jquery封装候的当前对象
this对象可以直接用this.style修改样式
$(this)可以使用jquery提供的方法访问样式

#### [Ajax及封装Ajax详解](https://blog.csdn.net/c__dreamer/article/details/80456565)

```
ajax({
    url : "a.php",  // url---->地址
    type : "POST",   // type ---> 请求方式
    async : true,   // async----> 同步：false，异步：true 
    data : {        //传入信息
        name : "张三",
        age : 18
    },
    success : function(data){   //返回接受信息
        console.log(data);
    }
})
```

[HTTP缓存机制](http://blog.csdn.net/xiaozhuxmen/article/details/52074211)

#### jQuery源码分析

```
$("ul li:last").addClass(function(index) {
   return"item-" + index;
});
$('.container').append($('h2'));
```

#### text()与html()方法的区别

```
function showDialog(txt) {
	$(".dialog-box").show();
	$(".mask").show();
	// $(".dialog-box .tiptxt").text(tiptxt);
	$(".dialog-box .tiptxt").html(tiptxt);
}
```

```
showDialog(result.msg + "<br/>测试测试测试测试测试");
加了<br/>不换行，原因可能是写入的时候用的是text()；改为html()；就可以，
因为<br/>在text()里面不会把它当一个标签，而是把它当作字符.
```

#### 数组里的字符串转换成数字或者把数字转换成字符串

```
var arr = [1,2,3,4,5,6,7,8,9];
arr.map(String);   //结果： ['1','2','3','4','5','6','7','8','9'];

var a = ['1','2','3','4','5','6','7','8','9'];
a.map(Number);   //结果：[1,2,3,4,5,6,7,8,9];
```

ES6，Array.fill()函数的用法

#### **onload 和 onunload 事件**

onload 和 onunload 事件会在用户进入或离开页面时被触发。

onload 事件可用于检测访问者的浏览器类型和浏览器版本，并基于这些信息来加载网页的正确版本。

onload 和 onunload 事件可用于处理 cookie。



![image-20220705154829046](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/JavaScript-%E7%AC%94%E8%AE%B0/image-20220705154829046.png)

#### [滑动时报错[Intervention\] Unable to preventDefault inside passive event listener due to target being treated as passive. See ](https://www.cnblogs.com/emma-zhao/p/10699330.html)

搜索`mousewheel`件，在后面加上`{passive: false}`

```
 addEvent("mousewheel", wheel, {passive: false});
```

#### 防抖和节流

###### [防抖与节流](https://www.jianshu.com/p/4616adf56ed8)

防抖、节流、去重、深浅拷贝、数组扁平化、乱序、柯里化

> 我们在平时开发的时候，会有很多场景会频繁触发事件，比如说搜索框实时发请求onmousemove,resize,onscroll等等，有些时候，我们并不能或者不想频繁触发事件
>

#### JavaScript兼容

`IE浏览器没有console方法 `

如果代码中写了console.log()，在IE浏览器会报错。所以测试完之后，`要把console.log的代码注释掉`。

![img](https://raw.githubusercontent.com/winney07/Images/main/Note/yuque_mind2.jpeg)

一个函数可以访问到它外部的成员，这个函数就可以称为闭包函数。

一个函数在另外一个函数里面定义，那这个函数就可以访问父函数里面的成员。那么这个函数（内部那个函数）就称为闭包函数。

```javascript
function f1(){
	var a = 10;
  var b = 20;
  function f2() {
    console.log(a);
  }
  f2();
}
f1();
```

f2引用了自由变量的函数，它引用了父函数的自由变量。f2是闭包函数

不同的浏览器有不同的处理法：

```javascript
Closure Variables
a:10
b:20
f2: function f2(){}

或
closure
a:10
function f1(){
	var a = 10;
  var b = 20;
 	return function f2() {
    console.log(a);
  }
}
var result = f1();
result();

// result相当于f2，它已经离开了创造它的环境了
```

![img](https://raw.githubusercontent.com/winney07/Images/main/Note/yuque_mind3.jpeg)

f2跳出了f1，但是f2的作用域还是f1的词法环境

**没有调用，不出现闭包：**

```javascript
function f1(){
	var m = 10;
  function f2(){
		console.log("asdf");
  }
	f2();
}
f1();
```

**调用父级的父级的变量，会出现闭包：**

```javascript
function f1(){
	var m= 10;
  function f2(){
		var n = 20;
    function f3(){
			console.log(m);
		}
		f3();
  }
	f2();
}
f1();
```

**闭包创建的时机：**

在f2被执行的时候，在预处理阶段，已经把f3放到它的词法环境。即在读取f3里面的代码，扫描里面的代码的过程（这个过程叫词法分析阶段），已经创建了闭包。（因为识别到它调用了父级的父级的变量） 因为这个过程是对字符串代码分析的阶段，所以它是静态的，所以称为静态的作用域。



**闭包的本质是它形成了一个作用域链**



**变量自加：（使用闭包减少全局变量）**

1. 全局变量的做法

```javascript
var a = 10;
function add(){
	a++;
  alert(a);
}
add();
add();
```

1. 闭包的做法

```javascript
function f() {
	var a = 10;
  return function() {
  	a++;
    alert(a);
  }
}
var result = f();
result();
result();
```

做一个基数加上1到max所有值的和，例如max=4，即基数+（1+2+3+4）这个功能，

一般的方法：传两个参数，add(base，max)

```javascript
function add (base,max){
	
}
function f(){
	var num = 1;
  function g(){
  	alert(num);
  }
  num++;
  g();
}
f();
```

g的scope等于f的词法环境，闭包生成的时候，num是1，但是g没有执行，后面num++，num是2，当g执行时，num是2了。所以说引用，不是复制。

**每调用一个函数时，会创建一个新的词法环境：**

```javascript
function f(){
	var num = 1;
 	return function(){
    num++;
  	alert(num);
  }
}

var result1 = f();
result1();    // 2
result1();		// 3

var result2 = f();
result2();		// 2
result2();		// 3
```

**全局变量**

每次输出都是4，因为i是全局的，当点击执行的时候，i己经是4了：

```javascript
<div id="1">1</div>
<div id="2">2</div>
<div id="3">3</div>

for(var i = 1; i<= 3; i++){
	var ele = document.getElementById(i);
  ele.onclick = function(){
  	alert(i);
  }
}
```

i是全局变量：

```javascript
<div id="1">1</div>
<div id="2">2</div>
<div id="3">3</div>

var i;
for(i = 1; i<= 3; i++){
	var ele = document.getElementById(i);
  ele.onclick = function(){
  	alert(i);
  }
}
```

当i等于1的时候，匿名函数立即执行，就把i传到id中，每次调用生成一个闭包·所以每点一个会弹出对应的i：

```javascript
<div id="1">1</div>
<div id="2">2</div>
<div id="3">3</div>

var i;
for(i = 1; i<= 3; i++){
	var ele = document.getElementById(i);
  ele.onclick = (function(id){   // id为形参
  	return function() {
    	alert(id);
    }
  })(i);		// i为实参
}
```

![img](https://raw.githubusercontent.com/winney07/Images/main/Note/yuque_mind4.jpeg)

```javascript
alert(a);				// undefined
alert(b);				// undefined
alert(c);				// c is not definded
alert(d)				// d也没有定义，因为它的作用域

var a = 1;
if(false){
	var b= 2;
}else {
	c = 3;
}
function f(){
	var d =4;
}
```

块作用域：

```javascript
for(var i = 0; i < 3; i++){

}
alert(i);    // 3
```

函数作用域：

```javascript
function f(){
	var x
	function g(){
    
  }
}
```

js没有动态作用域

```javascript
function f(){
	alert(x);
}
function f1(){
	var x = 5;
  f();
}
function f2(){
	var x = 6;
  f();
}
f1();     // Uncaught ReferenceError: x is not defined
```

静态作用域：

```javascript
var x = 100;
function f() {
	alert(x);
}

function f1() {
	var x = 5;
  f();   // 当f被执行的时候，它会在它自己的词法环境里找x，因为在预处理阶段，有x= 100，所以会弹出100
}

function f2() {
	var x = 6;
  f();
}

f1();
// 声明f时，预处理阶段，词法环境
f  [[scope]]  ==  lexicalEnv   == window
function f() {
	alert(x);
}

function f1(){
	var x = 5;
  f();   // 真正执行的时候le   -> f.[[scope]]   == window
}

function f2(){
	var x = 6;
  f();
}

// 当f被执行时，先进去里面找有没有x，如果没有就找它自己本身的词法环境（即window），如果还是找不到x，
那就报错。因为在f1和f2里面定义的变量没有在它的词法环境中。
```

词法环境（le）

```javascript
function f(){   	// scope == window
	var x = 100;		// le{x = 100}  ——> f.[[scope]]
  function g(){		// g.[[scope]] == f.le
  	// le -> g.[[scope]]
  }
  g();
}

// g.le -> g.[[scope]] -> f.le  -> f.[[scope]] == window
```

创建函数的方式

```javascript
function f(){
  ....
}
var f = function (){
  ....
}
var f = function x(argument){
  ....
}
var f = new Function("", "alert(x)")

// var f = new Function(函数参数, 函数体)
```

例如：

```javascript
function f(){
	var x = 100;
  var g = function() {
  	alert(x);     // 100
  }
  g();
}
f();
```

每次创建一个函数，它会形成一个新的作用域，会跟它的父形成一个链条。用new Function创建的函数的作用域永远指向的是全局，而不是他的父。

**g的作用域等于f的词法环境：**

```javascript
function f(){    //scope = window
	var x = 100;
  var g = function() {   // g.scope = f.le
  	alert(x);     // 100
  }
  g(); 
 // 预处理阶段，x和g放到window的词法环境，当运行g的时候，它在它自己的词法环境找不到x，
  	然后就往父级找，找到x为100.
}
f();
```

g的作用域是window：

用这种方法创建的g函数，g的作用域就是window，而window中没有x，所以是not defined。

```javascript
function f() {
	var x= 100;
	// g.[[scope]] = window
	var g = new Function("", "alert(x)");
  g();   //  Uncaught ReferenceError: x is not defined
}
f();
```

g的作用域指向window：

```javascript
var x = 12;
function f() {
	var x= 100;
	// g.[[scope]] = window
	var g = new Function("", "alert(x)");
  g();   // 12   因为g的作用域指向window
}
f();
```

大量使用全局变量，有可能导致冲突，很难调试，很难把问题找出来

```javascript
var a = 1;
var b = 2;
f1(){}
f2(){}
```

如果f1和f2想用同一个变量，应该不能在它们单独的函数里定义。一般我会想到用全局变量，但是用全局变量有一个弊端就是，如果引用的js文件比较多，命名一样的话，出了间题，难调试，不容易找出问题等等

**把变量放在一个匿名函数里面，那样外部就访问不了这些变量，起到一个信息隐藏的作用，把a，b，f都隐藏起来了。**

```javascript
function() {
	var a = 5;
  var b = 6;
  function f(){
  	alert(a);    // 在f的作用域可以访问到a
  }
}
a;   // 访问不了a
(function(){
	var a = 5;
  var b = 6;
  function f() {   // 写在一个匿名函数里面
  	alert(a);
  }
  window.f = f;    // 因为在外部是不能访问到a,b的，要想访问到，要加这句代码
})();
f();
```



- Hibird APP开发
- 微信小程序
- 网页游戏，flash，flex， ActionScript



放大镜效果——淘宝鼠标移到产品图上的放大显示效果

360度全景图片——360度旋转图片——360度看产品——秒味课堂

倒计时效果

QQ幻灯片

面向对象

BOM

DOM

Ajax

事件处理

cookie

事件详解

正则表达式

游戏开发

拖放操作

历史管理

canvas

响应式布局

螺旋矩阵算法

穿梭插件

无刷新分页效果

语音识别库-Jullus

G码兑换

围住神经猫游戏开发

事件委托

无缝切换

操作iframe

闭包

数码时钟

枚举算法

网页进度条

联动日历

瀑布流



vue 热更新

vuex

flux

Smarty—PHP模板引擎

tpl框架使用

React+Redux 的综合配置

angular + ionic





[JavaScript中原型对象的彻底理解](https://blog.csdn.net/u012468376/article/details/53121081)

[一张图理解prototype、proto和constructor的三角关系](https://www.cnblogs.com/xiaohuochai/p/5721552.html)

[三张图搞懂JavaScript的原型对象与原型链](https://www.cnblogs.com/shuiyi/p/5305435.html)

[一个例子让你明白原型对象和原型链](https://blog.csdn.net/kkkkkxiaofei/article/details/46474303)

[浅析Javascript匿名函数与自执行函数](https://www.jb51.net/article/79238.htm)

[jQuery中$(function() {});问题详解](https://www.jb51.net/article/70836.htm)

[Window.sessionStorage](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/sessionStorage)

[深入学习JavaScript: apply call方法 详解(转)](http://blog.csdn.net/bao19901210/article/details/21614761)

 [使用工厂方法创建JavaScript对象](http://www.htmleaf.com/ziliaoku/qianduanjiaocheng/201512132900.html)

[javascript简写技巧](https://www.geekjc.com/post/5a0a8c9a592e38541f7703c8)

[题解JavaScript作用域](https://juejin.cn/post/6844903540264009736)

[学习Javascript的8张思维导图](https://segmentfault.com/a/1190000011151972)



[从一个 JSON.parse 错误深入研究 JavaScript 的转义字符](https://zhuanlan.zhihu.com/p/31030352)

 [JavaScript深入之执行上下文栈](https://github.com/mqyqingfeng/Blog/issues/4 )

 [『多级目录结构』在移动端的交互设计](https://coffee.pmcaff.com/article/764896867122304/pmcaff?utm_source=forum&from=related)

 [一篇文章带你详解 HTTP 协议（网络协议篇一）](http://www.jianshu.com/p/6e9e4156ece3 )

 [一篇文章带你熟悉 TCP/IP 协议（网络协议篇二）](https://juejin.im/post/5a069b6d51882509e5432656 )

 [客栈说书：CSS遮罩CSS3 mask/masks详细介绍](http://www.zhangxinxu.com/wordpress/2017/11/css-css3-mask-masks/ )

 [CSS 实用 Tips](http://jartto.wang/2017/11/12/f2e-tips/ )

 [懒加载和预加载](http://www.jianshu.com/p/4876a4fe7731 )

[使用 JavaScript 实现分屏视觉效果](https://webdesign.tutsplus.com/tutorials/how-to-create-a-split-screen-slider-with-javascript--cms-28844 )

[打造自己的JavaScript武器库](https://juejin.im/post/5a091afe6fb9a044ff30f402 )

[Git分支管理](https://segmentfault.com/a/1190000011927868 )

[16种方法实现水平居中垂直居中](http://louiszhai.github.io/2016/03/12/css-center/ )

[手机/移动前端开发需要注意的20个要点](https://juejin.im/post/5a044fd5f265da43333ddabd )

 [移动端字体放大问题的研究](https://juejin.im/post/59f678d7f265da43333dabb7 )

[跨域，你需要知道的全在这里](https://juejin.im/entry/59feae9df265da43094488f6 )

[10 个独特的 CSS 背景视觉效果](https://juejin.im/entry/59ffb92bf265da43040600f9 )

[你不知道的14个jsvascript调试技巧](https://raygun.com/javascript-debugging-tips )



https://weui.io/#form_vcode