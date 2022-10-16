---
title: Javascript相关笔记
date: 2019-09-04 11:31:48
tags:
- Javascript
---

#### 基础知识

##### [javascript类型系统——undefined和null](https://www.cnblogs.com/xiaohuochai/p/5665637.html)

##### [ECMAScript 原始类型](https://www.w3school.com.cn/js/pro_js_primitivetypes.asp)

##### [javascript中的原始值和复杂值](https://www.cnblogs.com/xiaohuochai/p/5108837.html)

null是一个表示”无”的对象，转为数值时为0；undefined是一个表示”无”的原始值，转为数值时为NaN

**undefined** 【出现场景】**:**

【1】已声明未赋值的变量

【2】获取对象不存在的属性

【3】无返回值的函数的执行结果

【4】函数的参数没有传入

【5】void(expression)

**null被认为是空对象指针**

```
var myObject = {};
var copyOfMyObject = myObject;//没有复制值，而是复制了引用
myObject.foo = 'bar';//操作myObject中的值
//现在如果输出myObject和copyOfMyObject，则都会输出foo属性，因为它们引用的是同一个对象
console.log(myObject,copyOfMyObject);//Object{foo="bar"}
```

##### [ESLint - 简介](https://www.jianshu.com/p/2bcdce1dc8d4)

#### [URI、URL和URN的关系](https://blog.csdn.net/qq_46331050/article/details/118071887)

**1、URI: Uniform Resource Identifier 统一资源标志符**

**2、URL: Uniform Resource Locator 统一资源定位符**

**3、URN: Uniform Resource Name 统一资源名称**

#### [JavaScript 全局参考手册](https://www.w3school.com.cn/jsref/jsref_obj_global.asp)

全局对象只是一个对象，而不是类。既没有构造函数，也无法实例化一个新的全局对象。

#### 变量

变量是对“值”的引用，使用变量等同于引用一个值。每一个变量都有一个变量名

```
var x = 1;
var x;
x  // 1

// 上面代码中,变量x声明了两次，第二次声明是无效的。
// 但是,如果第二次声明的同时还赋值了，则会覆盖掉前面的值。

var x = 1;
var x = 2;
// 等同于
var x = 1;
var x；
x = 2； 
```

#### 变量提升

JavaScript引擎的工作方式是,先解析代码,获取所有被声明的变量,然后再一行一 行地运行。这造成的
结果,就是所有的变量的声明语句,都会被提升到代码的头部,这就叫做变量提升( hoisting )。

```
console.log(a);
var a = 1;
```

上面代码首先使用console. log方法,在控制台( console )显示变量a的值。这时变量a还没有声明和
赋值,所以这是一种错误的做法，但是实际上不会报错。因为存在变量提升,真正运行的是下面的代码。

```
var a;
console.log(a);
a = 1;
```

最后的结果是显示undefined ,表示变量a已声明,但还未赋值。
请注意,变量提升只对var命令声明的变量有效,如果一个变量不是用 var命令声明的,就不会发生变量
提升。

```
console.log(b);
b = 1;
```

上面的语句将会报错,提示"ReferenceError: b is not defined" ,即变量b未声明,这是因为b不是用var
命令声明的, JavaScrip引擎不会将其提升,而只是视为对顶层对象的b属性的赋值。

需要注意的是，`switch`语句后面的表达式与`case`语句后面的表示式,在比较运行结果时,采用的是严
格相等运算符( `===` ) ,而不是相等运算符(`== `) ,这意味着比较时不会发生类型转换。

```
var x =1;
switch (x) {
	case true :
		console.log('x发生类型转换');
	default :
		console.log('x没有发生类型转换');
}
// x没有发生类型转换
```

#### 标签（label）

JavaScript语言允许,语句的前面有标签( label) ,相当于定位符,用于跳转到程序的任意位置,标签的
格式如下。

```
label:
	statement
```

标签可以是任意的标识符,但是不能是保留字,语句部分可以是任意语句。
标签通常与break语句和continue语句配合使用，跳出特定的循环。

```
top:
	for(var i =0;i<3;i++){
    for(var j=0;j<3;j++){
    if(i===1 && j===1) break top;
      console.log('i='+ i + ', j='+ j);
    }
   }
// i=0,j=0
// i=0,j=1
// i=0,j=2
// i=1,j=0
```

