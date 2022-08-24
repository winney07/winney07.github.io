---
title: web前端功能代码参考
date: 2021-11-24 16:20:39
tags:
- 工作笔记
categories:
- 工作笔记
---

#### 生成随机密码

```
// 生成随机密码按钮
$("#generatePass").click(function() {
    function getRandom(min, max) {
        return Math.round(Math.random() * (max - min) + min);
    }

    function getCode() {
        let code = '';
        for (var i = 0; i < 12; i++) {
            var type = getRandom(1, 3);
            switch (type) {
                case 1:
                    code += String.fromCharCode(getRandom(48, 57));//数字
                    break;
                case 2:
                    code += String.fromCharCode(getRandom(97, 122));//小写字母
                    break;
                case 3:
                    code += String.fromCharCode(getRandom(65, 90));//大写字母
                    break;
            }
        }
        return code;
    }

    // 写入随机密码
    $("#password").val(getCode());
});
```

#### 监听页面刷新事件方法

[window.onbeforeunload](https://developer.mozilla.org/zh-CN/docs/Web/API/WindowEventHandlers/onbeforeunload)

```
// 监听刷新页面事件方法（手动刷新）
window.onbeforeunload = function(event){
    removeItem("formData");
};
```

#### 处理接口请求函数

```
// 处理接口请求函数
/*
    url: 请求地址
    data: 参数
    callback: 回调函数
*/
function ajaxFun(url, data, callback) {
    $.post(url, data, function(res){  
        callback(res);
        // return false;
    });
}
```

#### 在html中显示JSON数据的方法

其实JSON.stringify本身就可以将JSON格式化，具体的用法是：

```
JSON.stringify(res, null, 2);	// res是要JSON化的对象，2是spacing
```

[在html中显示JSON数据的方法](https://www.jb51.net/web/553898.html)

#### 时间戳转换格式

```
//时间戳转换格式
function formatDateTime(timeStamp) { 
    var date = new Date();
    date.setTime(timeStamp * 1000);
    var y = date.getFullYear();    
    var m = date.getMonth() + 1;    
    m = m < 10 ? ('0' + m) : m;    
    var d = date.getDate();    
    d = d < 10 ? ('0' + d) : d;    
    var h = date.getHours();  
    h = h < 10 ? ('0' + h) : h;  
    var minute = date.getMinutes();  
    var second = date.getSeconds();  
    minute = minute < 10 ? ('0' + minute) : minute;    
    second = second < 10 ? ('0' + second) : second;   
    return y + '-' + m + '-' + d+' '+h+':'+minute+':'+second;    
};
```

#### 复制功能

```
var clipboard = new ClipboardJS(".copy-btn");
clipboard.on('success', function(e) {
    layer.msg('复制成功', {id: 'clipboard', time: 1000});
    e.clearSelection();
});
```

#### serialize获取的数据格式转换为json对象

```
var data = $(formEl).serialize()                // 表单数据（筛选条件)
    ,arr = decodeURIComponent(data).split("&")  // 对数据拆分处理
    ,formData = {}                              // 需要缓存的数据对象

// 转为JSON对象
arr.map(function(item) {
    formData[item.split('=')[0]] =  item.split('=')[1];
})
// 缓存formData
setItem('formData', formData);
```

### 使用window.open(url, '_self')导出表格

使用window.open(url, '_self')导出表格后，页面会刷新，本来存放的localStorage会被清（因为刷新页面做了清空表格筛选条件和页码）

```
// 监听手动刷新页面事件(按浏览器的刷新按钮||使用js方法刷新页面)
window.onbeforeunload = function(event){
    // 清空表格缓存的页码数据
    removeItem("pages");
    // 清空表格筛选条件缓存数据
    removeItem("formData");
    console.log('刷新了页面')
};
```

解决方法：使用sessionStorage临时缓存一份

```
// 在导出表格前，先临时拷贝localStorage缓存数据到sessionStorage
// 使用window.open导出表格，会将localStorage中的formData清空
sessionStorage.setItem('formData', JSON.stringify(getItem('formData')));
sessionStorage.setItem('pages', JSON.stringify(getItem('pages')));
```

```
// 导出表格后，从sessionStorage中拷贝数据再次缓存到locaStorage
setItem('formData', sessionStorage.getItem('formData'));
setItem('pages', sessionStorage.getItem('pages'));
```

#### 通过url导出服务器端文件

```
// window.location.href= url;
// 或
window.open(url, '_self')
```

#### 防抖

```
//搜索框-搜索事件
var flag = true;
$(".subtitle .iptform").on("compositionstart", function() {
    flag = false;
});
$(".subtitle .iptform").on("compositionend", function() {
    flag = true;
});
$(".subtitle .iptform").on("keyup", function() {
    if(flag) {
        //搜索内容
        var txt = $(this).val().trim();

        //显示的列表
        var list = $(".layui-show .poplist li");
        //匹配查询结果
        for(var i  = 0; i< list.length; i ++) {
            var item = $(list[i]).html();
            if(item.indexOf(txt) > -1) {
                $(list[i]).show();
            } else {
                $(list[i]).hide();
            }
        }
    }
});
```

解决搜索框输入中文时，未输入完整词语就搜索的问题

```
//搜索框-搜索事件（解决中文输入法过程中，未输入完整就请求）
var flag = true;
$(".subtitle .iptform").on("compositionstart", function() {
    flag = false;
});
$(".subtitle .iptform").on("compositionend", function() {
    flag = true;
});
// 解决
$(".subtitle .iptform").on("keyup", function() {
    if(flag) {}
});
```

#### 时间戳转换时间格式

```
function formatDateTime(timeStamp) { 
    var date = new Date();
    date.setTime(timeStamp * 1000);
    var y = date.getFullYear();    
    var m = date.getMonth() + 1;    
    m = m < 10 ? ('0' + m) : m;    
    var d = date.getDate();    
    d = d < 10 ? ('0' + d) : d;    
    var h = date.getHours();  
    h = h < 10 ? ('0' + h) : h;  
    var minute = date.getMinutes();  
    var second = date.getSeconds();  
    minute = minute < 10 ? ('0' + minute) : minute;    
    second = second < 10 ? ('0' + second) : second;   
    return y + '-' + m + '-' + d+' '+h+':'+minute+':'+second;    
};
```

#### 滚动条css修改

```
// 火狐浏览器
.dashboard-container,
.no-page-table .layui-table-main{
    // scrollbar-color: #0064a7 #8ea5b5;   // 如果有scrollbar-width才设置
    scrollbar-width:none;				// 目前只有3个值可选：auto、thin、none
}

// 针对谷歌浏览器、360浏览器、safari浏览器、Edge、Opera等
.no-page-table ::-webkit-scrollbar,
.right-content ::-webkit-scrollbar{  /* 滚动条整体部分 */
    width: 0;
    margin-right:2px
}
.no-page-table ::-webkit-scrollbar-button,
.right-content ::-webkit-scrollbar-button { /* 滚动条两端的按钮 */
    width: 0;
    height: 0;
    background-color: transparent;
}
// ::-webkit-scrollbar:horizontal针对横向滚动条，为了方便鼠标拖动，如果也设置为0，不好控制
.no-page-table ::-webkit-scrollbar:horizontal,
.right-content ::-webkit-scrollbar:horizontal {   
    height:6px;
    margin-bottom:2px
}
.no-page-table ::-webkit-scrollbar-track,
.right-content ::-webkit-scrollbar-track  {  /* 外层轨道 */
    box-shadow: inset 0 0 5px transparent;
    border-radius: 0;
    background: transparent;
}
.no-page-table ::-webkit-scrollbar-track-piece,
.right-content ::-webkit-scrollbar-track-piece {  /*内层轨道，滚动条中间部分 */
    background-color: transparent;
    border-radius: 2px;
}
.no-page-table ::-webkit-scrollbar-thumb,
.right-content ::-webkit-scrollbar-thumb{  /* 滑块 */
    /* width:1px;
    border-radius: 5px;
    background: #CBCBCB; */
    /*滚动条里面小方块*/
    border-radius: 5px;
    box-shadow: inset 0 0 5px rgba(0, 0, 0, 0.2);
    background: rgba(0, 0, 0, 0.2);
}
.no-page-table ::-webkit-scrollbar-corner,
.right-content ::-webkit-scrollbar-corner { /* 边角 */
    width: 0;
    background-color: transparent;
}
.no-page-table ::-webkit-scrollbar-thumb:hover,
.right-content ::-webkit-scrollbar-thumb:hover { /* 鼠标移入滑块 */
    background: #909090;
}
```

如果要自定义设置其他样式，可根据上面的属性进行自定义设置

#### 如果设置滚动条宽度为0，可简略写：

```
/* 火狐浏览器 */
.dashboard-container,
.no-page-table .layui-table-main{
    scrollbar-width:none;    // 这个值要设置给真实滚动内容的盒子，直接给html，不会全部生效
}
// scrollbar-width的设置元素与谷歌浏览器::-webkit-scrollbar设置的元素可能不一样，要针对实际情况设置

/* 滚动条整体部分 */
.no-page-table ::-webkit-scrollbar,
.right-content ::-webkit-scrollbar{  
    width: 0;
}
/* 滚动条两端的按钮 */
.no-page-table ::-webkit-scrollbar-button,
.right-content ::-webkit-scrollbar-button {
    width: 0;
    height: 0;
    background-color: transparent;
}
/* 横向滚动条 */
.no-page-table ::-webkit-scrollbar:horizontal,
.right-content ::-webkit-scrollbar:horizontal {
    height:6px;
}
```

[Custom CSS Scrollbar for Firefox](https://stackoverflow.com/questions/6165472/custom-css-scrollbar-for-firefox)

[Custom scrollbars](https://stackoverflow.com/questions/7357203/custom-scrollbars)

[Custom CSS Scrollbar for Firefox](https://stackoverflow.com/questions/6165472/custom-css-scrollbar-for-firefox)

[scrollbar-color](https://developer.mozilla.org/zh-CN/docs/Web/CSS/scrollbar-color)

[如何用CSS修改浏览器滚动条的样式](http://www.divcss5.com/css3-style/c57127.shtml)

[浏览器滚动条样式修改](https://zhuanlan.zhihu.com/p/144204013)

```
 ::-webkit-scrollbar {  /* 滚动条整体部分 */
      width:10px;
      margin-right:2px
  }
  ::-webkit-scrollbar-button { /* 滚动条两端的按钮 */
      width:10px;
      background-color: yellow;
  }
  ::-webkit-scrollbar:horizontal {
      height:10px;
      margin-bottom:2px
  }
  ::-webkit-scrollbar-track {  /* 外层轨道 */
      border-radius: 10px;
  }
  ::-webkit-scrollbar-track-piece {  /*内层轨道，滚动条中间部分 */
      background-color: #333333;
      border-radius: 10px;
  }
  ::-webkit-scrollbar-thumb {  /* 滑块 */
      width:10px;
      border-radius: 5px;
      background: #CBCBCB;
  }
  ::-webkit-scrollbar-corner { /* 边角 */
      width: 10px;
      background-color: red;
  }
  ::-webkit-scrollbar-thumb:hover { /* 鼠标移入滑块 */
      background: #909090;
  }
```

[CSS设置滚动条样式](https://blog.csdn.net/cddcj/article/details/70332771)

#### 回车事件

[Vue封装回车事件](https://blog.csdn.net/SmallTeddy/article/details/107181087)



[JavaScript 深拷贝性能分析](https://segmentfault.com/a/1190000013107871)

[深入 js 深拷贝对象](https://www.cnblogs.com/makai/p/11249986.html)

日常深拷贝，建议序列化反序列化方法。

[兼容各个浏览器的事件监听代码](https://www.cnblogs.com/white0710/p/6686290.html)

[将网址url中的参数转化为JSON格式的两种方法](https://www.cnblogs.com/wangshucheng/p/11203097.html)



#### 第一种： for 循环方式

```
// 第一种： for循环
var GetQueryJson1 = function () {
  let url = location.href; // 获取当前浏览器的URL
  let arr = []; // 存储参数的数组
  let res = {}; // 存储最终JSON结果对象
  arr = url.split('?')[1].split('&'); // 获取浏览器地址栏中的参数
   
  for (let i = 0; i < arr.length; i++) { // 遍历参数
    if (arr[i].indexOf('=') != -1){ // 如果参数中有值
      let str = arr[i].split('=');
      res[str[0]] = str[1];
    } else { // 如果参数中无值
      res[arr[i]] = '';
    }
  }
  return res;
}
console.log(GetQueryJson1());
```

#### 第二种：正则表达式方式

```
// 第二种：正则表达式
var GetQueryJson2 = function () {
  let url = location.href; // 获取当前浏览器的URL
  let param = {}; // 存储最终JSON结果对象
  url.replace(/([^?&]+)=([^?&]+)/g, function(s, v, k) {
    param[v] = decodeURIComponent(k);//解析字符为中文
    return k + '=' +  v;
  });
  return param;
}
 
console.log(GetQueryJson2());
```

#### 监听滚动条事件

```

//监听内容区的滚动事件
$(".dashboard-container").scroll(function() {
    var timer = null;
    clearTimeout(timer);


    timer = setTimeout(function(){
        var hourDataTop = $("#hourData").offset().top;
        var viewWidth = window.innerWidth;
        var viewHeight = window.innerHeight;

        // 内容滚动高度
        var sctop = $(".dashboard-container").scrollTop(); 
        var isPC = IsPC();	// 是否PC端
        var isHorizontal = viewWidth > viewHeight;   // 是否横屏

        // alert(isHorizontal);

        var detailTablePos = isPC ? 153 : (isHorizontal ? 253 : 480);
        var hourDataPos = isPC ? 90  : (isHorizontal ? 140 : 140);
        console.log(hourDataTop);


        if(sctop >= detailTablePos) {
            $(".detailTable .layui-table-header").addClass("fixed-table-header");
            $(".hourData .layui-table-header").removeClass("fixed-table-header");

            //获取右侧内容宽度
            var w = $(".conditionWrap").width();
            $(".detailTable .layui-table-header").css("width", w - 2);
            $(".detailTable .layui-table-header").css("overflow", "hidden");

            //判断是否收起状态
            var isFold = $("#main-layout").hasClass("hide-side");
            if(isFold) {
                $(".detailTable .layui-table-header").addClass("fixed-table-header-left");
            } else {
                $(".detailTable .layui-table-header").removeClass("fixed-table-header-left");
            }
        }
        else{
            var total = getParams().total, this_table = '', lay_id = '';
            switch(total) {
                case '0' :
                    this_table = '.channelTable';
                    lay_id = 'mainChannel';
                    break;
                case '1' :
                    this_table = '.leaderTable';
                    lay_id = 'leaderDetail';
                    break;
                case '2' :
                    this_table = '.accountTable';
                    lay_id = 'accountDetail';
                    break;
                case '3' :
                    this_table = '.channelIdTable';
                    lay_id = 'channelIdDetail';
                    break;
            }	

            $(this_table + " .layui-table-header").removeClass("fixed-table-header");
            // 根据内容横向滚动多少，动态设置头部滚动多少
            var left = $('.layui-table-view[lay-id="' + lay_id + '"] .layui-table-body').scrollLeft();
            $(this_table + " .layui-table-header").scrollLeft(left);
        }

        if(hourDataTop <= hourDataPos) {
            var w = $(".conditionWrap").width();

            var hourW = $(".hourData .layui-table-header").width();
            //判断是否收起状态
            var isFold = $("#main-layout").hasClass("hide-side");
            if(isFold) {
                $(".hourData .layui-table-header").css("width", hourW);
                $(".hourData .layui-table-header").addClass("fixed-table-header-left");
            } else {
                $(".hourData .layui-table-header").css("width", hourW);
                $(".hourData .layui-table-header").removeClass("fixed-table-header-left");
            }

            $(".hourData .layui-table-header").addClass("fixed-table-header");
            $(".detailTable .layui-table-header").removeClass("fixed-table-header");
        } else{
            $(".hourData .layui-table-header").removeClass("fixed-table-header");
        }

    },150);
});

//左导航栏显示隐藏按钮
$("#hideBtn").click(function() {
    $(".fixed-table-header").toggleClass("fixed-table-header-left");
    setTimeout(function(){
        var w = $(".conditionWrap").width();
        $(".data-table .layui-table-header, [lay-id='hourData'] .layui-table-box").css("width", w);
    },400);
});
```





#### URL参数改为json格式

```
var data = $(formEl).serialize()                // 表单数据（筛选条件)
    ,arr = decodeURIComponent(data).split("&")  // 对数据拆分处理
    ,formData = {}                              // 需要缓存的数据对象
// 转为JSON对象
arr.map(function(item) {
    formData[item.split('=')[0]] =  item.split('=')[1];
})
```

#### 大于等于0小于等于100正数的正则表达式是多少

```
可以有小数：^100$|^(\d|[1-9]\d)(\.\d+)*$
不可以有小数：^100$|^(\d|[1-9]\d)$
```

#### 动态设置表格padding

```
// 动态设置表格padding
function setTablePdRight() {
    // 判断是否有竖向滚动条
    var maxH = $(".layui-table-body").height();
    var tableH =  $(".main-layout-body").find(".layui-table-main .layui-table").height();

    var pd_r = tableH > maxH ? '17px' : '0';
    $(".layui-table-box > .layui-table-header").css("padding-right", pd_r);
}
```

#### 模拟环形进度条

`circle-progress.js`

```
// 创建模拟环形进度条
// 导出文件过程中-网络请求卡顿/接口pending状态下的交互效果（假进度-只提供用户交互）
var canvas = new EnableCircle({
    id:'le-canvas',		// 被渲染元素的canvas的ID
    value: 96,			// 最大值
    target: 'primary',
    lineWidth: 10,		// 环形宽度
    lineCap: 'round',
});
```

#### 判断是否为PC端

```
// 判断是否为PC端
function IsPC() {
	var userAgentInfo = navigator.userAgent;
	var Agents = ["Android", "iPhone",
				"SymbianOS", "Windows Phone",
				"iPad", "iPod"];
	var flag = true;
	for (var v = 0; v < Agents.length; v++) {
		if (userAgentInfo.indexOf(Agents[v]) > 0) {
			flag = false;
			break;
		}
	}
	return flag;
}
```

#### 修改url参数

```
function changeURLArg(url,arg,arg_val){ 
    var pattern=arg+'=([^&]*)'; 
    var replaceText=arg+'='+arg_val; 
    if(url.match(pattern)){ 
        var tmp='/('+ arg+'=)([^&]*)/gi'; 
        tmp=url.replace(eval(tmp),replaceText); 
        return tmp; 
    }else{ 
        if(url.match('[\?]')){ 
            return url+'&'+replaceText; 
        }else{ 
            return url+'?'+replaceText; 
        } 
    } 
    return url+'\n'+arg+'\n'+arg_val; 
}
```

#### 改变hash值

```
//改变hash值
function changeHash(key, val) {
    location.hash= location.hash.match(key+"=([^&]*)") ? location.hash.replace(eval('/('+ key+'=)([^&]*)/gi'), key+"="+val) : location.hash + "&"+key+"="+val
}
```

#### 监听手动刷新页面事件

```
// 监听手动刷新页面事件(按浏览器的刷新按钮||使用js方法刷新页面)
window.onbeforeunload = function(event){
	// 清空缓存数据
	localStorage.clear();
};
```

#### 正则

```
if ( empty($data['name']) ) $this->error('姓名不能为空');
if ( mb_strlen($data['name']) > 20 ) $this->error('姓名请输入20位字符以内的中英文或数字');
if ( !preg_match("/^[A-Za-z0-9_\x{4e00}-\x{9fa5}]+$/u", $data['name']) ) $this->error('姓名请输入20位字符以内的中英文或数字');
if ( empty($data['username']) ) $this->error('登录账号不能为空');
if ( !preg_match('/^[A-Za-z0-9]{1,15}$/', $data['username']) ) $this->error('账号请输入15位字符以内的大小写字母或数字');
if ( empty($data['password']) ) $this->error('登录密码不能为空');
if ( !preg_match('/^(?![A-Z]+$)(?![a-z]+$)(?!\d+$)\S+$/', $data['password']) ) $this->error('密码请输入6-18位至少包含数字、大小字母中的两种');
if ( strlen($data['password']) < 6 ||  strlen($data['password']) > 18 ) $this->error('密码请输入6-18位至少包含数字、大小字母中的两种');
if ( empty($data['roleId']) ) $this->error('所属角色不能为空');
if ( AccountService::checkName(trim($data['name'])) ) $this->error('姓名已经存在，请重新定义');
if ( AccountService::checkUsername(trim($data['username'])) ) $this->error('请重新填写，该账号已存在');
```

遍历数组的指定值

```
// 遍历对象数组的指定值
function getObjectsVals(arr, key) {
    var objs = [], str = "";

    arr.forEach(function(value, index, array){
        objs.push(array[index][key])
    })

    str = objs.join(",")

    return str;
}
```

#### 阻止浏览器的默认行为 

```
function stopDefault(e) { 
	if ( e && e.preventDefault ) {
		e.preventDefault(); 
	}
}
```

[正则表达式](https://www.w3cschool.cn/regexp/bxrq1pqf.html)

[正则表达式](https://c.runoob.com/front-end/854/)

#### 数组增删元素

```
// 数组添加或删除元素
function filterArr(arr, item) {
    var _index;  //是否含有该选项
    var html = "";
    _index = arr.indexOf(item);
    if(_index > -1) {
        arr.splice(_index, 1);
    } else {
        arr.push(item);
    }

    // 数组转字符串
    html = arr.join(',');

    return html;
}
```

