---
title: HTML5-笔记
date: 2021-09-02 14:55:04
tags:
- HTML5
---

HTML5定义了一系列`新元素`，如新语义标签、智能表单、多媒体标签等，可以帮助开发者创建富互联网应用，还提供了一系列`Javascript API`，如地理定位、重力感应、硬件访问等，可以在浏览器内实现类原生应用，甚至结合Canvas我们可开发网页版游戏，同时结合`CSS3`的过渡、转换、动画等特性，可以极大的增强用户体验，提升开发功能的可应用性。,
我们日常讨论的H5其实是一个`泛称`，它指的是由`HTML5 + CSS3 + Javascript`，等技术组合而成的一个`应用开发平台`。

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>文字间距</title>
</head>
<body>
   
</body>
</html>
```



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





## 新增语义标签

| 区块标签 | 内容分组标签 | 文本级别标签 |
| -------- | ------------ | ------------ |
| article  | main         | time         |
| header   | figure       |              |
| footer   | figcaption   |              |
| nav      |              |              |
| aside    |              |              |
| section  |              |              |

```plain
<figure>
	<img src="images/caffe-2.jpg" alt="卡布奇诺"/><figcaption>卡布奇诺</figcaption>
</figure>
```

### ![img](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/HTML5-%E7%AC%94%E8%AE%B0/coffee.png)

### header

header标签的使用:

- 一个文档中可以包含多于一个的header标签
- header标签不一定非要显示在页面的上方，它的内容决定这里需要使用header标签，位置并不重要



—些使用aside的例子:

- 页面侧边栏
- 广告
- 友情链接
- 引语(内容摘要)



一个主题性的内容分组，通常包含一个头部( header ) ,可能还会有一个尾部( footer )。



### div

- 应用更广泛，只要你想为一个区域定义一个样式，就可以使用div标签

### section

- 包含的内容是一个明确的主题，通常有标题区域

### main

- 显示页面的主体内容。
- 每个页面只能包含一个main标签。
- main标签中不包含网站标题、logo、主导航、版权声明等信息。



HTML5中文本级别的语义标签

- time（表示一个日期，或者一个时间，或者同时表示一个日期和时间值）
- i和b
- em和strong

```plain
<time datetime="2015-06-30">2015年6月30日</time>

// datetime="2015-06-30"：
// 这里是一个固定格式的日期或时间值，可以被搜索引擎、屏幕阅读器等方便的识别。

// 2015年6月30日：
// 标签中间的文本只要人可以识别就可以，例如“今天”，“1小时前”，“结婚纪念日”，“情人节”等
   如果没有定义datetime属性，则这里的文本需要是一个固定格式
```

#### time的格式

- 指定年月日：2015-06-30
- 指定年月：2015-06
- 年份可以是两位数字：15-06-30
- 指定时间（ 24小时制)：14:54:39
- 指定时间(24小时制）：14:54
- 指定日期和时间：2015-06-30 14:54:39
- T表示时间，意义同上:2015-06-30T14:54:39
- Z表示使用UTC标准时间：2015-06-30T14:54Z

注：utc标准时间+8小时=北京时间

### i

HTML4：修饰文字样式的，将文字显示为*斜体*文本

HTML5：表示强调不同的情绪或声音，也可以表示技术术语、生物分类、来自另一种语言的成语或习语、一个想法等等

### b

HTML4：修饰文字样式的，将文字显示为粗体文本

HTML5：表示文档中的关键字、商品名称等

### em

标签中的内容是用来强调的重点内容

会被浏览器显示成*斜体*文本

### strong

表示非常重要、严重性或内容的紧迫性

会被浏览器显示成**粗体**文本

### 使用建议

如果你只是单纯的想要把文字的样式显示为斜体或粗体请不要使用这几个语义标签

w3C建议我们要在css样式表中定义文字样式

### small

small标签在HTML5中的语义：

注释或批注说明

### HTML5之前Web上的视频格式

| 格式      | 文件 |
| --------- | ---- |
| AVI       | .avi |
| WMV       | .wmv |
| QuickTime | .mov |
| Realvideo | .rm  |
| Mpeg-4    |      |
| Flash     |      |

浏览器要想播放视频，必须预先安装对应的浏览器插件

#### embed标签

在HTML4中不是web的标准

```plain
<embed type="application/x-shockwave-flash"
src="zq.swf" width="508" height="430">
</embed>
```

浏览器要想播放视频，必须预先安装对应的浏览器插件

#### object标签

在低版本IE中无法工作(<= IE8 )

```plain
<object type="application/x-shockwave-flash"data="zq.swf" width="500" height="430"></object>
```

除了低版本的IE (<= IE 10)，无法工作在任何其它的浏览器中

```plain
<object classid="clsid:D27CDB6E-AE6D-11cf-96B8-44455354000e"
width="500" height="430">
  <param name="src" value="zq.swf”/>
