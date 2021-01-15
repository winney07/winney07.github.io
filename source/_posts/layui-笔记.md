---
title: layui 笔记
date: 2020-06-24 15:41:32
tags:
- layui
categories: 
- 工作笔记
- layui
---

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