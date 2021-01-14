---
title: 前端CSS问题
date: 2020-06-30 17:35:17
tags:
- css问题
categories: 
- 工作笔记
- css问题
---
### iPhone Safari浏览器字体放大 ——解决方法
```
text-size-adjust: 100%;
-webkit-text-size-adjust: 100%;
```
{% asset_img css1.png %}

### 表格中内容超出指定宽度隐藏，鼠标上移，在指定宽度内换行显示。（不需要js，css的hover解决）

##### 需要在td里面加上span等标签来限制宽度和溢出隐藏
```
table{
    margin: 0 auto;
    width: 30%;
    border: 1px solid #666;
    text-align: center;
    border-collapse:collapse;
}
th{
    height:40px;
    line-height: 40px;
}
td{
    height: 40px;
    line-height: 40px;
}
tr{
    border-bottom: 1px solid #666;
}

td span {
    display: inline-block;
    width:160px;
    white-space: nowrap;
    text-overflow: ellipsis;
    overflow: hidden;
    vertical-align: middle;
}
td span:hover {
    white-space: inherit;
    text-overflow: inherit;
    overflow: visible;
}


<table border="1">
    <th>姓名</th>
    <th>年龄</th>
    <th>简介</th>
    <tr>
        <td>羊羊羊</td>
        <td>25</td>
        <td >
            <span>
                79942 79942 79942 79942 79942 79942 79942 79942 79942 79942 79942 79942
            </span>
        </td>
    </tr>
</table>
```
##### 溢出隐藏：
{% asset_img css2.png %}
##### 鼠标上移，换行显示全部内容：
{% asset_img css3.png %}

### css3超出宽度自动换行以及超出宽度显示...
#### css3超出宽度自动换行，并且首行缩进2字符
```
div{
    text-indent: 2em;
    word-wrap: break-word;
    word-break: break-all;
}
```
#### 单行超出宽度显示...
```
div {
    text-overflow: ellipsis;
    white-space: nowrap;
    overflow: hidden;
}
```
#### 多行超出宽度显示...以及要求显示几行或者说根据文字多少显示几行
```
div {
    overflow: hidden;
    text-overflow: ellipsis;
    display: -webkit-box;
    -webkit-line-clamp: 2;  //控制显示几行
    -webkit-box-orient: vertical;   //webbox方向
}
```
#### CSS3强制英文、中文换行与不换行 强制英文换行
```
1. word-break:break-all;只对英文起作用，以字母作为换行依据
2. word-wrap:break-word; 只对英文起作用，以单词作为换行依据
3. white-space:pre-wrap; 只对中文起作用，强制换行
4. white-space:nowrap; 强制不换行，都起作用 
5. white-space:nowrap; overflow:hidden; text-overflow:ellipsis;不换行，超出部分隐藏且以省略号形式出现（部分浏览器支持）
```

#### input输入框禁止显示历史记录 
在输入input时会提示原来输入过的内容，还会出现下拉的历史记录，禁止这种情况只需在input中加入：
autocomplete="off"
```
<input type="text"  autocomplete="off" />
```
[参考博客](https://blog.csdn.net/amao_aguai/article/details/83344455)

#### 浏览器记住密码的情况下，解决密码输入框自动填充密码框（input type="password" 的问题）
```
用户名：<input type='text' autocomplete='off'>
密码：<input type='password' autocomplete="new-password" style="background-color: #fff!important;" readonly onfocus="this.removeAttribute('readonly');" onblur="this.setAttribute('readonly',true);">

```