</object>
```

### 为了兼容所有的浏览器

使用object兼容所有的浏览器

```plain
<object classid="clsid:D27CDB6E-AE6D-11cf-96B8-44455354000o""
width="5e0" height="430"><!--兼容低版本IE-->
	<param name="src" value="zq.swf"/>
  <!--高版本IE和其他浏览器-->
	<object type="application/x-shockwave-flash"
data="zq.swf" width="50o" height="430"></object>
</object>
```

### video标签的属性

- src
- controls
- autoplay
- preload
- muted
- loop
- poster
- width和height

```plain
<video src="lesson-0.mp4" controls autoplay></video>
```

controls和autoplay是布尔属性：只有属性名，没有属性值。例如∶

如果有autoplay属性，视频就会自动播放

如果没有autoplay属性，视频就不会自动播放

```plain
<video src="lesson-0.mp4" controls="controls" autoplay="autoplay">x</video>
```

XHTML风格的代码语法更严格

属性必须由属性名和属性值两部分组成

```plain
<audio controls="controls" src="1.mp3" autoplay="autoplay">
  您的浏览器不支持播放此音频，请使用高级的浏览器
</audio>
```

### 

您的浏览器不支持这个视频的播放，想观看视频，请用高级的浏览器，chrome、Firefox、Opera、Safari等浏览器。

【这里插入的内容是供不支持video元素的浏览器显示的】

```plain
<video src="pian.mp4" width="600px" height="400px" border="1px solid #ccc" controls="controls">
<video width="500" autoplay="autoplay" loop="loop" controls="controls">
    <source src="pian.ogg" type="video/ogg">
    <source src="pian.mp4" type="video/mp4">
    <!--video 元素允许多个 source 元素。source 元素可以链接不同的视频文件。
    浏览器将使用第一个可识别的格式：-->
  Your browser does not support the video tag.
</video>

<!-- video的属性有autoplay,controls,height,loop,preload,src,width -->
<!-- <video src="pian.mp4" width="500px" controls="controls" autoplay="autoplay"></video> -->
 <div style="text-align:center;">
  <button onclick="playPause()">播放/暂停</button> 
  <button onclick="makeBig()">大</button>
  <button onclick="makeNormal()">中</button>
  <button onclick="makeSmall()">小</button>
  <br /> 
  <video id="video1" width="420" style="margin-top:15px;">
    <source src="pian.mp4" type="video/mp4" />
    Your browser does not support HTML5 video.
  </video>
</div> 

<script type="text/javascript">
var myVideo=document.getElementById("video1");

function playPause()
{ 
if (myVideo.paused) 
  myVideo.play(); 
else 
  myVideo.pause(); 
} 

function makeBig()
{ 
myVideo.width=560; 
} 

function makeSmall()
{ 
myVideo.width=320; 
} 

function makeNormal()
{ 
myVideo.width=420; 
} 
</script> 
```

### audio

audio 元素允许多个 source 元素。source 元素可以链接不同的音频文件。浏览器将使用第一个可识别的格式：

```plain
<audio controls="controls" autoplay="autoplay">
  <source src="1.mp3" type="audio/mp3" />
  <source src="1.ogg" type="audio/ogg" />
