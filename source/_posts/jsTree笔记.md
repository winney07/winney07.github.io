---
title: jsTree笔记
date: 2021-01-15 18:01:30
tags:
- jsTree
categories:
- 前端插件
- jsTree
---

[jsTree](https://www.jstree.com.cn/)

#### 清除上次操作记录

**需求**：当进来页面时，页面只展开第一级目录

![jstree只展开第一级目录](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/jsTree%E7%AC%94%E8%AE%B0/note1.png)

**目前存在问题**：当用户在树上操作了置换，重新刷新页面，进来置换，依然保持上次操作后的状态，如图：

![依然保持上次操作后的状态](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/jsTree%E7%AC%94%E8%AE%B0/note2.png)

解决方法：

在changed.jstree事件里面，让树重新刷新

```
$('#jstree_demo_div').on("changed.jstree", function (e, data) {
      $('#jstree_demo_div').jstree('refresh');
 });
```

写法1：

```
$('#treeId').jstree(true).refresh();
```

写法2：

```
$('#jstree_demo_div').jstree('refresh');
```

##### 只展开第一级目录

```
data[0].state.opened = true;
rendertree_group_admin(data);
```

> state.opened是控制展开还是收起，设置第一级的state.opened为true。



结合（解决jstree初始状态只展开第一级目录）

```
on('changed.jstree', function (e, data) {
    // 清除树用户之前的操作记录
    $('#group_ admin').jstree('refresh');
    .....
}
```

```
success: function (ret){
    if (ret.hasOwnProperty("code")) {
    	var data = ret.hasOwnProperty("data") && ret.data != "" ? ret.data : "";
        if (ret.code === 1) {
            $("#group_admin").jstree("destroy");
            data[Ø].state, opened = true;
            rendertree_group_admin(data);
         }
    }
}
```

存在bug：

```{
// 获取是否刚登录进来页面
var isFirst = localStorage.getItem('loginInPage');
if(isFirst == 'true'){
	// 清除树的用户之前的操作记录
	$('#group_admin').jstree('refresh');
}
```

##### 展开全部

```
$("#group_admin").jstree("close_all");
```

##### 收起全部

```
$("#group_admin").jstree("open_all");
```

