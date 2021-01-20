---
title: Javascript方法
date: 2020-04-07 14:23:17
tags:
- Javascript
categories: 
- 工作笔记
- Javascript
---

#### 判断某变量的值是否等于某数组中的一个元素

```
示例：

function IsInArray(arr,val){
var testStr=','+arr.join(",")+",";
return testStr.indexOf(","+val+",")!=-1;
}
var test=['a',23,-1];
alert(IsInArray(test,'a'));//true
alert(IsInArray(test,2));//false
alert(IsInArray(test,-1));//true
```
需求：
{% asset_img inarr.png %}

```
//当前页URL
var page = window.location.hash.split("?")[0];
//当前模块值
var this_module = page.split("/")[2];
（判断连接中是否是这几个模块下的链接）
//需要去掉游戏选择下拉框的模块
var moduleArr = ["app","channel","agent","config","white_list","account"];

// 判断模块值是否等于数组中的其中一个
function IsInArray(arr,val){
    var str=','+arr.join(",")+",";
    return str.indexOf(","+val+",")!=-1;
}
//是否在模块组中
var flag = IsInArray(moduleArr, this_module);
if(flag){
    $(".product-select").hide();
} else {
    $(".product-select").show();
}
```

###### 【参考】： [js:判断某变量的值是否等于某数组中的一个元素](http://www.imooc.com/wenda/detail/476679)



#### js高效修改对象数组里的对象属性名

```
appList: [
    {
        list:[
            {id: 118, name: "测试1", group_id: 4, os: 2}
            {id: 120, name: "测试11", group_id: 4, os: 2}
            {id: 123, name: "测试111", group_id: 4, os: 1}
        ]
        name: "测试1111"
    },
    {
        list:[
            {id: 118, name: "测试2", group_id: 4, os: 2}
            {id: 120, name: "测试22", group_id: 4, os: 2}
            {id: 123, name: "测试222", group_id: 4, os: 1}
        ]
        name: "测试2222"
    },
]

```
（因为插件的要求）改为：
```
productArr: [
    {
        children:[
            {value: 118, name: "测试1", group_value: 4, os: 2}
            {value: 120, name: "测试11", group_value: 4, os: 2}
            {value: 123, name: "测试111", group_value: 4, os: 1}
        ]
        name: "测试1111"
    },
    {
        children:[
            {value: 118, name: "测试2", group_value: 4, os: 2}
            {value: 120, name: "测试22", group_value: 4, os: 2}
            {value: 123, name: "测试222", group_value: 4, os: 1}
        ]
        name: "测试2222"
    },
]
```
代码：
```
var productArr = JSON.parse(JSON.stringify(appList).replace(/list/g, 'children'));
productArr = JSON.parse(JSON.stringify(productArr).replace(/id/g, 'value'));
```

###### 【参考】： [js高效修改对象数组里的对象属性名](https://blog.csdn.net/Mr_JavaScript/article/details/85236957)

#### 数组相减
```
//数组相减函数
function array_diff(a, b) {
    //拷贝数组
    var arr = [].concat(a);

    // 数组相减
    for (var i = 0; i < b.length; i++) {
        for (var j = 0; j < arr.length; j++) {
            if (arr[j]["id"] == b[i]["id"]) {
                arr.splice(j, 1);
                j = j - 1;
            }
        }
    }
    return arr;
}
```
#### JS 模拟浏览器 F5 自动刷新页面效果
```
1. window.location.replace(window.location.href);

2. window.location.href = window.location.href;

3. window.document.location.reload();
 
有iframe的使用这个：
4. window.top.document.location.reload();
 
5.window.top.document.location = “url”

6.window.document.location. = “url”
```

#### 对象格式转换
```
var data = [
    {
        id:'aaaaaa',
        title: '技术团队',
        description: '这就是技术',
        keywords: '技术团队',
        pid: "0",
        add_time: ""
    },
    {
        id:'bbbb',
        title: '技术团队',
        description: '这就是技术',
        keywords: '技术团队',
        pid: "1",
        add_time: ""
    }
];

转为这样的格式：
var idPidArr = {
    aaaaaa: "0",
    bbbb: "1",
}

代码：
var idPidArr = {};
for(var i = 0; i< data.length; i++){

    idPidArr[data[i].id] = data[i].pid;
}

console.log(idPidArr);
```

