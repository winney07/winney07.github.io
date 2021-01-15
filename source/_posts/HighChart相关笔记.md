---
title: HighChart相关笔记
date: 2021-01-15 15:26:30
tags:
- HighChart
categories:
- 工作笔记
- HighChart
---

#### 修改导出excel表表头的表名

1. 默认情况下，标题显示为Chart

   {% asset_img table1.png %}

2. 加上title属性之后，标题显示为title属性的值

   {% asset_img table2.png %}

3. 如果不想标题显示在页面中，就加样式：

   ```
   .highcharts-title{
       display:none;
   }
   ```



#### 修改下载的excel表名

设置title对象的text属性为图表的名称

```
title: {
    text: filename
},
```

若不想表名显示在页面的图表中，可以用样式将它隐藏

```
display：none
```

#### 修改导出后的excel表的第一列的标题Category

1. 第一列的标题默认是Category

   {% asset_img table3.png %}

2. 修改modules 中的export-data.src.js（导出excel表功能的js，未压缩版）

   > 调试可知，dataRows的值决定了标题的显示；而dataRows的值由topHeaders和subHeaders决定，所以动态将它的值修改。

   {% asset_img table4.png %}

3.  给options添加一个excelTitle0属性值

   ```
   topHeaders[0] = this.options.exporting.excelTitle0;
   subHeaders[0] = this.options.exporting.excelTitle0;    
   ```

    {% asset_img table5.png %}

4. 在下载excel表格之前，动态设置excelTitle0属性

    {% asset_img table6.png %}



#### 修改数据表格category值

{% asset_img table7.png %}

{% asset_img table8.png %}

1、给点击按钮加上data-category属性：

{% asset_img table9.png %}

2、重新调用hightcharts修改category属性的方法：

{% asset_img table10.png %}

#### 修改条形图柱子的宽度

```
plotOptions: {
  bar: {
     maxPointWidth: 20
  }
}
```

{% asset_img table11.png %}

#### 在条形图柱子后面加上数值

```
plotOptions: {
  bar: {
     dataLabels: {
     	enabled: true,
     	allowOverlap: true   // 允许数据标签重叠
     }
  }
}
```

{% asset_img table12.png %}



[将Highcharts图表数据生成Table表格](https://blog.csdn.net/wade01274536/article/details/50419114)

[重绘](https://blog.csdn.net/eengel/article/details/73497208)