上面代码为一个双重循环区块，`break`命令后面加上了`top`标签(注意，`top`不用加引号) ,满足条件
时,直接跳出双层循环。如果`break`语句后面不使用标签,则只能跳出内层循环,进入下一次的外层循
环。

`continue`语句也可以与标签配合使用。

```
top:
	for(var i =0;i<3;i++){
    for(var j=0;j<3;j++){
    if(i===1 && j===1) continue top;
      console.log('i='+ i + ', j='+ j);
    }
   }
// i=0,j=0
// i=0,j=1
// i=0,j=2
// i=1,j=0
// i=2,j=0
// i=2,j=1
// i=2,j=2
```

上面代码中，`continue`命令后面有一 个标签名,满足条件时,会跳过当前循环，直接进入下一轮外层循
环。如果`continue`语句后面不使用标签,则只能进入下一轮的内层循环。



JavaScript语言的每一个值,都属于某-种数据类型。 JavaScript 的数据类型,共有六种。( ES6又新增
了第七种Symbol类型的值,本教程不涉及。)

- 数值( number ) : 整数和小数(比如1和3.14 )
- 字符串( string) : 字符组成的文本(比如"Hello World" )
- 布尔值( boolean) : true ( 真)和false (假)两个特定值
- undefined : 表示“未定义”或不存在，即由于目前没有定义，所以此处暂时没有任何值
- null :表示无值，即此处的值就是“无”的状态。
- 对象( object ) :各种值组成的集合

通常,我们将数值、字符串、布尔值称为原始类型( primitive type )的值，即它们是最基本的数据类型,
不能再细分了。而将对象称为合成类型( complex type )的值,因为一个对象往往 是多个原始类型的值的
合成，可以看作是一个存放各种值的容器。至于`undefined`和`null` ,一般将它们看成两个特殊值。



对象又可以分成三个子类型。

- 狭义的对星星( object )
- 数组( array )
- 函数( function )

狭义的对象和数组是两种不同的数据组合方式,而函数其实是处理数据的方法。JavaScript把函数当成一
种数据类型,可以像其他类型的数据一样,进行赋值和传递,这为编程带来了很大的灵活性,体现了期
JavaScript作为“函数式语言”的本质。
这里需要明确的是, JavaScript的所有数据,都可以视为广义的对象。不仅数组和函数属于对象,就连原
始类型的数据(数值、字符串、布尔值)也可以用对象方式调用。为了避兔混淆,此后除非特别声明,本
教程的”对象“都特指狭义的对象。
本教程将详细绍所有的数据类型。`undefined` 和`null`两个特殊值和布尔类型Boolean比较简单,将在
本节介绍,其他类型将各自有单独的一节。



除此以外,其他情况都返回object。

```
typeof window  // "object"
typeof {} // "object"
typeof [] // "object" 
typeof null // "object"
```

从上面代码可以看到，空数组( [] )的类型也是`object` , 这表示在JavaScript内部,数组本质上只是一
种特殊的对象。
另外，`null`的类型也是`object `,这是由于历史原因造成的。1995年JavaScript语言的第一 版,所有值都
设计成32位,其中最低的3位用来表述数据类型，`object `对应的值是`000`。当时,只设计了五种数据类
型(对象、整数、浮点数、字符串和布尔值)，完全没考虑 `null` ,只把它当作`object`的一种特殊值,
32位全部为0。这是`typeof null`返回`object`的根本原因。
为了兼容以前的代码，后来就没法修改了。这并不是说null就属于对象，本质上null是个类似于
undefined的特殊值。
既然`typeof`对数组( array )和对象( object )的显示结果都是`object` , 那么怎么区分它们呢?
`instanceof`运算符可以做到。



1995年JavaScript 诞生时,最初像Java一样,只设置了`null`作为表示'无”的值。根据C语言的传统,
`null`被设计成可以自动转为0。

```
Number(null)  //0
5 + null //5
```

但是, JavaScript的设计者Brendan Eich ,觉得这样做还不够,有两个原因。首先，`null`像在Java里一
样，被当成一个对象。 但是, JavaScript的值分成原始类型和合成类型两大类, Brendan Eich觉得表
示”无”的值最好不是对象。其欺, JavaScript的最初版本没有包括错误处理机制,发生数据类型不匹配时，
往往是自动转换类型或者默默地失败。Brendan Eich觉得,如果`null`自动转为0 ,很不容易发现错误。
因此, Brendan Eich又设计了一个`undefined`。他是这样区分的: `null `是一个表示” 无”的对象,转为数
值时为`0`; `undefined` 是一个表示”无”的原始值 ,转为数值时为`NaN`.