#### 控制滚动条滚动到某个位置
```
document.getElementById('scrollBox').scrollTop = $(el).offset().top;

scrollBox：滚动的盒子的id
$(el).offset().top: 元素的位置
```

#### js字符串连接换行符没有效果解决办法

```
var a = 'aaaaa', b = 'bbbbb', c = 'ccccc';
var arr = [a,b,c];
var str = arr.join("\n");
console.log(str);  
```

#### js 去掉字符串前后空格

###### [js去掉字符串前后空格的五种方法](https://www.cnblogs.com/yingjie13/p/3534615.html)

###### [js 去掉字符串前后空格](https://www.cnblogs.com/mingforyou/p/3930638.html)

```
使用jquery

$.trim(str) 

jquery内部实现为：

function trim(str){   
    return str.replace(/^(\s|\u00A0)+/,'').replace(/(\s|\u00A0)+$/,'');   
}
```


```
<script type="text/javascript">
　　 function trim(str){ //删除左右两端的空格
　　   return str.replace(/(^s*)|(s*$)/g, "");
　　 }
　　 function ltrim(str){ //删除左边的空格
　　   return str.replace(/(^s*)/g,"");
　　 }
　　 function rtrim(str){ //删除右边的空格
　　   return str.replace(/(s*$)/g,"");
　　 }
</script>
```

```
JS 去字符串空格 总结

str为要去除空格的字符串:
去除所有空格: 
str = str.replace(/\s+/g,""); 
去除两头空格: 
str = str.replace(/^\s+|\s+$/g,"");
去除左空格：
str=str.replace( /^\s*/, '');
去除右空格：
str=str.replace(/(\s*$)/g, "");
```



#### [用js实现模糊查询的几种方法](https://www.jianshu.com/p/4cd4f74a0b20)

##### 1. indexof 方法

> 语法：stringObject.indexOf(searchvalue, fromindex)

> 参数：searchvalue 必需。规定需检索的字符串值。 fromindex
> 可选的整数参数。规定在字符串中开始检索的位置。它的合法取值是 0 到 stringObject.length - 1。如省略该参数，则将从字符串的首字符开始检索。

> 说明：该方法将从头到尾地检索字符串 stringObject，看它是否含有子串 searchvalue。开始检索的位置在字符串的 fromindex 处或字符串的开头（没有指定 fromindex 时）。如果找到一个 searchvalue，则返回 searchvalue 的第一次出现的位置。stringObject 中的字符位置是从 0 开始的。如果没有找到，将返回 -1。


```
  /**
   * 使用indexof方法实现模糊查询
   * @param  {Array}  list     进行查询的数组
   * @param  {String} keyWord  查询的关键词
   * @return {Array}           查询的结果
   */
  function fuzzyQuery(list, keyWord) {
    var arr = [];
    for (var i = 0; i < list.length; i++) {
      if (list[i].indexOf(keyWord) >= 0) {
        arr.push(list[i]);
      }
    }
    return arr;
  }
```

##### 2. split 方法

> 语法：stringObject.split(separator, howmany)

> 参数：separator 必需。字符串或正则表达式，从该参数指定的地方分割 stringObject。howmany 可选。该参数可指定返回的数组的最大长度。如果设置了该参数，返回的子串不会多于这个参数指定的数组。如果没有设置该参数，整个字符串都会被分割，不考虑它的长度。

> 说明：该方法通过在 separator 指定的边界处将字符串 stringObject 分割成子串并返回子串数组。返回的数组中的字串不包括 separator 自身。如果 stringObject 中不存在 separator，将返回一个只包含stringObject的数组。故可以根据返回数组的长度来判断是否存在子字符串 separator 。

```
  /**
   * 使用spilt方法实现模糊查询
   * @param  {Array}  list     进行查询的数组
   * @param  {String} keyWord  查询的关键词
   * @return {Array}           查询的结果
   */
  function fuzzyQuery(list, keyWord) {
    var arr = [];
    for (var i = 0; i < list.length; i++) {
      if (list[i].split(keyWord).length > 1) {
        arr.push(list[i]);
      }
    }
    return arr;
  }
```

