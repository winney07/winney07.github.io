---
title: HTML-笔记
date: 2021-01-18 14:17:09
tags:
- HTML
categories:
- 工作笔记
- HTML
---

## 传统前端

还原“活”的设计

设计稿→PS >HTML页面+效果

一切图→写标签和样式>实现效果



## HTML5时代的大前端

各种端的兼容开发(PC、移动端)

移动APP开发和移动站点开发

Ajax+服务器端技术开发

高级设计模式和框架(MVC、 AngularJS、 ..)

自动化工作流( Grunt)

网站安全、SEO、测试、源代码管理、团队合作

HTML5游戏



使用HTML5开发原生APP

### 全栈工程师

集前端和后端一体的大牛

专多能的时代

前后台通吃，快速解决问题

NodeJS：无所不能

现在的前端已经是突破所有边界的前端。

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



#### Html的命名规则
- ##### 文件名称命名规则

  - 统一使用小写的英文字母、数字和下划线的组合，不得包含汉字、空格和特殊字符

  - 命名的原则
    - 方便理解

    - 方便查找
- ##### 索引文件命名原则

  - index.htm
  - index.html
  - index.asp
  - index.aspx
  - index.jsp
  - index.php
- ##### 各子页命名的原则

  - 统一用翻译的英文命名
  - 统一用拼音命名
  - 注意：不要英语拼音混用

# Web前端基础课程内容

## 第一阶段: Web前端开发环境搭建

- 操作系统操作常用高级设置和快捷键
- Sublime安装和配置
- Atom安装和配置
- WebStorm安装和配置

## 第二阶段: HTML5基础

- HTML基础
- 语义化标签与SEO

## 第三阶段: CSS3基础

- CSS属性基础
- CSS布局
- 面向对象的CSS
- less、 sass、 styleus、 postcss

## 第四阶段: JavaScript基 础

- JavaScript语 法基础
- JavaScript数组、 字符串、流程控制语句、
- JavaScript高级 简介

## 综合项目

# HTML基础

#### 什么是浏览器?

- 360双核浏览器、qq浏览器

- 浏览器与浏览器内核:
- ie: trident、 safari：webkit、 ff：gecko 、chrome、opera：blink

#### 什么是服务器和服务器端程序?

浏览器浏览页面背后的秘密(了解)

- 浏览器接受用户操作→浏览器封装HTTP请求→连接服务器: DNS解析> 发送请求Request>服务器接收请求>处理请求>返回响应报文→浏览器接收响应报文→渲染页面呈现
- HTTP协议(了解，就业班详细讲)



服务器也是一台电脑，专门为用户进行服务，处理一些网站的请求。



![img](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/HTML-%E7%AC%94%E8%AE%B0/note3.png)



## HTML发展历程

HTML 1.0超文本标记语言(第一版)--在1993年6月发为互联网工程工作小组(IETF)工作草案发布(并非标准)

HTML 2.0-- 1995年11月作为RFC 1866发布,在RFC 2854于2000年6月发布之后被宣布已经过时

HTML3.2-- 1996年1月14日,W3C推荐标准

HTML 4.0-- 1997年12月18日,W3C推荐标准

HTML 4.01(微小改进) - 1999年12月24日,W3C推荐标准

XHTML 1.0--发布于2000年1月26日,是W3C推荐标准，后来经过修订于2002年8月1日重新发布

XHTML 1.1--于2001年5月31日发布

HTML5.0 2014年10月29日，万维网联盟宣布，经过接近8年的艰苦努力，该标准规范终于制定完成



## 名词解释

Internet：因特网，互联网。可以实现全球信息互联的网络。

WWW：万维网(world wide web)，它是提供网站相关服务，人们可以通过万维网服务进行网上聊天、网上冲浪、网购、搜索资料、查看天气、查看新闻、交友聊天等!

W3C：万维网联盟创建于1994年是Web技术领域最具权威和影响力的国际中立性技术标准机构。我们后面学的html、css等标准都是由此机构主导制定。