```
Number(undefined)  //NaN
5 + undefined //NaN
```

用下列运算符会返回布尔值:

```
两元逻辑运算符: && (And)， || (Or)
前置逻辑运算符: ! (Not)
相等运算符: ===，!== ，==，!=
比较运算符: >，>=，<，<=
```

如果JavaScript预期某个位置应该是布尔值,会将该位置上现有的值自动转为布尔值。转换规则是除了下
面六个值被转为`false` , 其他值都视为`true`。

```
undefined
null
false
0
NaN
""或''(空字符串)
```

布尔值往往用于程序流程的控制，请看 一个 例子。

```
if('') {
	console.log(true);
}
// 没有任何输出
```

上面代码的`if`命令后面的判断条件预期应该是一 个布尔值,所以JavaScript自动将空字符串 ,转为布尔
值`false` ,导致程序不会进入代码块,所以没有任何输出。
需要特别注意的是，空数组 (` []` )和空对象( `{}` )对应的布尔值,都是`true`。

```
if([]) {
	console.log(true);
}
// true
if({}) {
	console.log(true);
}
// true
```

在JavaScript内部,实际上存在2个`0`：一个是`+0` ,一个是`-0`。它们是等价的。

```
 
-0 === +0 // true
 0 === -0 // true
 0 === +0 // true
```

几乎所有场合 ，正零和负零都会被当作正常的`0`。

```
+0 // 0
-0 // 0
(-0).tostring() // '0'
(+0).tostring() // '0'
```

唯一有区别的场合是，`+0`或`-0`当作分母，返回的值是不相等的。

```
(1 / +0) === (1 / -0) // false
```

上面代码之所以出现这样结果，是因为除!以正零得到`+Infinity`，除以负零得到` -Infinity`，这两者是
不相等的（关于` Infinity` 详见后文）。



