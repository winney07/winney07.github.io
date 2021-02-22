---
title: layui 笔记
date: 2020-06-24 15:41:32
tags:
- layui
categories: 
- 工作笔记
- layui
---

[layui-github](https://github.com/sentsin/layui)

#### 判断复选框是否选中(获取复选框的值)

```
data.elem.checked
```

#### 设置layer-alert和layer-comfirm为不可resize

```
将resize参数设置为false
```

#### 导出excel表格

```
var ins1 = table.render ({
	elem: '#demo '
	,id: 'test'
	...
})
// 将上述表格示例导出为csv文件
table.exportFile(ins1.config.id，data) ; // data为该实例中的任意数量的数据
```

{% asset_img note1.png %}

#### 导出excel表格时，去掉页面表头显示的小图标

{% asset_img note2.png %}

{% asset_img note3.png %}

{% asset_img note4.png %}

> 点击下载时，将表格的头部图标去掉，执行了下载表格的函数之后，将表头的图标加上。
> 注意：由于表头cols是对象，指向地址，修改了，会影响全局的（例如：点击时间间隔时会拿到去掉图标的表头）
> 解决：（保留原来的不加以修改的表头数据）

#### 修改重载表格时的加载图标

{% asset_img note5.png %}

- 如果只修改样式

  ```
  .layui-table-view .layui-table-init .layui-icon-loading{
    	font-size: 60px;
    	color: #666;
  }
  ```

- 如果不想页面显示表格加载图标

  ```
  .layui-table-view .layui-table-init .layui-icon-loading{
      display: none !important;
  }
  ```



#### 表格表头标题之间边框不显示

{% asset_img note6.png %}

th本来是position：relative；改为position: static；

```
.layui-table td, .layui-table th{
    position: static\9;
}
```

#### 修改了layui表格的内容，不刷新页面，只刷新表格内容，页码不刷新解决方法

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
#### layui同时清空多个表单元素的值
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

#### 将MD5定义成layui的模块

[扩展一个 layui 模块](https://www.layui.com/doc/base/modules.html#extend)

1、在md5的js文件最后加上：

```
layui.define(function(exports){ 
  exports('mymd', {});
});
```

2、如果mymd.js文件放在与使用它的html文件同一个目录下，在html文件中直接使用：

```
//使用拓展模块
layui.use(['mymd'], function(){
  var mymd = layui.mymd;

  mymd.hash = md5;   //md5加密方法
  console.log(mymd.hash("md5加密"));
});
```

3、如果mymd.js文件放在与使用它的html文件不同目录下，在html文件中要在 extend 指定路径：

```
layui.extend({
  mymd: './js/mymd' 
})
```

再使用：

```
//使用拓展模块
layui.use(['mymd'], function(){
  var mymd = layui.mymd;

  mymd.hash = md5;   //md5加密方法
  console.log(mymd.hash("md5加密"));
});
```

#### laypage

```
layui.use(['laypage', 'layer'], function(){
  var laypage = layui.laypage
  ,layer = layui.layer;
  
  //完整功能
  laypage.render({
    elem: 'demo7'
    ,count: 100
    ,layout: ['count', 'prev', 'page', 'next', 'limit', 'skip']
    ,jump: function(obj){
      console.log(obj)
    }
  });
  
});
```

#### layui日期时间段的设置，开始时间-结束时间

```
var nowTime = new Date( ).valueOf( );

var start = laydate.render({
	elem: "#start",
	min: nowTime,
	done: function(value, date) {
		endMax = end.config.max;
		end.config.min = date;     // 根据开始时间来设置结束时间的最小值/最大值
		end.config.min.month = date.month - 1;
	}
})

var end = laydate.render({
	elem: "#end",
	min：nowTime,   //  结束时间初始化的时候要设置一个值，不然开始时间的回调中，设置了也不起作用。初始化的时候就要写上nowTime这个，不然动态控制不了
	done: function(value, date) {
		
	}
})
```

#### laytui表格内容超过表格长度的处理

当表格内容的文字长度超过表格的长度的时候，点击内容，会出现如图：

{% asset_img note7.png %}

解决方法：

```
.layui-table-tips-main{display:none}
.layui-table-tips-c{display:none}
```