</audio>
```

preload属性

| 属性值         | 详细说明                                                     |
| -------------- | ------------------------------------------------------------ |
| none           | 视频播放前，浏览器不会预先下载视频资源，当用户不点击播放按钮时会节省带宽。 |
| metadata       | 视频播放前，浏览器不会下载视频资源，但是会获取资源的元数据（视频大小、持续时间、视频格式、前几帧画面) |
| auto（默认值） | 浏览器根据实际情况动态决定。例如∶在wifi、3G、4G数据漫游等情况下，动态采用不同的加载方案。 |

muted：是否默认静音播放

```plain
<video src="lesson-0.mp4" controls muted loop></video>
```

poster属性设置视频的封面

```plain
<video src="let-it-go.mp4" controls
	poster="cover.jpg"
	width="854" height="480">
</video>
```

![img](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/HTML5-%E7%AC%94%E8%AE%B0/video.jpeg)

### 浏览器对视频格式的支持

浏览器对视频格式的支持情况: http://caniuse.com/#search=video



浏览器从上到下查找source元素，直到找到它能播放的一种格式

```plain
<video controls>
  <source src="tweetsip.mp4">
  <source src="tweetsip.webm">
  <source src="tweetsip.ogv">
	<p>对不起，您的浏览器不支持video标签</p>
</video>
```

对于这里的每个source元素，浏览器都会加载视频文件的元数据，查看能不能播放这个视频，这个过程可能很耗费时间。

### 兼容所有的浏览器



embed标签或object标签用在不支持video标签的旧版本额的浏览器中

```plain
<video controls>
  <source src="tweetsip.mp4" type='video/mp4; codecs="avc1.42E01E，mp4a.40.2"">
  <source src="tweetsip.webm" type='video/ogg; codecs="vp8，vorbis"'>
  <source src="tweetsip.ogv" type='video/ogg; codecs="theora，vorbis"">
  <embed src="tweetsip.swf" type="application/x-shockwave-flash"></embed>
</video> 
```

### HTML5支持的音频格式

HTML5支持的音频格式: http://en.wikipedia.org/wiki/HTML5_Audio

### 兼容所有的音频格式和浏览器

```plain
<audio controls>
  <source src="YouAreMySunshine.mp3" type='audio/mpeg; codecs="mp3"'>
  <source src="YouAreMySunshine.ogg" type='audio/ogg; codecs="vorbis"' >
  <p>对不起，您的浏览器不支持audio标签</p>
</ audio>
```

### 新增input类型

input标签新增type属性值

- search(搜索框)
- date(日期选择)
- email (邮件地址输入框)
- month(月份选择)
- url ( url地址输入框)
- week(周选择）
- tel(电话号码输入框)
- time (时间选择)
- number (数字输入框)
- datetime-local (日期时间)
- range(滑动条)
- datetime (包含时区)
- color（颜色选择)





它看起来是一个文本输入框，可以输入一个电子邮件地址在移动设备上有额外的特性:

```plain
<input type="email">
<input type="url">
<input type="tel">
```

专门用来输入一个数值的输入框，右侧有一组上下箭头，用来控制文本框中数值的大小

```plain
<input type="number">
```

通过滑动条选择一个数值范围

```plain
<input type="range">
```

在弹出的的日历中选择一个具体的日期

```plain
<input type="date">
```

选择一个具体的月份

```plain
<input type="month">
```

选择一个具体的星期

```plain
<input type="week">
```

在弹出的的日历中选择一个具体的时间

```plain
<input type="time">
```

选择日期和时间(本地时间)

```plain
<input type="datetime-local">
```

选择日期和时间( UTC世界标准时间)

```plain
<input type="datetime">
```

在弹出的颜色面板中选择一个颜色

```plain
<input type="color">
```

### datalist

为其它输入控件提供一个预定义的选项列表





```plain
<!--为输入框指定一个list属性-->
<input type="text" list="browsers">
<!--和文本框中list属性的值一致-->
<datalist id="browsers">
  <option value="Chrome"><option value="Firefox">
  <option value="Internet Explorer"><option value="opera">
  <option value="opera mini"><option value="Safari">
