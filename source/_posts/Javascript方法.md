---
title: Javascript方法
date: 2020-04-07 14:23:17
tags:
- Javascript
categories: 
- 工作笔记
- Javascript
---

#### 删除对象某个属性

```
var obj={
    name: 'zhagnsan',
    age: 19 
}
delete obj.name //true
```

#### 数组对象按照某个属性排序

```
group.sort(function(a, b){return Number(a.year) - Number(b.year)});
```



#### [js获取当前时间(昨天、今天、明天)](https://www.cnblogs.com/menxiaojin/p/13753525.html)

#### 获取时间戳-valueOf()

```
var d = new Date().valueOf();
```

#### new Date()方法

```
new Date().toDateString()
Wed Mar 02 2020
```

```
new Date().toLocaleDateString()
2020/3/2
```

```
new Date().toLocaleTimeString()
17:50:21
```

```
new Date().toLocaleString();
2020/3/2 17:46:52
```

```
new Date().toTimeString()
17:50:59 GMT+0800 (中国标准时间)
```

```
new Date().toUTCString()
Wed, 02 Mar 2020 09:51:30 GMT
```

#### 获取明天的日期并格式化

```
// 格式化日期
function format(t, symbol){
    var year = t.getFullYear()       // 年份
        , month = t.getMonth() + 1   // 月份
        , date = t.getDate()         // 日
        , symbol = symbol || '-';    // 分隔符，默认为-
    month = month < 10 ? '0' + month : month;
    date = date < 10 ? '0' + date : date;
    return year + symbol + month + symbol + date;
}

var now = new Date()               // 获取当前时间
    , time_stamp = now.setDate(now.getDate() +  1)
    , tomorrow = format(new Date(time_stamp));  // 明天
```

#### 获取前后相隔n天的日期

```
/*
* 根据间隔天数获取日期
* @param interval：间隔天数
* @param symbol：日期格式分隔符（默认：-）
* interval为-1：昨天
* interval为0：今天
* interval为1：明天
*/

function getDate(interval, symbol) {
    // getDate: 返回月份的某一天
    // setDate：设置为月份的某一天
    var now = new Date()               // 获取当前时间
        , time_stamp = now.setDate(now.getDate() +  parseInt(interval))
        , date = new Date(time_stamp);  // 根据间隔天数获取的日期
    // 返回格式化后日期
    return format(date);
}
```

#### 根据某天的前后几天获取日期

```
/*
* 根据某天的前/后几天
* @param interval：间隔天数
* @param value：某天的日期
* @param symbol：日期格式分隔符（默认：-）
* interval为-1：昨天
* interval为0：今天
* interval为1：明天
*/
function getPreDate(interval, value, symbol) {
    // getDate: 返回月份的某一天
    // setDate：设置为月份的某一天
    var now = new Date(value)               // 获取当前时间
        , time_stamp = now.setDate(now.getDate() +  parseInt(interval))
        , date = new Date(time_stamp);  // 根据间隔天数获取的日期
    // 返回格式化后日期
    return format(date);
}
```



#### 实现倒计时功能

```
// 倒计时功能
var div = document.getElementById("showtime");
setInterval (function () {
    div.innerHTML = showtime();
}, 1000); 

var showtime = function () {
    var nowTime = new Date(),  // 获取当前时间
        // endTime = new Date("2022/8/20");  // 定义结束时间  
        endTime = new Date("2022/8/20 23:59:59");  // 定义结束具体时间——即8月21凌晨结束
    var time = endTime.getTime() - nowTime.getTime(),  // 距离结束时间的毫秒数
        d = Math.floor(time/(1000*60*60*24)),  // 计算天数
        h = Math.floor(time/(1000*60*60)%24),  // 计算小时数
        m = Math.floor(time/(1000*60)%60),  // 计算分钟数
        s = Math.floor(time/1000%60);  // 计算秒数

    h = h < 10 ? "0" + h : h;
    m = m < 10 ? "0" + m : m;
    s = s < 10 ? "0" + s : s;
    return d + "天" + h + ":" + m + ":" + s;  //返回倒计时的字符串
}
```



