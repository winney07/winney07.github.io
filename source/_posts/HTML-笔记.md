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

[HTML elements reference](https://developer.mozilla.org/en-US/docs/Web/HTML/Element)

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





#### meta标签

```
<meta name="screen-orientation" content="portrait"><!-- uc强制竖屏 -->
<meta name="x5-orientation" content="portrait"><!-- QQ强制竖屏 -->
```

##### [移动前端常用meta标签](https://www.cnblogs.com/qiye2016/p/5807524.html)

摘自：[HTML meta标签总结,HTML5 head meta属性整理](http://caibaojian.com/mobile-meta.html)， 仅用于学习

```
!DOCTYPE html> <!-- 使用 HTML5 doctype，不区分大小写 -->
<html lang="zh-cmn-Hans"> <!-- 更加标准的 lang 属性写法 http://zhi.hu/XyIa -->
<head>
    <!-- 声明文档使用的字符编码 -->
    <meta charset='utf-8'>
    <!-- 优先使用 IE 最新版本和 Chrome -->
    <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1"/>
    <!-- 页面描述 -->
    <meta name="description" content="不超过150个字符"/>
    <!-- 页面关键词 -->
    <meta name="keywords" content=""/>
    <!-- 网页作者 -->
    <meta name="author" content="name, email@gmail.com"/>
    <!-- 搜索引擎抓取 -->
    <meta name="robots" content="index,follow"/>
    <!-- 为移动设备添加 viewport -->
    <meta name="viewport" content="initial-scale=1, maximum-scale=3, minimum-scale=1, user-scalable=no">
    <!-- `width=device-width` 会导致 iPhone 5 添加到主屏后以 WebApp 全屏模式打开页面时出现黑边 http://bigc.at/ios-webapp-viewport-meta.orz -->
 
    <!-- iOS 设备 begin -->
    <meta name="apple-mobile-web-app-title" content="标题">
    <!-- 添加到主屏后的标题（iOS 6 新增） -->
    <meta name="apple-mobile-web-app-capable" content="yes"/>
    <!-- 是否启用 WebApp 全屏模式，删除苹果默认的工具栏和菜单栏 -->
 
    <meta name="apple-itunes-app" content="app-id=myAppStoreID, affiliate-data=myAffiliateData, app-argument=myURL">
    <!-- 添加智能 App 广告条 Smart App Banner（iOS 6+ Safari） -->
    <meta name="apple-mobile-web-app-status-bar-style" content="black"/>
    <!-- 设置苹果工具栏颜色 -->
    <meta name="format-detection" content="telphone=no, email=no"/>
    <!-- 忽略页面中的数字识别为电话，忽略email识别 -->
    <!-- 启用360浏览器的极速模式(webkit) -->
    <meta name="renderer" content="webkit">
    <!-- 避免IE使用兼容模式 -->
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <!-- 不让百度转码 -->
    <meta http-equiv="Cache-Control" content="no-siteapp" />
    <!-- 针对手持设备优化，主要是针对一些老的不识别viewport的浏览器，比如黑莓 -->
    <meta name="HandheldFriendly" content="true">
    <!-- 微软的老式浏览器 -->
    <meta name="MobileOptimized" content="320">
    <!-- uc强制竖屏 -->
    <meta name="screen-orientation" content="portrait">
    <!-- QQ强制竖屏 -->
    <meta name="x5-orientation" content="portrait">
    <!-- UC强制全屏 -->
    <meta name="full-screen" content="yes">
    <!-- QQ强制全屏 -->
    <meta name="x5-fullscreen" content="true">
    <!-- UC应用模式 -->
    <meta name="browsermode" content="application">
    <!-- QQ应用模式 -->
    <meta name="x5-page-mode" content="app">
    <!-- windows phone 点击无高光 -->
    <meta name="msapplication-tap-highlight" content="no">
    <!-- iOS 图标 begin -->
    <link rel="apple-touch-icon-precomposed" href="/apple-touch-icon-57x57-precomposed.png"/>
    <!-- iPhone 和 iTouch，默认 57x57 像素，必须有 -->
    <link rel="apple-touch-icon-precomposed" sizes="114x114" href="/apple-touch-icon-114x114-precomposed.png"/>
    <!-- Retina iPhone 和 Retina iTouch，114x114 像素，可以没有，但推荐有 -->
    <link rel="apple-touch-icon-precomposed" sizes="144x144" href="/apple-touch-icon-144x144-precomposed.png"/>
    <!-- Retina iPad，144x144 像素，可以没有，但推荐有 -->
    <!-- iOS 图标 end -->
 
    <!-- iOS 启动画面 begin -->
    <link rel="apple-touch-startup-image" sizes="768x1004" href="/splash-screen-768x1004.png"/>
    <!-- iPad 竖屏 768 x 1004（标准分辨率） -->
    <link rel="apple-touch-startup-image" sizes="1536x2008" href="/splash-screen-1536x2008.png"/>
    <!-- iPad 竖屏 1536x2008（Retina） -->
    <link rel="apple-touch-startup-image" sizes="1024x748" href="/Default-Portrait-1024x748.png"/>
    <!-- iPad 横屏 1024x748（标准分辨率） -->
    <link rel="apple-touch-startup-image" sizes="2048x1496" href="/splash-screen-2048x1496.png"/>
    <!-- iPad 横屏 2048x1496（Retina） -->
 
    <link rel="apple-touch-startup-image" href="/splash-screen-320x480.png"/>
    <!-- iPhone/iPod Touch 竖屏 320x480 (标准分辨率) -->
    <link rel="apple-touch-startup-image" sizes="640x960" href="/splash-screen-640x960.png"/>
    <!-- iPhone/iPod Touch 竖屏 640x960 (Retina) -->
    <link rel="apple-touch-startup-image" sizes="640x1136" href="/splash-screen-640x1136.png"/>
    <!-- iPhone 5/iPod Touch 5 竖屏 640x1136 (Retina) -->
    <!-- iOS 启动画面 end -->
 
    <!-- iOS 设备 end -->
    <meta name="msapplication-TileColor" content="#000"/>
    <!-- Windows 8 磁贴颜色 -->
    <meta name="msapplication-TileImage" content="icon.png"/>
    <!-- Windows 8 磁贴图标 -->
 
    <link rel="alternate" type="application/rss+xml" title="RSS" href="/rss.xml"/>
    <!-- 添加 RSS 订阅 -->
    <link rel="shortcut icon" type="image/ico" href="/favicon.ico"/>
    <!-- 添加 favicon icon -->

    <!-- sns 社交标签 begin -->
    <!-- 参考微博API -->
    <meta property="og:type" content="类型" />
    <meta property="og:url" content="URL地址" />
    <meta property="og:title" content="标题" />
    <meta property="og:image" content="图片" />
    <meta property="og:description" content="描述" />
    <!-- sns 社交标签 end -->
 
    <title>标题</title>
</head>
```

上面给出了常用的一些meta属性，下面给一个对meta使用的理解。 meta是html语言head区的一个辅助性标签。也许你认为这些代码可有可无。其实如果你能够用好meta标签，会给你带来意想不到的效果，meta标签的作用有：搜索引擎优化（SEO），定义页面使用语言，自动刷新并指向新的页面，实现网页转换时的动态效果，控制页面缓冲，网页定级评价，控制网页显示的窗口等！ meta标签的组成：meta标签共有两个属性，它们分别是http-equiv属性和name属性，不同的属性又有不同的参数值，这些不同的参数值就实现了不同的网页功能。 **1、name属性** name属性主要用于描述网页，与之对应的属性值为content，content中的内容主要是便于搜索引擎机器人查找信息和分类信息用的。 meta标签的name属性语法格式是：

```
<meta name="参数"content="具体的参数值">。 
```

其中name属性主要有以下几种参数： **A、Keywords(关键字)** 说明：keywords用来告诉搜索引擎你网页的关键字是什么。 举例：

```
<meta name="keywords"content="meta总结,html meta,meta属性,meta跳转"> 
```

**B、description(网站内容描述)** 说明：description用来告诉搜索引擎你的网站主要内容。 举例：

```
<meta name="description"content="haorooms博客,html的meta总结，meta是html语言head区的一个辅助性标签。"> 
```

**C、robots(机器人向导)** 说明：robots用来告诉搜索机器人哪些页面需要索引，哪些页面不需要索引。 content的参数有all,none,index,noindex,follow,nofollow。默认是all。 举例：

```
<meta name="robots"content="none"> 
```

**具体参数如下：** 信息参数为all：文件将被检索，且页面上的链接可以被查询； 信息参数为none：文件将不被检索，且页面上的链接不可以被查询； 信息参数为index：文件将被检索； 信息参数为follow：页面上的链接可以被查询； 信息参数为noindex：文件将不被检索，但页面上的链接可以被查询； 信息参数为nofollow：文件将被检索，但页面上的链接不可以被查询； **D、author(作者)** 说明：标注网页的作者 举例：

```
<meta name="author"content="root,root@xxxx.com"> 
```

**E、generator**

```
<meta name="generator"content="信息参数"/> 
```

meta标签的generator的信息参数，代表说明网站的采用的什么软件制作。 **F、COPYRIGHT**

```
<META NAME="COPYRIGHT"CONTENT="信息参数"> 
```

meta标签的COPYRIGHT的信息参数，代表说明网站版权信息。 **G、revisit-after**

```
<META name="revisit-after"CONTENT="7days"> 
```

revisit-after代表网站重访,7days代表7天，依此类推。 **2、http-equiv属性** http-equiv顾名思义，相当于http的文件头作用，它可以向浏览器传回一些有用的信息，以帮助正确和精确地显示网页内容，与之对应的属性值为content，content中的内容其实就是各个参数的变量值。 meta标签的http-equiv属性语法格式是：

```
<meta http-equiv="参数"content="参数变量值">； 
```

其中http-equiv属性主要有以下几种参数： **A、Expires(期限)** 说明：可以用于设定网页的到期时间。一旦网页过期，必须到服务器上重新传输。 用法：

```
<meta http-equiv="expires"content="Fri,12Jan200118:18:18GMT"> 
```

注意：必须使用GMT的时间格式。 **B、Pragma(cache模式)** 说明：禁止浏览器从本地计算机的缓存中访问页面内容。 用法：

```
<meta http-equiv="Pragma"content="no-cache"> 
```

注意：这样设定，访问者将无法脱机浏览。 **C、Refresh(刷新)** 说明：自动刷新并指向新页面。 用法：

```
<meta http-equiv="Refresh"content="2;URL=http://www.haorooms.com"> //(注意后面的引号，分别在秒数的前面和网址的后面) 
```

注意：其中的2是指停留2秒钟后自动刷新到URL网址。 **D、Set-Cookie(cookie设定)** 说明：如果网页过期，那么存盘的cookie将被删除。 用法：

```
<meta http-equiv="Set-Cookie"content="cookie value=xxx;expires=Friday,12-Jan-200118:18:18GMT；path=/"> 
```

注意：必须使用GMT的时间格式。 **E、Window-target(显示窗口的设定)** 说明：强制页面在当前窗口以独立页面显示。 用法：

```
<meta http-equiv="Window-target"content="_top"> 
```

注意：用来防止别人在框架里调用自己的页面。 **F、content-Type(显示字符集的设定)** 说明：设定页面使用的字符集。 用法：

```
<meta http-equiv="content-Type"content="text/html;charset=gb2312"> 
```

**具体如下：** meta标签的charset的信息参数如GB2312时，代表说明网站是采用的编码是简体中文； meta标签的charset的信息参数如BIG5时，代表说明网站是采用的编码是繁体中文； meta标签的charset的信息参数如iso-2022-jp时，代表说明网站是采用的编码是日文； meta标签的charset的信息参数如ks_c_5601时，代表说明网站是采用的编码是韩文； meta标签的charset的信息参数如ISO-8859-1时，代表说明网站是采用的编码是英文； meta标签的charset的信息参数如UTF-8时，代表世界通用的语言编码； **G、content-Language（显示语言的设定）** 用法：

```
<meta http-equiv="Content-Language"content="zh-cn"/> 
```

**H、Cache-Control指定请求和响应遵循的缓存机制。** Cache-Control指定请求和响应遵循的缓存机制。在请求消息或响应消息中设置Cache-Control并不会修改另一个消息处理过程中的缓存处理过程。请求时的缓存指令包括no-cache、no-store、max-age、max-stale、min-fresh、on ly-if-cached，响应消息中的指令包括public、private、no-cache、no-store、no-transform、must-revalidate、proxy-revalidate、max-age。各个消息中的指令含义如下 Public指示响应可被任何缓存区缓存 Private指示对于单个用户的整个或部分响应消息，不能被共享缓存处理。这允许服务器仅仅描述当用户的部分响应消息，此响应消息对于其他用户的请求无效 no-cache指示请求或响应消息不能缓存 no-store用于防止重要的信息被无意的发布。在请求消息中发送将使得请求和响应消息都不使用缓存。 max-age指示客户机可以接收生存期不大于指定时间（以秒为单位）的响应 min-fresh指示客户机可以接收响应时间小于当前时间加上指定时间的响应 max-stale指示客户机可以接收超出超时期间的响应消息。如果指定max-stale消息的值，那么客户机可以接收超出超时期指定值之内的响应消息。 **J、http-equiv="imagetoolbar"**

```
<meta http-equiv="imagetoolbar"content="false"/> 
```

指定是否显示图片工具栏，当为false代表不显示，当为true代表显示。 **K、Content-Script-Type**

```
<Meta http-equiv="Content-Script-Type"Content="text/javascript"> 
```

W3C网页规范，指明页面中脚本的类型。 **HTML < base > 标签** 为页面上所有链接指定默认打开方式： 例如：

```
<base target="_self">
```





#### html实现打电话,发短信,发邮件

```
<a href="tel:10086">拨打电话</a>
<a href="sms:18945086283?body=短信内容">发送短信</a>
<a href="mailto:mail@mail.com">发送邮件</a>
```