</datalist>
```

### keygen

用于客户端访问服务器时的安全验证

当提交表单时，会生成两个键，一个是私钥，一个公钥私钥存储于客户端，公钥则被发送到服务器

公钥可用于之后验证用户的客户端证书

```plain
<form action="#" method="get">
  用户名:<input type="text" name="usrname">
  加密:<keygen name="security">
  <input type="submit">
</form>
```

### output

结合JavaScript，主要用于显示脚本输出

```plain
<form oninput="x.value=a.value">
  选择一个数字:
  <input type="range" name="a" value="o">
  <output name="x">o</output>
</form>
```

### 表单验证

表单验证是指，在用户提交表单之前，确保用户输入的数据是合法的。

- 输入类型
- 日期和时间范围
- 必填字段
- 步长
- 字符长度
- 正则表达式
- 数值范围
- 禁用表单验证

### 必填字段验证

- required属性是boolean属性
- 表单提交时输入域不能为空

### 字符长度验证

没有达到最少字符时浏览器提示位数不够达到最大字符数时浏览器禁止继续输入

```plain
<form action="success.html" method="post">
	<div>密码: <input type="password" minlength="6" maxlength="10"></div>
  <div><input type="submit"></div>
</form>
```

它们是很多input元素的共有属性

如text、search、password、email、url、tel



### 数值范围验证

输入的数值不能小于min指定的值不能大于max指定的值

```plain
<form action="success.html" method="post">
	<div>订购数量: <input type="number" min="5" max="10"></div>
  <div><input type="submit"></div>
</form>
```

用于number、range和日期时间类型

### 日期和时间范围验证

- 只能选择范围内的日期和时间
- 范围外的日期和时间无法选择

```plain
<form action="success.html" method="post" >
	<div>送货日期:<input type="date" min="2020-01-01" max="2020-01-10"></div>
  <div>送货时间:<input type="time" min="e8:0o" max="17:00"></div>
  <div><input type="submit"></div>
</form>
```

### 步长验证

```plain
<form action="success.htm1" method="post">
  <div>订购数量:<input type="number" min="10" max="5o" step="10"></div>
  <div><input type="submit"></div>
</form>
```

点击number输入框右侧的上下箭头，每次增加或减少一个步长的值

```plain
<form action="success.html" method="post" oninput=""out.value=count.value">
  <div>
    订购数量: <input name=" count" type="range"
    value="10" min="1e" max="5e" step="10">
    <output name="out">10</output>
  </div>
	<div><input type="submit"></div>
</form>
```

移动滑动条每次增加或减少—个步长的值



### 正则表达式验证

[0-4]{3}

[0-4]表示0到4之间的任意一个数字{3}

表示必须出现3次例如∶103、341、222

```plain
<form action="success.htm1" method="post">
	<div>编号: <input type="text" pattern="[e-4]{[3}"></div>
  <div><input type="submit"></div>
</form>
```

是所有的可输入的input元素共有的属性如text、search、password、email、url、tel

### 禁用表单验证

如果你更想使用基于JavaScript的更强大和灵活的表单验证功能，那么首先需要禁用HTML5表单验证

- novalidate
- formnovalidate

```plain
<form action="success.html" method="post" novalidate>
  <div>数字: <input type="number"></div>
  <div>邮箱: <input type="email"></div>
  <div>网址: <input type="ur1"></div>
  <div><input type="submit"></div>
</form>
<form action="success.html" method="post">
	<div>数字: <input type="number"></div>
  <div>邮箱:<input type="email"></div>
  <div>网址: <input type="ur1"></div>
  <div><input type="submit" formnovalidate></div>
</form>
```

在提交按钮中使用formnovalidate属性

### 总结

- 输入类型验证: number、email、url必填字段验证:required
- 字符长度验证: minlength、maxlength设置数值范围: min、max
- 设置日期和时间范围:min、max设置步长: step
- 正则表达式验证:pattern
- 禁用表单验证: novalidate、formnovalidate

### 新增表单属性

- list
- placeholder
- required
- autofocus（—个页面只能有一个autofocus属性的定义。如果有多个，则应用第一个）
- minlength和maxlength
- autocomplete（当我们填写表单，并成功提交后，再回到表单中填写时，会出现提醒功能，可以根据提醒功能进行快速输入。）（填写完，成功提交后，再回到表单填写时，没有上次的输入记录了。）
- multiple
- min和max
- form
- step
- formaction
- pattern
- formmethod
- novalidate
- formenctype
- formnovalidate
- formtarget



```plain
<form action="success.html" method="post" autocomplete="off">
  <!--把autocomplete="on"放在input标签中，它会覆盖form中的设置，
  这个属性可以用在所有可输入的input标签。
  -->
  <input placeholder="姓名" name="username" autocomplete="on">
  <input placeholder="账号" name="cardid">
  <input type="submit">
