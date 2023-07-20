---
title: SVG图片的使用
date: 2019-07-29 11:25:24
tags:
- SVG
categories:
- CSS
---

CSS也可以使用SVG文件

```
.logo{
    background: url(icon.svg);
}
```

SVG文件还可以转为BASE64编码，然后作为Data URL写入网页。

```
<img src="data:image/svg+xml; base64, [data]">
```

#### 语法

2.1`<svg>`标签
SVG代码都放在顶层标签`<svg>`之中。下面是一个例子。

```
<svg width=""1O0%" height=""100%">
    <circle id="mycircle" cx="50" cy="50" r="50"/>
</svg>
```

width属性和height属性，制定了SVG图像在HTML元素中所占据的宽度和高度。除了相对单位，也可以采用绝对单位（单位︰像素)。如果不指定这两个属性，SVG图像默认大小是300像素（宽）*150像素（高)。
如果只想展示SG图像的一部分，就要指定viewBox属性。

```
<svg width="100" height="100" viewBox="50 50 50 50">
	<circle id="mycircle" cx="50" cy="50" r="50"/>
</svg>
```

viewBox属性的值有四个数字，分别是左上角的横坐标和纵坐标、视口的高度和宽度。上面代码中，SVG图像是`100像素宽*100像素高`，viewBox属性指定视口从（ 50，50 )这个点开始。所以，实际看到的是右下角的四分之一圆。
注意，视口必须适配所在的空间。上面代码中，视口的大小是`50*50`，由于SVG图像的大小是`100*100`，所以视口会放大去适配SVG图像的大小，即放大了四倍。

如果不指定width属性和height属性，只指定viewBox属性，则相当于只给到定SVG图像的长宽比。这时，SVG图像的默认大小将等于所在的HTML元素的大小。

2.2`<circle>`标签
`<circle>`标签代表圆形。

```
<svg width="300"" height=""180">
    <circle cx="30" cy="50" r="25"/>
    <circle cx="90" cy="50" r="25" c1ass="red"/>
    <circle cx="150" cy="50" r="25" class="fancy"/>
</svg>
```

上面的代码定义了三个园。`<circle>`标签的cx、cy、r属性分别为横坐标、纵坐标和半径，单位为像素。坐标都是相对于`<svg>`画布的左上角原点。
class属性用来指定对应的CSS类。

```
.red {
    fill: red;
}
.fancy {
    fill: none;
    stroke: black;
    stroke-width:3pt;
}
```

SVG的CSS属性与网页元素有所不同。

- fill：填充色
- stroke：描边色
- stroke-width：边框宽度

2.3`<line>`标签
`<line>`标签用来绘制直线。

```
<svg width="300" height="180">
	<line x1="0" y1="0" x2="200" y2="0" style="stroke:rgb(0,0,0);stroke-width:5;"/>
</svg>
```

上面代码中，`<line>`标签的×1属性和y1属性，表示线段起点的横坐标和纵坐标;x2属性和y2属性，表示线段终点的横坐标和纵坐标; style属性表示线段的样式。

2.4` <polyline>`标签
`<polyline>`标签用于绘制—根折线。

```
<svg width="300"" height=""180">
	<polyline points="3,3 30,28 3,53" fill="none" stroke="black"/>
</svg>
```

`<polyline>`的points属性指定了每个端点的坐标，横坐标与纵坐标之间与逗号分隔，点与点之间用空格分隔。

2.5`<rect>`标签

`<rect>`标签用于绘制矩形

```
<svg width="300"" height=""180">
	<rect x="0" y="0" height="100" width="200" style="stroke:#70d5dd; fill: #dd524b"/>
</svg>
```

`<rect>`的x属性和y属性，指定了矩形左上角端点的横坐标和纵坐标；width属性和height属性指定了矩形的宽度和高度（单位像素)。

2.6`<ellipse>`标签

`<ellipse>`标签用于绘制椭圆

```
<svg width="300"" height=""180">
	<ellipse cx="60" cy="60" rx="40" ry="20" stroke="black" stroke-width="5" fill="silver"/>
</svg>
```

`<ellipse>`的cx属性和cy属性，指定了椭圆中心的横坐标和纵坐标（单位像素）; rx属性和ry属性，指定了椭圆横向轴和纵向轴的半径（单位像素）。

2.7`<polygon>`标签

`<polygon>`标签用于绘制多边形

```
<svg width="300"" height=""180">
	<polygon fill: "green" stroke="orange" stroke-width="1" points="0,0 100,0 100,100 0,100 0,0"/>
</svg>
```

`<polygon>`的points属性指定了每个端点的坐标，横坐标与纵坐标之间与逗号分隔，点与点之间用空格分隔。

2.8`<path>`标签

`<path>`标签用于制路径

