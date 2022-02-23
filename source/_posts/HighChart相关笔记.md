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

   ![标题显示为Chart](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/HighChart%E7%9B%B8%E5%85%B3%E7%AC%94%E8%AE%B0/table1.png)

2. 加上title属性之后，标题显示为title属性的值

   ![标题显示为title属性的值](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/HighChart%E7%9B%B8%E5%85%B3%E7%AC%94%E8%AE%B0/table2.png)

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

   ![ 第一列的标题默认是Category](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/HighChart%E7%9B%B8%E5%85%B3%E7%AC%94%E8%AE%B0/table3.png)

2. 修改modules 中的export-data.src.js（导出excel表功能的js，未压缩版）

   > 调试可知，dataRows的值决定了标题的显示；而dataRows的值由topHeaders和subHeaders决定，所以动态将它的值修改。

   ![修改modules 中的export-data.src.js](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/HighChart%E7%9B%B8%E5%85%B3%E7%AC%94%E8%AE%B0/table4.png)

3. 给options添加一个excelTitle0属性值

   ```
   topHeaders[0] = this.options.exporting.excelTitle0;
   subHeaders[0] = this.options.exporting.excelTitle0;    
   ```

   ```
   // Find longest row
   for (var i = 0, len = rows.length; i < len; ++i) {
   	if (rows[i].length > rowLength) {
   		rowLength = rows[i].length;
   	}
   }
   topHeaders[0] = this.options.exporting.excelTitle0;
   subHeaders[0] = this.options.exporting.excelTitle0;
   // Add header
   html += getTableHeaderHTML(
   	topHeaders ,
   	subHeaders ,
   	Math.max(rowLength, subHeaders.length)
   );
   ```

4. 在下载excel表格之前，动态设置excelTitle0属性

    ```
    function getCategory() {
    	var category = $(this).data("category");
    	if(category == "" || category == undefined){
    		var val = $("#dateRange").val();
    		var start = val.substring(0, 10);
    		var end = val.substring(13, 24);
            // 算两个日期之间的间隔
            var inter = getDays(start, end);
    
            if(inter = 0) {
                category = "小时";
            } else {
                category = "日期";
            }
         }
        return category;
    }
    
    
    Highcharts.charts[chartId].options.exporting.excelTitle0 = getCategory.call(this);
    ```



#### 修改数据表格category值

![修改数据表格category值](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/HighChart%E7%9B%B8%E5%85%B3%E7%AC%94%E8%AE%B0/table7.png)

![修改数据表格category值](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/HighChart%E7%9B%B8%E5%85%B3%E7%AC%94%E8%AE%B0/table8.png)

1、给点击按钮加上data-category属性：

```
<div class="eptWrap rc" data-chart="Ø" data-category="渠道">
    <span class= "eptList" ></span>
</div>
<div class"eptwrap ml10 down-file" data-chart="0" data-category="渠道">
    <span class="eptout"></span>
</div>
```

2、重新调用hightcharts修改category属性的方法：

```
function getCategory() {
	var category = $(this).data("category");
	if(category == "" || category == undefined){
		var val = $("#dateRange").val();
		var start = val.substring(0, 10);
		var end = val.substring(13, 24);
        // 算两个日期之间的间隔
        var inter = getDays(start, end);

        if(inter = 0) {
            category = "小时";
        } else {
            category = "日期";
        }
     }
    return category;
}


Highcharts.charts[chartId].options.exporting.excelTitle0 = getCategory.call(this);
```

#### 修改条形图柱子的宽度

```
plotOptions: {
  bar: {
     maxPointWidth: 20
  }
}
```

![修改条形图柱子的宽度](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/HighChart%E7%9B%B8%E5%85%B3%E7%AC%94%E8%AE%B0/table11.png)

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

![在条形图柱子后面加上数值](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/HighChart%E7%9B%B8%E5%85%B3%E7%AC%94%E8%AE%B0/table12.png)



[将Highcharts图表数据生成Table表格](https://blog.csdn.net/wade01274536/article/details/50419114)

[重绘](https://blog.csdn.net/eengel/article/details/73497208)

