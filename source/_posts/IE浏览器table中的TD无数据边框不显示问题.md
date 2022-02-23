---
title: IE浏览器table中的TD无数据边框不显示问题
date: 2019-07-19 11:43:34
tags:
- 兼容
categories: 
- 工作笔记
- 兼容
---
在IE(目前发现是ie9,ie10)浏览器下，无数据的时候：
![在IE(目前发现是ie9,ie10)浏览器下，无数据的时候](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/IE%E6%B5%8F%E8%A7%88%E5%99%A8table%E4%B8%AD%E7%9A%84TD%E6%97%A0%E6%95%B0%E6%8D%AE%E8%BE%B9%E6%A1%86%E4%B8%8D%E6%98%BE%E7%A4%BA%E9%97%AE%E9%A2%98/1.png)

原先代码：
合并单元格：
```bash
<tr><td colspan="4">暂无数据</td></tr>
```
<!--more-->
结构代码：
```bash
<div class="layui-clear">
    <div class="layui-table-body" id="table-body">
    //表格模板
    <include file="GlobalConfig/lib_table_platform_sdk" />
    </div>
</div>
```
解决方案：
将合并单元格的代码改为：
```bash
<tr>
    <td style="border:0;">&nbsp;</td>
    <td style="border:0;"><p class="no-table-data">暂无数据</p></td>
    <td style="border:0;">&nbsp;</td>
    <td style="border:0;">&nbsp;</td>
</tr>
```
由于无数据的情况下，“暂无数据”的显示都是相对于表头相同的位置，所以可以考虑使用定位来做。
同时要保证每个td里面都要有内容，所以使用空格符来代替。
添加样式：
```bash
.layui-clear{
  position: relative;
}
.no-table-data{
  position: absolute;
  left:50%; 
  margin-left:-24px;
  top:73px; 
  color: #263248;
  font-size: 12px;
}
```

###### 第二种解决方案
```bash
table{border-collapse: separate;}

这种方法，表格的边框会比较粗。还是不太能解决。
```
思路参考：{% link IE浏览器table中的TD无数据边框不显示问题 https://blog.csdn.net/da_zhuang/article/details/8736662%}

（使用表格的样式设置，解决不了，所以才用了定位的方法。若有更好的方法，可以给我留言。）