---
title: JavaScript-笔记
date: 2019-10-28 20:28:51
tags:
- JavaScript
categories: 
- 工作笔记
- JavaScript
---

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

