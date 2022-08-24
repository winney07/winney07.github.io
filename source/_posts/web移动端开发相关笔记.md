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