HTTP：超文本传输协议(HTTP， HyperText Transfer Protocol)，也就是浏览器和服务器端的网页传输数据的约束和规范。

Web：web ( 互联网总称) web的本意是蜘蛛网和网的意思，在网页设计中我们称为网页的意思。现广泛译作网络、互联网等技术领域。表现为三种形式，即超文本(hypertext) 、超媒体(hypermedia) 、超文本传输协议(HTTP)等。

DNS：DNS ( Domain Name System,域名系统)，因特网上作为域名和IP地址相互映射的一个分布式数据库，能够使用户更方便的访问互联网，而不用去记住能够被机器直接读取的IP数串。通过主机名，最终得到该主机名对应的IP地址的过程叫做域名解析(或主机名解析)



![img](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/HTML-%E7%AC%94%E8%AE%B0/note4.png)



## 网页的组成

- HTML：页面结构
- CSS：页面样式表现
- JavaScript：交互行为

HTML简介

\- HTML (英文Hyper Text Markup Language的缩写)中文译为超文本标记语言”，主要是通过HTML标记对网页中的文本、图片、声音等内容进行描述。

\- HTML提供了许多标记，如段落标记、标题标记、超链接标记、图片标记等，网页中需要定义什么内容，就用相应的HTML标记描述即可。

\- HTML之所以称为超文本标记语言，不仅是因为他通过标记描述网页内容，同时也由于文本中包含了所谓的“超级链接”点。通过超链接将网站与网页以及各种网页元素链接起来，构成了丰富多彩的Web页面。



#### end:让光标快速定位到结尾

#### home:让光标快速定位到行首



```plain
<html lang="zh_CN">
</html>
```



## HTML头部标签

doctype标签

head标签

title标签

link标签

meta标签

script标签

style标签



### 1.1 HTML文件的后缀

#### HTML文档的后缀名:.html    .htmn

在早期的dos8位机的时代，电脑只识别3个字母的后缀名文件。所以HTML文件的后缀为: htm

现在所有的电脑都支持多字符的文件后缀名，所以现在大家都在使用.html后缀名了，

当然用.htm  == .html进行命名html文档的后缀名都是一样的效果



#### 快速生成html

```plain
html:5 + tab键

html:4s + tab键

html:4t + tab键
```

#### 乱码处理

当浏览器解析当前文档的编码，和文档实际的编码不一-致的时候那么会出现乱码的问题。

```plain
<meta charset="UTF-8"> <!-- 设置了当前页面的编码用UTF-8 -->
```

Head标签中设置都是用于给浏览器使用的一些配置和设置。比如meta标签告诉浏览器当前文档的编码格式。



## HTML基本文档格式一`<meta>` 标记

- `<meta charset="UTF-8">`
- utf-8是目前最常用的字符集编码方式，常用的字符集编码方式还有gbk和gb2312。
- gb2312简单中文
- GBK包含全部中文字符繁体
- BIG5繁体中文
- UTF-8则包含全世界所有国家需要用到的字符
- 从二进制说起，符号表示文字，表示的模式就是编码:联想电报



`ctrl + shift + D`：快速复制一行代码



## Link标签

- dns预解析(了解)
- `<link rel="dns-prefetch" href="http://mimg.127.net">`
- 引入网站icon图标:
- `<link rel="shortcut icon" href="http://www.126.com/favicon.ico" />`
- 引入css样式， [后面讲]
- `<link rel="stylesheet" href="css/ bg.css">`



### 域名预解析-提高效率

域名预解析，可以有效地提高网站后续访问的效率。（网站优化的时候做）

如果在页面中访问的资源用到http://mimg.127.net，不用再进行域名解析。提高效率

### shortcut

`<link rel- shortcut icon" hret= "http://www.126. com/favicon.ico">`



## URL协议

URL协议: Uniform Resource Locator,统一资源定 位符是对可以从互联网上得到的资源的位置和访问方法的一种简洁的表示，是互联网上标准资源的地址。互联网上的每个文件都有一个唯一的URL,它包含的信息指出文件的位置以及浏览器应该怎么处理它。