##### 3. match 方法

> 语法：stringObject.match(searchvalue) 或 stringObject.match(regexp)

> 参数：searchvalue 必需。规定要检索的字符串值。regexp 必需。规定要匹配的模式的 RegExp 对象。如果该参数不是 RegExp 对象，则需要首先把它传递给 RegExp 构造函数，将其转换为 RegExp 对象。

> 说明：该方法将在字符串 stringObject 内检索指定的值，或找到一个或多个正则表达式的匹配。如果没有找到任何匹配的文本，将返回 null 。否则，它将返回一个数组，其中存放了与它找到的匹配文本有关的信息。


```
  /**
   * 使用match方法实现模糊查询
   * @param  {Array}  list     进行查询的数组
   * @param  {String} keyWord  查询的关键词
   * @return {Array}           查询的结果
   */
  function fuzzyQuery(list, keyWord) {
    var arr = [];
    for (var i = 0; i < list.length; i++) {
      if (list[i].match(keyWord) != null) {
        arr.push(list[i]);
      }
    }
    return arr;
  }
```

##### 4. test方法（正则匹配）

> 语法：RegExpObject.test(string)

> 参数：string 必需。要检测的字符串。

> 说明：该方法用于检测一个字符串是否匹配某个模式。如果字符串 string 中含有与 RegExpObject 匹配的文本，则返回 true，否则返回 false。


```
/**
   * 使用test方法实现模糊查询
   * @param  {Array}  list     原数组
   * @param  {String} keyWord  查询的关键词
   * @return {Array}           查询的结果
   */
  function fuzzyQuery(list, keyWord) {
    var reg =  new RegExp(keyWord);
    var arr = [];
    for (var i = 0; i < list.length; i++) {
      if (reg.test(list[i])) {
        arr.push(list[i]);
      }
    }
    return arr;
  }
```

#### 性能测试

> 测试条件：一个长度为100的数组，每个方法测试50次，取平均值。
> indexof 方法耗费时间： 0.048ms
> split 方法耗费时间： 0.037ms
> match 方法耗费时间： 0.178ms
> test 方法耗费时间： 0.039ms

#### 结论

1. 从上面测试结果可以看出在几百几千甚至几万条数据量的情况下，前端去处理都是没问题的，相比发送一个 ajax 请求去后台来说，前端还是具有很大优势的，能节省不少时间。

2. 相比其他方法，match 方法性能最差，消耗的时间差不多是其他方法的3-4倍，虽说这一点点时间相比发送ajax来说，也算提高了很多既然我们在一开始就是为了提高用户体验，那么我们也应该追求极致啦，所以 match 选手落败。

3. 除了 match 方法，其他三个方法在性能上差不多。不过在这里有一点需要提出的就是， test 方法因为使用到了正则表达式，所以能够实现的功能会比较强大，写出来的代码也更加简洁。打个比方，在不区分大小写的模糊搜索条件下， test 方法只需在正则表达式中添加修饰符 i 即可实现不区分大小写，而 indexof 方法和 split 方法则要通过多次的方法调用和逻辑运算符才能实现效果。

#### 屏蔽Backspace键返回上个页面

```
//屏蔽Backspace键返回上个页面
function banBackSpace(e) {
    var ev = e || window.event;//获取event对象  
    var flag=(ev.keyCode == 8) ? true:false;
    if(flag) {
        return false;
    }
}
window.onload=function(){
     //禁止后退键 作用于Firefox、Opera
     document.onkeypress=banBackSpace;
     //禁止后退键  作用于IE、Chrome
     document.onkeydown=banBackSpace;
 }
```

#### 阻止浏览器默认行为触发的通用方法 

```
 //阻止浏览器默认行为触发的通用方法 
 function stopDefault(e) {
    if (e && e.preventDefault) {
        e.preventDefault();//防止浏览器默认行为(W3C) 
    } else {
       window.event.returnValue = false;//IE中阻止浏览器行为 
    }
    return false;
}
```

#### H5本地缓存


#### jquery实时监听input输入框值的变化事件