`NaN` 是 Javascript 的特殊值，表示“非数字”(Not a Number），主要出现在将字符串解析成数字出错的场
合。

```
5 - "x' // NaN
```

上面代码运行时，会自动将字符串`x`转为数值，但是由于 `×`不是数值，所以最后得到结果为 `NaN` ，表示它
是“非数字”( `NaN `)。
另外，一些数学函数的运算结果会出现 `NaN `.

```
Math.acos(2) // NaN
Math.1og(-1) // NaN
Math.sqrt(-1) // NaN
```

`0`除以`0`也会得到 `NaN`

```
0 / 0  // NaN
```

需要注意的是，`NaN` 不是一种独立的数据类型而是一种特殊数值，它的数据类型依然厲于 `Number`
使用`typeof` 运算符可以看得很清楚。

```
typeof NaN   // 'number'
```

#### 判断NaN的方法

`isNaN` 方法可以用来判断一个值是否为` NaN`

```
isNaN(NaN) // true
isNaN(123) // false
```

但是，`isNaN` 只对数值有效，如果传入其他值，会被先转成数值。比如，传入字符串的时候，字符串会被
先转成`NaN`，所以最后返回 `true`，这一点要特别引起注意。也就是说，`isNaN `为`true` 的值，有可能不
是`NaN`，而是一个字符串。

```
isNaN('Hello") // true
// 相当于
isNaN(Number('Hello')) // true
```

出于同样的原因，对于对象和数组，`isNaN `也返回` true`.

```
isNaN({}) // true
//等同于
isNaN(Number({})) // true
isNaN(['xzy']) // true
//等同于
isNaN(Number(['xzy'])) // true
```

但是，对于空数组和只有一个数值成员的数组， `isNaN` 返回 `false`

```
isNaN([]) // false
isNaN([123]) // false
isNaN(['123']) // false
```

上面代码之所以返回 `false`，原因是这些数组能被`Number` 函数转成数值，请参见《数据类型转换》
节。
因此，使用 `isNaN` 之前，最好判断一下数据类型

```
function myIsNaN (value) {
	return typeof value	===	'number' && isNaN (value);
}
```

判断`NaN` 更可靠的方法是，利用`NaN` 是JavaScript之中唯一不等于自身的值这个特点，进行判断

```
function myIsNaN (value) {
  return value !== value;
}
```

#### 字符串与数组

字符串可以被视为字符数组 ，因此可以使用数组的方括号运算符，用来返回某个位置的字符（位置编号从
0开始）。

```
var s='hello';
s[0] // "h"
s[1] // "e"
s[4] // "o"
// 直接对字符串使用方括号运算符
"hello'[1] //"e"
```

如果方括号中的数字超过字符串的长度，或者方括号中根本不是数字，则返回 `undefined`

```
"abc'[3] // undefined
"abc'[-1] // undefined
'abc'['x'] // undefined
```

但是，字符串与数组的相似性仅此而已。实际上，无法改变字符申之中的单个字符。

```
var s = 'hello';

delete s[0];
s // "hello"

s[1] = 'a';
s //"hello"

s[5] ="!";
s //"hello"
```

上面代码表示，宁符串内部的单个字符无法改变和增删，这此操作会默默地失败。
字符串也无法直接使用数组的方法，必须通过` call`方法间接使用。

```
var s = 'hello':
s.join('') // TypeError: s.join is not a function
Array.prototype.join.call(s,'')  //"h e l l o"
```

上面代码中，如果直接对字符串使用数组的` join `方法，会报错不存在该方法。但是，可以通过` call` 方
法，间接对字符串使用 `join `方法。
不过，由于字符串是只读的，那些会改变原数组的方法，比如`push()`、`sortr()`、`reverse()`、`splice()`都对字符串无效，只有将字符串显式转为数组后才能使用，参见《标准库》一章的数组部分



```
var o1	= {};
var o2 = o1:
o1 = 1;
o2 // {}
```

上面代码中，	`o1`和`o2`指向同一个对象，然后`o1 `的值变为1，这时不会对`o2`产生影响，`o2`还是指向原
来的那个对象。
但是，这种引用只局限于对象，对于原始类型的数据则是传值引用，也就是说，都是值的拷贝。

```
var x = 1:
var y = x;
x = 2;
y //1
```

上面的代码中，当x的值发生变化后，y 的值并不变，这就表示y和x并不是指向同-—个内存地址。

#### 表达式还是语句？

对象采用大括号表示，这导致了一个问题：如果行首是一个大括号，它到底是表达式还是语句？

```
{ foo: 123 }
```

JavaScript引擎读到上面这行代码，会发现可能有两种含义。第一种可能是，这是一个表达式，表示一个包含 `foo `属性的对象；第二种可能是 ，这是一个语句 ，表示一个代码区块，里面有一个标签`foo`，指向表
达式 `123`。
为了避免这种歧义 ，JavaScript规定，如果行首是大括号，一律解释为语句（即代码块）。如果要解释为
表达式（即对象），心须在大括号前加上圆括号。

```
({ foo: 123})
```

这种差异在` eval` 语句中反映得最明显

```
eval('{foo: 123}') 	// 123
eval('({foo: 123})') 	// {foo: 123}
```

上面代码中，如果没有圆括号，`eval `将其理解为一个代码块；加上圆括号以后，就理解成一个对象

#### 查看所有属性

查看一个对象本身的所有厲性，可以使用` object.keys` 方法。

```
var o = {
  key1: 1,
  key2: 2
};
Object.keys (o);
// ['key1', 'key2']
```

```
// 假设变量x未定义
// 写法一:报错
if (x) { return 1; }
// 写法二:不正确
if (window.x) { return 1; }
// 写法三:正确
if ('x' in window) { return 1; }
```

上面三种写法之中,如果`x`不存在,第一种写法会报错;如果`x`的值对应布尔值`false `(比如`x`等于空字符串) ,第二种写法无法得到正确结果;只有第三种写法,才能正确判断变量`x`是否存在。

`in`运算符的一个问题是,它不能识别对象继承的属性。

```
var o = new object();
o.hasOwnProperty('toString')   // false
'toString' in o   // true
```

上面代码中，`tostring`方法不是对象`o`自身的属性,而是继承的属性，`hasOwnProperty `方法可以说明这一点。但是，`in`运算符不能识别,对继承的属性也返回`true`。



任何类型的数据，都可以放入数组。

```
var arr = [
  {a: 1},
  [1, 2, 3],
  function() {return true;}
]:
arr[0] // Object {a: 1}
arr[1] // [1,2,3]
arr[2] // function (){return true;}
```

上面数组` arr `的3个成员依次是对象、数组、函数。
如果数组的元素还是数组，就形成了多维数组。

```
var a = [[1, 2], [3, 4]];
a[0][1] // 2
a[1][1] // 4
```

#### script标签

##### 工作原理

浏览器加载JavaScript脚本，主要通过`<script>`标签完成。正常的网页加载流程是这样的

1. 浏览器一边下载HTML网页，一 边开始解析
2. 解析过程中，发现`<script>`标签
3. 暂停解析，网页渲染的控制权转交给JavaScrip引擎
4. 如果`<script＞`标签引用了外部脚本，就下载该脚本，否则就直接执行
5. 执行完毕，控制权交还道染 引擎，恢复往下解析HTML网页

> 加载外部脚本时，浏览器会暂停页面渲染，等待脚本下载并执行完成后，再继续渲染。原因是Javascript
> 可以修改DOM（比如使用`document.write` 方法），所以必须把控制权让给它，否则会导致复杂的线程
> 竞赛的门题。
> 如果外部脚本加载时间很长（比如一直无法完成下载），就会造成网页长时间失去响应，浏览器就会呈
> 现“假死'状态，这被称为“阻塞效应”。
> 为了避免这种情况，较好的做法是将`<script>`标签都放在页面底部，而不是头部。这样即使遇到脚本失
> 去响应 ，网页主体的渲染也已经完成了 ，用户至少可以看到内容，而不是面对一张空白的页面。
> 如果某些脚本代码非常重要，一定要放在页面头部的话，最好直接将代码嵌入页面，而不是连接外部脚本
> 文件，这样自縮短加载时间。
> 将脚本文件都放在网页尾部力载，还有一个好处。在DOM结构生成之前就调用DOM , JavaScript会报错，如果脚本都在网页尾部加载，就不存在这个问题，因为这时DOM肯定已经生成了。

#### base-64 编码

[btoa()](https://www.runoob.com/jsref/met-win-btoa.html) 方法用于创建一个 base-64 编码的字符串

```
window.btoa(str)
```

[atob()](https://www.runoob.com/jsref/met-win-atob.html)方法用于解码使用 base-64 编码的字符串。

```
window.atob(encodedStr)
```

```
var str = "RUNOOB";
var enc = window.btoa(str);
var dec = window.atob(enc);
 
var res = "编码字符串为: " + enc + "<br>" + "解码后字符串为: " + dec;
```

```
function b64Encode(str) {
    return btoa(encodeURIComponent(str));
}

function b64Decode(str) {
    return decodeURIComponent(atob(str));
}
```



#### JavaScript的垃圾回收机制

- 标记清除(mark and sweep )

​	这是JavaSoript 最常见的拉圾回收方式。当变量进入执行环境的时候，比如在函数中声明一个变量，垃圾回收器将其标记为“进入环境”。当变量离开环境的时候（函数执行结束），将其标记为 “离开环境”。
​	垃圾回收器会在运行的时候给存储在内存中的所有变量加上标记，然后去掉环境中的变量，以及被环境中变量所引用的变量(闭包）的标记。在完成这些之后仍然存在的标记就是要删除的变量。

- 引用计数 (reference counting )

​		在低版本的IE中经常会发生内存泄漏，很多时候就是因为它采用引用计数的方式进行垃圾回收。引用计数的第略是跟踪记录每个值被使用的次数。当声明了一个变量并将一个引用类型赋值给该变量的时候，这个值的引用次数就加 1。如果该变量的值变成了另外一个，则这个值的引用次数減1。当这个值的引用次数变为 0的时候，说明没有变量在使用，这个值没法被访问。因此，可以将它占用的空间回收，这样垃圾回收器会在运行的时候清理引用次数为0的值占用的空间。
​		在IE 中虽然Javascript 对象通过标记清除的方式进行垃圾回收，但是BOM 与 DOM对象是用引用计数的方式回收垃圾的。也就是说，只要涉及 BOM 和DOM，就会出现循环引用问题。

#### DOM 节点的类型

- 整个文档是一个文档(Document）节点。
- 每个 HTML 标签是一个元素（ Element）节点。
- 每一个HTML 属性是一个属性（Attribute）节点。
- 包含在HTML元素中的文本是文本（Text）节点。

#### script 标签中 defer 和async 属性的区别

1. defer 属性规定是否延迟执行脚本，直到页面加载为止。async 属性规定脚本一旦可用，就异步执行
2. defer 并行加载Javaseript 文件，会按照页面上script 标签的顺序执行。async 并行加加载JavaScript 文件，下载完成立即执行，不会按照页面上script 标签的顺序执行。

#### 闭包

使用闭包主要是为了设计私有的方法和变量。闭包的优点是可以避免全局变量的污染；缺点是闭包会常驻内存，增加内存使用量，使用不当很容易造成内存泄漏。在Javascript 中，函数即闭包，只有函数才会产生作用域

闭包有3个特性：

1. 函数嵌套函数
2. 在函数内部可以引用外部的参数和变量
3. 参数和变量不会以垃圾回收机制回收

#### unshift()方法

该方法在数组启动时起作用，与push()不同。它将参数成员添加到数组的顶部。

```
var name=["Miohn"]
name.unshift("charlie");
name.unshift("joseph", "Jane");
console.log(name);
```

```
["joseph", "Jane", "charlie", "john"]
```

#### encodeURI()和 decodeURI()的作用

encodeURI()用于将 URL 转换为十六进制编码。而 decodeURI()用于将编码的 URL转换回正常 URL

#### 不建议在 JavaScript 中使用 innerHTML

通过 innerHTML 修改内容，每次都会刷新，因此很慢。在ianerHTML 中没有验证的机会，因此更容易在文档中插入错误代码，使网页不稳定。

#### 在不支持 Javascript 的旧浏览器中隐藏 JavaScript 代码

在`<script>`标签之后的代码中添加`“<!--”`，不带引号。
在`</script>`标签之前添加`“// -->”`，代码中没有引号。
旧浏览器现在将 JavaScript 代码视为一个长的HTML 注释，而支持 JavaSoript 的浏览器则将`“<!--”` 和`“// -->”`作为一行注释

#### 在DOM 操作中创建、添加、移除、替换、插入和查找节点

##### 创建新节点

```
createDocumentFragment()		// 创建一个 DOM 片段
createElement)							// 创建一个具体的元素
createlextNode()						// 创建一个文本节点
```

##### 添加、移除、替换、插入节点

```
appendchild()
removeChild()
replaceChild()
insertBefore()		// 并没有insertAfter()
```

##### 查找节点

```
getElementsByTagName()	// 通过标签名称查找节点
getElementsByName()			// 通过元素的 name 属性的值查找节点(IE容错能力较强，会得到一个数组，其中包括 id 等于name 值的节点)
getElementById()				// 通过元素id 查找节点，具有唯一性
```

#### 实现浏览器内多个标签页之间的通信

调用localstorge、cookie 等数据存储通信方式

#### null 和undefined 的区别

null 是一个表示“无”的对象，转为数值时为 0; undefined 是一个表示“无”的原始值，转为数值时为 NaN。

当声明的变量还未初始化时，变量的默认值为 undefined.

null 用来表示尚未存在的对象，常用来表示西数企图返回一个不存在的对象。

undefined 表示“缺少值”，即此处应该有一个值，但是还没有定义，典型用法是如下：

1. 如果变量声明了，但没有赋值，它就等于 undefined.
2. 当调用函数时，如果没有提供应该提供的参数，该参数就等于 undefined.
3. 如果对象没有赋值，该属性的值为 undefined.
4. 当函数没有返回值时，默认返回 undefined.

null 表示“没有对象”，即此处不应该有值，典型用法是如下：

1. 作为函数的参数，表示该函数的参数不是对象
2. 作为对象原型链的终点

#### new 操作符的作用

（1）创建一个空对象。

（2）由this 变量引用该对象。

（3）该对象继承该函数的原型（更改原型链的指向）。

（4）把属性和方法加入到this 引用的对象中

（5）新创建的对象由this 引用，最后隐式地返回this，过程如下

```
var obj = {};
obj.__proto__ = Base.prototype;
Base.call(obj);
```

#### Javascript 延迟加载的方式

包括 defer 和async、动态创建DOM（创建script，插入DOM 中，加裁完毕后回调、按需异步载入 JavaScript.

#### call()和apply()的区别和作用

作用都是在函数执行的时候，动态改变函数的运行环境（执行上下文)。

call 和apply的第一个参数都是改变运行环境的对象

区别如下：
call从第二个参数开始，每一个参数会依次传递给调用函数；apply 的第二个参数是数组，数组的每一个成员会依次传递给调用函数

```
func.call(funcl, varl, var2, var3)
```

对应的 apply 写法为：

```
func.apply(funcl, [varl, var2, var3])
```

#### 造成内存泄漏的操作

内存泄漏指不再拥有或需要任何对象（数据）之后，它们仍然存在于内存中

> 垃圾回收器定期扫描对象，并计算引用了每个对象的其他对象的数量。如果一个对象的引用数量为0（没有其他对象引用过该对象），或对该对象的唯一引用是循环的，那么该对象占用的内存立即被回收。

如果 setTimeout 的第一个参数使用字符串而非函数，会引发内存泄漏。
闭包、控制台日志、循环（在两个对象彼此引用旦彼此保留时，就会产生一个循环）等会造内存泄漏。

#### IE与Firefox 的不同之处

(1）IE支持 currentStyle; Firefox 使用getComputStyle。
(2）IE使用innerText; Firefox 使用 textContent。
(3）在透明度滤镜方面，IE 使用 filter:alpha(opacity= num); Firefox 使用-moz-opacity: num
(4）在事件方面，IE使用attachEvent；Firefox 使用 addEventListener。
(5）对于鼠标位置：IE 使用event.clientX； Firefox 使用 event.pagex。
(6）IE使用event.stcElement; Firefox 使用event.target。
(7）要消除list 的原点，IE 中仅须使margin: 0即可达到最终效果；Firetox 中需要设置margin:0, padding:0 和 list-style:none.
(8）CSS 圆角：IE7以下不支持圆角。

#### JavaScript 对象的几种创建方式

(1) 0bject 构造函数式。
(2）对象字面量式。
(3）工厂模式。
(4） 安全工厂模式。
(5）构造函数模式。
(6）原型模式。
(7）混合构造函数和原型模式。
(8）动态原型模式。
(9）寄生构造函数模式。
(10）稳妥构造函数模式。

#### 实现异步编程

​		方法 1，通过回调函数。优点是简单、容易理解和部署；缺点是不利于代码的阅读和维护，各个部分之间高度耦合度（ Coupling )，流程混乱，而且每个任务只能指定一个回调函数。

​		方法 2，通过事件监听。可以绑定多个事件，每个事件可以指定多个回调函数，且可以“去耦合”（Decoupling )，有利于实现模块化；缺点是整个程序都要变成事件驱动型，运行流程会变得很不清晰。

​		方法3，采用发布/订阅方式。性质与“事件监听”类似，但是明显优于后者。

​		方法4，通过Promise 对象实现。Promise 对象是CommonJS工作组提出的一种规范，旨在为异步编程提供统一接口。它的思想是，每一个异步任务返回一个 Promise对象，该对象有一个then 方法，允许指定回调函数。

#### Javascript 的同源策略

​		同源策略是容户端脚本（尤其是Javascript）的重要安全度量标准。它最早出自Netscape Navigator 2.0，目的是防止某个文档或脚本从多个不同源装载

​		这里的同源策略指的是协议、域名、端口相同。同源策咯是一种安全协议。指一段脚本只能读取来自同一来源的窗口和文档的属性

#### 同源限制的原因

我们举例说明。比如一个黑客，他利用Iframe 把真正的银行登录页面嵌到他的页面上，当你使用真实的用户名、密码登录时，他的页面就可以通过 JavaScript 读取到你表单上input 中的内容，这样黑客就会轻松得到你的用户名和密码

#### 在Javascript 中，函数是第一类对象

第一类函数即JavaSaript 中的函数。这通常意味着这些函数可以作为参数传递给其他函数，作为其他函数的值返回，分配给变量，也可以存储在数据结构中

#### 事件/IE 与Firefox 的事件机制的区别/阻止冒泡

​		事件是在网页中的某个操作（有的操作对应多个事件）。例如，当单击一个按钮时，就会产生一个事件，它可以被JavaSeript 侦测到。

​		在事件处理机制上，IE支持事件冒泡;Firefox 同时支持两种事件模型，也就是捕获型事件和冒泡型事件。

​		阻止方法是 ev.stopPropagation()。注意旧版IE 中的方法 ev.cancelBubble =true。

#### 函数声明与函数表达式的区别

在 JavaScript 中，在向执行环境中加載数据时，解析器对函数声明和函数表达式并非是一视同仁的。解析器会首先读取函数声明，并使它在执行任何代码之前可用（可以访问）。至于函数表达式，则必须等到解析器执行到它所在的代码行，才会真正解析和执行它。

#### 删除一个 cookie

为了删除 cookie，要修改expires

```
document.cookie = 'user=icketang;expires = ' + new Date(0)
```

#### 求一个字符串的长度（单位是字节)

假设一个英文字符占用一字节，一个中文字符占用两字节：

```
function GetBytes (str){
	var len = str.length;
	var bytes = len;
	for(var i =0; i<len; i++) {
		if (str.charcodeAt(i) ＞255 ) bxtes ++;
	}
  return bytes;
}
alert (GetBvtes ("he11o, 您好！"）;
```

#### 对于元素，atribute 和 property 的区别

​		attibute 是DOM 元素在文档中作为HTML标签拥有的属性；property 就是 DOM元素在 JavaScript 中作为对象拥有的属性

​		对于HTML 的标准属性来说，attribute 和 property 是同步的，会自动更新，但是对于自定义的属性来说，它们是不同步的

#### 延迟脚本在 JavaScript 中的作用

默认情况下，在页面加载期间，HITML代码的解析将暂停；直到脚本停止执行。这意味着，如果服务器速度较慢或者脚本特别 “沉重”，则会导致网页延迟。在使用Deferred 时，脚本会延迟执行，直到HTML 解析器运行。这缩短了网页的加载时间，并且它们的显示速度更快。

#### 闭包(closure )

```
function hello(){
  // 函数执行完毕，变量仍然存在
  var num = 100:
  var showResult= function () { alert (num); }
  num++;
  return showResult;
}
var showResult= hello();
showResult()		// 执行结果：弹出 101
```

执行 hello()后，hello()用包内部的变量会存在，而闭包内部函数的内部变量不会存在，使得 Javascript 的垃圾回收机制不会收回 hello()占用的资源，因为 hello()中内部函数的执行需要依赖hello()中的变量。

#### 判断一个对象是否属于某个类

使用instanceof 关键字，判断一个对象是否是类的实例化对象；使用constructor属性，判断一个对象是否是类的构造函数

#### JavaScript 中使用事件处理程序

事件是由用户与页面的交互（例如单击链接或填写表单）导致的操作。需要一个事件处理程序来保证所有事件的正确执行。事件处理程序是对象的额外属性。此属性包括事件的名称和事件发生时采取的操作。

#### 在Javascript 中有一个函数，执行直接对象查找时，它始终不会查找原型，这个函数是hasOwnProperty.

#### 在Javascript 中使用 DOM

DOM 代表文档对象模型，并且负责文档中各种对象的相互交互。DOM 是开发网页所必需的，其中包括诸如段落、链接等对象。可以操作这些对象，如添加或删除等。为此，DOM还需要向网页添加额外的功能。

#### document.write 和 innerHTML 的区别

document.write 重绘整个 页面；innerHTML可以重绘页面的一部分，

#### 在 JavaScript 中读取文件的方法

##### 读取服务器中的文件内容

```
function readAjaxFile (url){
  // 创建xhr
  var xhr	= new XMLHttpRequest();
  // 监听状态
  xhr.onreadystatechange	= function(){
  // 监听状态值是 4
  if(xhr.readyState === 4 && shr.status === 200){
    console.log (xhr.responseText)
    // 打开请求
    xhr.open("GET', url, true)
    //发送数据
    xhr.send(nul1)
  }
}
```

##### 读取本地计算机中的内容

```
function readInputFile(id){
  var file = document.getElementById(id).files[0];
  // 实例化 FileReader
  var reader = new FileReader();
  // 读取文件
  reader.readAsText(file)
  // 监听返回
  reader.onload = function(data) (
    console.log(data, this.result)
  }
}
```

#### 分配对象属性

将属性分配给对象的方式与赋值给变量的方式相同。例如，表单对象的操作值以下列方式分配给"submit"：document.form.action ="submit"

#### 书写 JavaScript 语句的基本规范

1. 不要在同一行声明多个变量。
2. 应使用===/!==来比较true/false 或者数值。
3. 使用对象字面量替代new Array这种形式。
4. 不要使用全局函数。
5. switch 语句必须带有default 分支。
6. 函数不应该有时有返回值，有时没有返回值。
7. for循环必须使用大括号括起来。
8. 语句必须使用大括号括起来
9. for in 循环中的变量应该使用 var 关键字明确限定的作用域，从而避免作用域污染

#### 保留三位小数并四舍五入

```
const rounded = Math.round(val * 1000) / 1000;
```

[jquery判断页面滚动条(scroll)是上滚还是下滚，且是否滚动到头部或者底部](https://www.haorooms.com/post/jquery_scroll_upanddown)