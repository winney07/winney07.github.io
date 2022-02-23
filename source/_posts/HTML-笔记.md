---
title: HTML-笔记
date: 2021-01-18 14:17:09
tags:
- HTML
categories:
- 工作笔记
- HTML
---

![元素结构](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/HTML-%E7%AC%94%E8%AE%B0/note1.png)
![层级结构](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/HTML-%E7%AC%94%E8%AE%B0/note2.png)

1、html

HTML：hyperText markup language (超文本标记语言）

2、是由标签组成的，解释标签是怎样的

根标签：

```
<html>
</html>
```

3、头标签，身体标签，类似人，头部是装思想的，身体是衣服样子

写一个简单的英文，然后写中文乱码，因为是国外人创造的，不认识中文，需要告诉浏览器，要以中文的形式显示，然后要加meta标签，单加标签没有用。要加属性，解释属性

Lang属性是告诉搜索引擎爬虫，我们的网站是关于什么内容的

Lang = ‘en’ 英文的

Lang = ‘zh’ 中文的

```
<html lang="en">
<head>
	<meta charset="utf-8">
	<!-- gb2312 gbk unicode-->
	<!-- Utf-8是unicode的升级版 -->
</head>
	<body>
	Life is shit!!!美好的生活!!!
</body>
</html>

```

#### select下拉框，添加分组(optgroup)

```
<select>
  <optgroup label="蔬菜">
    <option value ="娃娃菜">娃娃菜</option>
    <option value ="西红柿">西红柿</option>
  </optgroup>

  <optgroup label="水果">
    <option value ="苹果">苹果</option>
    <option value ="蓝莓">蓝莓</option>
  </optgroup>
</select>
```

#### 添加网页图标（favicon)

```
<link rel="shortcut icon" href=" /favicon.ico" />
```