```
<svg width="300" height="180">
	<path d="
		M 18,3
		L 46,3
		L 46,40
		L 61,40
		L 32,68
		L 3,40
		L 18,40
		Z
    "></path>
</svg>
```

`<path>`的d属性表示绘制顺序，它的值是一个长字符串，每个字母表示一个绘制动作，后面跟着坐标。

- M：移动到( moveto )
- L：画直线到( lineto )
- Z：闭合路径

2.9`<text>`标签

`<text>`标签用于绘制文本

```
<svg width="300"" height=""180">
	<text x="50" y="25">He11o world</text>
</svg>
```

2.10`<use>`标签

`<use>`标签用于复制一个形状

```
<svg viewBox="0 0 30 10" xm7ns="http://www.w3.org/2000/svg">
    <circle id="mycircle" cx="5" cy="5" r="4"/>

    <use href="#myCircle" x="10" y="0" fill="blue"/>
    <use href="#myCircle" x="20"y="0" fill="white" stroke="blue"/>
</svg>
```

`<use>`的href属性指定所要复制的节点，x属性和y属性是左上角的坐标。 另外，还可以指定width和height坐标。

2.11`<g>`标签

`<g>`标签用于将多个形状组成一个组( group ) ，方便复用。

```
<svg width="300" height="100">
    <g id="mycircle">
        <text x="25" y="20">圆形</text>
        <circle cx="50" cy="50" r="20" />
    </g>

    <use href="#myCircle" x="100" y="0" fill="b1ue"/>
    <use href="#myCircle" x="200" y="0" fill="white" stroke="blue"/>
</svg>
```

2.12`<defs>`标签

`<defs>`标签用于自定义形状，它内部的代码不会显示，仅供引用。

```
<svg width="300" height="100">
    <defs>
        <g id="mycircle">
            <text x="25" y="20">圆形</text>
            <circle cx="50" cy="50" r="20" />
        </g>
    </defs>
    
    <use href="#myCircle" x="0" y="0"/>
    <use href="#myCircle" x="100" y="0" fill="blue"/>
    <use href="#myCircle" x="200" y="0" fill="white" stroke="blue'/>
</svg>
```

2.13`<pattern>`标签

`<pattern>`标签用于自定义一个形状，该形状可以被引用来平铺一个区域。

```
<svg width="500" height="500">
    <defs>
        <pattern id="dots" x="0" y="0" width="100" height="100" patternunits="userspaceonuse">
            <circle fill="#bee9e8" cx="50" cy="50" r="35"/>
        </pattern>
    </defs>
    <rect x="0" y="0" width="100%" height="100%" fill="ur1(#dots)"/>
</svg>

```

上面代码中，`<pattern>`标签将一个圆形定义为dots模式。`patternunits="userspaceonuse"`表示`<pattern>`

的宽度和长度是实际的像素值。然后，指定这个模式去填充下面的矩形。

2.14`<image>`标签

`<image>`标签用于插入图片文件

```
<svg viewBox="0 0 100 100" width="100" height="100">
    <image xlink:href="path/to/image.jpg" width="50%" height="50%" />
</svg>
```

上面代码中，`<image>`的`xlink:href`属性表示图像的来源。

2.15`<animate>`标签

`<animate>`标签用于产生动画效果

```
<svg width="500px" height="500px">
    <rect x="0" y="0" width="100" height="100" fill="#feac5e">
        <animate attributeName="x" from="0" to="500" dur="2s" repeatCount="indefinite"/>
    </rect>
</svg>
```

上面代码中，矩形会不断移动，产生动画效果。

`<animate>`的属性含义如下：

attributeName ：发生动画效果的属性名。

from：单次动画的初始值。

to：单次动画的结束值。

dur：单次动画的持续时间。

repeatCount：动画的循环模式。

可以在多个属性上面定义动画。

```
<animate attributeName="x" from="0" to="500" dur="2s" repeatcount="indefinite"/>
<animate attributeName="width" to="500" dur="2s" repeatCount="indefinite"/>
```

2.16`<animateTransform>`标签

`<animateTransform>`标签对CSS的transform属性不起作用，如果需要变形，就要使用`<animateTransform>`标签。

```
<svg width="500px" height="500px">
    <rect x="250" y="250" width="50" height="50" fill="#4bcOc8">
        <animateTransform attributeName="transform" type="rotate" begin="0s" dur="10s"
     from="0 200 200" to="360 400 400" repeatcount="indefinite"/>
     </rect>
</svg>

```

上面代码中，`<animateTransform>`的效果为旋转( rotate )，这时from和to属性值有三个数字，第一个数字是

角度值，第二个值和第三个值是旋转中心的坐标。`from="0 200 200"`表示开始时，角度为0，围绕(200,200)开始

旋转；`to="360 400 400"`表示结束时，角度为360，围绕(400，400)旋转。