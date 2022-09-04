---
title: HTML5-笔记
date: 2021-09-02 14:55:04
tags:
- HTML5
---

#### HTML5新特性

- 拖放(Drag and drop ) API.
- 语义化更好的内容标签 (header、nav、 footer、aside、article、 section )。
- 音频、视频 (audio、 video) API
- 画布( Canvas ) API.
- 地理(Geolocation) API.
- 本地离线存储（localStorage），即长期存储数据，浏览器关闭后数据不丢失。
- 会会话存储(sessionStorage），即数据在浏览器关闲后自动删除。
- 表单控件包括 calendar、date、time 、 email、url、 search
- 新的技术包括 webworker、 websocket、Geolocation.

#### HTML5 新增的API

新增的功能 API 包括 Media API、Text Track API、 Application Cache API、 User Interaction、Data Transfer API、 Command API.、Constraint Validation API、History API.

#### HTML5移除元素

移除的元素如下：

- 纯表现的元素，包括 basefont、big、center、 font、 s、 strike、tt、 u
- 对可用性产生负面影响的元素，包括 frame、frameset、 Noframes

#### 新的HTML5 文档类型和字符集

HTML5文档类型是`<!doctype html>`
HTML5 使用的宇符集`<meta charset="UTF-8">`

#### HTML5 的离线存储

- localStorage，可长期存储数据，即浏览器关闭后数据不丢失。
- sessionStorage，数据在浏览器关闭后自动删除。

#### HTML5 的form关闭自动补全功能

将不想要提示的form 元素下的 input 元素的autocomplete 属性设置为off.

#### HTML5 页面中嵌入音频

> 支持的格式包括 MP3、 Wav 和Ogg等

```
<audio controls>
  <source sr="icketang.mp3" type="audio/mpeg">
  Your browser does'nt support audio embedding feature
</audio>
```

#### HTML5 页面中嵌入视频

> 支持的格式包括MP4、 WebM和Ogg 等

```
<video width="450" height="340" controls>
  <source src="icketang.mp4" type="video/mp4">
  Your browser does'nt support video embedding feature.
</video>
```

#### HTML5 引入新的表单属性

datalist、datetime、output、keygen、date、month、week、time、number、 range、 emailurl.

#### HTML5 应用缓存和常规的 HTML 浏览器缓存的差别

HTML5应用缓存最关键的就是支持离线应用，可荻取少数或者全部网站内容包括 HTTML、CSS、图像和 JavaScript 脚本 并存在本地。该特性提升了网站的性能，可通过如下方式实现

```
<!doctype html>
  <html manifest="example.appcache">
</html>
```

> 与传统的浏览器缓存比较，该特性并不强制要求用户访问网站





> HTML5 没有使用 SGML 或者 XHTML，它是一个全新的类型，因此不需要参考DTD。对于HTML5，仅须放置下面的文档类型代码，让浏览器识别HTML5 文档。
> 如果不放入＜！doctype html>标签，HITML5 不会工作。浏览器将不能识别出它是HTML文档，同时HTMLS 的标签将不能正常工作。

#### WebSocket

它是 Web 应用程序的传输协议，提供了双向的、按序到达的数据流。它是HTML5新增的协议，webSocket 的连接是持久的，它在客户端和服务器之间保特双工连接，服务器的更新可以及时推送到客户端，而不需要客户端以一定的时间间隔去轮询

#### 实现浏览器内多个标签页之间的通信

在标签页之间，调用 localstorge、cookies 等数据存储，可以实现标签页之问的通信

#### localStorage 和cookie 的区别

​		localStorage 的概念和 cookie 相似，区别是 localStorage 是为了更大容量的存储设计的。cookie 的大小是受限的，并且每次请求一个新页面时，cookie 都会被发送过去，这样无形中浪费了带宽。另外，cookie 还需要指定作用域，不可以跨域调用。
​		除此之外，localStorage 拥有 setltem、getltem、removeltem、clear 等方法，cookie 则需要前端开发者自己封装 setCookie 和getcookie。但cookie 也是不可或缺的，因为 cookie的作用是与服务器进行交互，并且还是 HTTP 规范的一部分，而localStorage 仅因为是为了在本地“存储”数据而已，无法跨浏览器使用。

#### cookie 的特点

cookie 虽然为持久保存客户湍数据提供了方便，分担了服务器存储的负担，但是有以下局限性。

1. 每个特定的域名下最多生成20个 cookie。
2. IE6 或更低版本最多有20个cookie。
3. I7和之后的版本最多可以有50个 cookie.
4.  Firefox 最多可以有50个cookie。
5. Chrome 和 Safari 没有做硬性限制。

IE和Opera 会清理近期最少使用的cookie， Firefox 会随机清理 cookie.
cookie 最大为 4096字节，为了兼容性，一般不能超过 4095 字节。
IE提供了一种存储方式，可以让用户数据持久化，叫作userdata，从IE5.0 就开始支持此功能。每块数据最多 128KB，每个域名下最多1MB。这个持久化数据放在缓存中，如果果缓存没有被清理，就会一直存在。
优点如下：

1. 通过良好的编程，控制保存在cookie 中的 session 对象的大小
2. 通过加密和安全传输技术（SSL)，降低cookie被破解的可能性。
3. 只在cookie 中存放不敏感数据，即使被盗也不会有重大损失。
4. 控制cookie 的生命周期，使之不会永远有效。数据偷盗者很可能得到一个过期的cookie.

