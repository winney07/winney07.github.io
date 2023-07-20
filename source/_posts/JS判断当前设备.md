---
title: JS判断当前设备
date: 2018-09-14 11:20:31
tags:
- JavaScript
categories: 
- JavaScript
---
## 判断当前设备是否为移动端

```
function isMobile() {
    return /Android|webOS|iPhone|iPad|iPod|BlackBerry|IEMobile|Opera Mini/i.test(navigator.userAgent);
}
```

### 判断当前设备是否为Android设备

```
function isAndroid() {
  return /Android/i.test(navigator.userAgent);
}
```

### 判断当前设备是否为iOS设备

```
function isIOS() {
  return /iPhone|iPad|iPod/i.test(navigator.userAgent);
}
```

## 判断当前设备是否为PC端

```
function isDesktop() {
    const userAgent = navigator.userAgent;
    // 移动设备关键词
    const mobileKeywords = ['Mobile', 'Android', 'iPhone', 'iPad', 'Windows Phone', 'BlackBerry', 'Nokia', 'SymbianOS'];

    // 判断是否包含移动设备关键词
    for (let keyword of mobileKeywords) {
        if (userAgent.includes(keyword)) {
            return false; 
        }
    }

    return true; 
}
```

> JavaScript中的navigator.userAgent属性来获取用户代理字符串

> 如果将iPod也视为移动设备，可以将`iPod`添加到`mobileKeywords`中。

## 判断当前环境(当前所在客户端)

### 判断是否为微信

```
function isWeChat() {
    var ua = navigator.userAgent.toLowerCase();
    return ua.indexOf('micromessenger') > -1;
}
```

### 判断是否为QQ

```
function isQQ() {
    var ua = navigator.userAgent.toLowerCase();
    return ua.indexOf("qq") !== -1;
}
```

### 判断是否为支付宝

```
function isAlipay() {
    var ua = navigator.userAgent.toLowerCase();
    return ua.indexOf('alipayclient') > -1;
}
```

### 判断是否为微博

```
function isWeibo() {
    var ua = navigator.userAgent.toLowerCase();
    return ua.indexOf('weibo') > -1;
}
```

