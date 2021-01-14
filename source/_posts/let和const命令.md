---
title: let和const命令
date: 2019-07-04 18:57:38
tags:
- 阮一峰-ES6
categories: 
- 工作笔记
- 阮一峰-ES6
---
### 1.let命令
#### 基本用法
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
#### 不存在变量提升
#### 暂时性死区
只要块级作用域内存在let命令，它所声明的变量就“绑定”（binding）这个区域，不再受外部的影响。
```bash
var tmp = 123;

if (true) {
  tmp = 'abc'; // ReferenceError
  let tmp;
}
```

这样的设计是为了让大家养成良好的编程习惯，变量一定要在声明之后使用，否则就报错。

#### 不允许重复声明
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
#### ES6的块级作用域
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
#### 块级作用域与函数声明
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

### const命令
#### 基本用法
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
#### 本质
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