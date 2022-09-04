---
title: Javascript相关笔记
date: 2019-09-04 11:31:48
tags:
- Javascript
---

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
