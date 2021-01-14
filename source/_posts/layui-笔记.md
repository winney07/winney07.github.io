---
title: layui 笔记
date: 2020-06-24 15:41:32
tags:
- layui
categories: 
- 工作笔记
- layui
---

### 修改了layui表格的内容，不刷新页面，只刷新表格内容，页码不刷新解决方法

```
function render_table(tabledata, cur) {
  ·········
  , page: {
    curr: cur
  }
  , data: tabledata
   ·········
}

//获取当前页
var curr = $(".layui-laypage-skip input").val();
//重新渲染表格
<!-- res.data：修改数据后，重新返回渲染表格的数据 -->
<!-- 从curr页开始渲染表格 -->
render_table(res.data, curr);

```
### layui同时清空多个表单元素的值
```
1、 form 加上 lay-filter属性  lay-filter="group_form"
2、 
$("#cancel").click(function() {
    form.val("group_form", {
      "sdk": "",     //单选框清空不了
      "name": "",    //输入框可以清空
      "sort": "",    //复选框清空不了
      "ddddd": "",   //下拉框可以清空
      "password": "" //密码框可以清空
    })
  })
```