缺点如下：

1. scookie” 的数量和长度有限制。每个domain 最多只能有20条cookie，每个cookie 的长度不能超过 4KB，否则会被截掉。
2. 安全性问题。如果cookie 被别人拦截了，就可以取得所有的session 信息。即使加密也于事无补，因为拦截者并不需要知道cookie 的意义，他只要原样转发 cookie就可以达到目的。
3. 有些状态不可能保存在客产端。例如，为了防止重复提交表单，我们需要在服务器端保存一个计数器。如果把这个计数器保存在客户端，那么它起不到任何作用。

#### cookie 和session 的区别

1. cookie 数据存放在客户的浏览器上，session 数据存放在服务器上。
2. cookie 不是很安全，别人可以分析存放在本地的cookie 并进行 cookie 欺骗。考虑到安全问题应当使用 session。
3. session 会在一定时问内保存在服务器上。当访问增多时，会占用较多服务器的资源。为了减轻服务器的负担，应当使用 cookie。
4. 单个cookie 保存的数据不能超过 4KB，很多浏览器都限制一个站,点最多保存20 个cookie.

> 建议可以将登录信息等重要信息存放在session 中，其他信息（如果需要保留）可以存放在cookie 中

#### SVG

SVG即可缩放矢量因形(Scalable Vector Graphics )。它是基于文本的图形语言，使用文本、线条、点等来绘制图像，这使得它轻便、显示迅速

#### Canvas 和 SVG 的区别

1. 一旦 Canvas 绘制完成将不能访问像素或操作它；任何使用SVG绘制的形状都能被记忆和操作，可以被浏览器再次显示。
2. Canvas 对绘制动画和游戏非常有利；SVG对创建图形（如CAD）非常有利
3. 因为不需要记住以后事情，所以 Canvas 运行更快；因为为了之后的操作，SVG需要记录坐标，所以运行比较缓慢。
4. 在Canvas 中不能为绘制对象邬定相关事件；在SVG 中可以为绘制对象绑定相关事件
5. Canvas绘制出的是位图，因此与分辨率有关；SVG绘制出的是矢量图，因此与分辨率无关。

#### HTML5 中实现应用缓存

首先，需要指定"manifest” 文件，“manifest”文件帮助你定义缓存如何工作。

"manifest"文件的结构：

```
CACHE MANIFEST
# version 1.0
/demo.css
/demo.js
/demo.png
所有manifest 文件都以"CACHE MANIFEST"语句开始。
＃(散列标签）有助于提供缓存文件的版本。
manifest 文件的内容类型应是"text/cache-manifest"
```

创建一个缓存manifest 文件后，在HTML 页面中提供manifest 链接，代码如下所示。

```
<html manifest="icketang.appcache">
```

第一次运行以上文件时，它会添加到浏览器应用缓存中，在服务器宕机时，页面从应用缓存中获取数据

#### 刷新浏览器的应用缓存

应用缓存通过变更“#”标签后的版本号来刷新，如下所示：

```
CACHE MANIFEST
# version 2.0
/icketang.css
/icketang. js
/icketang.png
NETWORK
login.php
```

#### 应用缓存中的回退

应用缓存中的回退会帮助你指定在服务器不可访问时，品示某文件。例如在下面的manifest 文件中，如果用户输入了“/home”，同时服务器不可到达，“404.html”文件应送达

```
FAIIBACK:
/home/ /404. html
```

#### 应用缓存中网络命令的作用

网络命令描述不需要缓存的文件，例如以下代码中"login.php"始终都不应该缓存或者离线访问。

```
NEIWORK:
login.php
```

#### WebSql

Websql 是一个在浏览器客户端的结构关系数据库，是浏览器内的本地 RDBMS（关系型数据库管理系统），可以使用SQL 查询。

> websql 不是HTML5 的一个规范，这个规范是基于 SOLite

#### HTML5 实现跨域

在服务器端设置允许在其他域名下访问，例如允许所有域名访问以下内容

```
response.setHeader("Access-Control-Allow-Origin",
response.setHeader("Access-Control-Allow-Methods","pOST")
response. setHeader ("Access-Control-Allow-Headers" "x-requested-with, content-type") ;
```

