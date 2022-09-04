---
title: Bootstrap相关笔记
date: 2018-08-18 11:04:21
tags:
- Bootstrap
- 工作笔记
---





#### Bootstrap3与Bootstrap4的区别

| Bootstrap3               | Bootstrap4                                       |
| ------------------------ | ------------------------------------------------ |
| Less                     | Sass                                             |
| 4种栅格类                | 5种栅格类                                        |
| 使用px为单位             | 使用rem和em为单位（除部分margin和padding使用px） |
| 使用push和pull向左右移动 | 偏移列通过offset-类设置                          |
| 使用float的布局方式      | 选择弹性盒模型(flexbox)                          |

- Bootstrap4中的栅格系统可以不用添加指定的列数 如row 里面有2个col 会任何尺寸下均分row
- Bootstrap3只有4种栅格类 分别为（col-xs特小，col-sm小,col-md,中col-lg大）
- Bootstrap4有5种栅格类，（col-特小，col-sm-小，col-md-中，col-lg-大，col-xl-超大）
- Bootstrap4设置列偏移时通过 offset-sm-4,而Bootstrap3通过col-sm-offset-4
- Bootstrap4增加了响应式容器如 container-sm ,container-md….,当小于屏幕尺寸小于栅格类时会占满整个屏幕



#### [Bootstrap4与Bootstrap5之间的区别](https://www.imangodoc.com/120811.html)

Bootstrap5删除的一些类是：

- 表格-行
- 表格-内联
- 清单-内联
- 卡-甲板

一些添加的类：

- gx-*(类控制水平/列装订线的宽度)
- gy-*(类控制垂直/行装订线的宽度)
- g-*(类控制水平和垂直装订线的宽度)
- 行cols自动



#### [日期插件](https://getdatepicker.com/4/)

[文档](https://bootstrap-datepicker.readthedocs.io/en/stable/)

[demo](https://uxsolutions.github.io/bootstrap-datepicker/?markup=input&format=&weekStart=&startDate=&endDate=&startView=0&minViewMode=0&maxViewMode=4&todayBtn=false&clearBtn=false&language=en&orientation=auto&multidate=&multidateSeparator=&keyboardNavigation=on&forceParse=on#sandbox)

[github](https://github.com/uxsolutions/bootstrap-datepicker)——存在安全缺陷组件的影响

[CDN](https://www.bootcdn.cn/bootstrap-datetimepicker/)

[示例](https://www.eyecon.ro/bootstrap-datepicker/)

```
<!-- bootstrap样式表 -->
<link href="https://cdn.bootcss.com/bootstrap/3.3.7/css/bootstrap.min.css" rel="stylesheet">

<!-- 时间选择器样式表 -->
<link href="https://cdn.bootcss.com/bootstrap-datetimepicker/4.17.47/css/bootstrap-datetimepicker.min.css" rel="stylesheet">


<!-- jquery -->
<script src="https://cdn.bootcss.com/jquery/3.3.1/jquery.min.js"></script>

<!-- bootstrap脚本 -->
<script src="https://cdn.bootcss.com/bootstrap/3.3.7/js/bootstrap.min.js"></script>

<!-- 时间选择器前置脚本 -->
<script src="https://cdn.bootcss.com/moment.js/2.22.1/moment-with-locales.min.js"></script>

<!-- 时间选择器核心脚本 -->
<script src="https://cdn.bootcss.com/bootstrap-datetimepicker/4.17.47/js/bootstrap-datetimepicker.min.js"></script>
```

#### [Bootstrap Table](https://bootstrap-table.com/)

[bootstrapTable的使用及表格的导出](https://blog.csdn.net/Mr_XiMu/article/details/106059687)