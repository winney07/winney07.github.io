---
title: IE兼容性处理
date: 2021-01-15 15:09:48
tags:
- IE兼容
categories:
- 工作笔记
- IE兼容
---

#### js判断浏览器是否为IE浏览器

IE6-8和IE11都适用：

```
function isIE() { //ie?
     if (!!window.ActiveXObject || "ActiveXObject" in window)
            { return true; }
     else
            { return false; }
 }
```

> window.ActiveXObject：判断浏览器是否支持ActiveX控件，只有IE浏览器里面支持ActiveX控件
> 如果浏览器支持ActiveX控件，可以利用 var xml = new ActiveXObject("Microsoft.XMLHTTP"); 创建XMLHttpRequest 对象（这是在IE7以前的版本中）；
>
> 在较新的IE版本中可以利用 var xml = new ActiveXObject("Msxml2.XMLHTTP")的形式创建XMLHttpRequest对象;
>
> 而在IE7及非IE浏览器中可以利用v ar xml=new XMLHttpRequest()创建XMLHttpRequest对象。



#### IE浏览器固定定位（fixed）的弹窗

{% asset_img ie-fixed.png %}

解决：使用相对定位（absolute），弹出蒙层，body使用overflow:hidden样式，控制页面不滚动。



#### 去除IE10中输入框和密码框的X按钮和小眼睛

{% asset_img ie10-input.png %}

```
方法：
/*去除IE输入框的X标记*/
input[type=text]::-ms-clear {display: none;}

/*去除IE输入框的小眼睛标记*/
input[type=password]::-ms-reveal {display: none;}

如果想要单独去除某个输入框的话，可以把input[type=text]改为.target-class即可。
```

#### 去掉a标签点击(active)状态的背景色

```
ie浏览器，点击a标签时，点击状态，有个背景色
想去掉这个样式：
设置：
a:active{
    -webkit-tap-highlight-color: rgba(0,0,0,0);
    -webkit-tap-highlight-color: transparent;
    outline: none;
    background: none;
    text-decoration: none;
}
```

#### 复选框 input type="check"

```
普通浏览器：
<input type="checkbox" checked="" />
在IE浏览器中checked属性的写法是大写的:
<input type="checkbox" CHECKED="" />

所以js获取checked时，要考虑ie的情况。
```

