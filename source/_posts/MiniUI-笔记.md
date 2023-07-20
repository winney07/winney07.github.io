---
title: MiniUI-笔记
date: 2019-08-16 14:50:14
tags:
- MiniUI
categories: 
- 前端UI框架
- MiniUI
---

[MiniUI官网](http://www.miniui.com/)

#### 表单初始化

```
 <form id="fa" name="fa" autocomplete="off"></form>

function init(){
	mini.parse();
	form = new mini.Form("fa");	
}
jQuery(document).ready(function() {
	init();
});
```

#### 表格

是否显示分页：`showPager="true"`

分页显示条数：`pageSize="20"`

```
<div id="datagrid1" class="mini-datagrid" style="width:100%;height:100%;" url="{:U('')}"  idField="id" showPager="true" pageSize="20">
    <div property="columns">

        <div field="created_at" width="120" headerAlign="center" align="center" allowSort="false">申请时间</div>
        <div field="real_name" width="100" headerAlign="center" align="center" allowSort="false">申请人（代理）</div>
        <div field="name" width="200" headerAlign="center" align="center" allowSort="false">公司名称</div>
        <div field="money" width="100" headerAlign="center" align="center" allowSort="false">当次申请金额</div>
        <div field="pledge" width="100" headerAlign="center" align="center" allowSort="false">当次押金</div>
        <div field="agency_status_name" width="60" headerAlign="center" align="center" allowSort="false" renderer="onActionRenderer_agency_status_name">申请人状态</div>
        <div field="remit_time" width="120" headerAlign="center" align="center" allowSort="false">打款时间</div>
        <div field="remit_type_name" width="120" headerAlign="center" align="center" allowSort="false">打款方式</div>
        <div field="status_name" width="60" headerAlign="center" align="center" allowSort="false" renderer="onActionRenderer_status_name">打款状态</div>
        <div field="" width="100" headerAlign="center" align="center" allowSort="false" renderer="onActionRenderer">操作</div>

    </div>
</div>
```





#### 输入框提示语-类似placeholder

```
emptyText="请输入区服"
```

#### 表单元素必填及提示语

```
required="true"
requiredErrorText="区服不能为空"
```

#### 表单验证

1. ##### 自带验证方法

```
<a class="mini-button submit-button"onclick="SubmitData();">提交</a>  
```

```
// 提交事件
function SubmitData() 
{
	form.validate();   // 框架自带验证表单的方法
	if (form.isValid() == false) return false;   
	
	....// 其他代码
}
```

```
<input  
class="mini-textbox" 
name="server_id"  
required="true" 
requiredErrorText="区服不能为空" 
value=""
style="width:200px;" 
emptyText="请输入区服" />
```

2. ##### 自定义验证

```
function SubmitData() {
    var form_validate = true;

    // 错误信息内容
    var errorMsg = ["提示：区间比例必须连续！", "提示：区间范围错误！", "提示：区间比例必须在0-100以内！", "提示：区间必须输入0及正整数！", "提示：区间比例必须输入0及正整数！", "提示：请完整填写区间！", "提示：请填写区间比例！"];
    //错误提示函数
    function showError(msg, el) {
        var errorIcon = '<span class="mini-errorIcon" title="' + msg + '"></span>';
        var hasError = el.find(".mini-errorIcon").length;
        if(hasError != 1) {
            el.append(errorIcon);
        }
    }

	.......
    if(end_val != "" || percent_val != "") {
        showError(errorMsg[5], $(this));
        form_validate = false;
    }
    
    if(form_validate == false) {
		return false;
	}
		
	$.post("{:U('')}", $("form").serialize(), function(response) {
		if (response.success)
		{
			window.location.href = "{:U('index')}";
		} else {
			alert(response.msg);
		}
	},"json");
}
```



#### [表单验证规则总结](http://www.miniui.com/demo/form/rules.html)

#### miniui 结束日期不能小于起始日期

```
1.HTML代码：

<tr>
　　<th class="nui-form-label" style="width:15%;"><label for="report.startDate$text" >起始日期：</label></th>
　　<td style="width:35%;" >
　　<input id="report.startDate" class="nui-datepicker" style="width: 95%;" name="report.startDate" required="true"/>
　　</td>


　　<th class="nui-form-label" style="width:15%;"><label for="report.productCode$text">结束日期：</label></th>
　　<td style="width:35%;">
　　<input id="report.endDate" class="nui-datepicker" name="report.endDate" style="width: 95%;" required="true" onvaluechanged="onValueChanged"/>
　　</td>
</tr>

 

2.JS代码：

function onValueChanged(e){
　　var startDate = mini.get("report.startDate").getFormValue();
　　var endDate = e.value;
　　if(startDate!=""){
	　　startDate=startDate.substring(0,4) + startDate.substring(5,7) + startDate.substring(8,10);
	}
　　if(endDate!=""){
	　　endDate=endDate.substring(0,4) + endDate.substring(5,7) + endDate.substring(8,10);
	}
　　if(startDate>endDate){
	　　e.isValid=false;
		mini.alert(error);
		mini.get(end).setValue("");
　　}
}
```

#### 日期插件-加上时分秒

```
format="yyyy-MM-dd H:mm:ss"  showTime="true"
```

#### 文件上传按钮

```
<input class="mini-htmlfile" id="license" name="license" buttonText="浏览文件" limitType="*.bmp;*.gif;*.png;*.jpg;*.jpeg" required="true" style="width:250px;" onfileselect="fileChange(this)"/>
```

```
var inputFile = $("input:file").filter(":visible");
$.ajaxFileUpload({
    url: "{:U('')}",
    secureuri: false,
    fileElementId: inputFile,
    dataType: "json",
    data: data,
    success: function (response, status) {
        if (response.success){
            window.location.href = "{:U('index')}";
        } else if(response.msg.file_errors) {
            var obj = response.msg.file_errors;
            .....

        }else if(response.msg.status_error) {
           .....
        } else{
            alert(response.msg);
        }
    },
    complete: function () {
        $("#fa input:file").filter(":visible").each(function(i, e){
            e.replaceWith(inputFile[i]);
        });
    }
});
```

#### 文件上传-按钮的文字

```
buttonText="浏览文件"
```

#### 文件上传-文件类型限制

```
limitType="*.bmp;*.gif;*.png;*.jpg;*.jpeg"
```

#### 文件上传-上传时的自定义验证

```
<input class="mini-htmlfile" id="package_file" name="package_file" buttonText="浏览..." limitType="*.apk;*.ipa" onvalidation="fileValidation" style="width:250px;" />

function fileValidation(e) {
	if (e.value != '' && e.isValid) {
		var fileName = getFileName(e.value);
		var platform = $("input[name='type']:checked").val();

		var uPattern = /^[a-z0-9A-Z._]+$/;
		if(! uPattern.test(fileName)) {
			e.errorText = '母包文件名只能包含字母、数字、下横线"_"、点"."';
			e.isValid = false;
		}

		var arr = fileName.split(".");
		if(platform == 1 && arr[arr.length-1] != "apk") {
			e.errorText = '上传文件格式为：*.apk';
			e.isValid = false;
		}
		if(platform == 2 && arr[arr.length-1] != "ipa") {
			e.errorText = '上传文件格式为：*.ipa';
			e.isValid = false;
		}

	}
}
```

#### 获取表单数据

```
var data = form.getData(true);
```

```
function SubmitData() 
{
	form.validate();
	if (form.isValid() == false) return false;

	var data= form.getData(true);
	$.post("{:U('')}", data, function(response) {
		if (response.success)
		{
			alert(response.msg);
			form.reset();
		} else {
            alert(response.msg);
        }
	},"json");
}
```

#### 重置表单

```
form.reset();
```



#### 传多个数据

name值使用`[]`

```
<input name="start[]"/>
```

#### 渲染表格数据-grid.load(data);

```
<div id="datagrid1" class="mini-datagrid" style="width:100%;height:100%;" url="{:U('')}"  idField="id" showPager="true" pageSize="20">
    <div property="columns">
        <div field="money" width="150" headerAlign="center" align="center" allowSort="false">退款金额</div>
        <div field="time" width="150" headerAlign="center" align="center" allowSort="false">退款时间</div>
    </div>
</div>

function init()
{
    mini.parse();
    grid = mini.get("datagrid1");
    var form = new mini.Form("#fs");  
    var data = form.getData(true);
    
    data.agency_id = {$agency_id};
    
    grid.load(data);
}

```

#### 文本编辑器

`kindeditor`

```
var editor;
KindEditor.ready(function(K) {
	editor = K.create('textarea[name="content"]', {
		resizeType : 1,
		allowPreviewEmoticons : false,
		allowImageUpload : false,
		items : [
			'source', 'fontsize', '|', 'forecolor', 'hilitecolor', 'bold', 'italic', 'underline',
			'removeformat', '|', 'justifyleft', 'justifycenter', 'justifyright', 'insertorderedlist',
			'insertunorderedlist', '|', 'link']
	});

    // 安卓手机兼容性处理(KindEditor在移动端默认显示源码模式)
    var u = navigator.userAgent;
    var isAndroid = u.indexOf('Android') > -1 || u.indexOf('Adr') > -1;
    if(isAndroid) {
        $(".ke-outline[data-name='source']").click();
    }
});
```

#### alert弹窗

```
 mini.alert(result.msg);
```

#### 复选框-全选

```
<div id="all_apps" class="mini-checkbox" readOnly="false" text="全选" onvaluechanged="onValueChangedAll"></div>
<ul class="checkbox-list w60">
    <foreach name="app_list" item="item">
        <li title="{$item.app_name}">
            <div onValueChanged="onValueChanged" id="app_check{$item.app_id}" name="app_id[]" trueValue="{$item.app_id}" class="mini-checkbox app-check" text="{$item.app_name}" checked="<if condition="in_array($item['app_id'], $user_own_app)">true<else />false</if>"></div>
        </li>
    </foreach>
</ul>
```

```
//初始化全选
isCheckAll();
//判断是否全选
function isCheckAll(){
    var num = 0;
	for(var i = 0; i < id_list.length; i++) {
		var obj = mini.get(id_list[i]).checked;
		if(obj == true) {
			num +=1;
		}
	}
	//是否全选
	if(num == id_list.length){
		mini.get("all_apps").setChecked(true);
	} else {
		mini.get("all_apps").setChecked(false);
	}
}

//选某个游戏
function onValueChanged(e) {
    isCheckAll();
}
//全选按钮
function onValueChangedAll(e) {
	var checked = this.getChecked();

	for(var i = 0; i < id_list.length; i++) {
		var obj = mini.get(id_list[i]);
		if(checked){
			obj.setChecked(true);
		} else {
			obj.setChecked(false);
		}
	}

}
```

#### [输入框事件监听](http://www.miniui.com/docs/api/index.html#ui=textbox)

#### Events

| Name         | EventObject | Description    |
| :----------- | :---------- | :------------- |
| valuechanged |             | 值改变时发生   |
| validation   |             | 验证时发生     |
| enter        |             | 回车时发生     |
| keydown      |             | 键盘按下时发生 |
| keyup        |             | 键盘按起时发生 |
| focus        |             | 获取焦点时发生 |
| blur         |             | 失去焦点时发生 |

`注意：使用时，需要加上on`

```
 onblur="onValueChanged"
```

#### 设置表单的值

```
<input  class="mini-textbox" name="game_id" id="game_id" required="true"/>

// mini.get(ID值).setValue(str)
mini.get('game_id').setValue('7000,7001')
```

#### 1-60的整数的验证

`vtype="int;range:1,60"`, vtype中可以填写多个验证规则，用`;`隔开

```
<input  class="mini-textbox" name="act_days" vtype="int;range:1,60" intErrorText="请填写1-60的正整数" rangeErrorText="请填写1-60的正整数" required="true" requiredErrorText="活动天数不能为空" value="" style="width:200px;" emptyText="请输入活动天数" />
```

[表单验证规则总结](http://www.miniui.com/demo/form/rules.html)

[Properties](http://www.miniui.com/docs/api/index.html#ui=textbox)



#### 自定义表格里面的内容

使用`renderer`属性

```
<div class="mini-fit">
    <div id="datagrid1" class="mini-datagrid" style="width:100%;height:100%;" url="{:U('')}"  idField="id" showPager="true" pageSize="20">
        <div property="columns">
			.......
            <div field="" width="100" headerAlign="center" align="center" allowSort="false" renderer="onActionRenderer_package_upload">上传母包</div>
            <div field="" width="150" headerAlign="center" align="center" allowSort="false" renderer="onActionRenderer">操作</div>
            .......
        </div>
    </div>
</div>

// 上传母包
function onActionRenderer_package_upload(e) {
    var grid      = e.sender;
    var record    = e.record;
    
    var app_id    = record.app_id;
    var app_package_exists = record.app_package_exists;
    
    var package_edit = '{$access['package_edit']}';
    if (package_edit) {
    	if(app_package_exists == 1){
    		return '<span class="pointer" href="javascript:void(0)" onclick="jump(\'{:U('package_edit')}/app_id/'+app_id+'\')">重新上传</span>';
    	} else {
    		return '<span class="pointer" href="javascript:void(0)" onclick="jump(\'{:U('package_edit')}/app_id/'+app_id+'\')">+</span>';
    	}
    }
}
```

#### 行内写JavaScript-跳转

```
<a href=\"javascript:edit(" + record.id + ");\">编辑</a>

function edit(id)
{
	window.location.replace("{:U('HbSetting/edit')}" + '/id/' + id);
}
```

#### 格式化日期

```

function timeForm(e)
{
	if (e.value != '' ) {
		date = new Date(e.value);
	    return date.Format("yyyy-MM-dd hh:mm:ss");
	} else {
		return e.value;
	}
	
}
Date.prototype.Format =  function (fmt) {  // author: meizz 
    var o = {
       "M+":  this.getMonth() + 1,  // 月份 
       "d+":  this.getDate(),  // 日 
       "h+":  this.getHours(),  // 小时 
       "m+":  this.getMinutes(),  // 分 
       "s+":  this.getSeconds(),  // 秒 
       "q+": Math.floor(( this.getMonth() + 3) / 3),  // 季度 
       "S":  this.getMilliseconds()  // 毫秒 
   };
    if (/(y+)/.test(fmt)) fmt = fmt.replace(RegExp.$1, ( this.getFullYear() + "").substr(4 - RegExp.$1.length));
    for ( var k  in o)
    if ( new RegExp("(" + k + ")").test(fmt)) fmt = fmt.replace(RegExp.$1, (RegExp.$1.length == 1) ? (o[k]) : (("00" + o[k]).substr(("" + o[k]).length)));
    return fmt;
}
```

#### 表格页面的初始化

```
var grid;
var games = {$games};

jQuery(document).ready(function() {
    init();
});

function init()
{
    mini.parse();
    grid = mini.get("datagrid1");
    var form = new mini.Form("#fs");  
    var data = form.getData(true);
    grid.load(data);
}

function search()
{
    var form = new mini.Form("#fs");  
    form.validate();
    if (form.isValid() == false) return;
    var data = form.getData(true);
    grid.load(data);
}
```

#### 表单页面的初始化

```
var form;
function init(){
	mini.parse();
	form = new mini.Form("fa");	
}
jQuery(document).ready(function() {
    init();
});


// 表单验证
// 提交事件
function SubmitData() 
{
    form.validate();
    // form.isValid()   验证是否通过
    
    if (form.isValid() == false){
		return false
	};
	
	var data = $("form").serialize();
	
}
```



#### 弹窗

```
mini.open({
    url: "{:U('batch_check')}?id="+id + "&lock_status=" + status,
    title: "审核信息", 
    width: 800, 
    height: 380,
    onload: function (data) {
        console.log(data)
    },
    ondestroy: function (action) {
        if (action=='ok')
        {
            var iframe = this.getIFrameEl();
            var data = iframe.contentWindow.GetData();
            data = mini.clone(data);    //必须

            $.post("{:U('batch_check')}", data, function(result) {
                if (result.success == false)
                {
                    alert(result.msg);
                }
            }, "json");
        }

        grid.reload();
    }
});
```