#### [forEach()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach)

```
var arr = [1, 2, 3, 4, 5];

arr.forEach(function (item) {
    if (item === 3) {
        return;		// ---->3的元素跳过
    }
    console.log(item);
});
// 输出结果：
1
2
4
5
```



#### [js中数组常用方法总结](https://www.cnblogs.com/jinzhou/p/9072614.html)

#### 一、作用域

1、当看到script标签的时候就会进入到js作用

2、调用一个function的时候

#### 二、进入到作用域之后，发生了什么事情??

1、js预解析

​		开辟一个空间，找有没有var，有没有方法参数，有没有function，如果有var，有方法参数，就把var和方法参数定义的变量设置成undefined，如果有function，那么就储存function里面的所有内容。

2、js逐行执行

​	 从上往下执行，找有没有表达式，+  - * 、==   ++   -- ，如果有表达式，就修改js作用域里面的变量的值。

```
window.onload = function () {
	console.log(a);
	var a = 1;
	console.log(a);
    function a() {
        console.log(2); 
    }
	console.log(a);
    var a = 3;
    console.log(a);
    function a() { 
        console.log(4);
    }
    console.log(a);
	a();
)
```

#### 判断对象是否为空

```
// 判断对象是否为空
var obj = JSON.stringify(data);
if(obj === '{}') {
    console.log("对象为空");
}else {
    console.log("对象不为空");
}


或者直接判断是否具有某属性

var title = data.id ? "编辑" : "新增";
```

