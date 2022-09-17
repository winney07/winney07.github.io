---
title: SVG图片的使用
date: 2019-07-29 11:25:24
tags:
- SVG
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