- 协议规定格式: scheme://host.domain:port/path/filename
- scheme -定义因特网服务的类型。最常见的类型是http
- host-定义域主机(http的默认主机是www)
- domain-定义因特网域名，比如w3school.com.cn
- port-定义主机上的端口号(http的默认端口号是80)
- path-定义服务器上的路径(如果省略，则文档必须位于网站的根目录中)。
- filename-定义文档/资源的名称

常见协议: http、 https、 ftp、 迅雷协议等.

URL编码: url中的非ASCII码， 转为%ascii码



平时我们写的网址就是url 地址。

Url协议就是规定url地址的格式。



![img](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/HTML-%E7%AC%94%E8%AE%B0/note5.png)

协议名称://域名(ip 地址):80/路径文件a.htm



 

## URL编码

将中文或其他语言的文字转换为ascii码，便于在不同国家，浏览器没有安装对应字体字符集的情况下，能够正常地访问同一个网页。

为什么要有URL编码呢?

如果我写的一个中文的网页要在阿拉伯国家的电脑上进行显示。

http://www. sina com.cn/c/zg/2015-10-27/doc-传智播客61.html

中文字符在阿拉伯国家的电脑上会正常显示吗?

```plain
encodeURI('编码')
```

[URL在线编码解码工具（UrlEncode编码 和 UrlDecode解码）](http://www.jsons.cn/urlencode/)



## 常用的图像格式

#### GIF格式

GIF最突出的地方就是他支持动画，同时GIF也是一种无损的图像格式，也就是说修改图片之后，图片质量几乎没有损失。再加上GIF支持透明（全透明或全不透明)，因此很适合在互联网上使用。但GIF只能处理256种颜色。在网页制作中，GIF格式常常用于Logo、小图标及其他色彩相对单一的图像。
`总结:小、兼容性好、支持透明、色彩太多不行。`

#### JPG格式

JPEG格式是网络上比较流行的一种格式，其文件扩展名为.jpg或.jpeg。JPEG是一种有损压缩格式，其文件体积非常小，非常有利于网络传输，但由于是有损压缩，所以将一幅图像转换为JPEG格式后图像质量会降低。
`一般用于广告，大的宣传的图片，照片等`

#### PNG格式

PNG包括PNG-8和真色彩PNG(PNG-24和PNG-32）。相对于GIF，PNG最大的优势是体积更小，支持alpha透明(全透明，半透明，全不透明），并且颜色过渡更平滑，但PNG不支持动画。同时需要注意的是IE6是可以支持PNG-8的，但在处理PNG-24的透明时会显示为灰色。通常，图片保存为PNG-8会在同等质量下获得比GIF更小的体积，而半透明的图片只能使用PNG-24。



`IE浏览器选择Gif会更好一些。`

dtd：文档类型的定义

## 标题标签

h1： 一般情况下，一个页面只能有一个h1标题 

H1标题标签上标注当前页面中的文档最重要的核心主题的文本。

H1到H6标签，相对于当前文档的重要性依次降低。注意h1标签在整个页面中最多一次（当然可以超过，但是不利于搜索SEO)

H2以后的这些标签可以在一个页面中有多个，但是不要滥用，滥用会导致网页的SEO受影响，搜索引擎会认为我们作弊。

H1到H6标签不是用于字体大小的样式设置。

## 段落标签

段落标签也只能嵌套行内标签



## 水平线 

```plain
<hr/>
```

浏览器会将多个空格和换行合并为一个空格

## 换行

```plain
<br/>
```

## 锚点链接

```plain
<span id="demo">标题</span>

<a href="demo">去到标题的位置</a>
```

## 列表

无序：ul

有序：ol（order list）

定义列表：dl



## 表单组合标签

#### fieldset

```plain
<form>
  <fieldset>
    <legend>用户组1</legend>
  </fieldset>

  <fieldset>
    <legend>用户组2</legend>
  </fieldset>
</form>
```

## 内联框架标签iframe

尽量不用



## 字符实体HTML特殊符号处理

特殊字符标记



## HTML语义化