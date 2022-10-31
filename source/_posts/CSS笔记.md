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


##### iconfont自定义命名图标class名

1. 鼠标`移到需要修改的图标上`

2. 选择`编辑图标`

3. 修改`Font Class / Symbol` 为自己想要的class命名

   例如：填写`exit`， 使用的时候就是：  `class="icon icon-edit"`

4. 选择`仅保存`



### 前端轻松入门-CSS

#### 1.1CSS的定义

什么是CSS？

CSS指层叠样式表(Cascading Style Sheets)

CSS通常称为CSS样式表或层叠样式表（级联样式表），主要用于设置HTML页面中的文本内容（字体、大小、对齐方式等）、图片的外形（宽高、边框样式、边距等）以及版面的布局等外观显示样式。

- CSS以HTML为基础，提供了丰富的功能，如字体、颜色、背景的控制及整体排版等，而且还可以针对不同的浏览器设置不同的样式。
- CSS就是控制页面布局和样式CSS的版本：2.1→3.0
- 类比例子：奶油蛋糕、画画
- HTML和CSS的关系：HTML结构层负责从语义的角度搭建页面结构
- CSS样式层负责从审美的角度美化页面
- JavaScript行为层负责从交互的角度提升用户体验



#### 1.2引入CSS的方式

所有的标签都有一个默认样式，我们称为浏览器样式，或者默认样式

#### 1.2.1行内样式

行内样式，是通过在标签中设置style属性来达到实现控制标签的样式的效果。例如：

```plain
<h1 style="color: red;">传智播客-前端与移动开发学院的CSS基础视频教程</h1>
```

Style属性中，可以设置多条的CSS样式。

#### 1.2.2嵌入样式

在head标签中，嵌套一个style标签，在style标签中可以书写CSS的样式内容。Style标签有一个属性type属性，默认值就是text/css,可以省略。例如demo：

```plain
<style type="text/css">
  p {
    color: green; /*设置前景色，也就字体的颜色*/
    background-color: silver;
  }
  ul {
  	background-color: red;
  }
</style>
```

#### 1.3CSS注释

CSS的注释语法/*注释的内容*/注释不能嵌套，比如：

```plain
/*注释的*/内容*/
/* dsfsdfsd /* */ */
```

多行注释：

```
/*

放多行的注释内容1

放多行的注释内容2

*/
```

一般用于模块的注释

```plain
/* S导航条开始*/
ul {
	background-color: red;
}
/* E导航条结束*/
```

文件头的注释：

```plain
/*
* author:传智播客前端与移动开发学院
* des：当前文件用于....
* date：
*/
```

### 彻底搞懂行高

![彻底搞懂行高](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/CSS%E7%AC%94%E8%AE%B0/1.png)



#### CSS的定义

##### 什么是CSS？

- CSS指层叠样式表(Cascading Style Sheets)
- CSS通常称为CSS样式表或层叠样式表(级联样式表)，主要用于设置HTML页面中的文本内容（字体、大小、对齐方式等)、图片的外形（宽高、边框样式、边距等）以及版面的布局等`外观显示样式`。

- CSS以HTML为基础，提供了丰富的功能，如字体、颜色、背景的控制及整体排版等，而且还可以针对不同的浏览器设置不同的样式。
- CSS就是控制页面布局和样式
- CSS的版本：2.1→3.0
- 类比例子，奶油蛋糕、画画



##### HTML和CSS的关系：

- HTML结构层         负责从语义的角度搭建页面结构
- CSS样式层             负责从审美的角度美化页面
- JavaScript行为层      负责从交互的角度提升用户体验



#### 如何编写CSS

##### 如何编写CSS样式?

- 缺省样式（浏览器样式)
  - 可以通过设置修改浏览器的样式。
  - 所有的标签都有默认的样式：`h1 ,h2,p, div,span,ul`等



- 内联样式style属性

  ```
  <span style="color:red;"></span>
  ```

- 内嵌（嵌入，内部)样式，head标签中添加style标签。
  `在head标签中添加style标签`

  ```
  <head>
      <style> p {color:red}</style>
  </head>
  ```