</form>
```

### multiple

```plain
<select multiple>
  <option>美式咖啡</option>
  <option>卡布奇诺</option>
  <option>拿铁</option>
  <option>摩卡</option>
</select>
```

按住键盘上的ctrl键可以实现多选



选完一个之后，输入逗号，可以再输入一个地址。

```plain
<input placeholder="请输入邮件地址" type="email" list="contacts" multiple>
<datalist id="contacts">
  <option value="helen@qq.com">
  <option value="cohen@baidu.com">
  <option value="yaohuan@sina.com">
  <option value="annie@qq.com">
</datalist>
<!--按住Ctrl键，可以选择多个文件-->
<input type="file" multiple>
```

### form

```plain
<form action="success.htm1">
  <input placeholder="姓名" type="text" name="username">
  <input type="submit">
</form>
<input placeholder="账号" type="text" name="cardid">
```

提交后,在URL地址中，只有username，即在form外面的input没有被提交





在默认情况下，表单外的控件不会被提交，因此在form中加一个id,在input中加form="f";然后就可以一起提交到服务器了。

```plain
<form action="success.htm1" id="f">
  <input placeholder="姓名" type="text" name="username">
  <input type="submit">
</form>
<input placeholder="账号" type="text" name="cardid" form="f">
```

### form相关属性

```plain
<form action="success.htm1" method="post" target="_blank" 
enctype="application/x-www-form-urlencoded">
<! --其它表单控件-->
<input type="submit">
</form>
```

enctype：页面提交时的编码方式(仅限于post方式提交的表单)



这些属性是表单提交按钮的属性，当表单中的属性和提交按钮中存在同名属性时，提交按钮中的属性会被应用。

```plain
<form>
  <! --其它表单控件--><input type="submit"
  formaction="success.htm1"formmethod="post"
  formtarget="_blank"
  formenctype="application/x-www-form-urlencoded">
</form>
```

### accesskey



### svg

```plain
<html xmlns:svg="http://www.w3.org/2000/svg">
<body>

<p>This is an HTML paragraph</p>

<svg:svg width="300" height="100" version="1.1" >
<svg:circle cx="100" cy="50" r="40" stroke="black"
stroke-width="2" fill="red" />
</svg:svg>

</body>
</html>
<?xml version="1.0" standalone="no"?>
<!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN" 
"http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">

<svg width="100%" height="100%" version="1.1"
xmlns="http://www.w3.org/2000/svg">

<rect width="300" height="100"
style="fill:rgb(0,0,255);stroke-width:1;
stroke:rgb(0,0,0)"/>

</svg>
```

### drag

```plain
<style type="text/css">
#div1 {width:488px;height:70px;padding:10px;border:1px solid #aaaaaa;}
</style>
<script type="text/javascript">
function allowDrop(ev)
{
ev.preventDefault();
}

function drag(ev)
{
ev.dataTransfer.setData("Text",ev.target.id);
}

function drop(ev)
{
ev.preventDefault();
var data=ev.dataTransfer.getData("Text");
ev.target.appendChild(document.getElementById(data));
}
</script>
</head>
<body>

<p>请把 W3School 的图片拖放到矩形中：</p>

<div id="div1" ondrop="drop(event)" ondragover="allowDrop(event)"></div>
<br />
<img id="drag1" src="w3school_banner.gif" draggable="true" ondragstart="drag(event)" />

