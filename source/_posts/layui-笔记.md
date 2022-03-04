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

[layer文档](https://layer.layui.com/api.html)

[layer.comfirm弹窗按钮文字和事件](https://layer.layui.com/api.html#btn)

#### layui表格的复选框全选和单选的功能

1. 表格需要导出的，导出时，要将自定义的复选框去除

2. 
```bash
   { field: 'checkbox', title: '<input type="checkbox" lay-filter="allAccountList" lay-skin="primary">', width: 66 ,templet: function(res){
      return '<input type="checkbox" data-id="'+ res.id +'" lay-filter="accountList" lay-skin="primary">'
   }}
  
```

```bash
// 监听全选复选框
form.on('checkbox(allAccountList)', function(data){
    if(!list.length) {
        $('input[lay-filter="allAccountList"]').prop('checked', false);
    }
    // 是否全选
    var isAll = data.elem.checked ? true : false;

    // 是否被选中
    if(isAll) {
        ids = list.map(function(item){
            return item.id;
        })
    } else {
        ids = [];
    }

    // 更新复选框样式
    $('.layui-table input[type="checkbox"]').prop('checked', isAll);
    // 重新渲染
    form.render('checkbox');
}); 

// 监听单选复选框
form.on('checkbox(accountList)', function(data){
    // 是否被选中
    var isChecked = data.elem.checked;
    // 是否全选
    var isAll = false;
    // 当前项的id
    var _id = $(data.elem).data("id");

    if(isChecked) {
        // 追加
        ids.push(_id);
        isAll = (ids.length == list.length) ? true : false;
    } else {
        // 减去
        var index = ids.indexOf(_id);
        ids.splice(index, 1);

        isAll =  false;
    }

    // 更新全选复选框的样式
    $('input[lay-filter="allAccountList"]').prop('checked', isAll);
    // 重新渲染
    form.render('checkbox');

}); 

```



#### 移动端，点击日期插件不显示

解决方法：加上，trigger: 'click' //采用click弹出

```bash
laydate.render({
elem: '#compareTime' //指定元素
, type: 'date'
, max: endTime
, min: minTime
, trigger: 'click' //采用click弹出
, done: function (value, date, endDate) {
   ....
},
ready: function(date){
   .....
});

```

#### 判断复选框是否选中(获取复选框的值)

```bash
data.elem.checked
```

#### 设置layer-alert和layer-comfirm为不可resize

```bash
将resize参数设置为false
```

#### layui表格固定表头

给表格设置高度

```
table.render({
    elem: '#hourData'
    , data: res
    , height: 330
});
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

例子：

```
// 渲染表格
function table_list(list){
    var cols = getIndexs();
    console.log(cols);
    table.render({
        elem:"#campaigninfo_ table'
        , page: true  // 开启分市
        , id:"campaigninfoTable"
        , title:”推广活动详情"
        , cols: [cols]
        , data: list
    });
};

// 导出按钮
$(".down-file").click(function() {
    var cols = getIndexs();
    var arr = [] ;
    for(var i = 0; i< cols.length; i++) {
        arr.push(cols[i].title);
    }
    // 导出所有数据，所以用返回的全部数据
    table.exportFile("campaigninfoTable", list, 'xls'); // 默认导出csv, 也可以为: xls
})
```

#### 导出excel表格时，去掉页面表头显示的小图标

![去掉导出表格的表头显示的小图标](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/layui-%E7%AC%94%E8%AE%B0/note2.png)

```
var campaigninfoTable;
// 渲染表格
function table_list(list){
    var cols = getIndexs();
    // 不受影响的表头
    var colsold = $.extend(true,[],cols);

    campalgnintoTable = table.render( {
        elem:'#campaigninfo_table'
        , page: true // 开启分页
        , cellMinwidth: 160
        , id: "campaigninfoTable”
        , title: "推广活动详情”
        , cols:[colsold]
        , data: list
        , done: function (res, curr, count) {
            // 表格头部样式处理
            tableHeaderscroll(" #campaigninfo table", count);
            // 分页的显示隐藏
        }
    });
```

```
function downloadTable(tableobj, tableId, data) {
    // 循环表头，将图标去掉(下载表格前，将图标去掉) 
    var colsNew = table0bj.config.cols[0];
    var colsold = $.extend(true,[] , colsNew);
    for (var item in colsNew){
        var title = colsNew [item]['title'];
        if (title.index0f("</span>") > -1) {
            var arr = colsNew[item]['title'].split("</span>");
            colsNew[item]['title'] = arr[1];
        }
    }
    
    // 设置新表头
    table0bj.config.cols[0] = colsNew;
    if (data.length){
        // 导出所有数据，所以用返回的全部数据
        layui.table.exportFile(tableId, data,'xls'); // 默认导出csV,也可以为: xls
        // 设置有图标表头
        table0bi.config.cols[0] = cols0ld;
    }else{
        layer.msg('暂无数据');
    }
});
```

> 点击下载时，将表格的头部图标去掉，执行了下载表格的函数之后，将表头的图标加上。
> 注意：由于表头cols是对象，指向地址，修改了，会影响全局的（例如：点击时间间隔时会拿到去掉图标的表头）
> 解决：（保留原来的不加以修改的表头数据）

#### 修改重载表格时的加载图标

![修改重载表格时的加载图标](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/layui-%E7%AC%94%E8%AE%B0/note5.png)

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

**ie浏览器，layui表格的表头不显示边框**

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

#### 修改开始时间和结束时间之间的符号

方法：修改laydate.js文件里面的t.range = "-"为t.range = "/"

修改layui/lay/modules/laydate.js：

```
(t.range === !0 && (t.range = '/'))   改为： (t.range === !0 && (t.range = '-')) 
```



#### laytui表格内容超过表格长度的处理

当表格单元格的文字的长度超过表格当前列的宽度时，点击单元格的内容，会出现如图问题：

![当表格单元格的文字的长度超过表格当前列的宽度时](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/layui-%E7%AC%94%E8%AE%B0/note7.png)

解决方法(使用css样式控制它隐藏)：

```
.layui-table-tips-main{display:none}
.layui-table-tips-c{display:none}
```

https://www.cnblogs.com/pyspang/p/11164736.html

https://www.cnblogs.com/xxzb/p/12618226.html



layui分页插件，一直在调用方法的解决办法

（死循环）

由于每次加载时都会执行jump回调，所以初次不让它执行jump里的方法（!first）

```
laypage.render({
    elem: 'demo8'
    , count: totalCount
    , layout: ['count', 'prev', 'page', 'next', 'limit', 'refresh', 'skip']
    , jump: function (obj, first) {
        //模拟渲染
        page = obj.curr;
        limit = obj.limit;
        if (!first) {
             //执行方法
        }
    }
});
```

#### [requriejs加载layui](https://blog.csdn.net/radzhang/article/details/84927005)

#### 渲染动态表头

```
var dynamicCols = [];     //用来存放动态表头
var colsList = [];  //表头列表
$(数据返回的表头数组).each(function (i, item) {
    //设置表头
    var info = { field: item.field, title: item.title };
    colsList.push(info);
}
dynamicCols.push(colsList);

//执行渲染
table.render({
    elem: "#demo"  //指定原始表格元素选择器（推荐id选择器）
    ,height: 315   //容器高度
    ,cols:dynamicCols     //设置表头
    
    //,.....       //其他参数
});
```

#### 动态修改layui的select框的值

例如：点击表格的编辑按钮，获取当前行数据，根据不同的系统名称，在弹出的弹窗中，将系统选中

```
<form class="layui-form" lay-filter="whitelistForm">
	<input type="text" name="whiteKey" placeholder="搜索设备名" autocomplete="off" class="layui-input">
</form>

// 点击表格的编辑按钮
....
else if(obj.event === 'edit') {
	var dataValue = data.system === 'iOS' ? '1' : '2';
	
	// 方法一或方法二的代码
}
.....
```

1. 方法一：

   ```
   form.val('whitelistForm', {'whiteKey': dataVale});
   ```

2. 方法二：

   ```
   // 首先需要使用lay-value来确定需要设置哪个元素自动选择
   var select = 'dd [ lay-value=' +data.id + ']';
   // 触发点击事件，实现自动选择
   $("input[ name='system']").siblings("div.layui-form-select").find('dl').find(select).click();
   ```

#### layui日期时间段的设置，开始时间-结束时间

最小值最大值动态设置的问题

```
/* ----日期初始化-开始---- */
$("#baseTime").val(today);
$("#compareTime").val(adDate.getDate(-1)); // 前一天
// 基础日期
laydate.render({
    elem: '#baseTime' 
    , type: 'date'
    , min: minTime
    , max: today
    , trigger: 'click' // 采用click弹出
    , done: function (value, date, endDate) {
      ......
    }
});

// 对比日期
laydate.render({
    elem: '#compareTime' 
    , type: 'date'
    , min: minTime
    , max: today
    , trigger: 'click' // 采用click弹出
    , done: function (value, date, endDate) {
        .....
    },
    ready: function(date){
        var y = date.year
            , m = date.month 
            , d = date.date; 

        m = (m < 10) ? '0' + m : m; 
        d = (d < 10) ? '0' + d : d;

        // 获取输入框上一次的日期
        compareTime =  y + '-' + m + '-' + d; 
    }
});
```

```
var today = adDate.getDate(0);	// 今日(封装的一个方法)
// 激活时间段日期选择 
var activeTime = laydate.render({
    elem: '#actRange'  
    , type: 'date'
    , range: true
    , max: today		// 最大值为今天
    , trigger: 'click' 	// 采用click弹出
    , done: function (value, date, endDate) {
        // 设置付费时间段最小日期
        payRange.config.min = {
            year:date.year,
            month:date.month - 1,
            date:date.date
        }
       ......
    }
});
// 付费时间段选择
var payRange = laydate.render({
    elem: '#payRange' 
    , type: 'date'
    , range: true
    , min: today
    , max: today
    , trigger: 'click' // 采用click弹出
    , done: function (value, date, endDate) {
        .....
    }
});
```



#### 动态修改复选框的选中状态

```
if ($('.xxxx').attr("checked") === "checked") { //判断是否选中
     //设置选中 注意这里使用的是prop(), 这里要是使用了attr()是无效的
    $('.xxxx').prop("checked", true);
} else {
    $('.xxxx').prop("checked", false);
}
form.render(); //重新渲染       ————————最重要的记得加上这句话---------
```

#### [获取数据表格选中值](https://www.layui.com/doc/modules/table.html#method)

```
<table id="activity-manage" lay-filter="packageList"></table>


var activityManage = table.render({
    elem: '#activity-manage'
    , id: "activityManage"
    , cellMinWidth: 130
    .....
    
});


//监听数据表格的复选框
table.on('checkbox(packageList)', function (obj) { 
    console.log(obj.type); //如果触发的是全选，则为：all，如果触发的是单选，则为：one
    console.log(obj);  // 这里的data数据只针对当前选中的那一项

    // 选择状态 (activityManage是config里面的id)
    var checkStatus = table.checkStatus("activityManage");
    console.log(checkStatus.data) //获取选中行的数据
    console.log(checkStatus.data.length) //获取选中行数量，可作为是否有选中行的条件
    console.log(checkStatus.isAll ) //表格是否全选
    console.log(checkStatus);    // 这里的data，是当前已选中的所有数据的数组集合
    .........
    
});
```

#### 动态设置下拉框的值

```
//设置下拉框默认选项
form.val("deviceManage", {
    "os": 2
});
<form class="layui-form  margin-t10" action="" lay-filter="deviceManage" id="white_device">
    <select name="os" lay-filter="os">
        <option value="1">iOS</option>
        <option value="2" selected>Android</option>
    </select>
</form>
```

#### 提示信息弹完再做其他操作（处理新增/编辑页面跳转这种情况）

```
layer.msg(res.msg, {time: 1000}, function() {
    // 可点击
    $("#submitBtn").removeAttr("disabled");

    if ( res.code == 1 ){
        $.form.href("{:url('xy/account/role')}");
    }
});
```

#### 动态修改单选框的值

```
$('input[name="isDiscount"][value="0"]').prop('checked', true);
form.render("radio");

// 需要用到prop('checked', true);
```

```
form.val("addpackage", {
    "isDiscount": 0
});
```

[xmSelect下拉多选](https://fly.layui.com/extend/xmSelect/)

[xm-select文档](https://maplemei.gitee.io/xm-select/#/component/install)

#### 接口处理完，弹出提示，提示语结束才跳转页面

```
layer.msg(res.msg, {time: 1000}, function(){
    // 成功-页面跳转
    if(res.code == 1) {
        $.form.href("{:url('xy/account/index')}");
    }
});
```

#### layui获取已选复选框的值

```
var arr_box = [];
$('input[type=checkbox]:checked').each(function() {
  arr_box.push($(this).val());
});
```

#### 初始化表格渲染条数

```
table.init('data-detail', {
    limit: 10 //注意：请务必确保 limit 参数（默认：10）是与你服务端限定的数据条数一致
    //支持所有基础参数
});
```



#### 获取表单提交的数据

```
<button href="javascript:;" class="layui-btn layui-btn-normal" lay-submit lay-filter="setAuthority">保存</button>

form.on('submit(setAuthority)', function(data){
	var param = data.field;
	......
});
```

注：对应的提交按钮，要添加  lay-submit  属性

#### Tab的切换功能，切换事件监听等，需要依赖element模块

```
layui.use(['element'], function () {
    var element = layui.element;
});
```

#### 防止表单多次提交

```
// 设置提交按钮不可点击
$("#submitBtn").attr("disabled", true);

$("#submitBtn").removeAttr("disabled");
```



```
// 监听保存按钮
form.on('submit(save)', function(data){
    var params = data.field;

    // 设置提交按钮不可点击
    $("#submitBtn").attr("disabled", true);

    // 请求接口处理
    $.post('/xy/account/roleAdd', params, function(res){
        layer.msg(res.msg, {time: 1000}, function() {
            // 可点击
            $("#submitBtn").removeAttr("disabled");

            if ( res.code == 1 ){
                $.form.href("{:url('xy/account/role')}");
            }
        });
        return false;
    });

    return false;
});
```

#### layui表格合并行

```
// 表格合并行
function merge(res, names, indexs) {
    var data = res.data;
    //定位需要添加合并属性的行数
    var mergeIndex = 0;
    //这里涉及到简单的运算，mark是计算每次需要合并的格子数
    var mark = 1; 
    //需要合并的列名称
    var columsName = names;
    //需要合并的列索引值
    var columsIndex = indexs;

    //这里循环所有要合并的列
    for (var k = 0; k < columsName.length; k++) { 
        //所有行
        var trArr = $(".layui-table-body>.layui-table").find("tr");
        //这里循环表格当前的数据
        for (var i = 1; i < res.data.length; i++) { 
            //获取当前行的当前列
                var tdCurArr = trArr.eq(i).find("td").eq(columsIndex[k]);
                //获取相同列的第一列
                var tdPreArr = trArr.eq(mergeIndex).find("td").eq(columsIndex[k]);
            //后一行的值与前一行的值做比较，相同就需要合并
                if (data[i][columsName[k]] === data[i-1][columsName[k]]) { 
                        mark += 1;
                        //相同列的第一列增加rowspan属性
                        tdPreArr.each(function () {
                                $(this).attr("rowspan", mark);
                        });
                        //当前行隐藏
                        tdCurArr.each(function () {
                                $(this).css("display", "none");
                        });
                }else {
                        mergeIndex = i;
                        //一旦前后两行的值不一样了，那么需要合并的格子数mark就需要重新计算
                        mark = 1;
                }
        }
        mergeIndex = 0;
        mark = 1;
    }
}
```

#### layui-layer 遮罩

[弹出层区域默认自带0.3透明度的黑色背景蒙层](https://www.layui.site/doc/modules/layer.html#shade)

[layer.load(icon, options) - 加载层](https://www.layui.site/doc/modules/layer.html#shade)

```
//eg1
var index = layer.load();
//eg2
var index = layer.load(1); //换了种风格
//eg3
var index = layer.load(2, {time: 10*1000}); //又换了种风格，并且设定最长等待10秒 
//关闭
layer.close(index);  
```

#### [layui 时间插件laydate中动态设置改变min和max值](https://blog.csdn.net/bai_riqiang/article/details/80110000)

```
layui.use('laydate', function(){
  var laydate = layui.laydate;

  // 开始日期
  var startDate = laydate.render({
    elem: '#startDate'
    ,max : "2099-12-31"
    ,done: function(value,date){
      endDate.config.min ={
        year :date.year
        ,month: date.month-1
        ,date: date.date
      };
      // 可不加，根据需求来
      $('#endDate')[0].focus();
    }
  });
  // 结束日期
  var endDate = laydate.render({
    elem: '#endDate '
    ,min: "1900-1-1"
    ,done: function (value,date) {
      startDate.config.max={
        year :date.year
        ,month: date.month-1
        ,date: date.date
      }
    }
  });
});
```

#### 如果想去掉表单中所有输入框的浏览器历史记录

直接给form元素加上autocomplete="off"

```
<form autocomplete="off"></form>
```

#### layer弹两次

```
// 加上id-处理提示弹两次
layer.msg('复制成功', {id: 'clipboard', time: 1000});
```

[layui表格没有数据的时候，表头没有横向滚动条](https://gitee.com/sentsin/layui/issues/I2C2CT)

```
修改一下table.js源码
that.layMain.find('tbody').html('');
that.layHeader.css('overflow','auto');//新加的
```

[Layui数据表格显示无数据提示问题](https://blog.csdn.net/nuomizhende45/article/details/90108766)



#### layui-排序功能

如果不使用layui本身的前端排序功能，需禁止：

```
,autoSort: false // 禁用前端自动排序
```

更新全部表单元素：

```
form.render(); 
```



#### 扩展一个模板

```
 /**扩展一个模块**/      
layui.define(function(exports){ 
  var obj = {
    hello: function(str){
      alert('Hello '+ (str||'mymod'));
    },

  };

  // 输出接口
  exports('mymod', obj);
});


layui.extend({
  mod2: 'http://192.168.0.59/mymod/' // {/}的意思即代表采用自有路径，即不跟随 base 路径
});

// 使用拓展模块
layui.use(['mymod'], function(){
  var mymod = layui.mymod;

  mymod.hello('World!'); //弹出 Hello World!
});
```

