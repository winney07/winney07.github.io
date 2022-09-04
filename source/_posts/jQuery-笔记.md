---
title: jQuery-笔记
date: 2019-03-07 15:01:55
tags:
- jQuery
categories: 
- 工作笔记
- jQuery
---

#### 监听输入框的值变化事件

```
$(".search-input").bind('input porpertychange',function(){
	.....
});
```

不足：输入中文时，每输入一个字母，都会触发

#### 监听输入框的值变化-优化

改为使用compositionstart和compositionend

```
// 搜索框
var flag = true;
$(".optionList .searchIpt").on("compositionstart", function() {
    flag = false;
});
$(".optionList .searchIpt").on("compositionend", function() {
    flag = true;
});
$(".optionList .searchIpt").on("keyup", function() {
    if(flag) {
        var text = $(this).val().trim();
        // 匹配查询结果
        searchCheck(text, ".searchIpt");
    }
});
```

#### 回到页面顶部

```
window.onscroll = function(){
    if (document.documentElement.scrollTop || document.body.scrollTop > 0) {
        document.getElementById("test").style.display='block';
    }else{
        document.getElementById("test").style.display='none';
    }
}
test.onclick = function(){
    document.body.scrollTop = document.documentElement.scrollTop = 0;
    document.getElementById("test").style.display = "none";
}
```

