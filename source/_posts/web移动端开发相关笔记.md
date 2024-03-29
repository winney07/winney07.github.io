---
title: web移动端开发相关笔记
date: 2018-08-22 11:40:08
tags:
- 移动端
categories:
- 移动端
---

#### [移动端开发的资源与小技巧](https://github.com/jtyjty99999/mobileTech)

[Mobile - Table of contents](https://www.quirksmode.org/mobile/)

[移动端](https://www.yuque.com/docs/share/27e13760-a250-4376-ab7e-072b8bae0b5b?# 《移动端》)-语雀笔记

[移动前端知识总结](http://caibaojian.com/mobile-knowledge.html)

#### 网站收集

| [移动端Web解决方案](https://github.com/AlloyTeam/Mars)       | [移动前端开发收藏夹](https://github.com/hoosin/mobile-web-favorites) | [优化移动体验的HTML5技巧](https://www.oschina.net/translate/mobile-app-optimization-and-performance) |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| [移动端手势表](http://ww1.sinaimg.cn/bmiddle/c2c57f68jw1e4fh7dmw12j20fi2w6qe1.jpg) | [Mobile HTML5](http://mobilehtml5.org/)—html5移动端兼容性速查 | [Pixel Density Display Listing](https://pixensity.com/)—几乎所有设备的屏幕尺寸与像素密度表 |
| [Screen Sizes](https://screensiz.es/phone)—移动设备参数表    | [The iOS Design Guidelines](https://ivomynttinen.com/blog/ios-design-guidelines)—ios端移动设备参数速查 | [iPhone 6 屏幕揭秘](http://wileam.com/iphone-6-screen-cn/)   |
| [移动设备适配库2](http://detectmobilebrowsers.com/)          | [jQuery Mobile Demos](https://demos.jquerymobile.com/1.4.3/) | [zepto源码注释](https://www.cnblogs.com/sky000/archive/2013/03/29/2988952.html) |
| [移动端web开发技巧](http://www.imooc.com/article/1115)       |                                                              |                                                              |

#### 在移动端页面显示控制台（调试）-Vcode

[移动端h5网页、微信网页调试之利用vConsole真机调试+显示控制台打印信息、调试接口(附带vue项目里的具体使用方法)](https://blog.csdn.net/qq_22182989/article/details/125338389)

```
<script type="text/javascript" src='https://unpkg.com/vconsole@3.15.0/dist/vconsole.min.js'></script>

var vConsole = new window.VConsole(); 
```

#### 移动端H5页面适配问题总结

[移动端页面的适配](https://zhuanlan.zhihu.com/p/141964516)

[再聊移动端页面的适配](https://www.w3cplus.com/css/vw-for-layout.html)

##### 移动端H5页面使用rem做适配

1. `如果H5页面不需要放在App内做混合App开发`，可以使用`vw`做适配

   ```
   html, body{
       font-size: 0.13333333vw;
   }
   // 设计稿是用iPhone6的尺寸设计，设计稿多少px就写多少rem
   ```

2. `如果H5页面需要放在App内做混合App开发`，不需要兼容低版本的Android手机(9.0及以下)

   1. 使用`vw`的情况下，`不需要兼容Android低版本（≤10.0）手机 `   。可以直接使用`vw`做适配

   2. 使用`vw`的情况下，`需要兼容Android低版本（≤10.0）手机，不需要兼容9.0及以下 `  的做法

      原因：在Android手机低版本（≤10.0）的`webview`中，会出现`h5页面放大的情况`。低版本的webview获取错了字段，默认是8的，导致字体放大了8倍

      > 在在Android手机低版本（≤9.0）的手机自带浏览器中是显示正常的

      解决方法：在Android客户端加上以下两行代码，对webview进行相应的配置

      ```
      mWebView.getSettings().setMinimumFontSize(1);
      mWebView.getSettings().setMinimumLogicalFontSize(1);
      ```

      参考博客：[关于html：Android Webview Rem单元可将框的大小缩放](https://www.codenong.com/41179357/)

3. `如果H5页面需要放在App内做混合App开发`，且需要兼容低版本的安卓手机(9.0及以下)

   使用[mobile-util.js](https://github.com/re54k/mobileweb-utilities/blob/master/util/mobile-util.js)做适配

   **使用[mobile-util.js](https://github.com/re54k/mobileweb-utilities/blob/master/util/mobile-util.js)做适配的注意事项**

   1. 要在head中引入

   2. 要在样式表前引入

      ```
      <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
      <meta name="apple-mobile-web-app-capable" content="yes">
      <meta name="apple-mobile-web-app-status-bar-style" content="black">
      <meta name="format-detection" content="telephone=no">
      <meta name="format-detection" content="email=no">
      <meta name="applicable-device" content="mobile">
      <meta name="x5-orientation" content="portrait">
      <script src="./js/Plugins/Rem/mobile-util.js"></script>
      ```

      `注意：页面不写meta[name="viewport"]标签,代码自动判断插入`

   3. iPhone6中，`data-dpr="2"`，html的字体`style="font-size: 46.875px;"`

      ```
      26px——>0.55rem
      
      // 使用26px除以46.875就是0.55rem（设计稿中，多少px，除以46.875就是多少rem）
      ```

   `如果需要适配横屏`，修改`mobile-util.js`

   ```
   // 横竖屏字体设置
   if (window.orientation == 90 || window.orientation == -90) {
       // 横屏
       docEl.style.fontSize = rem/2 + 'px';   // 将字体缩小一倍
   } else {
       // 竖屏
       docEl.style.fontSize = rem + 'px';
   }
   
   // =========在文件最后将mobileUtil.fixScreen();修改为兼容横竖屏变化=========
   // 兼容横竖屏切换
   window.addEventListener("orientationchange", function(){
       mobileUtil.fixScreen();
   });
   ```

#### 获取设备信息

```
var u = navigator.userAgent;
```

#### 使用vw，rem做移动端适配--在低版本的安卓手机，页面样式显示错误（放很大）

webview设置可以解决此错误

```
mWebView.getSettings().setMinimumFontSize(1);
mWebView.getSettings().setMinimumLogicalFontSize(1);
```

Android Webview的rem单位会放大

参考：[关于html：Android Webview Rem单元可将框的大小缩放](https://www.codenong.com/41179357/)



#### 移动端meta头一些常用的属性

##### 1.meta标签

```
<meta name="viewport" content="width=device-width,user-scalable=no,initial-scale=1.0,maximum-scale=1.0,minimum-scale=1，shrink-to-fit=no, viewport-fit=cover">
```

- width=device-width：设备宽度；
- user-scalable=no：是否可以缩放，可以设置为no或者0；
- initial-scale=1.0：初始缩放比例
- maximum-scale=1.0 ：最大缩放比例 
- minimum-scale=1：最小缩放比例
- shrink-to-fit=no ： 解决ios9中的bug 识别屏幕宽度
- viewport-fit=cover： 解决苹果x 刘海的问题

##### 2.针对苹果手机：

可以把页面以app的方式添加到桌面：

```
<meta name="apple-mobile-web-app-capable" content="yes">
```

如果你把app添加到桌面，改状态条的颜色：

```
<meta name="apple-mobile-web-app-status-bar-style" content="black">
```

允许全屏展示：

```
<meta content=yes name=apple-touch-fullscreen>
```

禁止识别数字为电话,email：

```
<meta name="format-detection" content="telephone=no,email=no">
```

##### 3.不常用

应用信息，保留系统的历史记录，运动效果：

```
<meta name=App-Config content="fullscreen=yes,useHistoryState=yes,transition=yes">
```

max-age=180 响应时间

```
<meta http-equiv="Cache-Control" content="max-age=180">
```

解决 dns缓存问题——好处：访问快

```
<meta http-equiv="x-dns-prefetch-control" content="on" />
```

##### 4.其他

强制让360浏览器用chrome内核渲染页面

```
<meta name="renderer" content="webkit">
```

尽量用IE最新的模式渲染

```
<meta http-equiv="X-UA-Compatible" content="IE=edge">
```

针对手持设备优化，主要是针对一些老的不识别viewport的浏览器，比如黑莓

```
<meta name="HandheldFriendly" content="true">
```

微软的老式浏览器 

```
<meta name="MobileOptimized" content="320">
```

uc强制竖屏

```
<meta name="screen-orientation" content="portrait">
```

QQ强制竖屏

```
<meta name="x5-orientation" content="portrait">
```

UC强制全屏

```
<meta name="full-screen" content="yes">
```

QQ强制全屏 

```
<meta name="x5-fullscreen" content="true">
```

UC应用模式

```
<meta name="browsermode" content="application">
```

QQ应用模式

```
<meta name="x5-page-mode" content="app">
```

#### Rem-[mobile-util.js](https://github.com/re54k/mobileweb-utilities/blob/master/util/mobile-util.js)的使用

```
<meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black">
<meta name="format-detection" content="telephone=no">
<meta name="format-detection" content="email=no">
<meta name="applicable-device" content="mobile">
<meta name="x5-orientation" content="portrait">
<script src="./js/Plugins/Rem/mobile-util.js"></script>
```

`注意：页面不写meta[name="viewport"]标签,代码自动判断插入`

##### mobile-util.js—做横竖屏适配

```
// 横竖屏字体设置
if (window.orientation == 90 || window.orientation == -90) {
    // 横屏
    docEl.style.fontSize = rem/2 + 'px';   // 将字体缩小一倍
} else {
    // 竖屏
    docEl.style.fontSize = rem + 'px';
}
```

```
// 兼容横竖屏切换
window.addEventListener("orientationchange", function(){
    mobileUtil.fixScreen();
});
```

#### 移动端横竖屏适配

摘自：[JavaScript实现移动端横竖屏检测](https://www.jb51.net/article/256157.htm)， 仅用于学习

##### 一、HTML方法检测

```
<!-- 引用竖屏的CSS文件 portrait.css -->
  <link rel="stylesheet" media="all and (orientation:portrait)" href="portrait.css" rel="external nofollow"  >
   
  <!-- 引用横屏的CSS文件 landscape.css -->
<link rel="stylesheet" media="all and (orientation:landscape)" href="landscape.css" rel="external nofollow"  >

```

##### 二、CSS方法检测

css中通过媒体查询方法来判断是横屏还是竖屏

```
/* 竖屏 */
@media screen and (orientation:portrait) {
  /* 这里写竖屏样式 */
}

/* 横屏 */
@media screen and (orientation:landscape) {
  /* 这里写横屏样式 */
}
```

##### 三、JS方法检测

**【1】orientationChange事件**

苹果公司为移动 Safari中添加了 orientationchange 事件，orientationchange 事件在设备的纵横方向改变时触发

```
window.addEventListener("orientationchange",function(){
    alert(window.orientation);
}); 
```

**【2】orientation属性**

> window.orientation 获取手机的横竖的状态，window.orientation 属性中有 4个值：0和180的时候为竖屏（180为倒过来的竖屏），90和-90时为横屏（-90为倒过来的横屏）
>
> 0 表示肖像模式，90 表示向左旋转的横向模式（“主屏幕”按钮在右侧），-90 表示向右旋转的横向模 式（“主屏幕”按钮在左侧），180 表示 iPhone头朝下；但这种模式至今 尚未得到支持。如图展示了 window.orientation 的每个值的含义。

**【3】案例**

检测用户当前手机横竖屏状态，如果处于横屏状态，提示用户 “为了更好的观看体验，请在竖屏下浏览”，否则不提示

```
<!DOCTYPE html>
<html lang="en">
  
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <style>
    #box {
      position: fixed;
      box-sizing: border-box;
      padding: 50px;
      display: none;
      left: 0;
      top: 0;
      width: 100%;
      height: 100%;
      background: rgba(0, 0, 0, .5);
    }
  
    #box span {
      margin: auto;
      font: 20px/40px "宋体";
      color: #fff;
      text-align: center;
    }
  </style>
</head>
  
<body>
  <div id="box"><span>为了更好的观看体验，请在竖屏下浏览</span></div>
  <script>
    window.addEventListener("orientationchange", toOrientation);
    function toOrientation() {
      let box = document.querySelector("#box");
      if (window.orientation == 90 || window.orientation == -90) {
        // 横屏-显示提示
        box.style.display = "flex";
      } else {
        // 横屏-隐藏提示
        box.style.display = "none";
      }
    }
  </script>
</body>
  
</html>
```

#### 移动端VM适配-横竖屏适配

1. `html，body`的字体设置`font-size: 0.13333333vw; `
2. 元素`多少px`，就写`多少rem`

```
html, body{
    font-size: 0.13333333vw;
}

// 横屏适配
@media screen and (orientation: landscape){
    html, body{
        font-size: 0.065vw;
    }
}

header{
	font-size: 16rem;
}
```

## 移动端经验总结

#### 媒体查询常用样式表

```
<link rel="stylesheet" media="all and (orientation:portrait)" href="portrait.css">    // 竖放加载
<link rel="stylesheet" media="all and (orientation:landscape)"href="landscape.css">   // 横放加载

// 竖屏时使用的样式
<style media="all and (orientation:portrait)" type="text/css">
    #landscape { display: none; }
</style>

// 横屏时使用的样式
<style media="all and (orientation:landscape)" type="text/css">
    #portrait { display: none; }
</style>
```

#### 分链接

[如何自适应网页屏幕](https://www.icloud.com/keynote/000DIf8ISxFcuxka4YozKLaOg#Mobile_Webpage_%E5%A6%82%E4%BD%95%E8%87%AA%E9%80%82%E5%BA%94%E5%B1%8F%E5%B9%95_2)

配套的解决方案（设备判断等）—[generator-webappstarter](https://github.com/unbug/generator-webappstarter/blob/master/app/templates/app/src/util/MetaHandler.js)

```
var ua = navigator.userAgent,
  android = ua.match(/(Android);?[\s\/]+([\d.]+)?/),
  ipad = ua.match(/(iPad).*OS\s([\d_]+)/),
  ipod = ua.match(/(iPod)(.*OS\s([\d_]+))?/),
  iphone = !ipad && ua.match(/(iPhone\sOS)\s([\d_]+)/),
  os = {};

if (android) os.android = true, os.version = android[2];
if (iphone && !ipod) os.ios = os.iphone = true, os.version = iphone[2].replace(/_/g, '.')
if (ipad) os.ios = os.ipad = true, os.version = ipad[2].replace(/_/g, '.')
if (ipod) os.ios = os.ipod = true, os.version = ipod[3] ? ipod[3].replace(/_/g, '.') : null;
```

[Mobile开发经验沉淀](https://github.com/imweb/mobile/issues/2)—bug处理

[移动Web单页应用开发实践——页面结构化](https://github.com/maxzhang/maxzhang.github.com/issues/8)

[移动Web产品前端开发口诀——“快”](https://github.com/maxzhang/maxzhang.github.com/issues/1)

[移动Web开发，4行代码检测浏览器是否支持position:fixed](https://github.com/maxzhang/maxzhang.github.com/issues/7)

[使用border-image实现类似iOS7的1px底边](https://github.com/maxzhang/maxzhang.github.com/issues/4)

[移动端web页面使用position:fixed问题总结](https://github.com/maxzhang/maxzhang.github.com/issues/2)

[移动Web开发实践——解决position:fixed自适应BUG](https://github.com/maxzhang/maxzhang.github.com/issues/11)

[移动手机浏览器m3u8格式视频流播放支持程度测试](https://github.com/maxzhang/maxzhang.github.com/issues/19)

#### 指尖上的js系列

[指尖下的js ——多触式web前端开发之一：对于Touch的处理](http://www.cnblogs.com/pifoo/archive/2011/05/23/webkit-touch-event-1.html)

[指尖下的js ——多触式web前端开发之二：处理简单手势](http://www.cnblogs.com/pifoo/archive/2011/05/22/webkit-touch-event-2.html)

[指尖下的js —— 多触式web前端开发之三：处理复杂手势](http://www.cnblogs.com/pifoo/archive/2011/05/22/webkit-touch-event-3.html)

#### meta标签

##### [常用meta整理](https://segmentfault.com/a/1190000002407912)

meta标签，这些meta标签在开发webapp时起到非常重要的作用

```
<meta content="width=device-width; initial-scale=1.0; maximum-scale=1.0; user-scalable=0" name="viewport" />
<meta content="yes" name="apple-mobile-web-app-capable" />
<meta content="black" name="apple-mobile-web-app-status-bar-style" />
<meta content="telephone=no" name="format-detection" />
```

> 第一个meta标签表示：强制让文档的宽度与设备的宽度保持1:1，并且文档最大的宽度比例是1.0，且不允许用户点击屏幕放大浏览； 尤其要注意的是content里多个属性的设置一定要用分号+空格来隔开，如果不规范将不会起作用。
>
> 注意根据 [public_00](http://www.weibo.com/avajayam) 提供的资料补充，content 使用分号作为分隔，在老的浏览器是支持的，但不是规范写法。
>
> 规范的写法应该是使用逗号分隔，参考 [Safari HTML Reference - Supported Meta Tags](http://developer.apple.com/library/safari/#documentation/appleapplications/reference/SafariHTMLRef/Articles/MetaTags.html) 和 [Android - Supporting Different Screens in Web Apps](http://developer.android.com/guide/webapps/targeting.html)



> 第二个meta标签是iphone设备中的safari私有meta标签，它表示：允许全屏模式浏览； 第三个meta标签也是iphone的私有标签，它指定的iphone中safari顶端的状态条的样式； 第四个meta标签表示：告诉设备忽略将页面中的数字识别为电话号码
>
> 在设置了initial-scale=1 之后，我们终于可以以1:1 的比例进行页面设计了。 关于viewport，还有一个很重要的概念是：iphone 的safari 浏览器完全没有滚动条，而且不是简单的“隐藏滚动条”， 是根本没有这个功能。iphone 的safari 浏览器实际上从一开始就完整显示了这个网页，然后用viewport 查看其中的一部分。 当你用手指拖动时，其实拖的不是页面，而是viewport。浏览器行为的改变不止是滚动条，交互事件也跟普通桌面不一样。 (请参考：指尖的下JS 系列文章)
>
> 更详细的 viewport 相关的知识也可以参考

- width - viewport的宽度
- height - viewport的高度
- initial-scale - 初始的缩放比例
- minimum-scale - 允许用户缩放到的最小比例
- maximum-scale - 允许用户缩放到的最大比例
- user-scalable - 用户是否可以手动缩放

#### 适配的相关文章

[移动端高清、多屏适配方案](http://www.html-js.com/article/Mobile-terminal-H5-mobile-terminal-HD-multi-screen-adaptation-scheme 3041)

[手机淘宝的flexible设计与实现](http://www.html-js.com/article/2402)

#### 移动开发事件

[手机浏览器常用手势动作监听封装](http://wo.poco.cn/manson/post/id/268780)

#### 手势事件

- touchstart //当手指接触屏幕时触发
- touchmove //当已经接触屏幕的手指开始移动后触发
- touchend //当手指离开屏幕时触发
- touchcancel

#### 触摸事件

- gesturestart //当两个手指接触屏幕时触发
- gesturechange //当两个手指接触屏幕后开始移动时触发
- gestureend

#### 屏幕旋转事件

- onorientationchange

#### 检测触摸屏幕的手指何时改变方向

- orientationchange

#### touch事件支持的相关属性

- touches
- targetTouches
- changedTouches
- clientX　　　　// X coordinate of touch relative to the viewport (excludes scroll offset)
- clientY　　　　// Y coordinate of touch relative to the viewport (excludes scroll offset)
- screenX　　　 // Relative to the screen
- screenY 　　 // Relative to the screen
- pageX　　 　　// Relative to the full page (includes scrolling)
- pageY　　　　 // Relative to the full page (includes scrolling)
- target　　　　 // Node the touch event originated from
- identifier　　 // An identifying number, unique to each touch event
- 屏幕旋转事件：onorientationchange

#### 判断屏幕是否旋转

```
function orientationChange() {
    switch(window.orientation) {
      case 0:
            alert("肖像模式 0,screen-width: " + screen.width + "; screen-height:" + screen.height);
            break;
      case -90:
            alert("左旋 -90,screen-width: " + screen.width + "; screen-height:" + screen.height);
            break;
      case 90:
            alert("右旋 90,screen-width: " + screen.width + "; screen-height:" + screen.height);
            break;
      case 180:
          alert("风景模式 180,screen-width: " + screen.width + "; screen-height:" + screen.height);
          break;
    };
};
```

#### 添加事件监听

```
addEventListener('load', function(){
    orientationChange();
    window.onorientationchange = orientationChange;
});
```

#### JS 单击延迟

click 事件因为要等待单击确认，会有 300ms 的延迟，体验并不是很好。

开发者大多数会使用封装的 tap 事件来代替click 事件，所谓的 tap 事件由 touchstart 事件 + touchmove 判断 + touchend 事件封装组成。

[Creating Fast Buttons for Mobile Web Applications](https://developers.google.com/mobile/articles/fast_buttons?hl=de-DE)

[Eliminate 300ms delay on click events in mobile Safari](http://stackoverflow.com/questions/12238587/eliminate-300ms-delay-on-click-events-in-mobile-safari)

#### WebKit CSS

[携程 UED 整理的 Webkit CSS 文档](http://ued.ctrip.com/blog/wp-content/webkitcss/index.html) ，全面、方便查询，下面为常用属性。

①“盒模型”的具体描述性质的包围盒块内容，包括边界，填充等等

```
-webkit-border-bottom-left-radius: radius;
-webkit-border-top-left-radius: horizontal_radius vertical_radius;
-webkit-border-radius: radius;      //容器圆角
-webkit-box-sizing: sizing_model; 边框常量值：border-box/content-box
-webkit-box-shadow: hoff voff blur color; //容器阴影（参数分别为：水平X 方向偏移量；垂直Y 方向偏移量；高斯模糊半径值；阴影颜色值）
-webkit-margin-bottom-collapse: collapse_behavior; 常量值：collapse/discard/separate
-webkit-margin-start: width;
-webkit-padding-start: width;
-webkit-border-image: url(borderimg.gif) 25 25 25 25 round/stretch round/stretch;
-webkit-appearance: push-button;   //内置的CSS 表现，暂时只支持push-button
```

②“视觉格式化模型”描述性质，确定了位置和大小的块元素。

```
direction: rtl
unicode-bidi: bidi-override; 常量：bidi-override/embed/normal
```

③“视觉效果”描述属性，调整的视觉效果块内容，包括溢出行为，调整行为，能见度，动画，变换，和过渡。

```
clip: rect(10px, 5px, 10px, 5px)
resize: auto; 常量：auto/both/horizontal/none/vertical
visibility: visible; 常量: collapse/hidden/visible
-webkit-transition: opacity 1s linear; 动画效果 ease/linear/ease-in/ease-out/ease-in-out
-webkit-backface-visibility: visibler; 常量：visible(默认值)/hidden
-webkit-box-reflect: right 1px; 镜向反转
-webkit-box-reflect: below 4px -webkit-gradient(linear, left top, left bottom,
from(transparent), color-stop(0.5, transparent), to(white));
-webkit-mask-image: -webkit-gradient(linear, left top, left bottom, from(rgba(0,0,0,1)), to(rgba(0,0,0,0)));;   //CSS 遮罩/蒙板效果
-webkit-mask-attachment: fixed; 常量：fixed/scroll
-webkit-perspective: value; 常量：none(默认)
-webkit-perspective-origin: left top;
-webkit-transform: rotate(5deg);
-webkit-transform-style: preserve-3d; 常量：flat/preserve-3d; (2D 与3D)
```

④“生成的内容，自动编号，并列出”描述属性，允许您更改内容的一个组成部分，创建自动编号的章节和标题，和操纵的风格清单的内容。

```
content: “Item” counter(section) ” “;
This resets the counter.
First section
>two section
three section
counter-increment: section 1;
counter-reset: section;
```

⑤“分页媒体”描述性能与外观的属性，控制印刷版本的网页，如分页符的行为。

```
page-break-after: auto; 常量：always/auto/avoid/left/right
page-break-before: auto; 常量：always/auto/avoid/left/right
page-break-inside: auto; 常量：auto/avoid
```

⑥“颜色和背景”描述属性控制背景下的块级元素和颜色的文本内容的组成部分。

```
-webkit-background-clip: content; 常量：border/content/padding/text
-webkit-background-origin: padding; 常量：border/content/padding/text
-webkit-background-size: 55px; 常量：length/length_x/length_y
```

⑦ “字型”的具体描述性质的文字字体的选择范围内的一个因素。报告还描述属性用于下载字体定义。

```
unicode-range: U+00-FF, U+980-9FF;
```

⑧“文本”描述属性的特定文字样式，间距和自动滚屏。

```
text-shadow: #00FFFC 10px 10px 5px;
text-transform: capitalize; 常量：capitalize/lowercase/none/uppercase
word-wrap: break-word; 常量：break-word/normal
-webkit-marquee: right large infinite normal 10s; 常量：direction(方向) increment(迭代次数) repetition(重复) style(样式) speed(速度);
-webkit-marquee-direction: ahead/auto/backwards/down/forwards/left/reverse/right/up
-webkit-marquee-incrementt: 1-n/infinite(无穷次)
-webkit-marquee-speed: fast/normal/slow
-webkit-marquee-style: alternate/none/scroll/slide
-webkit-text-fill-color: #ff6600; 常量：capitalize, lowercase, none, uppercase
-webkit-text-security: circle; 常量：circle/disc/none/square
-webkit-text-size-adjust: none; 常量:auto/none;
-webkit-text-stroke: 15px #fff;
-webkit-line-break: after-white-space; 常量：normal/after-white-space
-webkit-appearance: caps-lock-indicator;
-webkit-nbsp-mode: space; 常量： normal/space
-webkit-rtl-ordering: logical; 常量：visual/logical
-webkit-user-drag: element; 常量：element/auto/none
-webkit-user-modify: read- only; 常量：read-write-plaintext-only/read-write/read-only
-webkit-user-select: text; 常量：text/auto/none
```

⑨“表格”描述的布局和设计性能表的具体内容。

```
-webkit-border-horizontal-spacing: 2px;
-webkit-border-vertical-spacing: 2px;
-webkit-column-break-after: right; 常量：always/auto/avoid/left/right
-webkit-column-break-before: right; 常量：always/auto/avoid/left/right
–webkit-column-break-inside: logical; 常量：avoid/auto
-webkit-column-count: 3; //分栏
-webkit-column-rule: 1px solid #fff;
style:dashed,dotted,double,groove,hidden,inset,none,outset,ridge,solid
```

⑩“用户界面”描述属性，涉及到用户界面元素在浏览器中，如滚动文字区，滚动条，等等。报告还描述属性，范围以外的网页内容，如光标的标注样式和显示当您按住触摸触摸 目标，如在iPhone上的链接。

```
-webkit-box-align: baseline,center,end,start,stretch 常量：baseline/center/end/start/stretch
-webkit-box-direction: normal;常量：normal/reverse
-webkit-box-flex: flex_valuet
-webkit-box-flex-group: group_number
-webkit-box-lines: multiple; 常量：multiple/single
-webkit-box-ordinal-group: group_number
-webkit-box-orient: block-axis; 常量：block-axis/horizontal/inline-axis/vertical/orientation
–webkit-box-pack: alignment; 常量：center/end/justify/start
```

动画过渡 这是 Webkit 中最具创新力的特性：使用过渡函数定义动画。

```
-webkit-animation: title infinite ease-in-out 3s;
animation 有这几个属性：
-webkit-animation-name： //属性名，就是我们定义的keyframes
-webkit-animation-duration：3s //持续时间
-webkit-animation-timing-function： //过渡类型：ease/ linear(线性) /ease-in(慢到快)/ease-out(快到慢) /ease-in-out(慢到快再到慢) /cubic-bezier
-webkit-animation-delay：10ms //动画延迟(默认0)
-webkit-animation-iteration-count： //循环次数(默认1)，infinite 为无限
-webkit-animation-direction： //动画方式：normal(默认 正向播放)； alternate(交替方向，第偶数次正向播放，第奇数次反向播放)
```

这些同样是可以简写的。但真正让我觉的很爽的是keyframes，它能定义一个动画的转变过程供调用，过程为0%到100%或from(0%)到to(100%)。简单点说，只要你有想法，你想让元素在这个过程中以什么样的方式改变都是很简单的。

```
-webkit-transform: 类型（缩放scale/旋转rotate/倾斜skew/位移translate）
scale(num,num) 放大倍率。scaleX 和 scaleY(3)，可以简写为：scale(* , *)
rotate(*deg) 转动角度。rotateX 和 rotateY，可以简写为：rotate(* , *)
Skew(*deg) 倾斜角度。skewX 和skewY，可简写为：skew(* , *)
translate(*,*) 坐标移动。translateX 和translateY，可简写为：translate(* , *)。
```

#### 自定义滚动条 from unknown

有没有觉得浏览器自带的原始滚动条很不美观，同时也有看到很多网站的自定义滚动条显得高端，就连chrome32.0开发板都抛弃了原始的滚动条，美观多了。那webkit浏览器是如何自定义滚动条的呢？ 参考：

[CSS3自定义滚动条样式 -webkit-scrollbar](https://www.xuanfengge.com/css3-webkit-scrollbar.html)

##### 滚动条组成

- ::-webkit-scrollbar 滚动条整体部分
- ::-webkit-scrollbar-thumb 滚动条里面的小方块，能向上向下移动（或往左往右移动，取决于是垂直滚动条还是水平滚动条）
- ::-webkit-scrollbar-track 滚动条的轨道（里面装有Thumb）
- ::-webkit-scrollbar-button 滚动条的轨道的两端按钮，允许通过点击微调小方块的位置。
- ::-webkit-scrollbar-track-piece 内层轨道，滚动条中间部分（除去）
- ::-webkit-scrollbar-corner 边角，即两个滚动条的交汇处
- ::-webkit-resizer 两个滚动条的交汇处上用于通过拖动调整元素大小的小控件

```
/*定义滚动条高宽及背景 高宽分别对应横竖滚动条的尺寸*/
::-webkit-scrollbar
{
    width: 16px;
    height: 16px;
    background-color: #F5F5F5;
}
 
/*定义滚动条轨道 内阴影+圆角*/
::-webkit-scrollbar-track
{
    -webkit-box-shadow: inset 0 0 6px rgba(0,0,0,0.3);
    border-radius: 10px;
    background-color: #F5F5F5;
}
 
/*定义滑块 内阴影+圆角*/
::-webkit-scrollbar-thumb
{
    border-radius: 10px;
    -webkit-box-shadow: inset 0 0 6px rgba(0,0,0,.3);
    background-color: #555;
}
```

[ie内核和webkit内核css滚动条样式](http://www.zhaoan.org/849.html)

##### ie内核：

```
*{
scrollbar-3dlight-color:#D4D0C8; 
   scrollbar-highlight-color:#fff; 
   scrollbar-face-color:#E4E4E4; 
   scrollbar-arrow-color:#666; 
   scrollbar-shadow-color:#808080; 
   scrollbar-darkshadow-color:#D7DCE0; 
   scrollbar-base-color:#D7DCE0; 
   scrollbar-track-color:#;
}
```

##### webkit内核：

```
/* Let's get this party started */
::-webkit-scrollbar {
    width: 12px;
}
 
/* Track */
::-webkit-scrollbar-track {
    -webkit-box-shadow: inset 0 0 6px rgba(0,0,0,0.3); 
    -webkit-border-radius: 10px;
    border-radius: 10px;
}
 
/* Handle */
::-webkit-scrollbar-thumb {
    -webkit-border-radius: 10px;
    border-radius: 10px;
    background: rgba(255,0,0,0.8); 
    -webkit-box-shadow: inset 0 0 6px rgba(0,0,0,0.5); 
}
::-webkit-scrollbar-thumb:window-inactive {
background: rgba(255,0,0,0.4); 
}
```

##### 隐藏滚动条

开发H5页面时为了美观，可能会隐藏滚动条，那么此时只要使用如下CSS代码即可实现

```
::-webkit-scrollbar { width: 0; height: 0; }
```

#### 页面描述

```
<link rel="apple-touch-icon-precomposed" href="http://www.xxx.com/App_icon_114.png" />
<link rel="apple-touch-icon-precomposed" sizes="72x72" href="http://www.xxx.com/App_icon_72.png" />
<link rel="apple-touch-icon-precomposed" sizes="114x114" href="http://www.xxx.com/App_icon_114.png" />
```

这个属性是当用户把连接保存到手机桌面时使用的图标，如果不设置，则会用网页的截图。有了这，就可以让你的网页像APP一样存在手机里了

```
<link rel="apple-touch-startup-image" href="/img/startup.png" />
```

这个是APP启动画面图片，用途和上面的类似，如果不设置，启动画面就是白屏，图片像素就是手机全屏的像素

```
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent" />
```

这个描述是表示打开的web app的最上面的时间、信号栏是黑色的，当然也可以设置其它参数，详细参数说明请参照：[Safari HTML Reference - Supported Meta Tags](https://developer.apple.com/library/safari/documentation/appleapplications/reference/SafariHTMLRef/Articles/MetaTags.html)

```
<meta name="apple-touch-fullscreen" content="yes" />
<meta name="apple-mobile-web-app-capable" content="yes" />
```

#### 常见的 iPhone 和 Android 屏幕参数。

- 设备 分辨率 设备像素比率
- Android LDPI 320×240 0.75
- Iphone 3 & Android MDPI 320×480 1
- Android HDPI 480×800 1.5
- Iphone 4 960×640 2.0

iPhone 4的一个 CSS 像素实际上表现为一块 2×2 的像素。所以图片像是被放大2倍一样，模糊不清晰。

解决办法：

1、页面引用

```
<link rel="stylesheet" media="screen and (-webkit-device-pixel-ratio: 0.75)" href="ldpi.css" />
<link rel="stylesheet" media="screen and (-webkit-device-pixel-ratio: 1.0)" href="mdpi.css" />
<link rel="stylesheet" media="screen and (-webkit-device-pixel-ratio: 1.5)" href="hdpi.css" />
<link rel="stylesheet" media="screen and (-webkit-device-pixel-ratio: 2.0)" href="retina.css" />
```

2、CSS文件里

```
#header {
    background:url(mdpi/bg.png);
}

@media screen and (-webkit-device-pixel-ratio: 1.5) {
    /*CSS for high-density screens*/
    #header {
        background:url(hdpi/bg.png);
    }
}
```

#### 移动 Web 开发经验技巧

##### 性能优化

###### 技术相关

- 离线缓存
- css优化【3d动画优化】
- js优化 【js worker】
- spdy,http2
- service worker
- 入口dns预解析
- 域名收敛
- cookie压缩
- 网速及网络情况侦测
- webp

### 策略相关

- 前端资源压缩去重
- 首屏前置与资源lazyload
- 页面模板与数据分离
- 适当的base64,首屏css不建议使用
- script 异步
- 后台智能加载下一页
- 图片渐进显示

#### 参考资料

[7 天打造前端性能监控系统](http://fex.baidu.com/blog/2014/05/build-performance-monitor-in-7-days/)

[16_ms_optimization—web_front-end_performance_optimization](http://velocity.oreilly.com.cn/2013/ppts/16_ms_optimization--web_front-end_performance_optimization.pdf)

[velocity 2011 移动互联网应用的性能优化](http://velocity.oreilly.com.cn/2011/index.php?func=session&name=%E7%A7%BB%E5%8A%A8%E4%BA%92%E8%81%94%E7%BD%91%E5%BA%94%E7%94%A)

[Medium图片加载模式](https://github.com/lx7575000/Translation/blob/master/（译）Medium图片加载模式/（译）Medium图片加载模式.md)

[Web性能权威指南](https://lwdgit.github.io/editor.md/)

[Google 性能优化](https://developers.google.com/web/fundamentals/performance/?hl=zh-cn)

[http2资料汇总](https://imququ.com/post/http2-resource.html)

[离线缓存使用规范](http://www.html5rocks.com/zh/tutorials/appcache/beginner/)

[12步创建高性能Web APP](http://www.cnblogs.com/qq309240790/p/5252992.html)

[css加载方式](https://jakearchibald.com/2016/link-in-body/)

[Google AMP (AMP is a way to build web pages for static content that render fast)](https://www.ampproject.org/docs/get_started/about-amp.html)

[缓存最佳实践](https://www.ampproject.org/docs/get_started/about-amp.html)

[以层为基础的渲染加速－chrome](http://www.html5rocks.com/zh/tutorials/speed/layers/)

#### 点击与click事件

对于a标记的点击导航，默认是在onclick事件中处理的。而移动客户端对onclick的响应相比PC浏览器有着明显的几百毫秒延迟。

在移动浏览器中对触摸事件的响应顺序应当是：

```
ontouchstart -> ontouchmove -> ontouchend -> onclick
```

因此，如果确实要加快对点击事件的响应，就应当绑定ontouchend事件。

使用click会出现绑定点击区域闪一下的情况，解决：给该元素一个样式如下

```
-webkit-tap-highlight-color: rgba(0,0,0,0);
```

如果不使用click，也不能简单的用touchstart或touchend替代，需要用touchstart的模拟一个click事件，并且不能发生touchmove事件，或者用zepto中的tap（轻击）事件。

```
body
{
    -webkit-overflow-scrolling: touch;
}
```

用iphone或ipad浏览很长的网页滚动时的滑动效果很不错吧？不过如果是一个div，然后设置 `height:200px;overflow:auto;`的话，可以滚动但是完全没有那滑动效果，很郁闷吧？

我看到很多网站为了实现这一效果，用了第三方类库，最常用的是iscroll（包括新浪手机页，百度等） 我一开始也使用，不过自从用了`-webkit-overflow-scrolling: touch;`样式后，就完全可以抛弃第三方类库了，把它加在`body{}`区域，所有的`overflow`需要滚动的都可以生效了。

另外有一篇比较全的移动端点击解决方案 http://www.zhihu.com/question/28979857

#### 锁定 viewport

```
ontouchmove="event.preventDefault()" //锁定viewport，任何屏幕操作不移动用户界面（弹出键盘除外）。
```

#### 利用 Media Query监听

Media Query 相信大部分人已经使用过了。其实 JavaScript可以配合 Media Query这么用：

```
var mql = window.matchMedia("(orientation: portrait)");
mql.addListener(handleOrientationChange);
handleOrientationChange(mql);
function handleOrientationChange(mql) {
    if (mql.matches) {
        alert('The device is currently in portrait orientation ')
    } else {
        alert('The device is currently in landscape orientation')
    }
}
```

借助了 Media Query 接口做的事件监听，所以很强大！

也可以通过获取 CSS 值来使用 Media Query 判断设备情况，详情请看：[JavaScript 依据 CSS Media Queries 判断设备的方法](http://yujiangshui.com/use-javascript-css-media-queries-detect-device-state/)。

#### rem最佳实践

rem是非常好用的一个属性，可以根据html来设定基准值，而且兼容性也很不错。不过有的时候还是需要对一些莫名其妙的浏览器优雅降级。以下是两个实践

1. http://jsbin.com/vaqexuge/4/edit 这有个demo，发现chrome当font-size小于12时，rem会按照12来计算。因此设置基准值要考虑这一点
2. 可以用以下的代码片段保证在低端浏览器下也不会出问题

```
html { font-size: 62.5%; } body { font-size: 14px; font-size: 1.4rem; } /* =14px / h1 { font-size: 24px; font-size: 2.4rem; } /=24px */
```

#### 被点击元素的外观变化，可以使用样式来设定：

```
-webkit-tap-highlight-color: 颜色
```

#### 检测判断 iPhone/iPod

开发特定设备的移动网站，首先要做的就是设备侦测了。下面是使用Javascript侦测iPhone/iPod的UA，然后转向到专属的URL。

```
if((navigator.userAgent.match(/iPhone/i)) || (navigator.userAgent.match(/iPod/i))) {
　　if (document.cookie.indexOf("iphone_redirect=false") == -1) {
　　　　window.location = "http://m.example.com";
　　}
}
```

虽然Javascript是可以在水果设备上运行的，但是用户还是可以禁用。它也会造成客户端刷新和额外的数据传输，所以下面是服务器端侦测和转向：

```
if(strstr($_SERVER['HTTP_USER_AGENT'],'iPhone') || strstr($_SERVER['HTTP_USER_AGENT'],'iPod')) {
　　header('Location: http://yoursite.com/iphone');
　　exit();
}
```



### 阻止旋转屏幕时自动调整字体大小

### 

```
html, body, form, fieldset, p, div, h1, h2, h3, h4, h5, h6 {-webkit-text-size-adjust:none;}
```

#### 禁止body滚动

```
document.body.ontouchmove=function(e){ e.preventDefault(); }
```

#### 页面长按，高亮全选文本

```
<http://blog.csdn.net/freshlover/article/details/40432247>
```

#### 模拟:hover伪类

因为iPhone并没有鼠标指针，所以没有hover事件。那么CSS :hover伪类就没用了。但是iPhone有Touch事件，onTouchStart 类似 onMouseOver，onTouchEnd 类似 onMouseOut。所以我们可以用它来模拟hover。使用Javascript：

```
var myLinks = document.getElementsByTagName('a');
for(var i = 0; i < myLinks.length; i++){
　　myLinks[i].addEventListener(’touchstart’, function(){this.className = “hover”;}, false);
　　myLinks[i].addEventListener(’touchend’, function(){this.className = “”;}, false);
}
```

然后用CSS增加hover效果：

```
a:hover, a.hover { /* 你的hover效果 */ }
```

这样设计一个链接，感觉可以更像按钮。并且，这个模拟可以用在任何元素上。

#### Flexbox 布局

[Flex 模板和实例](http://jsbin.com/ibuwol/2/edit)

[深入了解 Flexbox 伸缩盒模型](http://www.w3cplus.com/blog/666.html)

[CSS Flexbox Intro](http://yehao.diandian.com/post/2013-09-15/40052216426)

http://www.w3.org/TR/css3-flexbox/

#### 居中问题

居中是移动端跟pc端共同的噩梦。这里有两种兼容性比较好的新方案。

- table布局法

```
.box{ text-align:center; display:table-cell; vertical-align:middle; }
```

- 老版本flex布局法

```
.box{ display:-webkit-box; -webkit-box-pack: center; -webkit-box-align: center; text-align:center; }
```

以上两种其实分别是retchat跟ionic的布局基石。

这里有更详细的更多的选择[http://www.zhouwenbin.com/%E5%9E%82%E7%9B%B4%E5%B1%85%E4%B8%AD%E7%9A%84%E5%87%A0%E7%A7%8D%E6%96%B9%E6%B3%95/](http://www.zhouwenbin.com/垂直居中的几种方法/) 来自周文彬的博客

#### h5底部输入框被键盘遮挡问题

h5页面有个很蛋疼的问题就是，当输入框在最底部，点击软键盘后输入框会被遮挡。

可以使用这个api，在点击input的时候调用即可 https://developer.mozilla.org/zh-CN/docs/Web/API/Element/scrollIntoView

如果切换输入法，由于不同输入法高度不同，又会出现被遮挡问题。由于无法捕获切换输入法的事件，因此可以开一个计时器，不断执行sscrollintoview即可。

#### 移动端实现标题文字截断

http://www.75team.com/archives/611

#### placeholder--line-height

input 的placeholder会出现文本位置偏上的情况：PC端设置line-height等于height能够对齐，而移动端仍然是偏上，解决是设置line-height：normal，（stackoverflow也可查到这种解决办法）。

#### 处理 Retina 双倍屏幕

[（经典）Using CSS Sprites to optimize your website for Retina Displays](http://miekd.com/articles/using-css-sprites-to-optimize-your-website-for-retina-displays/)

[使用CSS3的background-size优化苹果的Retina屏幕的图像显示](http://www.w3cplus.com/css/css-background-size-graphics.html)

[使用 CSS sprites 来优化你的网站在 Retina 屏幕下显示](http://www.w3cplus.com/css/using-css-sprites-to-optimize-your-website-for-retina-displays.html)

[（案例）CSS IMAGE SPRITES FOR RETINA (HIRES) DEVICES](http://alexthorpe.com/uncategorized/css-sprites-for-retina-display-devices/683/)

#### input类型为date情况下不支持placeholder（来自于江水）

这其实是浏览器自己的处理。因为浏览器会针对此类型 input 增加 datepicker 模块。

对 input type date 使用 placeholder 的目的是为了让用户更准确的输入日期格式，iOS 上会有 datepicker 不会显示 placeholder 文字，但是为了统一表单外观，往往需要显示。Android 部分机型没有 datepicker 也不会显示 placeholder 文字。

桌面端（Mac）

- Safari 不支持 datepicker，placeholder 正常显示。
- Firefox 不支持 datepicker，placeholder 正常显示。
- Chrome 支持 datepicker，显示 年、月、日 格式，忽略 placeholder。

移动端

- iPhone5 iOS7 有 datepicker 功能，但是不显示 placeholder。
- Andorid 4.0.4 无 datepicker 功能，不显示 placeholder

解决方法：

```
<input placeholder="Date" class="textbox-n" type="text" onfocus="(this.type='date')"  id="date">
```

因为text是支持placeholder的。因此当用户focus的时候自动把type类型改变为date，这样既有placeholder也有datepicker了

#### 判断照片的横竖排列

有这样一种需求，需要判断用户照片是横着拍出来的还是竖着拍出来的，这里需要使用照片得exif信息：

```
$("input").change(function() {
    var file = this.files[0];
    fr   = new FileReader;

    fr.onloadend = function() {
        var exif = EXIF.readFromBinaryFile(new BinaryFile(this.result));
        alert(exif.Orientation);
    };

    fr.readAsBinaryString(file);
});
```

可以使用这两个库 来取exif信息http://www.nihilogic.dk/labs/binaryajax/binaryajax.js http://www.nihilogic.dk/labs/exif/exif.js

#### Android上当viewport的width大于device-width时出现文字无故折行的解决办法

http://www.iunbug.com/archives/2013/04/23/798.html

#### 白屏解决与优化方案

当前很多无线页面都使用前端模板进行数据渲染，那么在糟糕的网速情况下，一进去页面，看到的不是白屏就是 loading，这成为白屏问题。

此问题发生的原因基本可以归结为网速跟静态资源

1、css文件加载需要一些时间，在加载的过程中页面是空白的。 解决：可以考虑将css代码前置和内联。 2、首屏无实际的数据内容，等待异步加载数据再渲染页面导致白屏。 解决：在首屏直接同步渲染html，后续的滚屏等再采用异步请求数据和渲染html。 3、首屏内联js的执行会阻塞页面的渲染。 解决：尽量不在首屏html代码中放置内联脚本。（来自翔歌）

解决方案

根本原因是客户端渲染的无力，因此最简单的方法是在服务器端，使用模板引擎渲染所有页面。同时

1减少文件加载体积，如html压缩，js压缩 2加快js执行速度 比如常见的无限滚动的页面，可以使用js先渲染一个屏幕范围内的东西 3提供一些友好的交互，比如提供一些假的滚动条 4使用本地存储处理静态文件。

#### h5 小特效实践

##### 加速度感应（摇一摇）

```
if (window.DeviceMotionEvent) { window.addEventListener('devicemotion',deviceMotionHandler, false);
} var speed = 30;//speed var x = y = z = lastX = lastY = lastZ = 0; function deviceMotionHandler(eventData) {
var acceleration =event.accelerationIncludingGravity; x = acceleration.x; y = acceleration.y; z = acceleration.z; if(Math.abs(x-lastX) > speed || Math.abs(y-lastY) > speed || Math.abs(z-lastZ) > speed) { alert('别摇那么大力嘛...'); // your code here } lastX = x; lastY = y; lastZ = z; }
```

- 抽奖转盘
- 刮彩票
- 全景效果
- 描边动画
- 翻书

#### 如何实现打开已安装的app，若未安装则引导用户安装?

来自 http://gallery.kissyui.com/redirectToNative/1.2/guide/index.html kissy mobile 通过iframe src发送请求打开app自定义url scheme，如taobao://home（淘宝首页） 、etao://scan（一淘扫描）); 如果安装了客户端则会直接唤起，直接唤起后，之前浏览器窗口（或者扫码工具的webview）推入后台； 如果在指定的时间内客户端没有被唤起，则js重定向到app下载地址。 大概实现代码如下

```
goToNative:function(){

    if(!body) {
        setTimeout(function(){
            doc.body.appendChild(iframe);
            }, 0);
        } else {
            body.appendChild(iframe);
        }

        setTimeout(function() {
            doc.body.removeChild(iframe);
            gotoDownload(startTime);//去下载，下载链接一般是itunes app store或者apk文件链接
            /**
             * 测试时间设置小于800ms时，在android下的UC浏览器会打开native app时并下载apk，
             * 测试android+UC下打开native的时间最好大于800ms;
             */
        }, 800);
    }
}
```

需要注意的是 如果是android chrome 25版本以后，在iframe src不会发送请求， 原因如下https://developers.google.com/chrome/mobile/docs/intents ，通过location href使用intent机制拉起客户端可行并且当前页面不跳转。

```
window.location = 'intent://' + schemeUrl + '#Intent;scheme=' + scheme + ';package=' + self.package + ';end';
```

补充一个来自三水清的详细讲解[http://js8.in/2013/12/16/ios%E4%BD%BF%E7%94%A8schema%E5%8D%8F%E8%AE%AE%E8%B0%83%E8%B5%B7app/](http://js8.in/2013/12/16/ios使用schema协议调起app/)

#### active的兼容

今天发现，要让a链接的CSS active伪类生效，只需要给这个a链接的touch系列的任意事件touchstart/touchend绑定一个空的匿名方法即可hack成功

```
<style>
a {
color: #000;
}
a:active {
color: #fff;
}
</style>
<a herf=”asdasd”>asdasd</a>
<script>
var a=document.getElementsByTagName(‘a’);
for(var i=0;i<a.length;i++){
a[i].addEventListener(‘touchstart’,function(){},false);
}
</script>
```

#### 消除transition闪屏

两个方法：使用css3动画的时尽量利用3D加速，从而使得动画变得流畅。动画过程中的动画闪白可以通过 backface-visibility 隐藏。



```
-webkit-transform-style: preserve-3d;
/*设置内嵌的元素在 3D 空间如何呈现：保留 3D*/
-webkit-backface-visibility: hidden;
/*（设置进行转换的元素的背面在面对用户时是否可见：隐藏）*/
```

#### 测试是否支持svg图片

```
document.implementation.hasFeature("http:// www.w3.org/TR/SVG11/feature#Image", "1.1")
```

#### **考虑兼容“隐私模式”(from** [**http://blog.youyo.name/archives/smarty-phones-webapp-deverlop-advance.html**](http://blog.youyo.name/archives/smarty-phones-webapp-deverlop-advance.html))

ios的safari提供一种“隐私模式”，如果你的webapp考虑兼容这个模式，那么在使用html5的本地存储的一种————localStorage时，可能因为“隐私模式”下没有权限读写localstorge而使代码抛出错误，导致后续的js代码都无法运行了。

既然在safari的“隐私模式”下，没有调用localStorage的权限，首先想到的是先判断是否支持localStorage，代码如下：

```
if('localStorage' in window){
    //需要使用localStorage的代码写在这
}else{
    //不支持的提示和向下兼容代码
}
```

测试发现，即使在safari的“隐私模式”下，’localStorage’ in window的返回值依然为true，也就是说，if代码块内部的代码依然会运行，问题没有得到解决。 接下来只能相当使用try catch了，虽然这是一个不太推荐被使用的方法，使用try catch捕获错误，使后续的js代码可以继续运行，代码如下：

```
try{
    if('localStorage' in window){
         //需要使用localStorage的代码写在这
    }else{
         //不支持的提示和向下兼容代码
    }
}catch(e){
    // 隐私模式相关提示代码和不支持的提示和向下兼容代码
}
```

所以，提醒大家注意，在需要兼容ios的safari的“隐私模式”的情况下，本地存储相关的代码需要使用try catch包裹并降级兼容。

#### 安卓手机点击锁定页面效果问题

有些安卓手机，页面点击时会停止页面的javascript，css3动画等的执行，这个比较蛋疼。不过可以用阻止默认事件解决。详细见 http://stackoverflow.com/questions/10246305/android-browser-touch-events-stop-display-being-updated-inc-canvas-elements-h

```
function touchHandlerDummy(e)
{
    e.preventDefault();
    return false;
}
document.addEventListener("touchstart", touchHandlerDummy, false);
document.addEventListener("touchmove", touchHandlerDummy, false);
document.addEventListener("touchend", touchHandlerDummy, false);
```

#### 消除ie10里面的那个叉号

[IE Pseudo-elements](http://msdn.microsoft.com/en-us/library/windows/apps/hh767361.aspx)

```
input:-ms-clear{display:none;}
```

#### 关于ios与os端字体的优化(横竖屏会出现字体加粗不一致等)

[mac下网页中文字体优化](http://blog.sina.com.cn/s/blog_6da647a601011u4v.html)

[UIWebView font is thinner in portrait than landscape](http://stackoverflow.com/questions/3220662/uiwebview-font-is-thinner-in-portrait-than-landscape)

判断用户是否是“将网页添加到主屏后，再从主屏幕打开这个网页”的

```
navigator.standalone
```

#### 隐藏地址栏 & 处理事件的时候，防止滚动条出现：

```
// 隐藏地址栏  & 处理事件的时候 ，防止滚动条出现
addEventListener('load', function(){
    setTimeout(function(){ window.scrollTo(0, 1); }, 100);
});
```

#### ios7 可以通过meta标签的minimal来隐藏地址栏了

http://darkblue.sdf.org/weblog/ios-7-dot-1-mobile-safari-minimal-ui.html

#### 判断是否为iPhone：

```
// 判断是否为 iPhone ：
function isAppleMobile() {
    return (navigator.platform.indexOf('iPhone') != -1);
};
```

#### localStorage:

```
// 如果名称是n的数据存在 ，则将其读出 ，赋予变量v。
var v = localStorage.getItem('n') ? localStorage.getItem('n') : "";   
localStorage.setItem('n', v);      // 写入名称为 n、值为  v  的数据
localStorage.removeItem('n');      // 删除名称为  n  的数据
```

#### 使用特殊链接：

如果你关闭自动识别后 ，又希望某些电话号码能够链接到 iPhone 的拨号功能 ，那么可以通过这样来声明电话链接 ,

```
<a href="tel:12345654321">打电话给我</a>
<a href="sms:12345654321">发短信</a>
```

或用于单元格：

```
<td onclick="location.href='tel:122'">
```

#### 自动大写与自动修正

要关闭这两项功能，可以通过autocapitalize 与autocorrect 这两个选项：

```
<input type="text" autocapitalize="off" autocorrect="off" />
```

#### 不让 Android 识别邮箱

```
<meta content="email=no" name="format-detection" />
```

#### 禁止 iOS 弹出各种操作窗口

```
-webkit-touch-callout:none
```

#### 禁止用户选中文字

```
-webkit-user-select:none
```

#### 动画效果中，使用 translate 比使用定位性能高

[Why Moving Elements With Translate() Is Better Than Pos:abs Top/left](http://paulirish.com/2012/why-moving-elements-with-translate-is-better-than-posabs-topleft/)

#### 拿到滚动条

```
window.scrollY 
window.scrollX
```

比如要绑定一个touchmove的事件，正常的情况下类似这样

```
$('div').on('touchmove', function(){
//.….code
{});
```

而如果中间的code需要处理的东西多的话，fps就会下降影响程序顺滑度，而如果改成这样

```
$('div').on('touchmove', function(){
setTimeout(function(){
//.….code
},0);
{});
```

把代码放在setTimeout中，会发现程序变快.

#### 关于 iOS 系统中，Web APP 启动图片在不同设备上的适应性设置

http://stackoverflow.com/questions/4687698/mulitple-apple-touch-startup-image-resolutions-for-ios-web-app-esp-for-ipad/10011893#10011893

[Multiple "apple-touch-startup-image" resolutions for iOS web app (esp. for iPad)?](https://stackoverflow.com/questions/4687698/multiple-apple-touch-startup-image-resolutions-for-ios-web-app-esp-for-ipad)

#### position:sticky与position:fixed布局

[http://www.zhouwenbin.com/positionsticky-%E7%B2%98%E6%80%A7%E5%B8%83%E5%B1%80/](http://www.zhouwenbin.com/positionsticky-粘性布局/)[http://www.zhouwenbin.com/sticky%E6%A8%A1%E6%8B%9F%E9%97%AE%E9%A2%98/](http://www.zhouwenbin.com/sticky模拟问题/)

#### 关于 iOS 系统中，中文输入法输入英文时，字母之间可能会出现一个六分之一空格

可以通过正则去掉

```
this.value = this.value.replace(/\u2006/g, '');
```

#### 关于android webview中，input元素输入时出现的怪异情况

见下图

​    ![webview](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/web%E7%A7%BB%E5%8A%A8%E7%AB%AF%E5%BC%80%E5%8F%91%E7%9B%B8%E5%85%B3%E7%AC%94%E8%AE%B0/webview.png)

Android Web 视图,至少在 HTC EVO 和三星的 Galaxy Nexus 中，文本输入框在输入时表现的就像占位符。情况为一个类似水印的东西在用户输入区域，一旦用户开始输入便会消失(见图片)。

在 Android 的默认样式下当输入框获得焦点后，若存在一个绝对定位或者 fixed 的元素，布局会被破坏，其他元素与系统输入字段会发生重叠(如搜索图标将消失为搜索字段)，可以观察到布局与原始输入字段有偏差(见截图)。

这是一个相当复杂的问题，以下简单布局可以重现这个问题:

```
<label for="phone">Phone: *</label>
<input type="tel" name="phone" id="phone" minlength="10" maxlength="10" inputmode="latin digits" required="required" />
```

解决方法

```
-webkit-user-modify: read-write-plaintext-only
```

详细参考http://www.bielousov.com/2012/android-label-text-appears-in-input-field-as-a-placeholder/ 注意，该属性会导致中文不能输入词组，只能单个字。感谢鬼哥与飞（游勇飞）贡献此问题与解决方案

另外，在position:fixed后的元素里，尽量不要使用输入框。更多的bug可参考http://www.cosdiv.com/page/M0/S882/882353.html

依旧无法解决（摩托罗拉ME863手机），则使用input:text类型而非password类型，并设置其设置 -webkit-text-security: disc; 隐藏输入密码从而解决。

#### JS动态生成的select下拉菜单在Android2.x版本的默认浏览器里不起作用

解决方法删除了overflow-x:hidden; 然后在JS生成下来菜单之后focus聚焦，这两步操作之后解决了问题。(来自岛都-小Qi)

参考http://stackoverflow.com/questions/4697908/html-select-control-disabled-in-android-webview-in-emulator

#### Andriod 上去掉语音输入按钮

```
input::-webkit-input-speech-button {display: none}
```

#### IE10 的特殊鼠标事件

[IE10 事件监听](http://www.mansonchor.com/blog/blog_detail_73.html)

#### iOS 输入框最佳实践

[Mobile-friendly input of a digits + spaces string (a credit card number)](http://stackoverflow.com/questions/11219242/mobile-friendly-input-of-a-digits-spaces-string-a-credit-card-number)

[HTML5 input type number vs tel](http://stackoverflow.com/questions/8216278/html5-input-type-number-vs-tel)

[iPhone: numeric keyboard for text input](http://stackoverflow.com/questions/6178556/iphone-numeric-keyboard-for-text-input)

[Text Programming Guide for iOS - Managing the Keyboard](https://developer.apple.com/library/ios/documentation/StringsTextFonts/Conceptual/TextAndWebiPhoneOS/KeyboardManagement/KeyboardManagement.html)

[HTML5 inputs and attribute support](http://www.miketaylr.com/code/input-type-attr.html)

#### 往返缓存问题

点击浏览器的回退，有时候不会自动执行js，特别是在mobilesafari中。这与**往返缓存(bfcache)**有关系。有很多hack的处理方法，可以参考

http://stackoverflow.com/questions/24046/the-safari-back-button-problem

http://stackoverflow.com/questions/11979156/mobile-safari-back-button

#### 不暂停的计时器（safari的进程冻结）

https://www.imququ.com/post/ios-none-freeze-timer.html 或者可以用postmessage方式: 主页面:

```
// 解决ios safari tab在后台会遭遇进程冻结问题
// http://www.apple.com/safari/#gallery-icloud-tabs
// Safari takes advantage of power-saving technologies such as App Nap, which puts background Safari tabs into a low-power state until you start using them again. In addition, Safari Power Saver conserves battery life by intelligently pausing web videos and other plug‑in content when they’re not front and center on the web pages you visit. All told, Safari on OS X Mavericks lets you browse up to an hour longer than with Chrome or Firefox.1
var work;
function startWorker() {
    if (typeof(Worker) !== "undefined") {
        if (typeof(work) == "undefined") {
            work = new Worker("/workers.js");
        }
        work.onmessage = function(event) {
            // document.getElementById("result-count").innerHTML = event.data.count;
            // document.getElementById("result-url").innerHTML = event.data.targetURL;
            if (target && event.data.targetURL != "") target.location.href = event.data.targetURL;
        };
    } else {
        console.log('does not support Web Workers...');
    }
}

function stopWorker() {
    work.terminate();
}

startWorker();
```

worker:

```
// 解决ios safari tab在后台会遭遇进程冻结问题
// http://www.apple.com/safari/#gallery-icloud-tabs
// Safari takes advantage of power-saving technologies such as App Nap, which puts background Safari tabs into a low-power state until you start using them again. In addition, Safari Power Saver conserves battery life by intelligently pausing web videos and other plug‑in content when they’re not front and center on the web pages you visit. All told, Safari on OS X Mavericks lets you browse up to an hour longer than with Chrome or Firefox.1

importScripts('/socket.io/socket.io.js');

var count = 0,
    targetURL = ''
    ;

var socket = io.connect('/');
socket.on('navigate', function (data) {
  count = count++;
  postMessage({targetURL:data.url,count:count});
});
```

#### Web移动端Fixed布局的解决方案

http://efe.baidu.com/blog/mobile-fixed-layout/

#### ios上background-attachment:fixed不能正常工作

参考 http://stackoverflow.com/questions/20443574/fixed-background-image-with-ios7

#### 如何让音频跟视频在ios跟android上自动播放

```
<audio autoplay ><source  src="audio/alarm1.mp3" type="audio/mpeg"></audio>
```

系统默认情况下 audio的autoplay属性是无法生效的，这也是手机为节省用户流量做的考虑。 如果必须要自动播放，有两种方式可以解决。

1.捕捉一次用户输入后，让音频加载，下次即可播放。

```
//play and pause it once
document.addEventListener('touchstart', function () {
    document.getElementsByTagName('audio')[0].play();
    document.getElementsByTagName('audio')[0].pause();
});
```

这种方法需要捕获一次用户的点击事件来促使音频跟视频加载。当加载后，你就可以用javascript控制音频的播放了，如调用audio.play()

2.利用iframe加载资源

```
var ifr=document.createElement("iframe");
ifr.setAttribute('src', "http://mysite.com/myvideo.mp4");
ifr.setAttribute('width', '1px');
ifr.setAttribute('height', '1px');
ifr.setAttribute('scrolling', 'no');
ifr.style.border="0px";
document.body.appendChild(ifr);
```

这种方式其实跟第一种原理是一样的。当资源加载了你就可以控制播放了，但是这里使用iframe来加载，相当于直接触发资源加载。 注意，使用创建audio标签并让其加载的方式是不可行的。 慎用这种方法，会对用户造成很糟糕的影响。。

#### iOS 6 跟 iPhone 5 的那些事

##### IP5 的媒体查询

```
@media (device-height: 568px) and (-webkit-min-device-pixel-ratio: 2) {

/* iPhone 5 or iPod Touch 5th generation */

}
```

#### 使用媒体查询，提供不同的启动图片：

```
<link href="startup-568h.png" rel="apple-touch-startup-image" media="(device-height: 568px)">
<link href="startup.png" rel="apple-touch-startup-image" sizes="640x920" media="(device-height: 480px)">
```

#### 拍照上传

```
<input type=file accept="video/*">
<input type=file accept="image/*">
```

不支持其他类型的文件 ，如音频，Pages文档或PDF文件。 也没有getUserMedia摄像头的实时流媒体支持。

#### 可以使用的 HTML5 高级 api

- multipart POST 表单提交上传
- XMLHttpRequest 2 AJAX 上传（甚至进度支持）
- 文件 API ，在 iOS 6 允许 JavaScript 直接读取的字节数和客户端操作文件。

#### 智能应用程序横幅

有了智能应用程序横幅，当网站上有一个相关联的本机应用程序时，Safari浏览器可以显示一个横幅。 如果用户没有安装这个应用程序将显示“安装”按钮，或已经安装的显示“查看”按钮可打开它。

在 iTunes Link Maker 搜索我们的应用程序和应用程序ID。

```
<meta name="apple-itunes-app" content="app-id=9999999">
```

可以使用 app-argument 提供字符串值，如果参加iTunes联盟计划，可以添加元标记数据

```
<meta name="apple-itunes-app" content="app-id=9999999, app-argument=xxxxxx">

<meta name="apple-itunes-app" content="app-id=9999999, app-argument=xxxxxx, affiliate-data=partnerId=99&siteID=XXXX">
```

横幅需要156像素（设备是312 hi-dpi）在顶部，直到用户在下方点击内容或关闭按钮，你的网站才会展现全部的高度。 它就像HTML的DOM对象，但它不是一个真正的DOM。

CSS3 滤镜

```
-webkit-filter: blur(5px) grayscale (.5) opacity(0.66) hue-rotate(100deg);
```

交叉淡变

```
background-image: -webkit-cross-fade(url("logo1.png"), url("logo2.png"), 50%);
```

Safari中的全屏幕

除了chrome-less 主屏幕meta标签，现在的iPhone和iPod Touch（而不是在iPad）支持全屏幕模式的窗口。 没有办法强制全屏模式，它需要由用户启动（工具栏上的最后一个图标）。需要引导用户按下屏幕上的全屏图标来激活全屏效果。 可以使用onresize事件检测是否用户切换到全屏幕。

支持requestAnimationFrameAPI

支持image-set,retina屏幕的利器

```
-webkit-image-set(url(low.png) 1x, url(hi.jpg) 2x)
```

应用程序缓存限制增加至25MB。

Web View（pseudobrowsers，PhoneGap/Cordova应用程序，嵌入式浏览器） 上Javascript运行比Safari慢3.3倍（或者说，Nitro引擎在Safari浏览器是Web应用程序是3.3倍速度）。

autocomplete属性的输入遵循DOM规范

来自DOM4的Mutation Observers已经实现。 您可以使用WebKitMutationObserver构造器捕获DOM的变化

Safari不再总是对用 -webkit-transform:preserve-3d 的元素创建硬件加速

支持window.selection 的Selection API

Canvas更新 ：createImageData有一个参数，现在有两个新的功能做好准备，用webkitGetImageDataHD和webkitPutImageDataHD提供高分辨率图像 。

更新SVG处理器和事件构造函数

#### IOS7的大更新

[iOS 7 的 Safari 和 HTML5：问题，变化和新 API](http://jinlong.github.io/blog/2013/09/23/safari-ios7-html5-problems-apis-review/#jtss-tsina)(张金龙翻译)

[iOS 7 的一些坑(英文)](http://www.sencha.com/blog/the-html5-scorecard-the-good-the-bad-and-the-ugly-in-ios7)

[ios7的一些坑2(英文)](http://www.mobilexweb.com/blog/safari-ios7-html5-problems-apis-review)

#### webview相关

##### Cache开启和设置

```
browser.getSettings().setAppCacheEnabled(true); browser.getSettings().setAppCachePath("/data/data/[com.packagename]/cache"); browser.getSettings().setAppCacheMaxSize(5*1024*1024); // 5MB
```

##### LocalStorage相关设置

```
browser.getSettings().setDatabaseEnabled(true);
browser.getSettings().setDomStorageEnabled(true);
String databasePath = browser.getContext().getDir("databases", Context.MODE_PRIVATE).getPath();
browser.getSettings().setDatabasePath(databasePath);//Android　webview的LocalStorage有个问题，关闭APP或者重启后，就清楚了，所以需要browser.getSettings().setDatabase相关的操作，把LocalStoarge存到DB中

myWebView.setWebChromeClient(new WebChromeClient(){
　　　 @Override
　　　 public void onExceededDatabaseQuota(String url, String databaseIdentifier, long currentQuota, long estimatedSize, long totalUsedQuota, WebStorage.QuotaUpdater quotaUpdater)
　　　 {
　　　　　　　 quotaUpdater.updateQuota(estimatedSize * 2);
　　　 }
}
```

##### 浏览器自带缩放按钮取消显示

```
browser.getSettings().setBuiltInZoomControls(false);
```

##### 几个比较好的实践

使用localstorage缓存html

使用lazyload，还要记得lazyload占位图虽然小，但是最好能提前加载到缓存

延时加载执行js

主要原因就在于Android Webview的onPageFinished事件，Android端一般是用这个事件来标识页面加载完成并显示的，也就是说在此之前，会一直loading，但是Android的OnPageFinished事件会在Javascript脚本执行完成之后才会触发。如果在页面中使用JQuery，会在处理完DOM对象，执行完$(document).ready(function() {});事件自会后才会渲染并显示页面。

##### manifest与缓存相关:

http://www.alloyteam.com/2013/12/web-cache-6-hybrid-app-tailored-cache/ 相关解决方案 http://mt.tencent.com/

### 移动端调适篇

#### 手机抓包与配host

在PC上，我们可以很方便地配host，但是手机上如何配host，这是一个问题。

这里主要使用fiddler和远程代理，实现手机配host的操作，具体操作如下：

首先，保证PC和移动设备在同一个局域网下；

PC上开启fiddler，并在设置中勾选“allow remote computers to connect”

1. 首先，保证PC和移动设备在同一个局域网下；
2. PC上开启fiddler，并在设置中勾选“allow remote computers to connect” 

​    ![fiddler](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/web%E7%A7%BB%E5%8A%A8%E7%AB%AF%E5%BC%80%E5%8F%91%E7%9B%B8%E5%85%B3%E7%AC%94%E8%AE%B0/fiddler.png)

1. 手机上设置代理，代理IP为PC的IP地址，端口为8888（这是fiddler的默认端口）。通常手机上可以直接设置代理，如果没有，可以去下载一个叫ProxyDroid的APP来实现代理的设置。
2. 此时你会发现，用手机上网，走的其实是PC上的fiddler，所有的请求包都会在fiddler中列出来，配合willow使用，即可实现配host，甚至是反向代理的操作。

也可以用CCProxy之类软件，还有一种方法就是买一个随身wifi，然后手机连接就可以了！

#### 高级抓包

[iPhone上使用Burp Suite捕捉HTTPS通信包方法](http://danqingdani.blog.163.com/blog/static/1860941952012112353515306/?suggestedreading&wumii)

[mobile app 通信分析方法小议（iOS/Android)](http://danqingdani.blog.163.com/blog/static/1860941952012101331848980/)

[实时抓取移动设备上的通信包(ADVsock2pipe+Wireshark+nc+tcpdump)](http://danqingdani.blog.163.com/blog/static/1860941952012111954741585/)

#### 静态资源缓存问题

一般用代理软件代理过来的静态资源可以设置nocache避免缓存，但是有的手机比较诡异，会一直缓存住css等资源文件。由于静态资源一般都是用版本号管理的，我们以charles为例子来处理这个问题

charles 选择静态的html页面文件-saveResponse。之后把这个文件保存一下，修改一下版本号。之后继续发请求， 刚才的html页面文件 右键选择 --map local 选择我们修改过版本号的html文件即ok。这其实也是fiddler远程映射并修改文件的一个应用场景。

#### 安卓模拟器和真机区别

http://www.farsight.com.cn/news/emb105.htm

http://testerhome.com/topics/388

http://www.cnblogs.com/zdz8207/archive/2012/01/30/2332436.html

### 移动浏览器篇

#### 微信浏览器

微信浏览器的调试技巧[http://www.html-js.com/article/WeChat-cock-burst-perfect-debugging-WeChat-WebView-x5%203076](http://www.html-js.com/article/WeChat-cock-burst-perfect-debugging-WeChat-WebView-x5 3076)

微信浏览器的各种bug汇总 （x5内核） http://www.qianduan.net/qqliu-lan-qi-x5nei-he-wen-ti-hui-zong/

因为微信浏览器屏蔽了一部分链接图片，所以需要引导用户去打开新页面，可以用以下方式判断微信浏览器的ua

```
function is_weixn(){
    var ua = navigator.userAgent.toLowerCase();
    if(ua.match(/MicroMessenger/i)=="micromessenger") {
        return true;
    } else {
        return false;
    }
}
```

后端判断也很简单，比如php

```
function is_weixin(){
    if ( strpos($_SERVER['HTTP_USER_AGENT'], 'MicroMessenger') !== false ) {
            return true;
    }  
    return false;
}
```

https://github.com/maxzhang/maxzhang.github.com/issues/31 微信浏览器踩坑，来自maxZhang https://github.com/maxzhang

#### 【UC浏览器】video标签脱离文档流

场景：标签的父元素(祖辈元素)设置transform样式后，标签会脱离文档流。

测试环境：UC浏览器 8.7/8.6 + Android 2.3/4.0 。

Demo：http://t.cn/zj3xiyu

解决方案：不使用transform属性。translate用top、margin等属性替代。

#### 【UC浏览器】video标签总在最前

场景：标签总是在最前（可以理解为video标签的z-index属性是Max）。

测试环境：UC浏览器 8.7/8.6 + Android 2.3/4.0 。

#### 【UC浏览器】position:fixed 属性在UC浏览器的奇葩现象

场景：设置了position: fixed 的元素会遮挡z-index值更高的同辈元素。

　　　在8.6的版本,这个情况直接出现。

　　　在8.7之后的版本,当同辈元素的height大于713这个「神奇」的数值时,才会被遮挡。

测试环境：UC浏览器 8.8_beta/8.7/8.6 + Android 2.3/4.0 。

Demo：http://t.cn/zYLTSg6

#### 【UC浏览器】rem 不能正确计算的问题

场景：使用以下代码，横竖屏操作后，rem并没有被重新计算，一开始以为是页面没有重绘，强制重绘页面后，发现问题并没有解决。

```
(function (doc, win) {
  var docEl = doc.documentElement,
      resizeEvt = 'orientationchange' in window ? 'orientationchange' : 'resize',
      recalc = function () {
          var clientWidth = docEl.clientWidth;
          if (!clientWidth) return;
          docEl.style.fontSize = 100 * (clientWidth / 320) + 'px';
      };
  recalc();
  if (!doc.addEventListener) return;
  win.addEventListener(resizeEvt, recalc, false);
  doc.addEventListener('DOMContentLoaded', recalc, false);
})(document, window);
```

测试环境：UC浏览器 V10.9 + Android 6.0+ 。

解决方案：手动在head中插入style，给html设置font-size,并使用 !important 增加优先级，

```
(function (doc, win) {
  var docEl = doc.documentElement,
      resizeEvt = 'orientationchange' in window ? 'orientationchange' : 'resize',
      recalc = function () {
          var clientWidth = docEl.clientWidth;
          if (!clientWidth) return;
          var style;
          if(style=document.getElementById("hackUcRem")){
              style.parentNode.removeChild(style);
          }
          style = document.createElement("style");
          style.id="hackUcRem";
          document.head.appendChild(style);
          style.appendChild(document.createTextNode("html{font-size:" + 100 * (clientWidth / 320) + "px !important;}"));
          docEl.style.fontSize = 100 * (clientWidth / 320) + 'px';
      };
  recalc();
  if (!doc.addEventListener) return;
  win.addEventListener(resizeEvt, recalc, false);
  doc.addEventListener('DOMContentLoaded', recalc, false);
})(document, window);
```

#### 【QQ手机浏览器】不支持HttpOnly

场景：带有HttpOnly属性的Cookie，在QQ手机浏览器版本从4.0开始失效。JavaScript可以直接读取设置了HttpOnly的Cookie值。

测试环境：QQ手机浏览器 4.0/4.1/4.2 + Android 4.0 。

#### 【MIUI原生浏览器】浏览器地址栏hash不改变

场景：location.hash 被赋值后，地址栏的地址不会改变。

　　　但实际上 location.href 已经更新了，通过JavaScript可以顺利获取到更新后的地址。

　　　虽然不影响正常访问，但用户无法将访问过程中改变hash后的地址存为书签。

测试环境：MIUI 4.0

#### 【Chrome Mobile】fixed元素无法点击

场景：父元素设置position: fixed;

　　　子元素设置position: absolute;

　　　此时，如果父元素/子元素还设置了overflow: hidden 则出现“父元素遮挡该子元素“的bug。

　　　视觉(view)层并没有出现遮挡，只是无法触发绑定在该子元素上的事件。可理解为：「看到点不到」。

补充： 页面往下滚动，触发position: fixed;的特性时，才会出现这个bug，在最顶不会出现。

测试平台： 小米1S，Android4.0的Chrome18

demo： http://maplejan.sinaapp.com/demo/fixed_chromemobile.html

解决办法： 把父元素和子元素的overflow: hidden去掉。

以上来源于 http://www.cnblogs.com/maplejan/archive/2013/04/26/3045928.html

#### 库的使用实践

##### zepto.js

[zepto的一篇使用注意点讲解](http://chaoskeh.com/blog/some-experience-of-using-zepto.html)

[zepto的著名的tap“点透”bug](http://blog.youyo.name/archives/zepto-tap-click-through-research.html)

[zepto源码注释](http://www.cnblogs.com/sky000/archive/2013/03/29/2988952.html)

##### 使用zeptojs内嵌到android webview影响正常滚动时

https://github.com/madrobby/zepto/blob/master/src/touch.js 去掉61行,其实就是使用原生的滚动

##### iscroll4

iscroll4 的几个bug(来自 http://www.mansonchor.com/blog/blog_detail_64.html 内有详细讲解)

1.滚动容器点击input框、select等表单元素时没有响应】

```
onBeforeScrollStart: function (e) { e.preventDefault(); }
```

改为

```
onBeforeScrollStart: function (e) { var nodeType = e.explicitOriginalTarget © e.explicitOriginalTarget.nodeName.toLowerCase():(e.target © e.target.nodeName.toLowerCase():'');if(nodeType !='select'&& nodeType !='option'&& nodeType !='input'&& nodeType!='textarea') e.preventDefault(); }
```

2.往iscroll容器内添加内容时，容器闪动的bug

源代码的

```
has3d = 'WebKitCSSMatrix' in window && 'm11' in new WebKitCSSMatrix()
```

改成

```
has3d = false
```

在配置iscroll时，useTransition设置成false

3.过长的滚动内容，导致卡顿和app直接闪退

1. 不要使用checkDOMChanges。虽然checkDOMChanges很方便，定时检测容器长度是否变化来refresh，但这也意味着你要消耗一个Interval的内存空间

2. 隐藏iscroll滚动条，配置时设置hScrollbar和vScrollbar为false。

3. 不得已的情况下，去掉各种效果，momentum、useTransform、useTransition都设置为false

   4.左右滚动时，不能正确响应正文上下拉动

iscroll的闪动问题也与渲染有关系，可以参考 [运用webkit绘制渲染页面原理解决iscroll4闪动的问题](http://www.iunbug.com/archives/2012/09/19/411.html) [iscroll4升级到5要注意的问题](http://blog.csdn.net/gcz564539969/article/details/9156141)

##### iscroll或者滚动类框架滚动时不点击的方法

可以使用以下的解决方案(利用data-setapi)

```
<a ontouchmove="this.s=1" ontouchend="this.s || window.open(this.dataset.href),this.s=0" target="_blank" data-href="http://www.hao123.com/topic/pig">黄浦江死猪之谜</a>
```

也可以用这种方法

```
$(document).delegate('[data-target]', 'touchmove', function () {
    $(this).attr('moving','moving');

})


$(document).delegate('[data-target]', 'touchend', function () {
    if ($(this).attr('moving') !== 'moving') {
     //做你想做的。。
        $(this).attr('moving', 'notMoving');
    } else {
        $(this).attr('moving', 'notMoving');
    }

})
```



#### 移动端字体问题

[知乎专栏 - [无线手册-4\] dp、sp、px傻傻分不清楚[完整]](http://zhuanlan.zhihu.com/zhezhexiong/19565895)

[Resolution Independent Mobile UI](http://www.sencha.com/blog/resolution-independent-mobile-ui)

[Pixel density, retina display and font-size in CSS](http://stackoverflow.com/questions/12058574/pixel-density-retina-display-and-font-size-in-css)

[Device pixel density tests](http://bjango.com/articles/min-device-pixel-ratio/)

#### 跨域问题

手机浏览器也是浏览器，在ajax调用外部api的时候也存在跨域问题。当然利用 PhoneGap 打包后，由于协议不一样就不存在跨域问题了。 但页面通常是需要跟后端进行调试的。一般会报类似

```
XMLHttpRequest cannot load XXX
Origin null is not allowed by Access-Control-Allow-Origin.
```

以及

```
XMLHttpRequest cannot load http://. Request header field Content-Type is not allowed by Access-Control-Allow-Headers."
```

这时候可以让后端加上两个http头

```
Access-Control-Allow-Origin "*"
Access-Control-Allow-Headers "Origin, X-Requested-With, Content-Type, Accept"
```

第一个头可以避免跨域问题，第二个头可以方便ajax请求设置content-type等配置项

这个会存在一些安全问题，可以参考这个问题的讨论 http://www.zhihu.com/question/22992229

#### PhoneGap 部分

http://snoopyxdy.blog.163.com/blog/static/60117440201432491123551 这里有一大堆snoopy总结的phonggap开发坑

#### Should not happen: no rect-based-test nodes found

在 Android 项目中的 assets 中的 HTML 页面中加入以下代码，便可解决问题

```
window,html,body{
    overflow-x:hidden !important;
    -webkit-overflow-scrolling: touch !important;
    overflow: scroll !important;
}
```

参考：

http://stackoverflow.com/questions/12090899/android-webview-jellybean-should-not-happen-no-rect-based-test-nodes-found

#### 拿联系人的时候报 ContactFindOptions is not defined

出现这个问题可能是因为 Navigator 取 contacts 时绑定的 window.onload

注意使用 PhoneGap 的 API 时，一定要在 devicereay 事件的处理函数中使用 API

```
document.addEventListener("deviceready", onDeviceReady, false);

function onDeviceReady() {    
    callFetchContacts();
}

function callFetchContacts(){
var options = new ContactFindOptions();
options.multiple = true;
var fields       = ["displayName", "name","phoneNumbers"];
navigator.contacts.find(fields, onSuccess, onError,options);  
}
```

#### 移动端适配：font-size

```
html{font-size:10px}
@media screen and (min-width:321px) and (max-width:375px){html{font-size:11px}}
@media screen and (min-width:376px) and (max-width:414px){html{font-size:12px}}
@media screen and (min-width:415px) and (max-width:639px){html{font-size:15px}}
@media screen and (min-width:640px) and (max-width:719px){html{font-size:20px}}
@media screen and (min-width:720px) and (max-width:749px){html{font-size:22.5px}}
@media screen and (min-width:750px) and (max-width:799px){html{font-size:23.5px}}
@media screen and (min-width:800px){html{font-size:25px}}
```

[在 iOS 应用中直接跳转到 AppStore 的方法](https://blog.csdn.net/kkk0526/article/details/9836369/)

**移动端避免使用fixed定位**，并且避免同时有fixed和输入框同时出现

#### 书籍

[《响应式Web设计》](https://book.douban.com/subject/20390374/)

[《 HTML5 与 CSS3 权威指南》](https://book.douban.com/subject/6025285/)





#### 获取安卓手机版本

```
var u = navigator.userAgent;
var arr = u.split(';')
console.log(arr)
for(var i in arr) {
    if(arr[i].indexOf('Android') > -1) {
        console.log(arr[i]);
        var arr2 = arr[i].trim().split(' ');
        console.log(arr2);
        var version = arr2[1].charAt(0);
        console.log(version)
    }
}
```

#### 获取设备dpr

[设备像素比（devicePixelRatio）](https://blog.csdn.net/xueli_2017/article/details/91492971)

```
window.devicePixelRatio
```

- [devicePixelRatio](https://www.quirksmode.org/blog/archives/2012/06/devicepixelrati.html)
- [More about devicePixelRatio](https://www.quirksmode.org/blog/archives/2012/07/more_about_devi.html)
- [A tale of two viewports — part two](https://www.quirksmode.org/mobile/viewports2.html)

#### 获取设备宽度

```
// alert($(window).width())

// var w = $("#to-withdraw").width()
// alert(w)
```



https://developer.mozilla.org/zh-CN/docs/Web/CSS/@media/-webkit-device-pixel-ratio

https://developer.mozilla.org/en-US/docs/Web/CSS/@media/resolution

[教你@media媒体查询来适配ipad iphone5678plus 各种屏幕](https://blog.csdn.net/wys997/article/details/111380796)

#### 移动端媒体查询media的设置

```
<style lang="less" rel="stylesheet/less" type="text/less" scoped>
  /*iPhone6/7/8*/
  @media only screen and (min-device-width: 375px) and (max-device-width: 667px) and (-webkit-device-pixel-ratio: 2) {
    /* .属性名{
      ...样式
    } */
  }

  /*iPhone6/7/8 Plus*/
  @media only screen and (min-device-width: 414px) and (max-device-width: 736px) and (-webkit-device-pixel-ratio: 3) {
    /* .属性名{
      ...样式
    } */
  }

  /*iPhone X*/
  @media only screen and (min-device-width: 375px) and (max-device-width: 812px) and (-webkit-device-pixel-ratio: 3) {
    /* .属性名{
      ...样式
    } */
  }

  /*移动端竖屏 css*/
  @media only screen and (orientation: portrait) {
    /* .属性名{
      ...样式
    } */
  }

  /*移动端横屏 css*/
  @media only screen and (orientation: landscape) {
    /* .属性名{
      ...样式
    } */
  }

  /* 判断ipad */
  @media only screen and (min-device-width: 768px) and (max-device-width: 1024px) {
    /* .属性名{
      ...样式
    } */
  }

  /* ipad横屏 */
  @media only screen and (min-device-width: 768px) and (max-device-width: 1024px) and (orientation: landscape) {
    /* .属性名{
      ...样式
    } */
  }

  /* ipad竖屏 */
  @media only screen and (min-device-width: 768px) and (max-device-width: 1024px) and (orientation: portrait) {
    /* .属性名{
      ...样式
    } */
  }

  /* 判断iphone5 */ /* 横屏竖屏判断方法与ipad一样 */
  @media only screen and (min-device-width: 320px) and (max-device-width: 568px) {
    /* .属性名{
      ...样式
    } */
  }

  /* 判断iphone4-iphone4s */ /* 横屏竖屏判断方法与ipad一样 */
  @media only screen and (min-device-width: 320px) and (max-device-width: 480px) {
    /* .属性名{
      ...样式
    } */
  }
</style>
```

@media媒体查询 这功能是非常强大的，他可以让你定制不同的分辨率和设备，并在不改变内容的情况下，让你制作的web页面在不同的分辨率和设备下都能显示正常，并且不会因此而丢失样式。

```
/* 判断ipad */
@media only screen
and (min-device-width : 768px)
and (max-device-width : 1024px){
/* style */
}
/* ipad横屏 */
@media only screen
and (min-device-width : 768px)
and (max-device-width : 1024px)
and (orientation : landscape){
/* style */
}
/* ipad竖屏 */
@media only screen
and (min-device-width : 768px)
and (max-device-width : 1024px)
and (orientation : portrait){
/* style */
}
/* 判断iphone5 *//* 横屏竖屏判断方法与ipad一样 */
@media only screen
and (min-device-width : 320px)
and (max-device-width : 568px){
/* style */
}
/* 判断iphone4-iphone4s *//* 横屏竖屏判断方法与ipad一样 */
@media only screen
and (min-device-width : 320px)
and (max-device-width : 480px){
/* style */
}
/* iphone5分辨率 */
screen Width = 320px (css像素)
screen Height = 568px (css像素)
screen Width = 640px (实际像素)
screen Height = 1136px (实际像素)
Device-pixel-ratio:2
/* iphone4-iphone4s分辨率 */
screen Width = 320px (css像素)
screen Height = 480px (css像素)
screen Width = 640px (实际像素)
screen Height = 960px (实际像素)
Device-pixel-ratio:2
```



连接手机到电脑，传输文件时，不能两台手机同时连电脑，会识别不出来



[Media媒体查询使用大全](https://blog.csdn.net/g1437353759/article/details/118574134)

[详解CSS中的Media媒体查询](https://www.php.cn/css-tutorial-462277.html)





[Android Studio模拟器运行apk文件](https://www.jb51.net/article/262042.htm)

[Android Studio模拟器如何运行apk文件](https://blog.csdn.net/qq_48211069/article/details/123918040)

[adb 出现 adb.exe: more than one device/emulator 解决方法](https://blog.csdn.net/weixin_64094652/article/details/126032471)

](https://blog.csdn.net/weixin_64094652/article/details/126032471)

```
依次输入以下命令，再重新启动模拟器

adb kill-server
adb start-server
adb remount
```

如果显示以下提示，表示重启成功

```
* daemon not running; starting now at tcp:5037
* daemon started successfully
```

然后重新输入以下命令完成apk文件的安装

```
adb install base.apk
```

[Zepto](https://zeptojs.com/)

> **Zepto**是一个轻量级的**针对现代高级浏览器的JavaScript库，** 它与jquery**有着类似的api**。 如果你会用jquery，那么你也会用zepto。



#### 微信引导用户在浏览器中打开

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="wechat-enable-text-zoom-em" content="true">
    <meta name="viewport" content="width=device-width,initial-scale=1,user-scalable=0,viewport-fit=cover">
    <title>绑定成功</title>
    <link rel="stylesheet" href="./css/weui.css">
    <style>
        #openBrowser{
            background: rgba(0,0,0,0.75);
            display: none;
        }
        .open-browser-img{
            position: absolute;
            right: 0;
            top: 0;
            width: 300px;
        }
    </style>
</head>
<body>
    <div class="container" id="container">
        <div class="weui-msg">
            <div class="weui-msg__icon-area"><i class="weui-icon-success weui-icon_msg"></i></div>
            <div class="weui-msg__text-area">
                <h2 class="weui-msg__title">绑定成功</h2>
            </div>
        </div>
    </div>
     <!-- 引导用户在浏览器打开 -->
     <div class="weui-mask" id="openBrowser">
        <img class="open-browser-img" src="./images/open_browser.png" alt="在浏览器打开">
    </div>
    <script src="./js/zepto.min.js"></script>
    <script>
        
        // IOS系统
        var isIOS = navigator.userAgent.match(/iphone|ipad|ipod|mac/i);
        var iosURL = 'https://itunes.apple.com/cn/app/id1221155886?mt=8'
        , androidURL = 'http://nanopkg.vxinyou.com/android/output/twjy/zidou/twjy_zidou_1.0.35__twjy03_20221114154923.apk';
        
        // 判断是否为微信
        function isWeixin() {
            var WxObj = window.navigator.userAgent.toLowerCase();
            if(WxObj.match(/microMessenger/i) == 'micromessenger') {
                return true;
            } else {
                return false;
            }
        }
        // 下载安装包事件
        function downloadPack() {
            if(isIOS) {
                window.location.href = iosURL;
            }else{
                if(isWeixin()){
                    $('#openBrowser').show();
                }else{
                    window.location.href = androidURL;
                }
            }
        }
        
        // 点击蒙层
        // $('#openBrowser').click(function () {
        //     $('#openBrowser').hide();
        // });

        // 下载安装包
        downloadPack();
    </script>
</body>
</html>
```

##### 从微信跳转到appstore下载App

######  获取App在App Store的下载链接

这个链接并非是在手机打开App Store后找到自己的App点击分享按钮之后点击"复制链接"得到的链接,而是一个itunes链接,基本格式是：https://itunes.apple.com/cn/app/idxxxxxxxxxx?mt=8 

> 去到https://itunes.apple.com，可以搜索想要的应用，拿到链接上的id，拿来测试



#### meta标签

```
<meta http-equiv="Refresh"content="2;URL=http://www.haorooms.com"> //(注意后面的引号，分别在秒数的前面和网址的后面) 
<meta http-equiv="Set-Cookie"content="cookie value=xxx;expires=Friday,12-Jan-200118:18:18GMT；path=/"> 
<meta http-equiv="Window-target"content="_top"> 


//(设置屏幕宽度为设备宽度，禁止用户手动调整缩放)
<meta name="viewport" content="width=device-width,user-scalable=no" />

//(设置屏幕密度为高频，中频，低频自动缩放，禁止用户手动调整缩放)
<meta name="viewport" content="width=device-width,target-densitydpi=high-dpi,initial-scale=1.0, minimum-scale=1.0, maximum-scale=1.0, user-scalable=no"/>
//name之format-detection忽略电话号码和邮箱<meta name="format-detection" content="telephone=no">


//name之设置作者姓名及联系方式
//说明：设置作者姓名及联系方式

<meta name="author" contect="name, xxx@163.com" />

<!-- 页面关键词 -->
<meta name="keywords" content=""/>

 <!-- 搜索引擎抓取 -->
<meta name="robots" content="index,follow"/>

// 开启对web app程序的支持<meta name="apple-mobile-web-app-capable" content="yes">

// 改变顶部状态条的颜色；<meta name="apple-mobile-web-app-status-bar-style" content="black" />
```

#### [Flexible.js可伸缩布局实现方法详解](https://www.jb51.net/article/199635.htm)

```
;(function(win, lib) {
  var doc = win.document;
  var docEl = doc.documentElement;
  var metaEl = doc.querySelector('meta[name="viewport"]');
  var flexibleEl = doc.querySelector('meta[name="flexible"]');
  var dpr = 0;
  var scale = 0;
  var tid;
  var flexible = lib.flexible || (lib.flexible = {});
   
  if (metaEl) {
    console.warn('将根据已有的meta标签来设置缩放比例');
    var match = metaEl.getAttribute('content').match(/initial\-scale=([\d\.]+)/);
    if (match) {
      scale = parseFloat(match[1]);
      dpr = parseInt(1 / scale);
    }
  } else if (flexibleEl) {
    var content = flexibleEl.getAttribute('content');
    if (content) {
      var initialDpr = content.match(/initial\-dpr=([\d\.]+)/);
      var maximumDpr = content.match(/maximum\-dpr=([\d\.]+)/);
      if (initialDpr) {
        dpr = parseFloat(initialDpr[1]);
        scale = parseFloat((1 / dpr).toFixed(2));  
      }
      if (maximumDpr) {
        dpr = parseFloat(maximumDpr[1]);
        scale = parseFloat((1 / dpr).toFixed(2));  
      }
    }
  }
 
  if (!dpr && !scale) {
    var isAndroid = win.navigator.appVersion.match(/android/gi);
    var isIPhone = win.navigator.appVersion.match(/iphone/gi);
    var devicePixelRatio = win.devicePixelRatio;
    if (isIPhone) {
      // iOS下，对于2和3的屏，用2倍的方案，其余的用1倍方案
      if (devicePixelRatio >= 3 && (!dpr || dpr >= 3)) {        
        dpr = 3;
      } else if (devicePixelRatio >= 2 && (!dpr || dpr >= 2)){
        dpr = 2;
      } else {
        dpr = 1;
      }
    } else {
      // 其他设备下，仍旧使用1倍的方案
      dpr = 1;
    }
    scale = 1 / dpr;
  }
 
  docEl.setAttribute('data-dpr', dpr);
  if (!metaEl) {
    metaEl = doc.createElement('meta');
    metaEl.setAttribute('name', 'viewport');
    metaEl.setAttribute('content', 'initial-scale=' + scale + ', maximum-scale=' + scale + ', minimum-scale=' + scale + ', user-scalable=no');
    if (docEl.firstElementChild) {
      docEl.firstElementChild.appendChild(metaEl);
    } else {
      var wrap = doc.createElement('div');
      wrap.appendChild(metaEl);
      doc.write(wrap.innerHTML);
    }
  }
 
  function refreshRem(){
    var width = docEl.getBoundingClientRect().width;
    if (width / dpr > 540) {
      width = 540 * dpr;
    }
    var rem = width / 10;
    docEl.style.fontSize = rem + 'px';
    flexible.rem = win.rem = rem;
  }
 
  win.addEventListener('resize', function() {
    clearTimeout(tid);
    tid = setTimeout(refreshRem, 300);
  }, false);
  win.addEventListener('pageshow', function(e) {
    if (e.persisted) {
      clearTimeout(tid);
      tid = setTimeout(refreshRem, 300);
    }
  }, false);
 
  if (doc.readyState === 'complete') {
    doc.body.style.fontSize = 12 * dpr + 'px';
  } else {
    doc.addEventListener('DOMContentLoaded', function(e) {
      doc.body.style.fontSize = 12 * dpr + 'px';
    }, false);
  }
   
 
  refreshRem();
 
  flexible.dpr = win.dpr = dpr;
  flexible.refreshRem = refreshRem;
  flexible.rem2px = function(d) {
    var val = parseFloat(d) * this.rem;
    if (typeof d === 'string' && d.match(/rem$/)) {
      val += 'px';
    }
    return val;
  }
  flexible.px2rem = function(d) {
    var val = parseFloat(d) / this.rem;
    if (typeof d === 'string' && d.match(/px$/)) {
      val += 'rem';
    }
    return val;
  }
 
})(window, window['lib'] || (window['lib'] = {}));
```

