---
title: Vue2-基础知识
date: 2021-02-20 10:56:26
tags:
- 《Vue2实践揭秘》
categories:
- 工作笔记
- 《Vue2实践揭秘》
---

#### 找相关资源

vue.js官网的资源列表中的[awesome -vue](https://github.com/vuejs/awesome-vue)里面

#### vue特点

```
一个Vue实例必须与一个页面元素绑定

*.vue是Vue.js特有的文件格式，表示的就是一个Vue组件，被称为单页式组件

Vue2具有很高的兼容性，我们也可以用".js"文件来单纯地定义组件的逻辑，
甚至可以使用React 的JSX格式的组件（需要babel-plugin-transform-vue-jsx支持）

注： 从Vue2开始，组件模板必须且只能有一个顶层元素，如果在组件模板内设置多个顶层元素将会引发编译异常。
```

#### 单页组件由一下三部分组成：

```
<template></template> ——视图模板
<style></style> ——组件样式表
<script></script> ——组件定义
```

#### data使用函数返回是为了可以具有更高的灵活性

```
export default {
  name: '',
  data() { 
    return {
        
    }
  }
}
```

#### 使用less（直接使用CSS语法来编写样式表，代码量大）

```
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

```
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

参考《vue2实践揭秘》

#### 邂逅 Vue.js

##### 为什么学Vuejs？

项目需求、公司要求

##### 简单认识一下Vuejs

- 渐进式框架		

- vuejs全家桶：Core + Vue + router + Vuex			

- 特点和常见高级功能

  - 解耦视图和数据

  - 可复用的组件

  - 前端路由技术

  - 状态管理

  - 虚拟DOM


- 学习Vuejs的前提
  	- 从零学习Vue开发，不需要angular，react基础，甚至jQuery经验
  - 具备一定的HTML，CSS，Javascript基础

#### Vue.js安装

一、直接CDN引入

1、开发环境版本，包含了有帮助的命令行警告

```
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
```

2、生产环境版本，优化了尺寸和速度

	<script src="https://cdn.jsdelivr.net/npm/vue@2.6.0"></script>	

二、下载和引入

1、开发环境

https://cn.vuejs.org/js/vue.js
2、生产环境
https://cn.vuejs.org/js/vue.min.js

三、NPM安装
最新稳定版

```
npm install vue
```

#### Hello Vuejs

响应式（当数据发生改变的时候，界面内容发生改变）

```
const app = new Vue({
     el: '#app',
     data: {
     },
    methods: {
    }
})
```

案例：计数器
v-on:click简写： @click

#### Vue中的MVVM

#### 创建Vue实例传入的options

- el
- data（组件当中data必须是一个函数）
- methods
- 函数与方法的区别

#### Vue的生命周期

####  模板语法

```
缩进2个空格更合适也可以缩进4个空格

mustache语法中，不仅仅可以直接写变量，也可以写简单的表达式
1：{{firstName + ' ' + lastName}}
2：{{firstName}}  {{lastName}}

v-once（不想响应式显示内容时）

v-html（显示标签内容）	

v-text

v-pre（原封不动显示该内容）

v-cloak（数据没有加载出来时，不显示{{}}）

v-bind

- 动态绑定属性
- v-bind:src  简写： ：src
- 动态绑定class类名
  :class="{active: isActive, line: isLine}"
- 动态绑定style
```

#### 计算属性

#### Object侦测

![Object侦测](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/Vue2-%E5%9F%BA%E7%A1%80%E7%9F%A5%E8%AF%86/Object%E4%BE%A6%E6%B5%8B.png)