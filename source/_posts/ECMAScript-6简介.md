---
title: ECMAScript 6简介
date: 2019-07-04 16:00:29
tags:
- 阮一峰-ES6
categories: 
- 工作笔记
- 阮一峰-ES6
---
[阮一峰-ECMAScript 6](http://es6.ruanyifeng.com/)

ECMAScript 6.0（以下简称 ES6）。2015 年 6 月正式发布
#### ES6 与 ECMAScript 2015 的关系
ES6 的第一个版本，就这样在 2015 年 6 月发布了，正式名称就是《ECMAScript 2015 标准》（简称 ES2015）。
ES6 既是一个历史名词，也是一个泛指，含义是 5.1 版以后的 JavaScript 的下一代标准，涵盖了 ES2015、ES2016、ES2017 等等，而 ES2015 则是正式名称，特指该年发布的正式版本的语言标准。本书中提到 ES6 的地方，一般是指 ES2015 标准，但有时也是泛指“下一代 JavaScript 语言”。

#### 部署进度
各大浏览器的最新版本，对 ES6 的支持可以查看{% link 点这里前往  http://kangax.github.io/compat-table/es6/ %} 
Node 是 JavaScript 的服务器运行环境（runtime）。

#### Babel转码器
##### 1、安装Babel
```bash
npm install --save-dev @babel/core
```
##### 2、配置文件.babelrc
（使用命令行创建.babelrc文件）
Babel 的配置文件是.babelrc，存放在项目的根目录下。使用 Babel 的第一步，就是配置这个文件。
```bash
{
    "presets": [],
    "plugins": []
}
```
3、presets字段设定转码规则，官方提供以下的规则集，你可以根据需要安装。
```bash
# 最新转码规则
npm install --save-dev @babel/preset-env

# react 转码规则
npm install --save-dev @babel/preset-react
```
4、然后，将这些规则加入.babelrc。
```bash
{
    "presets": [
      "@babel/env",
      "@babel/preset-react"
    ],
    "plugins": []
}
```
注意，以下所有 Babel 工具和模块的使用，都必须先写好.babelrc。
##### 命令行转码
Babel 提供命令行工具@babel/cli，用于命令行转码。
5、安装命令：
```bash
npm install --save-dev @babel/cli
```
基本用法如下:
```bash
# 转码结果输出到标准输出
npx babel example.js

# 转码结果写入一个文件
# --out-file 或 -o 参数指定输出文件
npx babel example.js --out-file compiled.js
# 或者
npx babel example.js -o compiled.js

# 整个目录转码
# --out-dir 或 -d 参数指定输出目录
npx babel src --out-dir lib
# 或者
npx babel src -d lib

# -s 参数生成source map文件
npx babel src -d lib -s
```
6、如：npx babel es6.js -o es5.js



```
var obj1 = {name: 'yangyanyi'};
var obj2 = {name: 'yangyanyi'};

console.log(obj1 == obj2);  //因为指向的地址不一样

var obj3 = {age: 12};
var obj4 = obj3;

console.log(obj3 == obj4);  //指向同一个地址
```

```
// 包装类
// 自动创建的基本包装类型的对象，则只存在于一行代码的执行瞬间，然后立即被销毁
var s1 = 'some text';
s1.color = 'red';
console.log(s1.color);  //undefined

//使用new操作符创建的引用类型的实例，在执行流离开当前作用域之前都一直保存在内存中。
var s2 = new String('some text');
s2.color = 'red';
console.log(s2.color);
```

```
//可以通过new操作符显式创建包装对象
//两种方式显式创建包装类型的方式：
//Object方式
var a = new Object('abc');
//构造函数方式
var a = new String('abc');

// 常常使用“逻辑或运算符”给省略的参数设置一个合理的默认值

function add(x, y) {
    y = y || 2;
    console.log(x, y);
}
add(1);
```

```
let [a, b, c] = [1, 2, 3];
console.log(a, b, c);

let [x, , y] = [1, 2, 3];
console.log(x, y);

let[head, ...tail] = [1, 2, 3, 4];
console.log(head, tail);

let [q, w, ...e] = ['a'];
console.log(q, w, e);

// let [foo] = {};  //报错

let [l, m, n] = new Set(['a', 'b', 'c']);
console.log(l, m, n);

// ES6内部使用严格相等运算符（===），判断一个位置是否有值。所以只有当一个数组成员严格等于undefined，默认值才会成效

let [x = 1] =[undefined];

let [ y = 1] = [null];

console.log(x, y);  //1  null   
// 原因：因为null不严格等于undefined，所以默认值不会生效
```

```
// 对象的结构赋值            
let  { foo, bar } = { foo: 'aaa', bar: "bbb"};
console.log(foo, bar);

// 不是按照顺序，是根据键名
let { bbb, aaa } = { aaa: 'aaa', bbb: 'bbbb'};
console.log(aaa, bbb);

let { baz } = { bnv:'bnv', kjl: 'kjl'};
console.log(baz);

// 当变量名与属性名不一致，必须写成下面这样
let { foo: baz } = { foo: 'aaa', bar: 'bbb'};
console.log(baz);

let obj = { first: 'hello', last: 'world'};
let { first: f, last: l} = obj;
console.log(f, l);

let { foo: baz } = { foo: 'aaa', bar: 'bbb'};
console.log(baz, foo);    //foo is not defined
// 原因：foo是匹配的模式，baz才是变量。真正被赋值的是变量baz，而不是模式foo
```



### [let和const 命令](https://es6.ruanyifeng.com/#docs/let)

#### 1.let命令

##### 基本用法

所声明的变量，只在let命令所在的代码块内有效

```bash
{
  let a = 10;
  var b = 1;
}

a // ReferenceError: a is not defined.
b // 1
```

for循环的计数器，就很适合使用let命令

```bash
for (let i = 0; i < 10; i++) {
  // ...
}

console.log(i);
// ReferenceError: i is not defined
```

```bash
var a = [];
for (var i = 0; i < 10; i++) {
  a[i] = function () {
    console.log(i);
  };
}
a[6](); // 10
```

```bash
var a = [];
for (let i = 0; i < 10; i++) {
  a[i] = function () {
    console.log(i);
  };
}
a[6](); // 6
```

for循环还有一个特别之处，就是设置循环变量的那部分是一个父作用域，而循环体内部是一个单独的子作用域。

```bash
for (let i = 0; i < 3; i++) {
  let i = 'abc';
  console.log(i);
}
// abc
// abc
// abc
```

##### 不存在变量提升

##### 暂时性死区

只要块级作用域内存在let命令，它所声明的变量就“绑定”（binding）这个区域，不再受外部的影响。

```bash
var tmp = 123;

if (true) {
  tmp = 'abc'; // ReferenceError
  let tmp;
}
```

这样的设计是为了让大家养成良好的编程习惯，变量一定要在声明之后使用，否则就报错。

##### 不允许重复声明

let不允许在相同作用域内，重复声明同一个变量。

```bash
// 报错
function func() {
  let a = 10;
  var a = 1;
}

// 报错
function func() {
  let a = 10;
  let a = 1;
}
```

因此，不能在函数内部重新声明参数。

```bash
function func(arg) {
  let arg;
}
func() // 报错

function func(arg) {
  {
    let arg;
  }
}
func() // 不报错
```

##### ES6的块级作用域

```bash
// IIFE 写法
(function () {
  var tmp = ...;
  ...
}());

// 块级作用域写法
{
  let tmp = ...;
  ...
}
```

##### 块级作用域与函数声明

允许在块级作用域内声明函数。
函数声明类似于var，即会提升到全局作用域或函数作用域的头部。
同时，函数声明还会提升到所在的块级作用域的头部。

考虑到环境导致的行为差异太大，应该避免在块级作用域内声明函数。如果确实需要，也应该写成函数表达式，而不是函数声明语句。

```bash
// 块级作用域内部的函数声明语句，建议不要使用
{
  let a = 'secret';
  function f() {
    return a;
  }
}

// 块级作用域内部，优先使用函数表达式
{
  let a = 'secret';
  let f = function () {
    return a;
  };
}
```

另外，还有一个需要注意的地方。ES6 的块级作用域必须有大括号，如果没有大括号，JavaScript 引擎就认为不存在块级作用域。

```bash
// 第一种写法，报错
if (true) let x = 1;

// 第二种写法，不报错
if (true) {
  let x = 1;
}
```

上面代码中，第一种写法没有大括号，所以不存在块级作用域，而let只能出现在当前作用域的顶层，所以报错。第二种写法有大括号，所以块级作用域成立。

函数声明也是如此，严格模式下，函数只能声明在当前作用域的顶层。

```bash
// 不报错
'use strict';
if (true) {
  function f() {}
}

// 报错
'use strict';
if (true)
  function f() {}
```

#### const命令

##### 基本用法

const声明一个只读的常量。一旦声明，常量的值就不能改变。

```bash
const PI = 3.1415;
PI // 3.1415

PI = 3;
// TypeError: Assignment to constant variable.
```

上面代码表明改变常量的值会报错。

<b>const声明的变量不得改变值，这意味着，const一旦声明变量，就必须立即初始化，不能留到以后赋值。</b>

```bash
const foo;
// SyntaxError: Missing initializer in const declaration
```

上面代码表示，对于const来说，只声明不赋值，就会报错。

const的作用域与let命令相同：只在声明所在的块级作用域内有效。

```bash
if (true) {
  console.log(MAX); // ReferenceError
  const MAX = 5;
}
```

上面代码在常量MAX声明之前就调用，结果报错。

const声明的常量，也与let一样不可重复声明。

```bash
var message = "Hello!";
let age = 25;

// 以下两行都会报错
const message = "Goodbye!";
const age = 30;
```

##### 本质

const实际上保证的，并不是变量的值不得改动，而是变量指向的那个内存地址所保存的数据不得改动。

```bash
const foo = {};

// 为 foo 添加一个属性，可以成功
foo.prop = 123;
foo.prop // 123

// 将 foo 指向另一个对象，就会报错
foo = {}; // TypeError: "foo" is read-only
```

如果真的想将对象冻结，应该使用Object.freeze方法。

```bash
const foo = Object.freeze({});

// 常规模式时，下面一行不起作用；
// 严格模式时，该行会报错
foo.prop = 123;
```

