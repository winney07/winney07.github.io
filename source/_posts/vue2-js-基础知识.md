---
title: vue2.js 基础知识
date: 2019-06-19 15:53:43
tags:
- 《Vue2实践揭秘》
categories:
- 工作笔记
- 《Vue2实践揭秘》
---
#### vue特点
```bash
一个Vue实例必须与一个页面元素绑定

*.vue是Vue.js特有的文件格式，表示的就是一个Vue组件，被称为单页式组件

Vue2具有很高的兼容性，我们也可以用".js"文件来单纯地定义组件的逻辑，
甚至可以使用React 的JSX格式的组件（需要babel-plugin-transform-vue-jsx支持）

注： 从Vue2开始，组件模板必须且只能有一个顶层元素，如果在组件模板内设置多个顶层元素将会引发编译异常。

```
<!--more-->
#### 单页组件由一下三部分组成：
```bash
<template></template> ——视图模板
<style></style> ——组件样式表
<script></script> ——组件定义
```
#### data使用函数返回是为了可以具有更高的灵活性
```bash
export default {
  name: '',
  data() { 
    return {
        
    }
  }
}
```
#### 使用less（直接使用CSS语法来编写样式表，代码量大）
```bash
npm i less style-loader css-loader less-loader -D

在/assets/中添加一个todos.less文件，并在App.vue的组件定义内引入less样式表

import './assets/todo.less'

注：通过import将样式文件导入是一种全局性的做法，也就是说，在每一个页面内的
<head></head>中都会有一个样式表，这样做的缺点是很容易导致样式冲突。如果希
望样式表仅应用于当前组件，可以使用<style scoped></style>，然后用css的
@import导入样式表：

<style scoped>
    @import './assets/todos.less'
</style>

```
#### 注：如果在元素属性中不加上":",Vue认为是向这个属性赋上字符串值而不是Vue组件上定义的属性引用！

注：无论是绑定的是样式类还是样式属性，:class和:style表达式内一定是一个JSON对象。
如： :class="{'btn': true}"     :style="{'color': 'red'}"
:class的JSON对象的值一定是布尔型的，true表示加上样式，false表示移除样式类。
:style的JSON对象则像是一个样式配置项，key声明属性名，value则是样式属性的具体值。

#### 时间格式化专用的包——moment.js
```bash
npm i moment -S

引入moment,并设定moment的区域为中国
import moment from 'moment'
import 'moment/locale/zh-cn'
moment.locale('zh-cn')

加入date的过滤器

export default {
    //省略.....
    filters: {
        date(val) {
            return moment(val).calendar()
        }
    }
}

在模板上应用过滤器
<time> {{ todo.created | date}}</time>

注：在所有的过滤器中是没有this引用的，过滤器内的this是一个undefined的值，所以要在过滤器内尝试引用组件实例内的变量或方法，否则会引发空值引用的异常。
```

<-- 参考《vue2实践揭秘> -->