- 外部样式，外联样式(link)

  - 通过link标签引入css样式文件

    ```
    <link rel="stylesheet" href="a.css"" >
    ```

  - type属性：只有一个选项，“text/css"，指定当前为css文本文件

  - rel：指定当前HTML文件与CSS文件的关系是样式表。

  -  href：指定外联样式表的路径

- 导入样式:
  - @impot，导入样式会导致，css文件不能并行下载。不推荐使用。
  - 导入样式的书写必须在所有的css规则书写之前

#### Emmate语法：

```plain
ul(li>a[href="#"])*3
```

#### 浏览器可以设置默认样式

所有标签都有默认样式，我们称为浏览器样式，或默认样式。

#### css语法

![css](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/CSS%E7%AC%94%E8%AE%B0/2.png)



#### css注释

- CSS的注释格式：

```
/* 注释内容 */
```

- 可以同时注释多行语句比如:

```
/* 单行注释 */


/* 多行注释
多行注释
多行注释*/

// 常用用法，不是语法
/* 
* 文件声明注释
* 作者：winney
* 目的：演示注释的用法
*/
```

```
/* S 导航条开始 */
ul{
	background-color: red;
}
/* E 导航条结束 */
```

```
<!-- S 导航条开始 -->
<ul>
	<li><a href="#">上海</a></li>
	<li><a href="#">北京</a></li>
	<li><a href="#">广州</a></li>
</ul>
<!-- E 导航条结束 -->
```

##### 文件头的注释

```
/* 
* author: winney
* des：当前文件用于...
* date：....
*/
```

#### CSS选择器综述

所有标签选择器：`*{}`

标签选择器：`p{}、div{}`

ID选择器：`#head{}`

类选择器：`.head{}`

层级选择器

分组选择器

属性选择器

子元素选择器

相邻兄弟选择器

伪类选择器

伪元素选择器

#### 通配符选择器

通配符选择器用“*”号表示，他是所有选择器中作用范围最广的，能匹配页面中所有的元素。其基本语法格式如下:

```
*{属性1:属性值1;属性2:属性值2;属性3:属性值3;}
```

例如下面的代码，使用通配符选择器定义CSS样式，清除所有HTML标记的默认边距。

```
*{
    margin: 0;	/* 定义外边距 */
    padding: 0;	/* 定义内边距 */
}
```

通配符的穿透力很强，优先级高于继承的样式，会覆盖继承的样式。`一般不用`。

#### css复合选择器

复合选择器是由两个或多个基础选择器，通过不同的方式组合而成的，具体如下

##### 1、标签指定式选择器(即....又...)

标签指定式选择器又称交集选择器，由两个选择器构成，其中第一个为标记选择器，第二个为class选择器或id选择器，两个选择器之间不能有空格，如`h3.special`或`p#one`。

```
h3.class {color:red}   // h3:标记选择器， class：类别选择器
```

##### 3、并集选择器

并集选择器是各个选择器通过逗号连接而成的，任何形式的选择器（包括标记选择器、class类选择器id选择器等），都可以作为并集选择器的一部分。如果某些选择器定义的样式完全相同，或部分相同，就可以利用并集选择器为它们定义相同的CSS样式。

```
.class, h3{color:red; font-size:25px;}
```

#### 属性选择器

- 简单属性选择

  ```
  h1[class]{color: red;}		// 选择所有拥有class属性的h1标签
  h1[class][id]{color: red;}
  ```

- 根据属性值选择

  ```
  p[id="aside"]{color: red;}	 // 根据属性名相等选择
  ```

- 属性名全包含

  ```
  p[class~="a"]{color: red;}  // 只要包含属性，就被选择。ie6不支持
  ```

- 属性模糊选择

  选择具有alt属性且属性值为以val开头（结尾）的字符串的E元素

  ```
  E[alt^="Val"]{sRules}
  E[alt$="Val"]{sRules}
  ```

- 属性模糊匹配包含

  ```
  E[alt*="Val"]{sRules}  // 选择具有alt属性且属性值为包含val的字符串的E元素
  ```

  