[参考](https://blog.csdn.net/qq_41756580/article/details/81287095)

1.只需要同时绑定 oninput 和 onpropertychange 两个事件，获取input元素,并实时监听用户输入。

```
$('input').bind('input propertychange', function(){
	if($(this).val()){
		console.log("hhhhhhhh");
	}else{
		console.log("xxxxxxxx");
	}
})
```

但这并不完美，因为用的bind，所以当遇到追加的新input标签时，则不能监听了。

2.为了解决上面的问题，可以使用live替代


```
$('input').live('input propertychange', function()
{
  //获取input 元素,并实时监听用户输入
  //逻辑
})


后期生成的元素，用:
$(本来存在的父元素).on("input propertychange","监听的元素", function() {
    
});
```

#### 表单input中disabled提交后得不到值的解决办法

[参考](https://www.cnblogs.com/yuanwenha/p/7390326.html)

使用readonly


模拟下拉框获取不了角度，可以让它附近的文字获取焦点。   【文字是可以获取焦点的，不是文字，一般的元素获取不了焦点】

#### 防止事件冒泡

```
window.event? window.event.cancelBubble = true : e.stopPropagation();
```

#### 返回上一页

```
javascript:window.history.go(-1);
```

#### 刷新页面

```
window.location.reload(); 
```

[参考教程](https://www.jb51.net/article/124389.htm)

#### 获取单选框选中的值

```
$('input[name="plan"]:checked').val();
```

#### 监听单选按钮事件改变

```
$('input[type=radio][name=type]').change(function() {
    if (this.value == 3) {
        $(".license_tr").hide();
        $(".license_code_tr").hide();
    }
    else {
        $(".license_tr").show();
        $(".license_code_tr").show();
    }
});
```

#### JS中对象赋值只传值不传对象（地址）的方法，改变新值不影响旧值

[参考教程](https://blog.csdn.net/tg928600774/article/details/83651608)

```
var newModel = $.extend(true,{},oldModel)
```

```
var newModel = $.extend(true,[],oldModel)
```

#### 只赋值不改变原来对象

```
var data={a:1,b:2,c:3,d:4};
var newData= $.extend(true,{},data);;
```

#### 判断是否为移动端

```
var isMobile = /Android|webOS|iPhone|iPod|BlackBerry/i.test(navigator.userAgent);
```

#### 判断输入框是否获取焦点

```
var isFocus=$("#tRow").is(":focus");  
```

#### 单页面应用判断页面是不是刷新（谷歌浏览器）

在刷新页面的时候使用window.onbeforeunload向sessionstorage或localstorage存入一个标记譬如reloadFlag作为判断是否是刷新的依据，页面刷新后从sessionstorage或localstorage中获取存储的标记，然后执行相应的回调向后端发起请求，完成之后将sessionstorage或localstorage中获取存储的标记删除即可。

```
// reLoadFlag.js
;(function(){
   	window.onbeforeunload = function(){
   		sessionStorage.setItem('reLoadFlag', 'true');
   	}
})();

// 需要判断的地方进行判断操作
if (sessionStorage.getItem('reLoadFlag') === 'true') {
   // 执行其他的逻辑
   // ...............
   sessionStorage.removeItem('reLoadFlag');
}
```

> 第一次向后端发起请求得到数据后存储到sessionstorage或localstorage之中，之后的逻辑是每次需要数据时从sessionstorage或localstorage中去取，取不到的时候（比如关闭页面重新打开或者手动清除缓存）再重新向后端发起请求获取数据。但是这样会存在一个问题，即希望通过刷新页面向后端重新发起请求的时候因为sessionstorage或localstorage的数据仍然存在，所以不会向后端发起请求。

#### filter函数做数据匹配

只有一个筛选条件的时候

```
var res = datas.filter(function (data) {
     return data[type] === val;
});
```

多个筛选条件的时候（注意：要加上  > -1，不然返回有问题）

```
var searchList = [];
searchList = list.filter(function(item) {
  var flag = (item.name.indexOf(txt) > -1) || (item.key.indexOf(txt)  >-1) || 		 (item.account_id.indexOf(txt)  >-1) || (item.user_name.indexOf(txt)  >-1) || (item.user_id.indexOf(txt)  >-1);					
   return flag;
});
```

{% asset_img filter.png %}

#### 处理textarea换行数据

先使用换行符“\n"截取，然后用"~"获取

{% asset_img br.png %}

#### 火狐浏览器，报ev is undefined

获取当前操作对象时，要记得传参

封装函数加上参数e

{% asset_img ev1.png %}

调用时加上参数e

{% asset_img ev2.png %}

#### 搜索框——实时匹配

（输入完文字就直接匹配，包括中文输入）实现中文输入法下，仅在选词后触发input事件。[参考教程](https://www.jianshu.com/p/e9c837eba083)

```
描述
在使用oninput监控输入框内容变化时，我们期望仅在value值变化时，才触发oninput事件，而在中文输入下，未选词时的按键也会触发oninput事件。
input事件触发效果

关键
compositionstart事件
compositionend事件

方法
使用一个变量表示拼写状态，在oninput事件中判断是否在拼写状态，当拼写状态结束，继续执行下一步操作。
var typing = false;
$('#ipt').on('compositionstart',function(){
    typing = true;
})
$('#ipt').on('compositionend',function(){
    typing = false;
})
//oninput在oncompositionend之前执行，需加定时器
$('#ipt').on('input',function(){
    setTimeout(function() {
        if(!typing) {
            //To do something...
        }
    },0);
})

//或用keyup代替input
$('#ipt').on('input',function(){
    if(!typing) {
        //To do something...
    }
})
```

#### 获取横向滚动条位置

```
var left = $(".layui-table-body").scrollLeft();
```

#### 设置横向滚动条位置

```
$(".layui-table-body").scrollLeft(left);
```

#### 利用js打开新页面（在另外新建窗口中打开窗口）

```
window.open("http://doc.trackingio.com/qu-dao-pei-zhi-shuo-ming/guang-dian-tong.html","_blank");  
```

#### jQuery--复制克隆（复制节点）

```
 //文档准备就绪函数
$(function () {
    //获取li标签及点击事件
    $("ul li").click(function () {
        //对这个li标签使用clone克隆（clone(true)添加true使复制过的还能继续复制）
        //，然后添加到ul标签里面
        $(this).clone(true).appendTo("ul");
    });
});
```

#### js获取日期（例如：昨天、今天和明天）

```
function GetDateStr(AddDayCount, nowDay) { 
var dd = new Date(nowDay); 

console.log("dd");
console.log(dd);
dd.setDate(dd.getDate()+AddDayCount);//获取AddDayCount天后的日期 
var y = dd.getFullYear(); 
var m = dd.getMonth()+1;//获取当前月份的日期 
var d = dd.getDate(); 

if(m < 10) {
	m = "0" + m;
}
				
if(d < 10) {
	d = "0" + d;
}

return y+"-"+m+"-"+d; 
}

GetDateStr(-1, 2019-04-02);

new Date(curDate);
var preDate = new Date(curDate.getTime() - 24*60*60*1000); //前一天
```

#### 给对象添加变量属性（空数组）

使用[]

```
selectChannel[selectList[i]] = [];
使用selectChannel.push({selectList[i]]:[]})是错的。
```

#### 改变checkbox选中状态

[参考教程](https://blog.csdn.net/brucecheng22/article/details/50408199)

使用prop方法    [动态改变checkbox的选中状态](https://www.jianshu.com/p/d544167bd715)

> 使用1.6.1 以上版本（测试使用1.10.1版本可以）



#### 捕获错误信息

```
<body> 
    <input type="button" value="获取页面错误信息" onclick="adlert('函数函数')" />
</body> 

<script type="text/javascript"> 
 var errorTxt = "";
 window.onerror = function(errorMessage, scriptURI, lineNumber,columnNumber,errorObj) { 
    errorTxt = "接收到的错误信息如下：\n\n";
    errorTxt += "错误信息：" + errorMessage + "\n";
    errorTxt += "出错文件：" + scriptURI + "\n";
    errorTxt += "出错行号：" + lineNumber + "\n";
    errorTxt += "出错列号：" + columnNumber + "\n";
    errorTxt += "错误详情：" + errorObj + "\n";

    alert(errorTxt);
  } 
</script> 
```

