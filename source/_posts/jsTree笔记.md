---
title: jsTree笔记
date: 2021-01-15 18:01:30
tags:
- jsTree
categories:
- 工作笔记
- jsTree
---

[jsTree](https://www.jstree.com.cn/)

#### 清除上次操作记录

**需求**：当进来页面时，页面只展开第一级目录

{% asset_img note1.png %}

**目前存在问题**：当用户在树上操作了置换，重新刷新页面，进来置换，依然保持上次操作后的状态，如图：

{% asset_img note2.png %}

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

{% asset_img note3.png %}

存在bug：

{% asset_img note4.png %}



##### 展开全部

```
$("#group_admin").jstree("close_all");
```

##### 收起全部

```
$("#group_admin").jstree("open_all");
```

