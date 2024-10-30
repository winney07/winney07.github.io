---
title: 前端CSS处理
date: 2020-03-22 10:12:23
tags:
- CSS
categories: 
- CSS
---

#### 要让一张图片在页面中以最佳效果铺满整屏，同时在不同设备上保持一致的显示效果

```
html, body {
    margin: 0;
    padding: 0;
    height: 100%;
    overflow: hidden;
}

img {
    width: 100%;
    height: 100%;
    object-fit: cover;
}
```





#### 压缩字体文件的大小



### 处理`CSS`兼容性

> 如果一个浏览器在解析你所书写的 CSS 规则的过程中遇到了无法理解的属性或者值，它会忽略这些并继续解析下面的 CSS 声明。在你书写了错误的 CSS 代码（或者误拼写），又或者当浏览器遇到对于它来说很新的还没有支持的 CSS 代码的时候上述的情况同样会发生（直接忽略）。
>
> 相似的，当浏览器遇到无法解析的选择器的时候，他会直接忽略整个选择器规则，然后解析下一个 CSS 选择器。

> 这样做好处多多，代表着你使用最新的 CSS 优化的过程中浏览器遇到无法解析的规则也不会报错。当你为一个元素指定多个 CSS 样式的时候，浏览器会加载样式表中的最后的 CSS 代码进行渲染（样式表，优先级等请读者自行了解），也正因为如此，你可以为同一个元素指定多个 CSS 样式来解决有些浏览器不兼容新特性的问题（比如指定两个`width`）。
>
> 这一特点在你想使用一个很新的 CSS 特性但是不是所有浏览器都支持的时候（浏览器兼容）非常有用，举例来说，一些老的浏览器不接收`calc()`(calculate 的缩写，CSS3 新增，为元素指定动态宽度、长度等，注意此处的动态是计算之后得一个值) 作为一个值。我可能使用它结合像素为一个元素设置了动态宽度（如下），老式的浏览器由于无法解析忽略这一行；新式的浏览器则会把这一行解析成像素值，并且覆盖第一行指定的宽度。

```
.box {
  width: 500px;
  width: calc(100% - 50px);
}
```

### 控制用户是否可以选择文本-[user-select](https://developer.mozilla.org/zh-CN/docs/Web/CSS/user-select)

```
<p>你应该可以选中这段文本。</p>
<p class="unselectable">嘿嘿，你不能选中这段文本！</p>
<p class="all">点击一次就会选中这段文本。</p>
```

```
.unselectable {
  -webkit-user-select: none; /* Safari */
  user-select: none;
}

.all {
  -webkit-user-select: all;
  user-select: all;
}
```