#### CSS伪类

伪类：元素的某个状态

- :link
  伪类将应用于未被访问过的链接。lE6不兼容，解决此问题，直接使用a标签。
- :hover
  伪类将应用于有鼠标指针悬停于其上的元素。在IE6只能应用于a连接，lE7+所有元素都兼容。
- :active
  伪类将应用于被激活的元素，如被点击的链接、被按下的按钮等。

- :visited
  伪类将应用于已经被访问过的链接

- :focus
  伪类将应用于拥有键盘输入焦点的元素。

**顺序问题: `LoVe HAte`原则。**
**综合案例，电商菜单。**

#### CSS伪元素

伪元素是控制内容

:first-line伪元素

:first-letter伪元素
注释:以上两个伪元素只能用于块级元素

:first-child 伪元素，选择属于第一个子元素的元素。
例如：` span:first-child{}` `/*选择属于第一个子元素的所有span标签。*/`

:before与:after伪元素，可以设置元素之前后之后的内容，并且配合content设置相关内容。比如`:#demo:after,demo:before { content:"--";,display:block; }`

```
.wrap:before, .wrap:after{
	content: "-------";
	display: block; /* 这个是让当前伪元素转换成块级元素 */
}

<div class="wrap">
	wrap
</div>
```

### CSS的层叠性和继承性

#### CSS的优先级

1. 内联样式
2. ID选择器
3. 类选择器
4. 标签选择器

内联样式最大．内联样式的优先级最高。

ID选择器的优先级．仅次于内联样式。

类选择器优先级低于ID选择器

标签选择器低于类选择器。

256个标签选择器相加  大于   一个类选择器

256个类选择器相加   大于   一个ID选择器



#### CSS字体样式属性

1、font-size：字号大小

font-size属性用于设置字号，该属性的值可以使用相对长度单位，也可以使用绝对长度单位。其中，相对长顾单位比较常用，推荐使用像素单位px，绝对长度单位使用较少。

可选参数值:` x-small | x-small | small | medium | large | x-large| xx-large| smaller | larger`

一般页面中: 12px14px例如:
p { font-size: 32px; }



#### 复用代码

##### 居中对齐

```
-webkit-transform: translate(-50%, -50%);
   -moz-transform: translate(-50%, -50%);
    -ms-transform: translate(-50%, -50%);
     -o-transform: translate(-50%, -50%);
        transform: translate(-50%, -50%);
```

##### 圆角

```
border-radius: rem(10);
-o-border-radius: rem(10);
-ms-border-radius: rem(10);
-moz-border-radius: rem(10);
-webkit-border-radius: rem(10);
```

```
border-top-left-radius: <length> <length> //左上角
border-top-right-radius: <length> <length> //右上角
border-bottom-right-radius:<length> <length> //右下角
border-bottom-left-radius:<length> <length> //左下角
```

##### 圆角不一样时的简写

```
 border-radius：rem(10) 0 rem(10) 0;
```

#### 去掉input ,button,select 在ios的默认样式

```
-webkit-appearance:none;
outline:none
```

#### ios input阴影 去除

```
/* ios input阴影 */  
input {  
  outline: none;  
  -webkit-appearance: none;  
  /*去除系统默认的样式*/  
  -webkit-tap-highlight-color: rgba(0, 0, 0, 0);  
  /* 点击高亮的颜色*/  
}  
  
  
// IOS点击阴影  
select{  
  -webkit-tap-highlight-color: transparent;  
  -webkit-touch-callout: none;  
  -webkit-user-select: none;  
  user-select:none;  
} 
```

#### [手机页面上面 按钮点击的时候有阴影 如何除去](http://blog.csdn.net/orichisonic/article/details/49583077)

```
*{
	-webkit-tap-highlight-color: rgba(0,0,0,0);
	-webkit-tap-highlight-color: transparent; /* For some Androids */ 
} 
```

#### 输入框的样式

```
input{
    vertical-align: middle;
    font-size: rem(28);
    height: rem(34);
    line-height: normal;
    width: 70%;
}
```

#### 自定义输入框placeholder 的样式

