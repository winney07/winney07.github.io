---
title: 《Vue.js前端开发技术》
date: 2020-06-15 11:12:57
tags:
- Vue.js
categories: 
- 前端开发框架
- Vue.js
---
## 第1章 Vue入门
Vue.js是构建Web界面的JavaScript库，也是一个通过简洁的API提供高效数据绑定和灵活组件的系统。

Weex

#### 主要特点
1. 轻量级的框架
2. 双向数据绑定
    声明式渲染是数据双向绑定的主要体现，同样也是Vue.js的核心
3. 指令
4. 组件化
    是Vue.js最强大的功能之一，可大量减少代码编写量，组件还支持热重载（当我们做了修改时，不会刷新页面，只是对组件本身进行立刻重载，不会影响整个应用当前的状态。CSS也支持热重载。）
5. 客户端路由
    Vue-router的Vue.js官方的路由插件
6. 状态管理
    就是一个单向的数据流,State驱动View的渲染，而用户对View进行操作产生Action,使State产生变化，从而使View重新渲染，形成一个单独的组件

#### Vue.js的优势
与其他几个框架比，最轻量化

npm速度慢的话，可以使用淘宝镜像安装

#### Vue-cli
vue-cli脚手架是Vue.js提供的一个官方命令行工具，用于快速搭建大型单页应用

创建项目——进入项目目录安装依赖项——运行项目

#### 项目文件目录结构
```
├── build               ——保存webpack的基本配置
├── config              ——保存项目基本配置
├── node_modules        ——npm加载的项目依赖的模块
├── src                 ——我们要开发的目录           
├    |——assets          ——放置图片
├    |——common          ——存放字体文件和通用的样式文件
├    |——components      ——放组件文件
├    |——App.vue         ——项目入口文件
├── static              ——放置静态资源目录
├── index.html          ——首页入口文件
├── package.json        ——项目配置文件
```

#### 数据挂载
```
created() {} ——> mounted() {} ——>  updated () {}
```

#### MVVM模式
Model-View-ViewModelD 的缩写，是基于前端开发的架构模式
**专注于View层**
它的核心是MVVM中的VM，也就是ViewModel,负责连接View和Model，保证视图和数据的一致性
**ViewModel是Vue.js的核心，它是一个Vue实例。**

DOM Listeners 和Data Bindings看作两个工具，是实现双向绑定的关键。

## 第2章 Vue数据绑定
### Vue模板语法
#### 模板语法
```
mustache 语法 “{{ }}”
```

#### 插值
```
<p>你好： {{ name }}</p>

如果要插入html要使用v-html

<div v-html="message"></div>

message: '用户名<input type="text" value=""/>'
（这里不支持换行，如果要换行，用单引号括起来后用+号连接
```
#### 表达式
Vue支持JavaScript的所有表达式
```
{{ number + 1}}
{{ ok ? 'yes' : 'no' }}
{{ number + 1}}
{{ message.split('').reverse().join('') }}
<div v-bind:id="'list-' + id"></div>
```
但有一个限制，每个绑定都只能包含单个表达式，所以下面的例子都不会生效。
```
<!-- 这是语句，不是表达式 -->
{{ var a = 1}}
<!-- 流控制也不会生效，请使用三元表达式 -->
{{ if (ok) { return message } }}
```
只适用简单的表达式，复杂的可以使用computed

### 响应式声明渲染机制
Vue是一个响应式系统，模型(Model)层只是普通的JavaScript对象，修改它则视图(View)自动更新。Vue的工作原理是当把一个普通的JavaScript对象传给Vue实例的data选项时，Vue的工作原理是一个普通的JavaScript对象传给Vue实例的data选项时，Vue会遍历此对象的所有属性，在属性被访问和修改时通知变化，并把数据渲染进DOM。

#### 响应式声明渲染机制简介
采用简洁的模板语法声明式地将数据渲染进DOM的系统。
使用v-model绑定输入框

#### Vue属性绑定
```
<a href= {{ url}}></a>
运行后会发现并没有生成超链接

要使用v-bind绑定

<a v-bind:href="url"></a>
<a :href="url"></a>
```

#### Vue双向数据绑定
一种是表达式绑定，一种是属性名也是一种指令，如v-model就是双向绑定

### Vue计算属性
#### 计算属性
computed，有缓存功能，可防止复杂计算逻辑多次调用引起的性能问题
```
computed: {
  totalPrice() {
    return (this.book.price*this.book.count)*this.discount + this.deliver
  }
}

通过计算属性的使用，view层的代码会变得非常精简，且容易维护。
```
```
  firstName: 'Foo',
  lastName: 'Bar',

   computed: {
    fullname: {
      //gettet
      get() {
        return this.firstName + ' ' + this.lastName
      },
      //setter
      set(newValue) {
        var names = newValue.split(' ');
        this.firstName = names[0];
        this.lastName = names[names.length - 1];
      },
    }
  }

  在浏览器控制层输入vm.fullname = 'menu Bar'，再输出vm.firstName是menu，vm.lastName是Bar。
  setter和getter的区别在于，setter是当computed这个属性的值变化时所触发。
```

