---
title: web移动端开发相关笔记
date: 2018-06-18 11:40:08
tags:
- 移动端开发
- 工作笔记
---



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

#### 



```
<li>
<div class="left">
    <div class="hb-price">
        <strong>红包提现</strong>
        <p>2022-08-01 19:09:09</p>
    </div>
</div>
<div class="right r-flex">
    <strong>+888</strong>
    <p>
        审核中
    </p>
</div>
</li>
```

