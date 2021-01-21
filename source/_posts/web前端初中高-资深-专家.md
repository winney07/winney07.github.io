---
title: web前端初中高+资深+专家
date: 2021-01-21 17:31:35
tags:
- 听课笔记
categories:
- 工作笔记
- 听课笔记
---

课程网址：[【极客学院】web前端工程师 初级+中级+高级+资深+专家级（五部分完）](https://www.bilibili.com/video/av46236917?from=search&seid=11530041288730825105)

### HTML5与HTML4的区别

#### 一、推出的理由及目标

HTML5的出现，对于Web来说意义是非常重大的，因为他的意图是想要把目前Web上存在的各种问题一并解决掉了。

- Web浏览器之间的兼容性很低

- 文档结构不够明确

- Web应用程序的功能受到了限制

  世界知名浏览器厂商对HTML5的支持
  微软、Google、苹果、Opera、Mozilla

#### 二、语法的改变

- 内容类型
- DOCTYPE声明
- 指定字符编码
- 可以省略标记的元素
- 具有boolean值的属性
- 省略引号

```
<input type="checkbox" checked="checked">
```

可省略引号：

```
<input type="checkbox" checked=checked>
```

#### 三、新增的元素和废除的元素

- 新增的结构元素

  section、article、aside、header、hgroup、footer、nav、figure

- 新增的其他元素
  video、audio、embed、mark、progress、meter、time、ruby、rt、rp、wbr、canvas、command、details、datalist、datagrid、keygen、output、source、menu

- 新增的input元素的类型
  email、url、number、range、Date Pickers

#### 四、新增的属性和废除的属性

- contentEditable属性
- designMode属性
- hidden属性
- spellcheck属性
- tabindex属性

> hidden属性：hidden的元素不渲染

tabindex为-1时按tab获取不了焦点，但开发中js可以获取

```
<a href="#"tabindex=""1">hello</a>
<a href="#"tabindex="3">hello</a>
<a href="#"tabindex="2">hello</a>
<ul tabindex="-1">
	<li>1</li>
	<li>1</li>
	<li>1</li>
	<li>1</li>
</ul>
```

#### 五、全局属性