</body>
 <head>
 	<meta charset="UTF-8">
 	<title>拖放</title>
 	<style>
		p{
			font-size: 16px;
		}
		#div1{
			width: 390px;
			height: 260px;
			padding: 10px;
			border: 1px solid #ccc;
			background-color: yellowgreen;
			border-radius: 10px;
			display: inline-block;
		}
		img{
			border-radius: 10px;
		}
 	</style>
 	<script type="text/javascript">
 		function allowDrop(ev){
 			ev.preventDefault();
 		}
 		function drag(ev){
 			ev.dataTransfer.setData("text",ev.target.id);
 		}
 		function drop(ev){
 			ev.preventDefault();
 			var data = ev.dataTransfer.getData("text");
 			ev.target.appendChild(document.getElementById(data));
 		}
 	</script>
 </head>
 <body>
 	<p>请把单车的图片拖放到下面的矩形中：</p>
 	<div id="div1" ondrop="drop(event)" ondragover="allowDrop(event)"></div>
 	<img id="img1" src="bike.png" height="260" alt="单车" draggable="true" ondragstart="drag(event)">
 </body>
<head>
	<meta charset="UTF-8">
	<title>来回拖放</title>
	<style>
		div{
			width: 300px;
			height: 220px;
			border: 1px solid #000;
			border-radius: 10px;
			background-color: pink;
			display: inline-block;
			margin-right: 20px;
			overflow: hidden;
			padding: 10px;
		}
	</style>
	<script type="text/javascript">
		function allowDrop(ev){
			ev.preventDefault();
		}
		function drag(ev){
			ev.dataTransfer.setData("text",ev.target.id);
		}
		function drop(ev){
			ev.preventDefault();
			var data = ev.dataTransfer.getData("text");
			ev.target.appendChild(document.getElementById(data));
		}
	</script>
</head>
<body>
	<div id="div1" ondrop="drop(event)" ondragover="allowDrop(event)">
		<img id="img2" src="bike.png" alt="单车" width="280px" draggable="true" ondragstart="drag(event)">
	</div>
	<div id="div2" ondrop="drop(event)" ondragover="allowDrop(event)"></div>
	<div id="div3" ondrop="drop(event)" ondragover="allowDrop(event)"></div>
</body>
<style type="text/css">
#div1, #div2
{float:left; width:100px; height:35px; margin:10px;padding:10px;border:1px solid #aaaaaa;}
</style>
<script type="text/javascript">
function allowDrop(ev)
{
ev.preventDefault();
}

function drag(ev)
{
ev.dataTransfer.setData("Text",ev.target.id);
}

function drop(ev)
{
ev.preventDefault();
var data=ev.dataTransfer.getData("Text");
ev.target.appendChild(document.getElementById(data));
}
</script>
</head>
<body>

<div id="div1" ondrop="drop(event)" ondragover="allowDrop(event)">
  <img width="100px" src="bike.png" draggable="true" ondragstart="drag(event)" id="drag1" />
</div>
<div id="div2" ondrop="drop(event)" ondragover="allowDrop(event)"></div>

</body>
```

#### HTML5标签兼容处理

#### 微数据

徼数据是在如 span、div的标签内添加属性，让机器（如搜索引擎）识别其含义，某些特定类型的信息，例如评论、人物信息或事件都有相应的属性，用来描述其含义，可以理解成新语义标签的一种补充。 

```
<div itemscope>
	<ul></ul>
</div>


<div>
	<span itemprop="description">评论内容</span>
</div>
```

#### 表单类型

[HTML5 的输入（input）类型](https://developer.mozilla.org/zh-CN/docs/Learn/Forms/HTML5_input_types)

#### 获取元素

[Document.querySelector()](https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelector)

```
document.querySelector(".myclass");
```

[Document.querySelectorAll()](https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelectorAll)

#### 类名操作

[Element.classList](https://developer.mozilla.org/en-US/docs/Web/API/Element/classList)

```
const div = document.createElement("div");
div.className = "foo";
div.classList.remove("foo");
div.classList.add("anotherclass");
div.classList.toggle("visible");
div.classList.replace("foo", "bar");
```

#### 自定义属性

```
data-*=""
```

##### WebApp

使用HTML5编写的移动Web应用

#### 全屏显示