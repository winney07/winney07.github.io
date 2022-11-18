---
title: jQuery-笔记
date: 2019-03-07 15:01:55
tags:
- jQuery
categories: 
- 工作笔记
- jQuery
---



[jQuery UI](https://www.jqueryui.org.cn/)

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

#### 过滤选择器

[jQuery 学习之路（2）：选择器与过滤器](https://www.lmlphp.com/user/58650/article/item/808868/)

一、基本选择器

```
标签选择器：　　$('button')

ID选择器：　　$('#id1')

类选择器：　　$('.class1')

多重选择器：　　$('#id1,.class1,button')

全体选择器：　　$('*') 
```

基本选择器完全根据 CSS 选择器的规范而来，对于了解 CSS 的用户非常容易掌握。

**二、层次选择器**

```
子选择器：　　$('parent > child')　　　　　　　　
后代选择器：　　$('ancester descendant')
单一兄弟选择器：　　$('prev + next')
所有兄弟选择器：　　$('prev ~ siblings')
```

　　子选择器和后代选择器的区别：子选择器是后代选择器的子集，前者只筛选出符合条件的直接子元素，后者筛选出符合条件的所有子孙元素。
　　单一兄弟选择器与所有兄弟选择器类似，前者只筛选出符合条件的下一个同辈元素，后者筛选出符合条件的后面的所有的同辈元素。

**三、属性选择器**

　　属性选择器可以筛选出包含特定属性的元素，或者根据属性的值的格式来筛选出元素。

```
属性包含：　　　　　　　　[attr]
属性值为指定字符串：　　　　[attr = "value"]
属性值不为指定字符串：　　　　[attr != "value"]
属性值以指定字符串开始：　　　　[attr ^= "value"]
属性值以指定字符串结束：　　　　[attr $= "value"]
属性值包含指定字符串：　　　　[attr *= "value"]
多属性筛选：　　　　　　　　[attr1 *= "value1"][attr2 = "value2"]
```

　　其中，[name != "value"] 的实现效率较低，可以使用 :not([attr = 'value']) 的形式

**四、基本过滤器**

　　有些过滤器的实现并不高效，原因参见官网，对于这部分过滤器，建议使用 .filter(selector) 来调用，如 $('div').filter(':hidden') ，后面所有的这类过滤器都以红色特殊标出。

```
:animated　　　　    当前执行动画的元素
:eq(index)　　　　    取出指定索引的元素（jQuery 对象是集合，索引从0开始）
:gt(index)　　　　　　取出索引大于指定值的元素
:lt(index)　　　　　　　　取出索引小于指定值的元素
:first 　　　　　 取出第一个元素，即索引为0的元素
:last　　　　　　取出最后一个元素，即索引为 size()-1 的元素
:even　　　　　　取出索引为偶数的元素
:odd　　　　　　取出索引为奇数的元素
:header　　　　　取出所有标题元素，如 h1,h2,h3 等
:root　　　　　　取出根元素
:not(selector)　　取出所有不匹配指定过滤器的元素　
:focus　　　　　　　　　　当前得到焦点的元素
```

**五、子元素过滤器**

```
:first-child　　　　　　　　是其父元素的第一个子元素
:last-child　　　　　　　　是其父元素的最后一个元素
:first-of-type　　　　　　　　是同辈同类元素中的第一个元素
:last-of-type　　　　　　　　是同辈同类元素中的最后一个元素
:only-child　　　　　　　　是其父元素的唯一子元素
:only-of-type　　　　　　在同辈元素中，没有同类元素的元素，即此元素是同辈元素中唯一的该类型元素
:nth-child(index)　　　　其父元素的第 index 元素，该 index 从 1 开始
:nth-last-child(index)　　　　其父元素的倒数第 index 元素，该 index 从 1 开始
:nth-of-type(index)　　　　　　是同辈的同类元素中的第 index 元素，该 index 从 1 开始
:nth-last-of-type(index)　　　　是同辈的同类元素中倒数第 index 元素，该 index 从 1 开始
```

**六、内容过滤器**

```
:contains(text)　　　　　　包含指定字符串的元素
:empty　　　　　　　　　　没有子元素的元素
:has(selector)　　　　　　 包含至少一个指定的选择器匹配的元素
:parent　　　　　　　　　　包含至少一个子节点的（一个元素或文本）元素
```

**七、表单过滤器**

```
:input
:text
:password
:button
:reset
:submit
:radio
:checkbox
:checked
:selected
:file
:image
:focus
:enabled
:disabled
```

**八、可见性过滤器**

```
:hidden　　　　当前隐藏的元素
:visible　　　　当前显示的元素
```

#### 



#### jQuery自定义扩展



#### 插件

- jquery-ui
- jquery-lazyload
- jquery-color