#### 计算属性与methods的区别
计算属性只有在它的相关依赖发生变化时才回重新求值。这意味着只要book的属性还没有发生改变，多次访问totalPrice计算属性会立即返回之前的计算结果，而不必再次执行函数。

相比之下，每当触发重新渲染时，调用方法将总是再次执行函数。为什么需要缓存？假设有一个性能开销比较大的计算属性，需要遍历一个巨大的数组并做大量的计算，然后又缓存，所以每次访问都要重新执行。如果你不需要缓存功能，就使用methods。

计算属性的特点：

1. 计算属性使数据处理结构清晰
2. 依赖于数据，若数据更新，则处理结果自动更新
3. 计算属性内部this指向vm实例
4. 在模板调用时，直接写计算属性名即可。
5. 常用的是getter方法，用于获取数据，也可以使用setter方法改变数据
6. 相较于methods，不管改变依赖的数据是否改变，methods都会重新计算，但是依赖数据不变的时候，computed从缓存中获取，不会重新计算。

### Vue生命周期
#### Vue生命周期详解
activated：需要配合动态组件keep-alive属性使用，在动态组件初始化渲染的过程中调用该方法
deactivated：需要配合动态组件keep-alive属性使用，在动态组件初始化移出的过程中调用该方法

#### Vue各生命周期适合开发的业务逻辑
```
created：进行AJAX请求异步数据的获取、初始化数据
mounted：挂载元素内DOM节点的获取
nextTick： 针对单一事件更新数据后立即操作DOM
updated：数据更新的统一业务逻辑处理
watch：监听具体数据变化，并做相应的处理
```

## 第3章 Vue指令
### Vue指令概述
#### 指令
```
<p v-if="flag">插入或移除<p>标签</p>
```
#### 指令修饰符
```
"."表示特殊后缀，表示指令应该以特殊的方式绑定
<from v-on:submit.prevent="check"></from>

.prevent 阻止表单默认的提交行为，相当于调用了事件的event.preventDefault()

.stop 修饰符将阻止事件向上冒泡，相当于调用了事件的event.stopPropagation()
```

### Vue指令详解
#### v-if
根据表达式的值在DOM中生成或移除一个元素
注意：v-if是一个指令，需要添加到一个元素上才有效，如果想要切换多个元素，可以把<template>元素当作包装元素，使用v-if来切换元素

```
<!-- <template>是Vue的容器元素，目前不支持v-show，但支持v-if -->

<template v-if="flag">
  <h1>通知</h1>
  <p>限时免费</p>
  <p>全场店庆5折起</p>
</template>
```

**v-else**
```
<span v-if="ok">
  当ture时，显示本内容
</span>
<span v-else>
  当flase时，显示本内容
</span>
```

**v-else-if**
```
<span v-if="type== 'A'">
  A
</span>
<span v-else-if="type== 'B'">
  B
</span>
<span v-else-if="type== 'C'">
  C
</span>
<span v-else>
  NOT A/B/C
</span>
```

