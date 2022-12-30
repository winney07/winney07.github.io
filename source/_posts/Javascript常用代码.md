---
title: Javascript常用代码
date: 2018-03-20 05:28:46
tags:
- Javascript
---

在谷歌浏览器控制台（console）中，编写多行代码时，实现换行的快捷键：`shift + 回车`

谷歌浏览器全局搜索关键字：`alt + shift + f`

#### 日期时间Date的处理

```
var d = new Date();
var n = d.toLocaleDateString();    // 2020/10/11
var n = d.toLocaleString(); 	  	  // 2020/10/11 15:53:22
var n = d.toLocaleTimeString(); 	  // 15:53:22
```

#### jQuery获取动态生成的元素

[jQuery获取动态生成的元素示例](https://www.jb51.net/article/51085.htm)

[jquery获取动态生成的元素](https://blog.csdn.net/h_025/article/details/51821766)

```
$(".button").live("click",function(){ 
     console.info($("#mytd").html()); 
}) 
```

```
$("td").on("focus","input",function(){
    alert("niha");
});
```

#### 返回上一页

```
href="javascript:window.history.back(-1);"
```

#### window.onload

当需要获取页面中的元素时，如果这script放在元素的前面，那么需要加window.onload；如果script放在元素后面，就不需要加window.onload。

```
// 回到顶部
window.onscroll = function(){
    if (document.documentElement.scrollTop || document.body.scrollTop > 0) {
        document.getElementById("toTop").style.display='block';
    }else{
        document.getElementById("toTop").style.display='none';
    }
}

document.getElementById("toTop").onclick = function(){
    document.body.scrollTop = document.documentElement.scrollTop = 0;
    document.getElementById("toTop").style.display = "none";
}
```

#### 原生ajax请求

```
$.ajax({
    type: 'POST',
    async:false,
    dataType: 'json',
    url: "http://api.qmgjs.weiduanxian.com:7000/account/registerVerifyCode.json?telMobile="+mobile+"&token="+tokenValue+"&resultCode="+postResultCode,
    success: function(data){
      if(data.code == '0'){
           //做处理，如果正确
          toastShow();
          $(".toast_content").text("验证码已发送，请查收！");

      }else{
           errorShow();
           $("#error").text(data.errMsg);
      }
    },
    error: function(data) {
       errorShow();
       $("#error").text(data.errMsg);
    }
});
```

#### 自动执行的函数

```
;(function(){
  var a;
})();
```

#### 追加列表

```
var template="",wqListLen,strHtml="";//整个列表的html内容，单个li的内容
var area = document.getElementById('ssq_list');//往期列表的盒子
for(var i=0;i < wqListLen;i++){
    strHtml+= '<li><span>第'+wqList[i].issue+'期</span><span>'+wqList[i].time+'</span></li>';
}
template = template + strHtml; 
area.innerHTML = template;
```

#### 刷新页面

```
window.location.reload(); //刷新页面
```

#### 页面跳转

```
window.location.href="cashCoupon.html";
```

#### 是否允许页面滑动

例如：在弹出弹窗和蒙层的情况下，是否允许蒙层底下的页面滑动

```
 var mo=function(e){e.preventDefault();}; //默认事件
```

##### (1)允许滑动

```
document.body.style.overflow='';//出现滚动条
document.removeEventListener("touchmove",mo,false);  
```

##### (2)禁止滑动

```
document.body.style.overflow='hidden';        
document.addEventListener("touchmove",mo,false);//禁止页面滑动
```

#### 控制移动端显示倍数

可行：直接把maximum-scale改为一个放大倍数

```
<meta name="viewport" content="target-densitydpi=device-dpi, width=device-width, initial-scale=1.0, minimum-scale=1.0, maximum-scale=2.5, user-scalable=yes">
```

可参考：[JS制作手机端自适应缩放显示](https://www.jb51.net/article/67670.htm)

```
var _width = parseInt(window.screen.width);
var dpr =  parseInt(window.devicePixelRatio);
var scale = (_width/640)*dpr;
var ua = navigator.userAgent.toLowerCase();
var result = /android (\d+\.\d+)/.exec(ua);
if (result){
var version = parseFloat(result[1]);
if(version>2.3){
document.write('<meta name="viewport" content="width=device-width, initial-scale = '+scale+',minimum-scale = 1.0, maximum-scale = 3,user-scalable=yes, target-densitydpi=device-dpi">');
}else{
document.write('<meta name="viewport" content="width=640, target-densitydpi=device-dpi">');
}
} else {
document.write('<meta name="viewport" content="width=640, user-scalable=no, target-densitydpi=device-dpi">');
}
alert(dpr);
alert(scale);
```

#### 监听输入框是否有值，改变按钮的可用性和背景颜色

```
$('#tel').keyup(function () {
	var v = $('#tel').val();
	if (!v) {
		$('.telBtn').attr('disabled', true)
		$('.telBtn').css("background", "#abb2c1")
	} else {
		$('.telBtn').attr('disabled', false);
		$('.telBtn').css("background", "#0087e2");
	}
});
```

#### 输入框获取焦点，页面放大，解决方法：

[参考博客](http://www.qdfuns.com/notes/16438/5e38b8c6cf888c6f69adc98048d7836f.html)

#### 监听点击事件

```
<input type="text" id="text" />
<input type="button" id="btn" value="提交"/>
<script type="text/javascript">
       document.getElementById("btn").addEventListener("click", function(event){alert("请输入内容")}, false);
</script>
```

#### 设备判断：

```
var ua = navigator.userAgent.toLowerCase(); 
var browser = {
versions: function () {
   var u = navigator.userAgent, app = navigator.appVersion;
   return {//移动终端浏览器版本信息
       trident: u.indexOf('Trident') > -1, //IE内核
       presto: u.indexOf('Presto') > -1, //opera内核
       webKit: u.indexOf('AppleWebKit') > -1, //苹果、谷歌内核
       gecko: u.indexOf('Gecko') > -1 && u.indexOf('KHTML') == -1, //火狐内核
       mobile: !!u.match(/AppleWebKit.*Mobile.*/), //是否为移动终端
       ios: !!u.match(/\(i[^;]+;( U;)? CPU.+Mac OS X/), //ios终端
       android: u.indexOf('Android') > -1 || u.indexOf('Linux') > -1, //android终端或uc浏览器
       iPhone: u.indexOf('iPhone') > -1, //是否为iPhone或者QQHD浏览器
       iPad: u.indexOf('iPad') > -1, //是否iPad
       webApp: u.indexOf('Safari') == -1 //是否web应该程序，没有头部与底部
   };
}(),
language: (navigator.browserLanguage || navigator.language).toLowerCase()
}
```

#### 判断是否为移动端

```
var ua = navigator.userAgent;
var ipad = ua.match(/(iPad).*OS\s([\d_]+)/),
isIphone = !ipad && ua.match(/(iPhone\sOS)\s([\d_]+)/),
isAndroid = ua.match(/(Android)\s+([\d.]+)/),
isMobile = isIphone || isAndroid;
```

##### 判断是否为微信

```
function isWeiXin() {   
  var ua = window.navigator.userAgent.toLowerCase();
  // alert(ua);
  if (ua.match(/MicroMessenger/i) == 'micromessenger') {
      return true;
  }else{
      return false;
  }
}
```

##### 判断是否为PC端

```
function IsPC(){  
  var userAgentInfo = navigator.userAgent;  
  var Agents = new Array("Android", "iPhone", "SymbianOS", "Windows Phone", "iPad", "iPod");  
  var flag = true;  
  for (var v = 0; v < Agents.length; v++) {  
        if (userAgentInfo.indexOf(Agents[v]) > 0) { flag = false; break; }  
   }  
   return flag;  
} 
```

##### 是不是手机端

```
if(isMobile){
  if(isIphone){
          location.href = 'http://um0.cn/XbXW0';
  }else if(isAndroid){
          location.href = 'http://dl.fa.weiduanxian.com/downloads/guijsh-wd.apk';
   } 
}else{
    console.log("computer");
}
```

##### 是不是微信

```
if (isWeiXin()) {
  //跳转到中转页
  window.location="slide.html";
}else{
   // '不是微信
   if(isMobile){
        if(isIphone){
                location.href = 'http://um0.cn/XbXW0';
        }else if(isAndroid){
                 location.href = 'http://dl.fa.weiduanxian.com/downloads/guijsh-wd.apk';
        } 
   }else{
        console.log("computer");
   }
   // window.location = 'http://um0.cn/XbXW0';
   // window.location="http://weiduanxian.com/downloads/guijsh-wd.apk";
}
```

#### 截取url参数

```
function GetQueryString(name) {
    var reg = new RegExp("(^|&)" + name + "=([^&]*)(&|$)");
    var r = window.location.search.substr(1).match(reg);
    if(r != null) return unescape(r[2]);
    return null;
}
```

#### 截取url参数

```
function GetQueryString(name) {
    var reg = new RegExp("(^|&)" + name + "=([^&]*)(&|$)");
    var r = window.location.search.substr(1).match(reg);
    if(r != null) return decodeURIComponent(r[2]);
    return null;
}

var platform=GetQueryString('platform');
```

#### 修改页面Title

```
document.title = "第" + data.data.imgData.issue + "期图库" ;
```

#### 设置定时器

```
setTimeout("show()",1900);//1000为1秒钟,设置为1分钟。

setTimeout(function(){location.reload();},1000);
```

#### 动态生成的节点，触发点击事件

##### 移动端触屏点击要用：touchend

```
$(document).on('touchend','#rechargeList li',function(){
  $(this).addClass("cur").siblings().removeClass("cur");
  rechargeValue = $(this).data("money");
});
```

#### 设置电脑定时关机

```
shutdown -s -t 7200   // （两个小时后自动关机）
```

**Math.PI** 

```
3.141592653589793
```

#### 微信返回按钮监听函数

```
function pushHistory() { 
  var state = { 
      title: "title", 
      url: "#"
  }; 
  window.history.pushState(state, "title", "#"); 
} 
```

#### 微信处理返回按钮

```
pushHistory(); 
window.addEventListener("popstate", function(e) { 
    （这里写按了返回按钮之后，执行的事件）
例如：
     $("#couponNoUse").show();
}, false);
```

#### 捕捉页面错误信息

```
<input type="text" onclick="adlert('函数函数')" />

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

#### 监听手机输入框值变化的事件

```
$('#username').bind('input propertychange', function() {  
   $('#result').html($(this).val().length + ' characters');  
}); 
```

#### 判断对象是否为空对象

```
function isEmptyObject(obj) {
    if (obj.length != null && obj.length == 0) return false;
    if (Object.prototype.toString.apply(obj) !== '[object Object]') return false;
    for (var p in obj) if (obj.hasOwnProperty(p)) return false;
    return true
};
```

#### console.log()在IE浏览器的兼容模式下不可用

[关于console.log()在IE浏览器的兼容模式下不可用的问题](https://blog.csdn.net/escapeplan/article/details/55210495)

解决方法：

```
<script type="text/javascript">
    if(!window.console){
        window.console = {};
    }
    if(!window.console.log){
        window.console.log = function(msg){};
    }
</script>
```

#### JSON字符串与JSON对象之间的转换

[JS 处理JSON数据及javascript处理对象、JSON对象、hash对象、数组对象的方法](https://blog.csdn.net/chenxiaodan_danny/article/details/40656559)

```
var str1 = '{"name":"yangyanyi","age":"25"}';//JSON字符串
var str2 = {"name":"yangyanyi","age":"25"}//JSON对象
var str3 = eval('(' + str1 + ')');//JSON字符串转换为JSON对象
console.log(JSON.parse(str1));//JSON字符串转换为JSON对象
console.log(JSON.stringify(str2));//JSON对象转换为JSON字符串
```

#### 获取对象的长度

```
function countProperties (obj) {
    var count = 0;
    for (var property in obj) {
        if (Object.prototype.hasOwnProperty.call(obj, property)) {
            count++;
        }
    }
    return count;
}
```

#### for  in 

[javascript中的for in循环和for循环的使用](http://caibaojian.com/js-loop-for-in.html)

#### 将字符串反向排序

```
var message = "yangyanyi";
message.split('').reverse().join('');    //iynaygnay
```

#### [JavaScript获取页面宽度高度大全](https://www.cnblogs.com/wcg249165510/archive/2009/02/20/1394749.html)

网页可见区域宽：document.body.clientWidth

网页可见区域高：document.body.clientHeight

网页可见区域宽：document.body.offsetWidth(包括边线的宽)

网页可见区域高：document.body.offsetHeight(包括边线的宽)

网页正文全文宽：document.body.scrollWidth

网页正文全文高：document.body.scrollHeight

网页被卷去的高：document.body.scrollTop(IE7无效)

网页被卷去的左：document.body.scrollLeft(IE7无效)

网页被卷去的高：document.documentElement.scrollTop(IE7有效)

网页被卷去的左：document.documentElement.scrollLeft(IE7有效)

网页正文部分上：window.screenTop

网页正文部分左：window.screenLeft

屏幕分辨率的高：window.screen.height

屏幕分辨率的宽：window.screen.width

屏幕可用工作区高度：window.screen.availHeight

屏幕可用工作区宽度：window.screen.availWidth

相对于窗口左上角的X：window.event.clientX

相对于窗口左上角的Y：window.event.clientY

相对于整个页面的X：window.event.X

相对于整个页面的Y：window.event.Y

#### iOS移动端(H5)alert/confirm提示信息去除网址(URL)

[iOS移动端(H5)alert/confirm提示信息去除网址(URL)](https://www.jb51.net/article/97633.htm)

重写alert方法

```
window.alert = function(name){
  var iframe = document.createElement("IFRAME");
  iframe.style.display="none";
  iframe.setAttribute("src", 'data:text/plain,');
  document.documentElement.appendChild(iframe);
  window.frames[0].window.alert(name);
  iframe.parentNode.removeChild(iframe);
};
```

#### [js获取网页屏幕可见区域高度](http://qiaolevip.iteye.com/blog/2076034)

获取页面高度

```
var windowHeight =  document.documentElement.clientHeight;
console.log(windowHeight);
$('.content').css('height', (windowHeight- 80)+'px');
```

```
// 获取当前页面可视高度(注意，此处行到的是当前页面的可视高度，而不是浏览器的可视高度
function getClientHeight(){
    var clientEeight = 0 ;
    if(document.body.clientHeight && document.documentElement.clientHeight){
        clientHeight = Math.min(document.body.clientHeight, document.documentElement.clientHeight);
    }else{ 
        clientHeight = Math.max(document.body.clientHeight, document.documentElement.clientHeight) ;
    return clientHeight ;
}
```

```
// 加上这个就可以直接使用document.body.clientHeight

html, body{
	height:100%;
}
```

#### localStorage

1. localStorage是一个普通对象，任何对象的操作都适用。
2. localStorage对象的属性值只能是字符串。

方法：

```
localStorage.getItem(key):获取指定key本地存储的值
localStorage.setItem(key,value)：将value存储到key字段
localStorage.removeItem(key):删除指定key本地存储的值
```

```
添加键值对：localStorage.setItem(key,value)
获取键值：localStorage.getItem(key)
删除键值对：localStorage.removeItem(key)。
清除所有键值对：localStorage.clear()。
获取localStorage的属性名称（键名称）：localStorage.key(index)。
还有一个和普通对象不一样的属性length:
获取localStorage中保存的键值对的数量：localStorage.length。
```

#### 删除对象属性

```
delete localObj.username;//删除属性
```

[关于给javascript对象添加、删除、修改对象的属性](https://www.cnblogs.com/goweb/p/5357640.html)

#### IE浏览器  点击事件不生效

当按F12有点击有反应的时候，查一下代码中有没有console.log()的代码，因为ie没有这个方法。

#### 点击动态生成的元素

##### 使用on.()   要阻止冒泡事件

![动态生成元素](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/Javascript%E5%B8%B8%E7%94%A8%E4%BB%A3%E7%A0%81/%E7%82%B9%E5%87%BB%E5%90%8E%E6%9C%9F%E7%94%9F%E6%88%90%E5%85%83%E7%B4%A0.png)

#### [浏览器的重绘与重排](https://www.cnblogs.com/gyjWEB/p/4547140.html)

将需要多次重排的元素，position属性设为absolute或fixed

#### ajax请求

```
/**
 * HTTP请求
 * 
 * @param url
 * @param data
 * @param type
 * @param async
 * @returns
 */
function http_request(url, data, type, async, dataType) {
    // 默认能数
    async = (async ? async : false);
    data = (data ? data : '');
    type = (type ? type : 'POST');
    dataType = (dataType ? dataType : 'JSON');

    var result;
    $.ajax({
        'url' : url,
        'type' : type,
        'data' : data,
        'async' : async,
        'dataType' : dataType,
        'success' : function(res) {
            result = res;
        }
    });
    return result;
}

/**
 * HTTP_GET
 * 
 * @param url
 * @param data
 * @param async
 * @returns
 */
function http_get(url, data, async) {
    return http_request(url, data, 'GET', async, 'JSON');
}

/**
 * HTTP_POST
 * 
 * @param url
 * @param data
 * @param async
 * @returns
 */
function http_post(url, data, async) {
    return http_request(url, data, 'POST', async, 'JSON');
}
```

#### 获取字符串的首字母

```
str.charAt(0)
str.substr(0, 1)
```

#### 获取字符串的末字母

```
str.charAt(str.length - 1)
```

#### 获取汉字首字母

[JS获取中文拼音首字母，并通过拼音首字母快速查找页面内的中文内容](https://blog.csdn.net/testcs_dn/article/details/25116655)

#### F12审核元素，搜索全部文件有没有某字符

 快捷键 ：`ctrl +shift +F`

#### 用[QQ](https://www.baidu.com/s?wd=QQ&tn=44039180_cpr&fenlei=mv6quAkxTZn0IZRqIHckPjm4nH00T1dWuhRLryn3ny7-ujNbPH010ZwV5Hcvrjm3rH6sPfKWUMw85HfYnjn4nH6sgvPsT6K1TL0qnfK1TL0z5HD0IgF_5y9YIZ0lQzqlpA-bmyt8mh7GuZR8mvqVQL7dugPYpyq8Q1RzP1TLPjT1n6)登录

```
<meta property="qc:admins" content="2432050734660161756375" />
```

> 这个是让网站加入[QQ](https://www.baidu.com/s?wd=QQ&tn=44039180_cpr&fenlei=mv6quAkxTZn0IZRqIHckPjm4nH00T1dWuhRLryn3ny7-ujNbPH010ZwV5Hcvrjm3rH6sPfKWUMw85HfYnjn4nH6sgvPsT6K1TL0qnfK1TL0z5HD0IgF_5y9YIZ0lQzqlpA-bmyt8mh7GuZR8mvqVQL7dugPYpyq8Q1RzP1TLPjT1n6)登录接口，这段代码可放在之间。
>
> 申请腾讯接口后，会得到这样的代码，加入接口之后，你的网站上面的注册登录功能，别人可以直接用[QQ](https://www.baidu.com/s?wd=QQ&tn=44039180_cpr&fenlei=mv6quAkxTZn0IZRqIHckPjm4nH00T1dWuhRLryn3ny7-ujNbPH010ZwV5Hcvrjm3rH6sPfKWUMw85HfYnjn4nH6sgvPsT6K1TL0qnfK1TL0z5HD0IgF_5y9YIZ0lQzqlpA-bmyt8mh7GuZR8mvqVQL7dugPYpyq8Q1RzP1TLPjT1n6)登录，省去注册的麻烦。

#### 去除字符串两端的空白字符

```
$.trim( str )
```

#### [previousSibling、previousElementSibling的区别](https://blog.csdn.net/sunlizhen/article/details/73437102)

previousSibling：获取元素的上一个兄弟节点；（既包含元素节点、文本节点、注释节点）；

previousElementSibling：获取上一个兄弟元素节点；（只包含元素节点）；

#### 解决ios软键盘弹起遮盖住底部输入框的问题

解决ios软键盘弹起遮盖住底部输入框的问题（终极解决方案！！！绝对好用）

```
<div class="layout_flex">
    <!-- 头部 -->
    <div class="header">header</div>
    <!-- 中间内容区域 -->
    <div class="content" id="content">
        <div class="dataList">
            <ul>
                <li>数据趋势图/数据列表均调用此接口</li>
                <li>数据趋势图/数据列表均调用此接口</li>
                <li>数据趋势图/数据列表均调用此接口</li>
            </ul>
        </div>
    </div>
    <!-- 底部输入框部 -->
    <div class="footer">
        <div class="foter"><input type="text" name=""/></div>
        <div class="fcont">使用定时器是为了让输入框上滑时更加自然</div>
    </div>
</div>

css样式

/*flex布局*/
html, body{height:100%;}
.layout_flex{display:-webkit-box;-webkit-box-orient:vertical;height:100%;}
.layout_flex .content{-webkit-box-flex:1;overflow:auto;-webkit-overflow-scrolling:touch;position:relative;height:100%;}

/*头部*/
.header{height: 5rem;background-color: red;font-size: 2rem;line-height: 5rem;color: #fff;}

/*底部评论框*/
.footer{background-color: green;font-size: 2rem;color: #fff;padding: 0 1rem;}
.foter{padding: 1rem 0;}
.foter input{width: 100%;height: 3rem;line-height: 3rem;text-indent: 1rem;}
.content{background-color: yellow;}
.fcont{height: 2rem;line-height: 2rem;color: #fff;font-size: 1rem;}

js代码(可以不使用js)

var bfscrolltop = document.body.scrollTop;
$("input").focus(function(){
    interval = setInterval(function(){
    document.body.scrollTop = document.body.scrollHeight;
    },100)
}).blur(function(){
    clearInterval(interval);
    document.body.scrollTop = bfscrolltop;
});
```

#### 动态改变和获取input的checked属性值

pop()方法

#### 搜索匹配，keyup事件

##### 中文输入时，要等输入法按确定之后才匹配

[**compositionstart** ](https://developer.mozilla.org/zh-CN/docs/Web/Events/compositionstart)

[**compositionend**](https://developer.mozilla.org/zh-CN/docs/Web/Events/compositionend)

![keyup](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/Javascript%E5%B8%B8%E7%94%A8%E4%BB%A3%E7%A0%81/keyup.png)



#### 获取url的参数

```
function parseParams(url){
    if( url == undefined){
        url = window.location.href;
    }   
    var indexOfQ = url.indexOf('?');
    if( indexOfQ == -1){
        return {}; 
    }   
    var search = url.slice(indexOfQ + 1); 
    var hashes = search.split('&');
    var params = {};
    for(var i = 0; i < hashes.length; i++){
        var hash = hashes[i].split('=', 2); 
        if ( hash.length == 1){ 
            params[hash[0]] = ''; 
        } else {
            params[hash[0]] = decodeURIComponent(hash[1]).replace(/\+/g, " ");
        } 
    }
    return params;
}



function getParam(key){
    var params = parseParams();
    return params[key];
}
```

#### 设备判断

```
var ua = navigator.userAgent.toLowerCase(); 
// 设备判断
var browser = {
   versions: function () {
       var u = navigator.userAgent, app = navigator.appVersion;
       return {//移动终端浏览器版本信息
           trident: u.indexOf('Trident') > -1, //IE内核
           presto: u.indexOf('Presto') > -1, //opera内核
           webKit: u.indexOf('AppleWebKit') > -1, //苹果、谷歌内核
           gecko: u.indexOf('Gecko') > -1 && u.indexOf('KHTML') == -1, //火狐内核
           mobile: !!u.match(/AppleWebKit.*Mobile.*/), //是否为移动终端
           ios: !!u.match(/\(i[^;]+;( U;)? CPU.+Mac OS X/), //ios终端
           android: u.indexOf('Android') > -1 || u.indexOf('Linux') > -1, //android终端或uc浏览器
           iPhone: u.indexOf('iPhone') > -1, //是否为iPhone或者QQHD浏览器
           iPad: u.indexOf('iPad') > -1, //是否iPad
           webApp: u.indexOf('Safari') == -1 //是否web应该程序，没有头部与底部
       };
   }(),
   language: (navigator.browserLanguage || navigator.language).toLowerCase()
}
```

#### 显示弹窗时，禁止页面滚动

```
// 遮罩层
var tipIos = document.getElementById("tipIos");		//ios提示语
var tipAndroid = document.getElementById("tipAndroid");		//安卓提示语
var mask = document.getElementById("mask");		//透明度遮罩层
var mo=function(e){e.preventDefault();};		//默认事件

// 显示遮罩层和提示语
function showMask(){
    mask.style.display="block";		//透明度遮罩层
    document.body.style.overflow='hidden';		//溢出隐藏        
    document.addEventListener("touchmove",mo,false);		//禁止页面滑动
    //根据不同平台显示不同提示语
    if(navigator.userAgent.match(/(iPhone|iPod|iPad);?/i)){
        tipIos.style.display="block";
        
    }else if(navigator.userAgent.match(/android/i)){
        tipAndroid.style.display="block";
    }

}
// 隐藏遮罩层和提示语
function hide(){
  tipIos.style.display="none";
  tipAndroid.style.display="none";
  mask.style.display="none";
  document.body.style.overflow='';		//出现滚动条
  document.removeEventListener("touchmove",mo,false);  
}
```

#### 错误提示

```
// 提示信息
function errorShow(){
   document.getElementById("error").style.display="block";
   window.setTimeout(function() {
        document.getElementById("error").style.display="none";
   },2500)
   
}
```

#### 打开App/安装App

```
   // 打开APP/安装APP
function openApp(){
    if (ua.match(/MicroMessenger/i) == "micromessenger") {	//微信
        showMask();	 //显示提示语
    }else if(ua.match(/WeiBo/i) == "weibo"){//微博
        showMask();	 //显示提示语
    }else if(browser.versions.ios){//ios浏览器
        window.location.href = "quanminguijinshu://";//ios app协议
        window.setTimeout(function() {
            window.location.href = "https://itunes.apple.com/cn/app/***?mt=8";//ios下载链
        },2000)
        document.getElementById("error").innerHTML="正在尝试打开APP";
        errorShow();    //提示信息
    }else if(browser.versions.android){//安卓浏览器
       // window.location.href = "myapp://xxx/openwith?data=mydata";//android app协议
        window.location.href = "myapp1://xxx/openwith1?data=mydata";//android app协议
        document.getElementById("error").innerHTML="正在尝试打开APP";
        errorShow();    //提示信息
        window.setTimeout(function() {
            document.getElementById("error").innerHTML="您还没下载我们的APP";
            errorShow();
        }, 3500)
        window.setTimeout(function() {
           window.location.href = "http://***/downloads/qmgjsh_wd.apk";	//android下载地址
       },4000)    
    }else{	//PC端
        document.getElementById("btn1").href="http://***";	//跳转官网
       	document.getElementById("btn3").href="http://***";	//跳官网页面
		document.getElementById("footer").href="http://***";	//跳官网页面
        document.getElementById("btn-logo").href="http://***";	//跳官网页面
     // document.getElementById("btn3").href="eia1013.html?platform=else";	//跳初请页面
    }
} 
```

```
// 获取参数platform的值
function getPlatform(){
    var params = parseParams();
    var platform = params.platform;
    return platform;
}

//platform的值
var platform = getPlatform();
// 活动页面分享之后
if(platform =="else"){
   //  document.getElementById("btn3").href="adp1102.html?platform=else";//跳初请页面
    //分享TOP小弹窗
     document.getElementById("TopBer").style.display="block";   //document.getElementById("Oa").style.paddingBottom="1.4rem"; 
    if(browser.versions.ios){
        document.getElementById("btn1").href="javascript:;";
        if(ua.match(/QQ/i) == "qq"){
           document.getElementById("btn1").href="quanminguijinshu://";
        }
        document.getElementById("btn3").href="javascript:;";
        if(ua.match(/QQ/i) == "qq"){
           document.getElementById("btn3").href="quanminguijinshu://";
        } 
		document.getElementById("footer").href="javascript:;";
        if(ua.match(/QQ/i) == "qq"){
           document.getElementById("footer").href="quanminguijinshu://";
        }
        document.getElementById("btn-logo").href="javascript:;";
        if(ua.match(/QQ/i) == "qq"){
           document.getElementById("btn-logo").href="quanminguijinshu://";
        }
    }
    if(browser.versions.android){
       document.getElementById("btn").href="javascript:;";
       document.getElementById("btn2").href="javascript:;";
     //   document.getElementById("btn-logo").href="javascript:;";
    }
    //点击按钮时触发打开APP/安装APP
    document.getElementById("btn1").onclick = function(){
        openApp();
    }
    document.getElementById("btn3").onclick = function(){
        openApp();
    }
    document.getElementById("footer").onclick = function(){
        openApp();
    };
	document.getElementById("btn-logo").onclick = function(){
        openApp();
    }
}else{//在平台内
   document.getElementById("btn1").href="open_index=cz";//跳交易页面
    document.getElementById("btn3").href="open_index=3";//跳直播间页面
	document.getElementById("footer").href="open_index=3";//跳直播间页面
 //  document.getElementById("btn-logo").href="open_index=3";//跳直播间页面
 //  document.getElementById("btn3").href="adp1102.html";//跳初请页面
}
```

#### 判断是否为微信

```
// 判断是否为微信
function isWechat(){
    var ua = navigator.userAgent.toLowerCase();
    return ua.indexOf('micromessenger') != -1;
}
```

#### 判断是否为iPhone

```
// 判断是否为iPhone
function isIphone(){
    var ua = navigator.userAgent.toLowerCase();

    var params = parseParams();
    var channel_id = params.channel_id;
   
    if(channel_id == '9ff9' || channel_id == '9ff8'){
        return true;
    }

    return ua.indexOf('iphone') != -1 || ua.indexOf('ipad') != -1;
}
```

#### 判断是否为PC端

```
// 判断是否为PC端
function isPC() {
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



#### 添加雪花动画

```
<style>
    body{background-color: #999;}
</style>

<canvas id="canvas"></canvas>

//添加雪花动画
//canvas init
var canvas = document.getElementById("canvas");
var ctx = canvas.getContext("2d");

//canvas dimensions
var W = window.innerWidth;
var H = window.innerHeight;
canvas.width = W;
canvas.height = H;

//snowflake particles
var mp = 60; //max particles
var particles = [];
for(var i = 0; i < mp; i++)
{
particles.push({
  x: Math.random()*W, //x-coordinate
  y: Math.random()*H, //y-coordinate
  r: Math.random()*4+1, //radius
  d: Math.random()*mp //density
})
}

//Lets draw the flakes
function draw()
{
ctx.clearRect(0, 0, W, H);

ctx.fillStyle = "rgba(255, 255, 255, 0.6)";
ctx.strokeStyle = 'rgba(255, 255, 255, 0.4)';
ctx.lineWidth = '0.01';
ctx.beginPath();
for(var i = 0; i < mp; i++)
{
  var p = particles[i];
  ctx.moveTo(p.x, p.y);
  ctx.arc(p.x, p.y, p.r, 0, Math.PI*2, true);
}
ctx.fill();
ctx.stroke();
update();
}

//Function to move the snowflakes
//angle will be an ongoing incremental flag. Sin and Cos functions will be applied to it to create vertical and horizontal movements of the flakes
var angle = 0;
function update()
{
angle += 0.01;
for(var i = 0; i < mp; i++)
{
  var p = particles[i];
  //Updating X and Y coordinates
  //We will add 1 to the cos function to prevent negative values which will lead flakes to move upwards
  //Every particle has its own density which can be used to make the downward movement different for each flake
  //Lets make it more random by adding in the radius
  p.y += Math.cos(angle+p.d) + 1 + p.r/6;
  p.x += Math.sin(angle) * 2; 

  //Sending flakes back from the top when it exits
  //Lets make it a bit more organic and let flakes enter from the left and right also.
  if(p.x > W+5 || p.x < -5 || p.y > H)
  {
    if(i%3 > 0) //66.67% of the flakes
    {
      particles[i] = {x: Math.random()*W, y: -10, r: p.r, d: p.d};
    }
    else
    {
      //If the flake is exitting from the right
      if(Math.sin(angle) > 0)
      {
        //Enter from the left
        particles[i] = {x: -5, y: Math.random()*H, r: p.r, d: p.d};
      }
      else
      {
        //Enter from the right
        particles[i] = {x: W+5, y: Math.random()*H, r: p.r, d: p.d};
      }
    }
  }
}
}
//animation loop
setInterval(draw, 33);
```