```
::-webkit-input-placeholder { 
    padding-top: rem(3);
} 
:-moz-placeholder { 
    padding-top: rem(3);
} 
::-moz-placeholder { 
    padding-top: rem(3);
} 
:-ms-input-placeholder { 
    padding-top: rem(3);
} 
```

##### input placeholder 颜色

```
input::-webkit-input-placeholder,
textarea::-webkit-input-placeholder {
  color: #666;
}
input:-moz-placeholder, textarea:-moz-placeholder {
  color:#666;
}
input::-moz-placeholder, textarea::-moz-placeholder {
  color:#666;
}
input:-ms-input-placeholder, textarea:-ms-input-placeholder {
  color:#666;
}
```

##### 让输入框中的placeholder 文字垂直居中

加padding-top

#### 输入框不可用

```
disabled：disabled；
readonly：readonly；
```

#### [IOS Input Disabled默认样式问题](https://www.jianshu.com/p/c4e3bc4048f8)

`input`或`textarea`设置为`disabled`后，在iphone手机上样式将被覆写。解决方案就是：

```
input:disabled, textarea:diabled {
    -webkit-text-fill-color: #000;
    -webkit-opacity: 1;
    color: #000;
}
```

以上样式将覆盖其系统默认设置的值，能够实现android和ios的兼容性。
其中,`-webkit-text-fill-color`是用来做填充色使用的，如果有设置这个值，则`color`属性将不生效。

这个属性也经常用于制作镂空字体等特效。
如:

```
<div class="demo">
  hello
</div>

.demo {
  width: 100px;
  height: 100px;
  font-size: 40px;
  -webkit-text-fill-color: transparent;
  -webkit-text-stroke: 1px #000; /* 外面描线的样式 */
}
```

#### 垂直居中

```
top: 50%;
transform: translateY(-50%);
-o-transform: translateY(-50%);
-ms-transform: translateY(-50%);
-moz-transform: translateY(-50%);
-webkit-transform: translateY(-50%);
```

#### [CSS3中的Opacity多浏览器透明度兼容性问题](https://www.jb51.net/css/398056.html)

```
.opacity{   
  filter:alpha(opacity=50); /* IE */  
  -moz-opacity:0.5; /* 老版Mozilla */  
  -khtml-opacity:0.5; /* 老版Safari */  
  opacity: 0.5; /* 支持opacity的浏览器*/  
} 
```

#### 兼容所有浏览器

```
.transparent_class {          
  filter:alpha(opacity=50);          
  -moz-opacity:0.5;          
  -khtml-opacity: 0.5;          
  opacity: 0.5;          
}   
```

#### 文字超出长度，省略号显示

```
overflow: hidden;
text-overflow: ellipsis;
white-space: nowrap;  // 可以不加这个
```

#### 文字超出长度，换行

```
word-wrap:break-word;
word-break:break-all;
overflow: hidden;
```

#### 文字超出长度，不换行，省略号显示

```
overflow: hidden;
white-space: nowrap;
text-overflow: ellipsis;
word-break: keep-all;
```

#### 只显示两行文字，多出的用省略号代替

```
overflow: hidden;
text-overflow: ellipsis;
display: -webkit-box;
 -webkit-line-clamp: 2;
-webkit-box-orient: vertical;
```

#### 字体垂直居中

```
<div style="
    width: 100%;
    height: 100px;
    background-color:
    gray;color: white;
    font-size: 30px;
    display: -webkit-flex;
    display: flex;
    -webkit-align-items: center;
    align-items: center;
    -webkit-justify-content: center;
    justify-content: center;"
   >
       this  is title this is title thle
</div>
```

#### 当提示信息的文字长度不确定的时候

给最小宽度，然后不允许换行

最小长度：min-width

不允许换行：white-space:nowrap;

例如：

```
display: none;
position: fixed;
z-index: 5000;
min-width: rem(150);
min-height: rem(40);
padding: rem(20);
top:rem(480);
left: 50%;
transform: translateX(-50%);
background: rgba(0, 0, 0, 0.5);
text-align: center;
border-radius: rem(10);
color: $white;
font-size: rem(26);
white-space:nowrap;
```

