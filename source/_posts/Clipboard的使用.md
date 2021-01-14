---
title: Clipboard的使用
date: 2020-11-04 14:44:28
tags: 
- Clipboard
categories: 
- 工作笔记
- Clipboard
---

#### 如果存在clipboard,先将它销毁
```
if(clipboard) {
    clipboard.destroy();
}
```
##### [Clipboard官网使用教程](http://www.clipboardjs.cn/)

##### 复制成功和复制失败的提示
```
var u = navigator.userAgent;
clipboard.on('success', function(e) {
    layer.msg('复制成功', {time: 1000});
    e.clearSelection();
});
clipboard.on('error', function(e) {
    if(u.indexOf('UCBrowser') > -1){
        layer.msg('您的浏览器不支持，请长按内容手动复制！', {time: 1000});
    } else {
        layer.msg('复制失败', {time: 1000});
    }
});
```

##### 如果提示信息弹两次
```
自己写一个copySuccessTip提示信息
$(".copySuccessTip").addClass("mymove");
setTimeout(function() {
    $(".copySuccessTip").removeClass("mymove");
},1000);
```




```
引入图片：
{% asset_img css1.png %}
引入链接：
[参考的博客](https://juejin.im/post/5b15022ff265da6e163720c6)
```