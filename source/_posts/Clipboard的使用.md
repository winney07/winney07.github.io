---
title: Clipboard的使用
date: 2020-11-04 14:44:28
tags: 
- Clipboard
categories: 
- 前端插件
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

#### 解决clipboard复制弹多次提示的问题

1、使用destroy（在单页面里面，回来页面，如果存在这个对象，就删除。）

```
// 如果存在clipboard，先将它销毁
if(clipboard){
	clipboard.destroy();
}

var clipboard =new ClipboardJS('.copyBtn', {
	text: function(trigger){
		var txt = $(trigger).data( "clipboard-text");
		return txt;		//	返回需要复制的内容
    }
});

var u = navigator.userAgent;

clipboard.on('success', function(e){
	layer.msg('复制成功');
	e.clearselection();
});

clipboard.on('error', function(e) {
	if(u.indexOf("UCBrowser") >-1){
		layer.msg('您的浏览器不支持，请长按内容手动复制!');
	}else {
		layer.msg('复制失败');
	}
});
```

2、换成setTimeout，不用layer.msg（copySuccessTip的样式模拟layer.msg的样式即可）

```
clipboard.on('success', function(e){
	$('.copySuccessTip').show();
	
	setTimeout(function(){
		$('.copySuccessTip').hide();
	}, 1000);
});
```