#### 背景图

```
display: block;
border: 0;
outline: 0;
width: 100%;
height: 100%;
position: absolute;
left: 0;
top:0;
z-index: -1;
```

#### 错误信息提示框样式

```
p#error {
  //	display: none;
  position: fixed;
  left: 50%;
  top: 30%;
  z-index: 999;
  -webkit-transform: translateX(-50%);	
  -moz-transform: translateX(-50%);
  -o-transform: translateX(-50%);
  transform: translateX(-50%);
  margin: 0 auto;
  padding: rem(20);
  font-size: rem(30);
  color: $white;
  background: rgba(0,0,0,.7);
  border-radius: rem(10);
  -webkit-border-radius: rem(10);
  -moz-border-radius: rem(10);	
  -o-border-radius: rem(10);
  text-align: center;
  border: 0;
  text-indent: 0;
  width: auto;
  min-width: 45%;
}
```

#### 过渡效果

```
-webkit-transition: all .25s ease|linear|ease-in|ease-out|ease-in-out|cubic-bezier(<number>,<number>,<number>,<number>);
-moz-transition: all .25s ease|linear|ease-in|ease-out|ease-in-out|cubic-bezier(<number>,<number>,<number>,<number>);
-ms-transition: all .25s ease|linear|ease-in|ease-out|ease-in-out|cubic-bezier(<number>,<number>,<number>,<number>);
-o-transition: all .25s ease|linear|ease-in|ease-out|ease-in-out|cubic-bezier(<number>,<number>,<number>,<number>);
transition: all .25s ease|linear|ease-in|ease-out|ease-in-out|cubic-bezier(<number>,<number>,<number>,<number>);

transition: property duration timing-function delay;
```

#### transform 属性向元素应用 2D 或 3D 转换。该属性允许我们对元素进行旋转、缩放、移动或倾斜

```
-webkit-transform: ;
   -moz-transform: ;
    -ms-transform: ;
     -o-transform: ;
       	transform: ;
```

####  允许改变textarea 不同方向的大小

```
textarea { resize:both; } /* none|horizontal|vertical|both */
textarea.vert { resize:vertical; }
textarea.noResize { resize:none; }
```

#### 禁止输入框调整大小

```
textarea {
  	resize: none;
}
```

#### 固定定位在IE6下是不兼容的

#### 在使用clientX和clientY时，要使用scrollTop和scrollLeft。避免出现问题

#### [css input[type=file] 样式美化-input上传按钮美化](https://www.haorooms.com/post/css_input_uploadmh)

##### DOM结构

```
<a href="javascript:;" class="a-upload">
    <input type="file" name="" id="">点击这里上传文件
</a>

<a href="javascript:;" class="file">选择文件
    <input type="file" name="" id="">
</a>
```

CSS样式1：

```
/*a  upload */
.a-upload {
    padding: 4px 10px;
    height: 20px;
    line-height: 20px;
    position: relative;
    cursor: pointer;
    color: #888;
    background: #fafafa;
    border: 1px solid #ddd;
    border-radius: 4px;
    overflow: hidden;
    display: inline-block;
    *display: inline;
    *zoom: 1
}

.a-upload  input {
    position: absolute;
    font-size: 100px;
    right: 0;
    top: 0;
    opacity: 0;
    filter: alpha(opacity=0);
    cursor: pointer
}

.a-upload:hover {
    color: #444;
    background: #eee;
    border-color: #ccc;
    text-decoration: none
}
```

样式2：

```
.file {
    position: relative;
    display: inline-block;
    background: #D0EEFF;
    border: 1px solid #99D3F5;
    border-radius: 4px;
    padding: 4px 12px;
    overflow: hidden;
    color: #1E88C7;
    text-decoration: none;
    text-indent: 0;
    line-height: 20px;
}
.file input {
    position: absolute;
    font-size: 100px;
    right: 0;
    top: 0;
    opacity: 0;
}
.file:hover {
    background: #AADFFD;
    border-color: #78C3F3;
    color: #004974;
    text-decoration: none;
}
```

