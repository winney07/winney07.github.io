---
title: CSS3-笔记
date: 2018-09-02 16:28:27
tags:
- CSS3
---

 [CSS3参考手册](http://caibaojian.com/css3/)

[CSS 官方参考文档](https://www.w3cschool.cn/doc_css/)

[CSS3/CSS2/CSS 教程/参考/帮助](CSS3/CSS2/CSS 教程/参考/帮助)

[media媒体查询相关属性](https://www.w3cschool.cn/doc_css/css-@media.html?lang=en)

[QuirksBlog](https://www.quirksmode.org/blog/)

[@media](https://developer.mozilla.org/en-US/docs/Web/CSS/@media)

#### CSS3新特性

- 圆角(border-radius );
- 阴影(box-shadow );
- 对文字加特效(text-shadow );
- 线性渐变（gradient );
- 变换(transform），如 transform: rotate(9deg) scale(0.85,0.90) translate(0px,-30px) skew(-9deg,0deg)//旋转、缩放、定位、倾斜.
- 更多的 CSS 选择器；
- 多背景设置；
- 色彩模式，如rgba;
- 伪元素：selection;
- 媒体杏询；
- 多栏布局；
- 图片边框 (border-image )。

#### CSS3 新增伪类

新增伪类有以下几个：

- p:first-of-type，选择属于其父元素的首个`<p>`元素的每个`<p>`元素。
- p:last-of-type，选择属于其父元素的最后一个`<p>`元素的每个`<p>`元素
- p:only-of-type，选择属于其父元素的唯一`<p>`元素的每个`<p>`元素。
- p:only-child，选择属于其父元素的唯一子元素的每个`<p>`元素。
- p:nth-child(2)，选择属于其父元素的第二个子元素的每个`<p>`元素。
- :enabled:disabled，控制表单控件的禁用状态。
- :checked，单选框或复选框被选中。

#### first-child 与first-of-type 的区别

first-child 匹配的是父元素的第一个子元素，可以说是结构上的第一个子元素

first-oftype 匹配的是该类型的第一个元素，类型就是指冒号前面匹配到的元素。并不限制是第一个子元泰，只要是该类型元素的第一个即可。当然，这些元素的范国都属于同一级，也就是同辈

```
<div>
  <p></p>
  <span></span>
</div>
```

p:tirst-child 匹配到p元素，因为p元素是div的第一个子元素。
span:first-chid 匹配不到 span 元素，因为span 是div的第二个子元素。
p:first-of-type 匹配到p元素，因为p是div所有为p的子元素中的第一个。
span:first-of-type 匹配到span 元素，因为span是div 所有为span 的子元素中的第一个。

#### 解决使用 transform:translate 属性时出现闪烁现象的问题

```
-webkit-backface-visibility:hidden;		// 隐藏转换的元素的背面
-webkit-transform-style: preserve-3d;	// 使被转换的元素的子元素保留其3D转换
-webkit-transform: translate3d(0,0,0);// 开启GPU硬件加速模式，使用GPU代替CPU渲染动画
```

> 在某些 Android 系统中，有时会有莫名其妙的 Bug，建议慎重使用

#### CSS3 动画在动作结束时保持该状态不变

采用animation-fill-mode。其可以设置为以下值

- none，不改变默认行为。
- forwards，当动画完成后，保持最后一个属性值（在最后一个关键帧中定义)。
- backwards， 在animation-delay 所指定的一段时间内，在动画显示之前，应用开始属性值（在第一个关键帧中定义）。
- both，向前和向后填充模式都可以应用

#### 实现某 DIV 元素以每秒50px 的速度左移 100px

方法一，使用 jQuery：

```
$('div').animate({'left': 100}, 2000);
```

方法二，使用JavaScript + CSS3：

```
div {
  transition: al1 2s 1inear; // 1inear 规定以相同速度（匀速）开始至结束的过渡效果
}
```

```
div.style.left = (div.offsetLeft + 100) + 'px';
```

#### box-sizing 属性

box-sizing 属性主要用来控制元素盒模型的解析模式。默认值是content-box.

content-box 让元素维持 W3C的标准盒模型。元素的宽度/高度由border + padding +content 的宽度/高度决定，设置width/height 属性指的是指定content 部分的宽度/高度。

border-box 让元素维持正 传统盒模型（IE6以下版本和IE6、IE7 的怪异模式）。设置width/height 属性指的是指定border + padding + content 的宽度/高度

标淮浏览器下，按照 W3C 规范解析盒模型。一旦修政了元素的边框或内距，就会影响元素的盒子尺寸，就不得不重新计算元素的盒子尺寸，从而影响整个页面的布局。

#### content-box 盒模型

```
Width(布局所占宽度) = width + padding-left + padding-right + border-left + border-right
```

```
Height(布局所占高度) = height + padding-top + padding-bottom + border-top + border-bottom
```

#### padding-box 盒模型

```
Width(布局所占宽度) = width（包含 padding-left + padding-right) + border-top + border-bottom
```

```
Height(布局所占高度) = height（包含 padding-top + padding-bottom) + border-top + border-bottom
```

#### border-box 盒模型

```
Width(布局所占宽度) = width(包含 padding-left + padding-right + border-left + border-right)
```

```
Height(布局所占高度) = height (包含padding-top + padding-bottom + border-top + border-bottom)
```

#### CSS3 动画的优缺点

优点：

（1）在性能上会稍微好一些，浏览器会对 CSS3 的动画做一些优化。
（2）代码相对简单

缺点：

（1）在动画控制上不够灵活。
（2）兼容性不好。
（3）部分动画功能无法实现

#### Animation 与 Transition 的异同

Animation 与Transition 的功能相同，都是通过改变元素的属性值来实现动画效果的。
它们的区别在于，使用Transition 的功能时只能用指定属性的开始值和结束值，然后在这两个属性值之问使用平滑过渡的方式实现动画效果，因此不能实现比较复杂的动画效果。Animation 功能通过定义多个关键帧，以及定义每个关键帧中元素的属性值来实现更为复杂的动画效果。

#### Animation 属性值

两个必要属性如下

- animation-name，即动画名称。
- animation-duration，即动画持续时间。

其他属性值如下。

- animation-play-state，即播放状态（running 表示播放，paused 表示暂停），可以用来控制动画暂停
- animation-timing-function，即动画运动形式。
- animation-delay，即动画延迟时间。
- animation-iteration-count，即重复次数。
- animation-direction，即播放前重置（alternate 动画,直接从上一次停止的位置开始执行）。

#### 媒体查询的使用方法

```
@media 媒体类型 and（媒体特性）{样式规则}
```

两个缺点
(1）适配屏幕的尺寸不是连续的。
(2）会在CSS文件中添加大段的查询代码，增加了CSS 文件的大小，
为改进上述缺点，可以使用 Javascript 获取移动设备屏幕的宽度，根据设计稿的原型尺寸，动态地计算 font-size 的值

#### 设置 CSS3 文本阴影

```
hl {text-shadow：水平阴影，重直阴影，模糊距离，阴影颜色}
```

#### 把元素从左侧移动 50 像素，从顶端移动 100 像素

```
div{
  transform: translate (50px, 100px);
  -ms-transform: translate (50px, 100px) ;/*IE 9*/
  -webkit-transform: translate (50px, 100px) ;/* Safari 和 Chrome */
  -o-transform: translate (50px, 100px) ;/* Opera */
  -moz-transform: translate (50px, 100px) ;/* Firefox */
}
```

#### 把一个元素旋转 30°

```
div{
  transform: rotate(30deg);
  -ms-transform: rotate(30deg);/*IE 9*/
  -webkit-transform: rotate(30deg);/* Safari 和 Chrome */
  -o-transform: rotate(30deg);/* Opera */
  -moz-transform: rotate (30deg);/* Firefox */
}
```

#### 使用 matrix()将div元素旋转 30°

```
div{
  transform:matrix (0.866,0.5,-0.5,0.866, 0, 0) ;
  -ms-transform:matrix (0.866, 0.5,-0.5,0.866, 0, 0) ;/*IE 9*/
  -moz-transform:matrix(0.866,0.5,-0.5,0.866,0,0);/* Safari 和 Chrome */
  -webkit-transform:matrix (0.866,0.5,-0.5,0.866, 0, 0) ;/* Opera */
  -0-transform:matrix (0.866,0.5,-0.5,0.866, 0, 0);/* Firefox */
}
```

#### 利用 CSS3 制作淡入淡出的动画效果

（1）定义动画关键帧，名称为 fadeln

```
@-webkit-keyframes fadeIn {
  from {
    opacity：0;/* 初始状态，透明度为 0 */
  }
  to {
    opacity：1; /* 结尾状态，透明度为 1 */
  }
}

@-webkit-keyframes fadeOut{
  from{
    opacity：1; /*初始状态，透明度为 1*/
  }
  to {
    opacity：0; /*结尾状态，透明度为 0*/
  }
}
```

（2）为div增加动画代码

```
div{
  -webkit-animation-name:fadeIn;	/*动画名称*/
  -webkit-animation-duration:3s;	/*动画持线时间*/
  -webkit-animation-iteration-count:1;	/*动画次数*/
  -webkit-animation-delay: 0s;	/*延迟时间*/
}
```

#### 盒阴影

盒阴影的语法结构与文本阴影类似，如:

```
box-shadow:5px 5px 5px rgba(255,15,255,0.5);
```

但是，盒阴影多了一个属性，即外延值 inset， 如：

```
box-shadow: 5px 5px 25px rgba(0,0,255,0.5）inset;
```

#### 为盒子添加蒙版

```
.demo {
  height: 144px;
  width: 144px;
  background: url(logo.png);
  -webkit-mask-image: url (shadow.png) ;
  -webkit-mask-position: 50% 50%;
  -webkit-mask-repeat: no-repeat;
}
```

蒙版复合属性的语法是`-webkit-mask: url(pro_pho_ show_ pic.png) 50% 50% no-repeat`

蒙版相关属性如下:

- -webkit-mask-clip，即蒙版裁剪位置。
- -webkit-mask-origin，即蒙版原点位置。

#### CSS3 实现背景颜色线性渐变

```
div{
  background: -webkit-linear-gradient (left, red, green 50%, blue) ;
}
```

### 实现 CSS3 倒影

通过`-webkit-box-reflect`设置方向、距离。
方向可以设置为below、 above、left、 right.

```
demo {
  height: 144px:
  width: 144px;
  background: url (logo.png) ;
  -webkit-box-reflect: below 10px;
}
```

#### 当元素不面向屏幕时，定义其可见性

```
使用 backface-visibility : visible | hidden.
```

#### CSS3中transition 属性值及含义

transition 属性是一个简写属性，用于设置以下4个过渡属性

- transition-property，哪个属性需要实现过渡。
- transition-duration，完成过渡效果需要多少秒/毫秒
- transition-timing-function，速度效果的运动曲线，如linear ease-in ease、ease-out、ease-in-out、 cube-bezier.
- transition-delay，规定过渡开始前的延迟时问。

#### 相对于内容框定义图像

```
.demo{
  height: 200px;
  width: 200px;
  padding: 50px;
  border: 1px solid #ccc;
  background-image: url ('logo.png');
  background-repeat: no-repeat;
  background-position: left top;
  background-origin: content-box;
}
```

语法为` background-origin: padding-box | border-box | content-box;`

#### background-clip 和 background-origin 的区别

background-olip 规定背景（包括背景颜色和背景图片）的绘制区域。
它有3种属性，分别是border-box、padding-box、 content-box.

- border-box，即背景从边框开始绘制。
- padding-box，即背景在边框内部绘制。
- content-box，即背景从内容部分绘制。

background-origin 规定背景图片的定位区域。

它也有了种属性：border-box、padding-box、content-box。但要注意，它描述的是“背景图片”。也就是说，它只能对背景做样式上的操作。一旦规定了图片开始绘制的区域，就当于规定图片的左上角从什么地方开始，其他的它就不负责了

#### 把文本分隔为 4列并使两列之问间隔30 像素

```
div{
  -moz-column-count:4;
  -webkit-column-count:4;
  column-count:4;
  -moz-column-gap:40px;
  -webkit-column-gap:40px;
  column-gap:40px;
  width: 600px;
}
```

#### 实现文本换行

使用word-wrap 属性。

- normal，只在允许的断字点换行（浏览器保持默认处理）。

- break-word，在长单词或 URL 地址内部进行换行。

#### 用@keytrames 使 dliv 元素移动 200 像素

```
div{
  width: 100px;
  height: 50px;
  background: #f30;
  animation: move 3s;
  @keyframes move
  from {
  margin-left: 0px;
  to
  margin-left: 200px;
}
```

