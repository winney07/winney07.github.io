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