### 指令v-for
根据一组数组的选项列表进行渲染，需要用一个item in items的特殊语法，items是源数据数组，item是数组元素迭代的别名。
#### v-for 迭代数组
```
<li v-for="item in items" :key="item.message">
  {{ item.message }}
</li>

items: [
  { message: 'Foo' },
  { message: 'Bar' }
]
```
**[官网文档](https://cn.vuejs.org/v2/guide/list.html)**
#### v-for 迭代对象

```
（4）整数迭代
<span v-for="n in 10"> {{ n }}</span>
```
#### v-for Template
利用带有 v-for 的 <template> 来循环渲染一段包含多个元素的内容,template标签不显示，只是起到了包裹作用。
```
<ol>
  <template v-for="item in items">
    <li>{{ item.msg }}</li>
    <p class="divider" role="presentation"></p>
  </template>
</ol>
```

#### v-on
v-on指令绑定一个事件监听器
**[官网文档-事件处理](https://cn.vuejs.org/v2/guide/events.html)**
```
<button v-on:click="warn('Form cannot be submitted yet.', $event)">
  Submit
</button>

warn: function (message, event) {
  // 现在我们可以访问原生事件对象
  if (event) {
    event.preventDefault()
  }
  alert(message)
}
```
事件修饰符
```
<!-- 阻止单击事件继续传播 -->
<a v-on:click.stop="doThis"></a>

<!-- 提交事件不再重载页面 -->
<form v-on:submit.prevent="onSubmit"></form>

<!-- 修饰符可以串联 -->
<a v-on:click.stop.prevent="doThat"></a>

<!-- 只有修饰符 -->
<form v-on:submit.prevent></form>

<!-- 添加事件监听器时使用事件捕获模式 -->
<!-- 即内部元素触发的事件先在此处理，然后才交由内部元素进行处理 -->
<div v-on:click.capture="doThis">...</div>

<!-- 只当在 event.target 是当前元素自身时触发处理函数 -->
<!-- 即事件不是从内部元素触发的 -->
<div v-on:click.self="doThat">...</div>
```
按键修饰符
.enter
.tab
.delete (捕获“删除”和“退格”键)
.esc
.space
.up
.down
.left
.right

系统修饰键
.ctrl
.alt
.shift
.meta

#### v-show
控制元素的显示隐藏，即控制元素的display，v-hide与v-show相反

v-if有更高的切换消耗，而v-show有更高的初始渲染消耗，因此，如果需要频繁切换，则使用v-show较好；
如果在运行时条件不大可能改变，则使用v-if较好。

### Vue动态样式绑定
#### v-bind绑定class
**[官网文档-绑定HTML Class](https://cn.vuejs.org/v2/guide/class-and-style.html)**
```
<!-- 采用对象表达式 -->
<div
  class="static"
  v-bind:class="{ active: isActive, 'text-danger': hasError }"
></div>

data: {
  isActive: true,
  hasError: false
}


<div v-bind:class="classObject"></div>
data: {
  classObject: {
    active: true,
    'text-danger': false
  }
}

或：
computed: {
  classObject: function () {
    return {
      active: this.isActive && !this.error,
      'text-danger': this.error && this.error.type === 'fatal'
    }
  }
}

<!-- 数组表达式 -->
<div v-bind:class="[activeClass, errorClass]"></div>

data: {
  activeClass: 'active',
  errorClass: 'text-danger'
}

<div v-bind:class="[isActive ? activeClass : '', errorClass]"></div>
```
#### 绑定内联样式
```
<div v-bind:style="{ color: activeColor, fontSize: fontSize + 'px' }"></div>
```

### Vue表单输入绑定
**[官网文档-表单输入绑定](https://cn.vuejs.org/v2/guide/forms.html)**

#### v-model
#### 修饰符
##### .lazy
```
在默认情况下，v-model 在每次 input 事件触发后将输入框的值与数据进行同步 (除了上述输入法组合文字时)。
你可以添加 lazy 修饰符，从而转为在 change 事件_之后_进行同步：
<!-- 在“change”时而非“input”时更新 -->
<input v-model.lazy="msg">
```
##### .number
```
如果想自动将用户的输入值转为数值类型，可以给 v-model 添加 number 修饰符：
<input v-model.number="age" type="number">
这通常很有用，因为即使在 type="number" 时，HTML 输入元素的值也总会返回字符串。如果这个值无法被 parseFloat() 解析，则会返回原始的值。

```
##### .trim
```
如果要自动过滤用户输入的首尾空白字符，可以给 v-model 添加 trim 修饰符：
<input v-model.trim="msg">
```

### Vue事件处理
**[官网文档-表单输入绑定](https://cn.vuejs.org/v2/guide/events.htm)**
#### 监听事件
监听事件直接把事件写在v-on指令中.
```
<div id="example-1">
  <button v-on:click="counter += 1">Add 1</button>
  <p>The button above has been clicked {{ counter }} times.</p>
</div>
```

#### 方法事件处理器
然而许多事件处理逻辑会更为复杂，所以直接把 JavaScript 代码写在 v-on 指令中是不可行的。
因此 v-on 还可以接收一个需要调用的方法名称。
```
<div id="example-2">
  <!-- `greet` 是在下面定义的方法名 -->
  <button v-on:click="greet">Greet</button>
</div>
```

#### 内联处理器中的方法
除了直接绑定到一个方法，也可以在内联 JavaScript 语句中调用方法
```
<div id="example-3">
  <button v-on:click="say('hi')">Say hi</button>
  <button v-on:click="say('what')">Say what</button>
</div>

传参
```
有时也需要在内联语句处理器中访问原始的 DOM 事件。可以用特殊变量 $event 把它传入方法：
```
<button v-on:click="warn('Form cannot be submitted yet.', $event)">
  Submit
</button>

 warn: function (message, event) {
    // 现在我们可以访问原生事件对象
    if (event) {
      event.preventDefault()
    }
    alert(message)
  }
```