[js判断对象是否为空对象的几种方法](https://www.cnblogs.com/jpfss/p/9105119.html)

[javascript怎么判断对象是否为空？](https://m.html.cn/qa/javascript/11178.html)

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

在后台的某些模块中，不显示表头的游戏下拉筛选框：

```
// 当前页URL
var page = window.location.hash.split("?")[0];
// 当前模块值
var this_module = page.split("/")[2];
（判断连接中是否是这几个模块下的链接）
// 需要去掉游戏选择下拉框的模块
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
#### js拷贝对象，不改变原来对象

```
var obj = {a:1,b:2}  
var newObj = JSON.parse(JSON.stringify(obj)); 
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

#### [如果动态设置json对象的key](https://www.cnblogs.com/strangerqt/p/4465114.html)

项目中要求动态设置json的key属性，如果按照一般的json设置方法是不行的。假如你把一个key设置为一个变量的话，那么最后js解析出来的就是key为这个变量名而不是这个变量的值。

解决：通过使用

var o = {};

o[变量名] = 变量值

再把这个变量赋值给json即可

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

#### javascript禁止页面滚动（但是ie8及以下不支持）

```
var scrollFunc=function(e){
	e=e||window.event;
    if (e&&e.preventDefault){
        e.preventDefault();
        e.stopPropagation();
    }else{
        e.returnvalue=false;
        return false;
    }
}
if(window.addEventListener){
    window.addEventListener('DOMMouseScroll',scrollFunc,false);
    window.addEventListener('mousewheel',scrollFunc,false);
}else{
    window.onmousewheel=scrollFunc;
}
```

#### js数组与字符串的相互转换

###### 一、数组转字符串

```
需要将数组元素用某个字符连接成字符串，示例代码如下：
var a, b,c; 
a = new Array(a,b,c,d,e); 
b = a.join('-'); //a-b-c-d-e  使用-拼接数组元素
c = a.join(''); //abcde
```

###### 二、字符串转数组

```
实现方法为将字符串按某个字符切割成若干个字符串，并以数组形式返回，示例代码如下：
var str = 'ab+c+de';
var a = str.split('+'); // [ab, c, de]
var b = str.split(''); //[a, b, +, c, +, d, e]
```

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

#### 设置复选框选中

```
$("input").attr("checked", true);
或
$("input").attr("checked", "true");
```

#### 判断复选框是否被选中

```
var isChecked = $("input").is(":checked");
```

#### 设置复选框不选中

```
$("input").attr("checked", false); 
或
$("input").prop("checked", false); 
```

#### 全选/全不选复选框

```
$('#selectAll').bind('change',function(event) {
    var isCheck=$("#selectAll").is(':checked');  //获得全选复选框是否选中
    $("input[name='platform']").each(function() {  
        this.checked = isCheck;       //循环赋值给每个复选框是否选中
    });


    var selectArr = [], checkbox;  
    checkbox = $('input[name ="platform"]');

    for(var i = 0; i < checkbox.length;i++){
        if(checkbox[i].checked == true){
            selectArr.push(checkbox[i].value);
        }
    }
    console.log(selectArr);
});
```

#### 全选复选框和普通复选框联合

```
var $all_check = $('#all_check');
var $check = $('.check');

/**
 * 全选按钮点击事件
 */
$all_check.bind('click', function () {
    if ($(this).is(':checked')) {
        $check.prop('checked', true);
    } else {
        $check.prop('checked', false);
    }
});

/**
 * 普通按钮点击事件
 */
$check.bind('click', function () {
    if ($(this).is(':checked')) {
        var isAllCheck = true;
        $check.each(function () {
            if (!$(this).is(':checked')) {
                isAllCheck = false;
            }
        });
        if(isAllCheck){
            $all_check.prop('checked', true);
        }
    } else {
        $all_check.prop('checked', false);
    }
});
```

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

```
(function(){
    var o=navigator.userAgent;
    if(o.indexOf("iPhone")!=-1 || o.indexOf("iPad")!=-1 || o.indexOf("iPod")!=-1 || o.indexOf("Android")!=-1){
        self.location='/mobile/';
    }}
)();
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
  var flag = (item.name.indexOf(txt) > -1) || (item.key.indexOf(txt)  >-1) || (item.account_id.indexOf(txt)  >-1) || (item.user_name.indexOf(txt)  >-1) || (item.user_id.indexOf(txt)  >-1);					
   return flag;
});
```

#### 处理textarea换行数据

先使用换行符“\n"截取，然后用"~"获取

![处理textarea换行数据](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/Javascript%E6%96%B9%E6%B3%95/br.png)

#### 火狐浏览器，报ev is undefined

- 获取当前操作对象时，要记得传参

- 封装函数加上事件参数e

- 调用时加上事件参数e


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

#### 按回车触发的事件

```
document.onkeydown = function(e){ 
    var ev = document.all ? window.event : e;
    if(ev.keyCode==13) {
        $(".login-btn").click();
    }
}
```



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

#### 返回文档的根节点（html）

```
document.documentElement
```

#### 返回DOM对象中的body节点

```
document.body
```

> 在标准模式下，document.body.scrollTop恒为0；
>
> 但在怪异模式下，document.documentElement.scrollTop；
>
> 但是document.documentElement.scrollTop和document.body.scrollTop在标准模式或者是奇怪模式下都只有一个会返回有效的值，所以获取scrollTop时两个都加上

#### 获取滚动条当前位置高度

```
function getScrollTop(){
	var scrollTop = 0;
	if(document.documentElement && document.documentElement.scrollTop){

		scrollTop = document.documentElement.scrollTop;

	}else if(document.body){

		scrollTop = document.body.scrollTop;

	}
	return scrollTop;
}
```

#### 获取当前页面可视高度(注意，此处得到的是当前页面的可视高度，而不是浏览器的可视高度)

```
function getClientHeight(){

	var clientHeight = 0;
	if(document.body.clientHeight && document.documentElement.clientHeight){

		clientHeight = Math.min(document.body.clientHeight,document.documentElement.clientHeight);

	}else{

		clientHeight = Math.max(document.body.clientHeight,document.documentElement.clientHeight);

	}

	return clientHeight;
}
```

#### 获取文档完整高度

```
function getScrollHeight(){

	return Math.max(document.body.scrollHeight,document.documentElement.scrollHeight);

}
```

#### 判断是否到达页面底部

```
// 当滚动条高度加上页面可视高度等于整个文档完整高度，则页面已达到底部
getScrollTop() + getClientHeight() == getScrollHeight() 
```

#### 清空尚未执行完的动画队列

```
$(".mobie_show").stop().animate({"top":"70px","opacity":"1"});
```

> 把当前元素接下来尚未执行完的动画队列清空    （例如：当用户鼠标经过某元素的时候，执行某个动画，用户不断地让鼠标经过元素，但上一个动画还没有执行完毕。  加上stop是为了避免用户不停地操作）

#### swobject的使用

```
var params = {wmode:"transparent"};
swfobject.embedSWF("http://images.vxinyou.com/gd/images1510/hh.swf", "hh", "1920", "450", "9.0.0","http://images.vxinyou.com/jsCommon/expressinstall.swf", {}, params);  
```

#### JS禁止查看网页源代码的实现方法

查看源代码的方法：

1、直接按F12

2、Ctrl+Shift+I查看

3、鼠标点击右键查看

> 把以上三种状态都屏蔽掉就可以了，document有onkeydown(键盘按键事件)，该事件里面找到对应的keycode并处理就可以，document也有oncontextmenu鼠标右键事件，屏蔽即可。

```
window.onload = function(){
    document.onkeydown = function(){
        var e = window.event || arguments[0];
        console.log(e);
        if(e.keyCode == 123){
            // alert("小样你想干嘛？");
            return false;
        }else if((e.ctrlKey)&&(e.shiftKey)&&(e.keyCode == 73)){
            // alert("还是不给你看。。");
            return false;
        }
    };
    document.oncontextmenu = function(){
        // alert("小样不给你看");
        return false;
    }
}
```

#### 网站个性化设置-换肤

结构：

```
<body class="green">
<div>
    <div class="theme">
        <button class="btn btn-default">默认</button>
        <button class="btn btn-green”>绿色</button>
        <button class="btn btn-blue">蓝色</button>
        <button class="btn btn-orange">橙色</button>
    </div>
    <div class="main-nav">
        <ul>
            <li><a href="#”>首页<span>Home</span></a></li>
            <li><a href="#">公司概况<span>Company</span></a></li>
            <li><a href="#">新闻中心<span>News</span></a></li>
        </ul>
    </div>
    <div id="content">
        <p>网站个性化设置-换肤!</p>
    </div>
</div>
</body>
```

样式：

```
#content p {
	padding: 10px;
}
/*默认主题*/
body.default {
	background:url(../images/bg1.jpg) no-repeat;
}
.default .main-nav {
	background: #c5000;
}
.default #content {
	background: #c5000;
}
/*绿色主题*/
body.green {
	background:ur1(../images/bg2-jpg) no-repeat;
}
.green .main-nav {
	background: #5cb85c;
}
.green #content {
	background: #5cb85c;
}
/*蓝色主题*/
body.blue {
	background:url(../images/bg3.jpg) no-repeat;
}
```

方法：

- 方法一：点击按钮改变body的样式

  用replace替换，拿到后面的值（default、green）用replace把（btn btn-）替换为空

  ```
  $(function() {
  	// 单击不同的按纽,加载不同的样式
  	$(".theme button").click(function(){
  	// replace()用于替换字符串
  	// attr()获取属性
  	var theme = $(this).attr('class').replace('btn btn-','');
  	alert(theme);
  	$("body").attr('class', theme);  // body添加属性
  }
  ```

  > 弊端（如果button 后面还有别的类名，就不好使了）

- 方法二：自定义属性

  ```
  <div class="theme">
      <button class="btn btn-default" btn-name="default">默认</button>
      <button class="btn btn-green” btn-name="green">绿色</button>
      <button class="btn btn-blue" btn-name="blue">蓝色</button>
      <button class="btn btn-orange" btn-name="orange">橙色</button>
  </div>
  ```

  ```
  $(function() {
  	// 单击不同的按纽,加载不同的样式
  	$(".theme button").click(function(){
  	// replace()用于替换字符串
  	// attr()获取属性
  	var theme = $(this).attr('btn-name');
  	alert(theme);
  	$("body").attr('class', theme);  // body添加属性
  }
  ```

#### 获取form表单全部value值

  ```
  var data = $("#form").serializeArray();
  ```

  #### 鼠标在图片上，滚动滚轮，可放大缩小图片

  ```
  <img src="./blog-head-img.jpg" onmousewheel="return bbimg(this)" 
  onload="if(this.width > screen.width - 500) this.style.width = screen.width - 500;">
  
  function bbimg(obj){
      var zoom = parseInt(obj.style.zoom, 10) || 100;
      zoom += event.wheelDelta/12;
      if (zoom>0) {
          obj.style.zoom = zoom + '%';
      } 
      return false;
  }
  ```

  #### delegate() 方法

> [delegate() 方法](https://www.w3school.com.cn/jquery/event_delegate.asp)为指定的元素（属于被选元素的子元素）添加一个或多个事件处理程序，并规定当这些事件发生时运行的函数。
>
> 使用 delegate() 方法的事件处理程序适用于当前或未来的元素（比如由脚本创建的新元素）。

```
$("div").delegate("button","click",function(){
  $("p").slideToggle();
});
```

```
$(selector).delegate(childSelector,event,data,function)
```

#### 记录及清空搜索历史记录



#### 回到页面顶部

[基于JS实现回到页面顶部的五种写法(从实现到增强)](https://www.jb51.net/article/91824.htm)

#### 移动端设备判断

```
var ua=navigator.userAgent, 			     wxv=parseInt(ua.substring(ua.toLowerCase().indexOf("micromessenger/")+15));
var uClient = "mq";
if(wxv >= 5){
    uClient = "wx";
}else{
    isQzone = ua.match("Qzone");
    if(isQzone){
        uClient = 'qzone';
    }
}
var iPad = ua.match(/(iPad).*OS\s([\d_]+)/),
    iPhone = !iPad && ua.match(/(iPhone\sOS)\s([\d_]+)/),
    iPod = ua.match(/(iPod).*OS\s([\d_]+)/),
    android = ua.match(/(Android)\s+([\d.]+)/)||ua.match(/Android/),
    wp = ua.match(/Windows Phone ([\d.]+)/),
    isMobile = iPad || iPhone || iPad || wp || android;
```

#### 回调函数：

```
var foo = 1;
function bar(callback) {
    foo = 10;
    console.log(foo);
    console.log(this);
    console.log(this.foo);
    return;
    function foo() {}
}
bar(function(){
    console.log('回调');
    console.log(foo);
});

console.log(this);
console.log(this.foo);

console.log(foo);
```

```
 var func = (function(a) {
    this.a = a;
    return function(a) {
        a += this.a;
        return a;
    }
})
(function(a, b) {
    return a;
}(1, 2));

console.log(func(4));
```

#### 数组按一定原则排序

```
var arr5 = [{id:10},{id:5},{id:6},{id:9},{id:2},{id:3}];
arr5.sort(function(a,b){
    return a.id - b.id
})
```



#### 对返回的数据进行处理-专为数组或对象格式

```
var data ={
    'yangyibing':{
        name: '杨伊冰',
        age: '25',
        job: 'web',
        city: 'guangzhou' 
    },
    'liyishun':{
        name: '李一瞬',
        age: '25',
        job: 'web',
        city: 'guangzhou' 
    }
}

function getList(data){
    var obj = {}, list = [], returnData = {};

    for(var key in data){
        var item = {
            k: key,
            v: data[key]
        }

        obj[key] = data[key];

        list.push(item);
    }

    returnData['list'] = list;
    returnData['obj'] = obj;

    return returnData;
}

var obj = getList(data)['obj'];
var list = getList(data)['list'];
console.log(obj);
console.log(list);
```

#### 输入框获取焦点-放大/缩小页面（scale）

```
<div class="login-box">
    <input type="text" id="login-input">
</div>
```

```
// var clientH = document.documentElement.clientHeight;
// var clientW = document.documentElement.clientWidth;
$(function(){
    // $(".login-box").css({"width":clientW + "px","height":clientH + "px"});
    $("#login-input").focus(function(){
        zoomout();
    })
    $("#login-input").blur(function(){
        zoomin();
    })
})
var size = 1.0;

function zoomout() {
   size = size + 0.5;

   set();
 }

function zoomin() {
    size = size - 0.5;
    set();
}

function set() {
    document.body.style.cssText = document.body.style.cssText + '; -webkit-transform: scale(' + size + ');-webkit-transform-origin: 0 0;';
}
```

#### 打开页面，直接跳转到百度

```
window.onload = function(){
    // window.location.href = "http://baidu.com";
    location.href = "http://baidu.com";
}
```

#### 动态追加script脚本或js文件

```
function loadScript (url) {
    loadScript.mark = 'load';
    var script = document.createElement("script");
    script.type = "type/javascript";
    script.src = url;
    document.body.appendChild(script);
}

// loadScript ("js/jquery.min.js");
// console.log(loadScript.mark);

var btn = document.getElementById('btn');
btn.onclick = function () {
    if(loadScript.mark != 'load') {
        loadScript("js/script.js");
    }
}
```

#### 打开一个新的浏览器窗口

[菜鸟教程](https://www.runoob.com/jsref/met-win-open.html)

```
<button onclick="openwindow()">创建窗口</button>
```

```
var w = window;
function openwindow(){
    w.open('http://www.runoob.com','菜鸟教程', 'width=800,height=800');
    w.focus();
}
```

#### 捕获错误信息

```
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
```

#### 阻止事件冒泡

```
oSpan.onclick = function(e){
    // 阻止冒泡
    e = e || event;
    if(e.stopPropagation){
        e.stopPropagation();
    }else{
        e.cancelBubble = true;
    }
}
```

#### 使用定时器是为了让输入框上滑时更加自然-移动端

```
var bfscrolltop = document.body.scrollTop;
var interval;
$("input").focus(function(){
    interval = setInterval(function(){
    document.body.scrollTop = document.body.scrollHeight;
    },100)
}).blur(function(){
    clearInterval(interval);
    document.body.scrollTop = bfscrolltop;
});
```

#### jQuery插件扩展

#### 数组里的字符串转换成数字或者把数字转换成字符串

数字转字符串：

```
var arr = [1,2,3,4,5,6,7,8,9];
arr.map(String);   // 结果: ['1','2'，'3','4'，'5','6','7','8','9']
```

字符串转数字：

```
var a = ['1','2'，'3','4'，'5','6','7','8','9'];
a.map(Number);  // 结果:[1,2,3,4,5,6,7,8,9]
```

#### jquery获取第一个子节点元素

```
$("#body").children(":first")
```

#### [JS数组添加元素的三种方式](https://www.cnblogs.com/meng-ma-blogs/p/8352787.html)

1、push() 结尾添加

　　数组.push(元素)

| 参数        | 描述                             |
| ----------- | -------------------------------- |
| newelement1 | 必需。要添加到数组的第一个元素。 |
| newelement2 | 可选。要添加到数组的第二个元素。 |
| newelementX | 可选。可添加多个元素。           |

2、unshift() 头部添加

　　数组.unshift(元素)

| 参数        | 描述                           |
| ----------- | ------------------------------ |
| newelement1 | 必需。向数组添加的第一个元素。 |
| newelement2 | 可选。向数组添加的第二个元素。 |
| newelementX | 可选。可添加若干个元素。       |

3、splice() 方法向/从数组指定位置添加/删除项目，然后返回被删除的项目。

| 参数              | 描述                                                         |
| ----------------- | ------------------------------------------------------------ |
| index             | 必需。整数，规定添加/删除项目的位置，使用负数可从数组结尾处规定位置。 |
| howmany           | 必需。要删除的项目数量。如果设置为 0，则不会删除项目。       |
| item1, ..., itemX | 可选。向数组添加的新项目。                                   |

获取URL指定参数值（js/vue)

[参考博客](https://www.cnblogs.com/linjiangxian/p/11466087.html)

```
function getParam(name) {
    var reg = new RegExp("(^|&)" + name + "=([^&]*)(&|$)");
    var r = window.location.search.substr(1).match(reg);
    if (r != null) return unescape(r[2]);
    return null;
}
```

#### $.each

[jQuery中$.each的用法详解！](https://blog.csdn.net/u010786902/article/details/50954002)

[jquery中$each()方法的使用指南](https://www.jb51.net/article/65215.htm)



**Vue中**

方法一:

```
this.$route.query.xxx  //只要是在url里用?拼接的都可以
```

方法二:

```
getParam function(paramName) { 
    return decodeURIComponent((new RegExp('[?|&]' +
      paramName + '=' + '([^&;]+?)(&|#|;|$)').exec(location.href) || [, ""])[1].replace(/\+/g, '%20')) || null
}
```

[模糊搜索](https://github.com/Stevenzwzhai/plugs)

#### 处理移动端点击延迟

[移动端web开发，click touch tap区别](https://blog.csdn.net/sly94/article/details/51701188)

[移动端WEB开发，click,touch,tap事件浅析](https://www.xuebuyuan.com/2174858.html)



[JS 插件 fastclick.js 解决手机端click点击延迟](http://www.bubuko.com/infodetail-1015581.html)

对于非移动浏览器不启作用，禁用缩放标签。



#### call和 apply

[web开发JS调用打印机打印Web页面](https://blog.csdn.net/u010670689/article/details/9065903)

[JS实现浏览器打印、打印预览示例](https://www.jb51.net/article/106915.htm)



#### 原生JS获取元素焦点

```
document.getElementById(id).focus();
```

#### 获取今天，昨天，明天日期

自己写的函数

```
/**
// 获取日期函数
@param days 时间间隔天数
       -1：昨天
        0: 今天
        1：明天
@param symbol 年月日之间的分隔符
*/
function getDateFun(days, symbol){
    // 当前时间
    var now = new Date();
    var date = now.setDate(now.getDate() + days);
    
    // 格式化日期
    function format(t) {
        var year = t.getFullYear();     // 年份
        var month = t.getMonth() + 1;   // 月份
        month = month < 10 ? "0" + month : month;
        var date = t.getDate();         // 日
        date = date < 10 ? "0" + date : date;

        return year + symbol + month + symbol + date;
    }

    // 返回格式化后的日期
    return format(new Date(date));
}
```

#### 判断数组中是否存在某值

```
//  arr数组   value需判断的元素
function isInArray(arr, value) {
    for (var i = 0; i < arr.length; i++) {
        if (value === arr[i]) {
            return true;
        }
    }

    return false;
}
```

#### 数组对象减去某值

```
function removeValue(arr, val) {
    for (var i = 0; i < arr.length; i++) {
        if (arr[i] == val) {
            arr.splice(i, 1);
            break;
        }
    }
}
```

#### [LayUI + js实现全选、多选、翻页勾选（LayUI数据表格 方法渲染 模式）](https://www.cnblogs.com/java-hui/p/12170230.html)



[JavaScript单例模式](https://zhuanlan.zhihu.com/p/113456049)

[JavaScript中常见的十五种设计模式](https://www.cnblogs.com/imwtr/p/9451129.html)



[JavaScript 函数 Apply](https://www.w3school.com.cn/js/js_function_apply.asp)

[JavaScript constructor 属性](https://www.w3school.com.cn/jsref/jsref_constructor_array.asp)



##### 判断元素显示/隐藏，然后显示隐藏元素

```
function toggleMask() {
    var mask = $(".main-mask");
    if(mask.is(":hidden")) {
        mask.show();
    } else {
        mask.hide();
    }
}
```

[js的内联和外部调用](https://www.cnblogs.com/ivuu/p/7136408.html)



#### 监听手动刷新事件

```
// 监听刷新页面事件方法
window.onbeforeunload = function(event){
    removeItem("formData");
};
```

#### [JS如何在数组指定位置插入元素](https://www.jb51.net/article/182300.htm)

```
// 在数组指定位置插入
var fruits = ["Banana", "Orange", "Apple", "Mango"];
fruits.splice(2, 0, "Lemon", "Kiwi");
// 输出结果
// Banana, Orange, Lemon, Kiwi, Apple, Mango
```

##### 阻止事件冒泡

```
window.event? window.event.cancelBubble = true : e.stopPropagation();
```

[JS阻止冒泡和取消默认事件(默认行为)](http://caibaojian.com/javascript-stoppropagation-preventdefault.html)

当需要停止冒泡行为时，可以使用

```
function stopBubble(e) { 
//如果提供了事件对象，则这是一个非IE浏览器 
if ( e && e.stopPropagation ) 
    //因此它支持W3C的stopPropagation()方法 
    e.stopPropagation(); 
else 
    //否则，我们需要使用IE的方式来取消事件冒泡 
    window.event.cancelBubble = true; 
}
```

当需要阻止默认行为时，可以使用

```
//阻止浏览器的默认行为 
function stopDefault( e ) { 
    //阻止默认浏览器动作(W3C) 
    if ( e && e.preventDefault ) 
        e.preventDefault(); 
    //IE中阻止函数器默认动作的方式 
    else 
        window.event.returnValue = false; 
    return false; 
}
```

#### [JS 删除数组中某个元素的几种方式](https://blog.csdn.net/Li_dengke/article/details/105249837)

#### 删除数组最后两个元素

```
arr.slice(0, -2)
```

#### 删除数组最后一个元素

```
arr.slice(0, -1)
```

```
arr.pop()
```



#### 瀑布流的实现

[pinterest](https://www.pinterest.com/)

#### JQuery动态添加元素方法

| append()       | 在父级最后追加一个子元素                 |
| -------------- | ---------------------------------------- |
| appendTo()     | 在父级最后追加一个子元素                 |
| prepend()      | 在父级最前面追加一个子元素               |
| prependTo()    | 在父级最前面追加一个子元素               |
| after()        | 在当前元素之后追加（是同级关系）         |
| before()       | 在当前元素之前追加（是同级关系）         |
| insertAfter()  | 将元素追加到指定对象的后面（是同级关系   |
| insertBefore() | 将元素追加到指定对象的前面（是同级关系） |
| appendChild()  | 在节点的最后追加子元素                   |

#### 监听动态生成的元素

```
// 监听下拉框改变事件
$(".singleGame").on("change", "select.game-select", function () {
	.....
})
```



#### JS高级进阶（作用域，闭包，递归，this关键字）

```
//理解闭包
function setup(x) {
    var i =0 ;
    return function() {
        console.log(i);
        return x[i++];
    }
}

var next = setup(['a', 'b', 'c']);
console.log(next());    //i 输出 0  返回 a
console.log(next());    //i 输出 1  返回 b
console.log(next());    //i 输出 2  返回 c

//自调用
var fun = (function setup(x) {
    var i =0 ;
    return function() {
        console.log(i);
        return x[i++];
    }
}(['a', 'b', 'c']));   //传参

console.log(fun);   //输出返回的函数体
console.log(fun()); //i 输出 0  返回 a

//递归  自己调自己   (用递归很容易写成死循环)
function fact(num) {
    if(num <= 1) {
        return 1;
    }else{
        return num * fact(num - 1);
        // 执行过程：
        // 4*f(3);
        // 4*3*f(2);
        // 4*3*2*f(1);
        // 4*3*2*1;
    }
}

console.log(fact(4));   //24
```

