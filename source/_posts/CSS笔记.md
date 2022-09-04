---
title: CSS笔记
date: 2019-08-21 17:29:52
tags:
- CSS
- 工作笔记
---



#### CSS选择器

1. id选择器
2. 类选择器
3. 标签选择器
4. 相邻选择器（+）
5. 子选择器（>）
6. 后代选择器（li a)
7. 通配符选择器（*）
8. 属性选择器（button[disabled="true"])
8. 伪类选择器（a:hover、li:nth-child）表示一种状态
8. 伪元素选择器（li:before、":after"、":first-letter"、":first-line"、":selecton"）表示文档某个部分的表现

> 在CSS3规范中，为了区别伪元素和伪类，CSS3建议伪类用单冒号“:“，伪元素用双冒号”::“。
>

#### 可继承的样式

- font-size
- font-family
- color

#### 不可继承的样式

- border
- padding
- margin
- width
- height

> 注：与字体相关的样式通常可以继承，与尺寸相关的样式通常不能继承

博客：[css那些样式可以继承](https://blog.csdn.net/weixin_51109349/article/details/109580508)

#### CSS优先级排序

!important>style行内样式> id[选择器](https://so.csdn.net/so/search?q=选择器&spm=1001.2101.3001.7020)（权重100）> 类选择器（权重10）>标签（权重1）>通配符> 继承 > 浏览器默认样式(最低)。同类别动样式中，后面的会覆盖前面的

#### 初始化CSS

最简单的初始化方法就是：

```
*{margin: 0; padding: 0;}
```

#### 居中对齐

```
div{
    width: 400px;
    height: 200px;
    margin: -100px 0 0 -200px;
    position: relative;
    left: 50%;
    top: 50%;
    /* 便于看效果 */
    background-color: aqua;
}
```

#### [display的值和作用](https://blog.csdn.net/CM22222/article/details/115555369)

#### 左右固定宽度，中间自适应实现3拦布局

双飞翼布局或两翼齐飞布局

```
<div class="container">
    <!-- 中间自适应 -->
    <div class="main"></div>
    <!-- 左边固定宽带 -->
    <div class="left"></div>
    <!-- 右边固定宽度 -->
    <div class="right"></div>
</div>
```

```
.container div{
    height: 200px;
}
.container{
    padding: 0 200px;
}
.main,
.left,
.right{
    position: relative;
    float: left;
}
.left,
.right{
    width: 200px;
}
.main{
    width: 100%;
    background-color: yellow;
}
.left{
    background-color: blue;
    margin-left: -100%;
    left: -200px;
}
.right{
    background-color: green;
    margin-left: -200px;
    left: 200px;
}
```

> 要想使元素浮动，必须为元素设置一个宽度



#### 在高效CSS时需要考虑的问题

1. 类型选择器的速度，id最快，*最慢
2. 不要用标签限制ID选择器（如ul#main，ID已经是唯一的，不需要tag来限制，这样做会让选择器变慢）
3. 后代选择器最糟糕（html body ul li a是很低效的）
4. CSS3选择器
5. ID选择器速度最快，但都用ID选择器，会降低代码的可读性和可维护性

#### display:none和visibility:hidden的区别

- display:none—不分配空间，脱离文档流
- visibility:hidden—在文档流中仍保留原来的空间



#### :before/:after伪元素中content属性

```
body{
    counter-reset: chapter;
}
ul li::before{
    content: "第"counter(chapter)"章";
}
ul li{
    counter-increment: chapter;
}
```

```
<ul>
    <li></li>
    <li></li>
    <li></li>
</ul>
```

效果：

```
第1章
第2章
第3章
```

> 放置元素的前后，可插入文本、图像、引号，并可以结合计数器，为页面元素插入编号

#### 定义高度很小的容器

1. `overflow:hidden`
2. `font-size:容器高度px`

#### 在图片下方设置几像素的空白间隙

- 定义img为`display:block`
- 定义父容器为f`ont-size:0`;

#### 超出宽度的文字显示为省略号

```
{
  overflow:hidden;
  width:**px;
  white-space:nowrap;
  text-overflow: ellipsis;
}
```

#### 使英文单词发生词内断行

```
word-wrap:break-word;
```

#### 实现 lE6 下的 position:fixed

```
html (overflow: hidden; )
body (overflow: auto;height: 100%;}
•fixed(position:fixed; position: absolute;left:0;top: 0;padding: 10px;background: #000;}
```

#### 让 min-height 兼容 IE6

```
.min-heicht{
  min-height:100px;
  height: 100px;
  background: red;
}
```

#### 已知高度的容器在页面中水平垂直居中

```
#box{
  width: 200px;
  height: 200px;
  background: red;
  position: absolute;
  left: 50%;
  top: 50%;
  margin:-100px 0 0 -100px;
  /*或者 marign:-100px* /
}
```

#### px和em 的区别

px和en都是长度单位，两者的区别是：px的值是固定的，指定为多少就是多少，计算比较容易；em 的值不是固定的，是相对于容器宇体的大小，并且en 会继承父级元素的字体大小

浏览器的默认字体高都是16px，所以未经调整的浏览器都符合1em = 16px，那么12px = 0.75em，10px = 0.625em.

与em对应的另一个长度单位是rem，是指相对于根元素（通常是HTML 元素）字体的大小



#### Sass报错

如果按照了sass，使用`<style lang="scss" scoped>`时报错，原因可能是安装的sass版本是最新的，版本太高的原因，安装以下两个版本，再使用sass就不会报错。

```
"node-sass": "^4.12.0",
"sass-loader": "^8.0.2",
```

#### 优雅降级与渐进增强的区别

`优雅降级graceful degradation` 是指一开始就构建完整的功能，然后再针对低版本浏览器进行兼容
`渐进增强 progressive enhancement `是指针对低版本浏览器构建页西，保证最基本的功能，然后再针对高级浏览器进行效果、交互等政进并追加功能，以达到更好的用户体验

两者的区别如下：

1. 优雅降级从复杂的现状开始，并试图减少用户体验的供给。
2. 渐进增强则从一个非常基础并且能够起作用的版本开始，并不断扩充，以适应未来环境的需要
3. 降级（功能衰減）意味着往回看，而渐进增强则意味着朝前看，同时保证其根基处于安全地带

####  图片格式

- JPG：压缩率高，文件小，最常用。
- PNG：支持无损压缩，色彩损失小，保真度高，文件稍大。
- GIF：支持动画品示，但只支持256 色显示，目前已经被 Flash 大量取代。

#### CSS的content 属性的作用和应用

作用：CSS 的content 属性专门应用在before/after 伪元素上，用于插入生成的内容。

应用：最常见的应用是利用伪类清除浮动。

#### 对行内元素设置 margin-top 和margin-bottom 不起作用

对行内元素设置 margin-top 和margin-bottom 不起作用（需要注意行内元素的替换元素 img、input，它们是行内元素，但是可以设置它们的宽度和高度，并且margin 属性也对它们起作用，margin-top 和margin-botton 有
着类似于 inline-block 的行为）。

#### div+css 的布局较 table 布局的优点

（1）改版的时候更方便，只须改动CSS文件。
（2）页面加载速度更快、结构清晰、页面简洁。
（3）表现与结构分离
（4）搜索引擎优化（SEO）更友好，排名更靠前。



#### 各种规范

- BFC(Block Formatting Context）指块级格式化上下文
- IFC (Inline Formatting Context）指内联格式化上下文
- GFC ( GridLayout Formatting Context）指网格布局格式化上下文
- FFC ( Flex Formatting Context）指自适应格式化上下文

#### 访问超链接后 hover 样式就不出现的原因及解决方法

因为访问过的超链接样式覆盖了原有的 hover 和active 伪类选择器样式，解决方法是将 CSS 属性的排列顺序改为L->V->H->A (link, visited, hover, active )。

#### rgba()和 opacity 的透明效果的区别

gba()和 opacity 都能实现透明效果，但它们最大的不同是opacity 作用于元素，并且可以设置元素内所有内容的透明度；而rgba()只作用于元素的颜色或其背景色（设置rgba 透明的元素的子元素不会继承透明效果)。

#### CSS 中可以让文字在垂直和水平方向上重叠的两个属性

垂直方向的属性是line-height。水平方向的属性是letter-spacing。

#### letter-spacing 的妙用

可以用于消除 inline-block 元素间的换行符空格间隙

#### 使DOM元素不显示在浏览器可视范围内的CSS属性

- 设置 display 属性为none，

- 设置visibility 属性为hidden。
- 技巧性的方式如下：
  - 设置宽高为0，
  - 透明度为0，
  - 设置z-index 位置为-1000。

#### 浏览器标淮模式和怪异模式之间的区别

它们的区别是盒子模型的渲染模式不同

可以使用 window.top.document.compatMode 判断当前模式为何种模式。
结果为 BackCompat，表示怪异模式．
结果为 CSSICompat，表示标准模式

#### 避免文档流中的空白符合并现象

空白符合并是标淮文档流的特征之一，可以通过设置white-spac 修改这一特征，
属性值如下。

- pre 表示不会合并空自符，渲染换行符，不会自动换行，相当于pre 元素。
- pre-wrap 表示不会合并空白符，渲染换行符，自动换行。
- pre-line 表示合并空白符，渲染换行符，自动换行。
- nowrap 表示合并空白符，不会渲染换行符，不会自动换行。
- normal 表示默认值，按照文档流特点渲染，合并空白符，不会渲染换行符，自
  动换行.

#### 透明度具有继承性，如何取消透明度的继承

使用rgba 给元素的背景设置透明度的方式，来替代使用 opacity 设置元素透明度的方式，解決子元素继承父元素透明度的问题

#### CSS 中，自适应的单位

- 百分比：％
- 相对于视口宽度的单位：vw
- 相对于视口高度的单位：vh
- 相对于视口宽度或者高度（取决于哪个小）的单位：vm
- 相对于父元素宇体大小的单位：em
- 相对于根元素字体大小的单位：rem





#### 外边距重叠，重叠的结果

#### 引入字体图标

1. 使用cdn链接，在public目录下的`index.html`中引入`iconfont字体图标链接`

   ```
   <link rel="stylesheet" href="//at.alicdn.com/t/font_907707_neo27xdny5.css">
   ```

   > 登录账号——资源管理——我的项目——选中项目——选中“Font class”——复制链接——放到`public/index.html`	

2. 在页面中调用，要加上iconfont

   ```
   <i class="iconfont icon-IOS"></i>
   ```

   
