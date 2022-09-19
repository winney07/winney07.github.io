---
title: Javascript常用代码
date: 2018-03-20 05:28:46
tags:
- Javascript
---

在谷歌浏览器控制台（console）中，编写多行代码时，实现换行的快捷键：`shift + 回车`

谷歌浏览器全局搜索关键字：`alt + shift + f`

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

