---
title: ECMAScript 6简介
date: 2019-07-04 16:00:29
tags:
- 阮一峰-ES6
categories: 
- 工作笔记
- 阮一峰-ES6
---
{% link 阮一峰-ECMAScript 6 http://es6.ruanyifeng.com/ %} 

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