![样式](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/CSS%E7%AC%94%E8%AE%B0/input_upload.png)



#### 限制textarea文本域拉动

> textarea:resize属性值：both（表示横向纵向均可拉动）horizontal（表示只有横向可以拉动）vertical（表示只有纵向才可以拉动）none（禁止拉动）

##### 设置文本域宽高

```
cols="30" rows="5"
```

#### CSS 前缀

主流浏览器引擎前缀

- -webkit- (谷歌, Safari, 新版Opera浏览器等)
- -moz- (火狐浏览器)
- -o- (旧版Opera浏览器等)
- -ms- (IE浏览器 和 Edge浏览器)

#### [不用 JS 显示“更多”的按钮来展开更多内容](https://mp.weixin.qq.com/s?__biz=MzI1MTA2MDcyOQ==&mid=2649567547&idx=1&sn=e022597760c3e5734a9505a71268e856&chksm=f1e159adc696d0bb7c87a84a56074a280efec840af9493da10f2fda8c683dcbac14ba96ddb30&scene=21#wechat_redirect)

#### 自定义滚动条样式

```
scrollbar::-webkit-scrollbar{
  width: 5px;
  height: 5px;
  background:#f3f3f3;
}
/*定义滑块，内阴影及圆角*/
.scrollbar::-webkit-scrollbar-thumb{
  height: 20px;
  background:rgba(0,0,0,.1);
}
.onhost-data {
  text-align: center;
  padding-top:30px;
}
```

#### 解决移动端fixed定位

[小技巧css解决移动端ios不兼容position:fixed属性，无需插件](https://blog.csdn.net/liu__hua/article/details/40106595)

需要解决的问题：头部fixed的情况下，右侧内容如果有输入框的话，在UC浏览器，当输入框获取焦点的时候，页面往上滚动，超过顶部固定导航。

![样式](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/CSS%E7%AC%94%E8%AE%B0/fixed1.png)

获取焦点后：

![样式](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/CSS%E7%AC%94%E8%AE%B0/fixed2.png)

##### 解决方法：

让右侧内容也固定定位



#### 网页适配 iPhoneX

[网页适配 iPhoneX，就是这么简单](https://jelly.jd.com/article/6006b1055b6c6a01506c87fd)

#### 溢出文字省略号显示兼容IE

原来：

```
.essential-info td:nth-child(2) a:nth-child(1){
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
}
```

解决：加上宽度即可

```
.essential-info td:nth-child(2) a:nth-child(1){
    display: inline-block;
    width:100%;
    width: 1000px\9;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
}
```

#### IE浏览器图片兼容问题

在IE浏览器，图片有边框

解决方法：给img加上`border:0;`的样式，去掉边框

#### [textarea placeholder文字换行](https://www.cnblogs.com/wangmeijian/p/6953813.html)

##### 谷歌浏览器和火狐浏览器支持

方法一：

```
<textarea rows="5" cols="50" ></textarea>

document.querySelector('textarea').setAttribute('placeholder','1、textarea\n2、success')
```

```
var txtArr = ["自定义参数，格式如下:","key_1=value_1","key_2=value_2","...","key_n=value_n","key和value之间用等号'='分隔，不要带空格","每一组key和value占用一行"];
var placeholderTxt= txtArr.join("\n");
$(".sdk-textarea").attr("placeholder", placeholderTxt);
```

方法二：

```
<textarea rows="5" cols="50" placeholder="1、textarea&#10;2、success"></textarea>
```

#### CSS实现固定表头  内容溢出滚动

```
thead{
  tr {
    display:table;
    width:100%;
    table-fixed:fixed;
  }
}


tbody{
  width:calc(100% + 17px);
  display:block;
  height:420px;
  overflow-y:auto;
  overflow-x:hidden;
  tr{
  	display:table;
    width:100%;
    table-layout:fixed;
  }
}
```

#### 解决苹果网页-手机字体变大

解决移动端iPhone（苹果手机）网页兼容（部分字号变大）

 safari浏览器是webkit内核

```
body{-webkit-text-size-adjust:none;}
```

