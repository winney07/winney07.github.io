---
title: Web阅读器开发-笔记
date: 2021-01-29 15:55:19
tags:
---



[课程链接](https://www.imooc.com/video/17794)

#### 课程介绍

- 了解阅读器工作原理，了解epub格式的解析原理
- 运用Vue.js+epub.js实现一个简单的阅读器
- 实现阅读器的基础功能，如字号选择、背景色选择等

#### 课程安排

1. 阅读器原理学习
2. 搭建vue-cli环境
3. 编写阅读器源码
4. 总结学习知识点

#### 知识点解析

##### 阅读器

- 阅读器的工作原理

  - 工作流程

  - 阅读器引擎

- 常见电子书格式

- epub格式电子书解析原理
  - mimetype
  - container.xml
  - content.opf
  - toc.ncx

##### vue

- transition过渡
- 组件化
- class与style
- 绑定父组件与子组件通信
- 子组件与父组件通信
- nextTick0方法
- dom操作

##### epub.js

- epub下载
- Book
- Rendition
- Theme

#### scss

- import
- function
- mixin
- 变量

#### css

- 伪类和伪元素
- resetcss
- 定位
- 过渡动画
- flex布局

#### 阅读器工作原理简介

1. 电子书

   - txt

   - pdf

   - epub

   - mobi
   - .....

2. 阅读器引擎

   2.1 解析

   - 书名
   - 作者
   - 目录
   - 封面
   - 章节

   2.2 渲染

3. 功能

   - 字号
   - 背景色
   - 目录
   - 书签
   - 笔记
   - .....

#### ePub和mobi

- ePub(Electronic Publication)电子出版物
- mobi是Amazon Kindle的电子书格式

#### 开发流程

1. 开发准备
2. vue-cli
3. 依赖包下载
4. 项目配置
5. 阅读器解析
6. 阅读器渲染
7. 翻页功能
8. 字号背景
9. 进度条
10. 目录

#### 开发准备+搭建Vue脚手架

- 安装Node.js和Vue.js环境
- 通过vue init搭建Vue脚手架
- 通过VSCode打开项目，使用npm run dev启动项目

> 下载脚手架模板： https://github.com/vuejs-templates/webpack

#### viewport配置

- viewport用来设置用户在手机上的可视区域
- width=device-width :指定viewport宽度为设备宽度，initial-scale=1.0∶指定默认缩放比例为1:1
- 通过maximum-scale和minimum-scale限定屏幕缩放比例为1:1通过user-scalable限制用户对屏幕进行缩放

> 在dom加载完毕之后，动态设置根元素的font-size

#### rem配置

- rem是css3新增的一个相对长度单位

- rem的值相当于根元素font-size值的倍数

  1rem =根元素font-size
  2rem =根元素font-size * 2

- DOMContentLoaded事件动态设置根元素font-size

  html.style.fontSize = window.innerWidth / 10 + 'px'

```
export default {name: 'App'}
document.addEventListener('DOMContentLoaded',()=> {
    const html = document.querySelector('html')
    let fontSize = window.innerwidth / 10
    fontSize = fontSize > 50 ? 50 : fontSize
    html.style.fontSize = fontSize + 'px'
});
```

#### reset.scsS和global.scss

- reset.scss的目的是为了消除不同浏览器默认样式的不一致性
- global.scss规定了整个站点的公共样式、公共方法和公共参数等
- 实现px2rem方法，将px转化为rem

```
Reset.css :https://meyerweb.com/eric/tools/css/reset/
```

