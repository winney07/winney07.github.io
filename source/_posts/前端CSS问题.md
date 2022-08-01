---
title: 前端CSS问题
date: 2020-06-30 17:35:17
tags:
- css问题
categories: 
- 工作笔记
- css问题
---



[html页面在苹果手机内，safari浏览器，微信中滑动不流畅问题解决方案](https://www.cnblogs.com/autoXingJY/p/11576469.html)

[iPhone mobile safari fixed 元素滚动慢的问题处理](https://blog.csdn.net/weixin_30896511/article/details/98370605)

[html页面在苹果手机内，safari浏览器，微信中滑动不流畅问题解决方案](http://www.wjhsh.net/autoXingJY-p-11576469.html)



#### CSS控制字体自动转换成大写字母

```
text-transform: uppercase;
```



#### 修改滚动条样式

```
/* 滚动条样式 */
::-webkit-scrollbar{
  width: 2px;
  height: 5px;
  position: absolute;
}
::-webkit-scrollbar-thumb{
  background-color: #fff;
}
::-webkit-scrollbar-track{
  background-color: #001529;
}
```



##### html5 video在固定的宽度和高度内铺满

一般是视频的缩略图或者视频需要铺满我们固定的区域。
video ： poster是缩略图

```css
video{
    object-fit:fill;
}
```

https://developers.weixin.qq.com/community/develop/doc/0004403ab0c158af9f0adf1bd5b800

https://bbs.csdn.net/topics/392450329

https://blog.csdn.net/sepier/article/details/112780701



##### 隐藏video的全屏按钮

```
video::-webkit-media-controls-fullscreen-button {
    display: none;
}
```

##### video按全屏按钮后变形，因为只设置了宽度，要给video设置宽度和高度



#### [Chrome下面查看placeholder的样式](https://blog.csdn.net/weixin_30657999/article/details/95180171)

F12——>Settings——>Preferences——>Element——>Show user agent shadow DOM（将这个勾选上）

#### 浏览器默认滚动条默认样式

1. **火狐和IE浏览器不可以修改浏览器滚动条默认样式**，IE浏览器可以修改滚动条颜色，但不能修改宽度

2. 谷歌和360浏览器修改默认样式代码：

   ```
    /*滚动条样式*/
   ::-webkit-scrollbar {/*滚动条整体样式*/
     width: 2px;     /*高宽分别对应横竖滚动条的尺寸*/
     height: 2px;
   }
   ::-webkit-scrollbar-thumb {/*滚动条里面小方块*/
     border-radius: 5px;
     box-shadow: inset 0 0 5px rgba(0,0,0,0.2);
     background: rgba(0,0,0,0.2);
   }
   ::-webkit-scrollbar-track {/*滚动条里面轨道*/
     box-shadow: inset 0 0 5px rgba(0,0,0,0);
     border-radius: 0;
     background: rgba(0,0,0,0);
   }
   
   // 如果只修改某个盒子的滚动条：
   .box-name::-webkit-scrollbar{}
   .box-name::-webkit-scrollbar-thumb{}
   .box-name::-webkit-scrollbar-track{}
   ```

   

#### 获取已知元素的前一个元素

css不能实现，使用js

```
$("已知元素").prev("需要获取的元素")
$("#certify  .swiper-slide-prev").prev(".swiper-slide")
```

#### 获取已知元素的后一个元素，使用 +

```
#certify .swiper-slide.swiper-slide-next + .swiper-slide{
    transform: translateX(-986px) scale(0.6) !important;
}
```



#### safari浏览器下 input/select 表单的阴影

```
input{
	-webkit-appearance: none;
}
加上这个，单选/复选框按钮会不显示
select{
	-webkit-appearance: none;
}
```

### iPhone Safari浏览器字体放大 ——解决方法

```
text-size-adjust: 100%;
-webkit-text-size-adjust: 100%;
```
![iPhone Safari浏览器字体放大](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/%E5%89%8D%E7%AB%AFCSS%E9%97%AE%E9%A2%98/css1.png)

### 去除Safari浏览器下复选框和下拉框默认样式

```
select{
    -webkit-appearance: none;
}
```



### 表格中内容超出指定宽度隐藏，鼠标上移，在指定宽度内换行显示。（不需要js，css的hover解决）

##### 需要在td里面加上span等标签来限制宽度和溢出隐藏
```
table{
    margin: 0 auto;
    width: 30%;
    border: 1px solid #666;
    text-align: center;
    border-collapse:collapse;
}
th{
    height:40px;
    line-height: 40px;
}
td{
    height: 40px;
    line-height: 40px;
}
tr{
    border-bottom: 1px solid #666;
}

td span {
    display: inline-block;
    width:160px;
    white-space: nowrap;
    text-overflow: ellipsis;
    overflow: hidden;
    vertical-align: middle;
}
td span:hover {
    white-space: inherit;
    text-overflow: inherit;
    overflow: visible;
}


<table border="1">
    <th>姓名</th>
    <th>年龄</th>
    <th>简介</th>
    <tr>
        <td>羊羊羊</td>
        <td>25</td>
        <td >
            <span>
                79942 79942 79942 79942 79942 79942 79942 79942 79942 79942 79942 79942
            </span>
        </td>
    </tr>
</table>
```
##### 溢出隐藏：
![溢出隐藏](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/%E5%89%8D%E7%AB%AFCSS%E9%97%AE%E9%A2%98/css2.png)
##### 鼠标上移，换行显示全部内容：
![鼠标上移，换行显示全部内容](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/%E5%89%8D%E7%AB%AFCSS%E9%97%AE%E9%A2%98/css3.png)

### css3超出宽度自动换行以及超出宽度显示...
#### css3超出宽度自动换行，并且首行缩进2字符
```
div{
    text-indent: 2em;
    word-wrap: break-word;
    word-break: break-all;
}
```
#### 单行超出宽度显示...
```
div {
    text-overflow: ellipsis;
    white-space: nowrap;
    overflow: hidden;
}
```
#### 多行超出宽度显示...以及要求显示几行或者说根据文字多少显示几行
```
div {
    overflow: hidden;
    text-overflow: ellipsis;
    display: -webkit-box;
    -webkit-line-clamp: 2;  //控制显示几行
    -webkit-box-orient: vertical;   //webbox方向
}
```
#### CSS3强制英文、中文换行与不换行 强制英文换行
```
1. word-break:break-all;只对英文起作用，以字母作为换行依据
2. word-wrap:break-word; 只对英文起作用，以单词作为换行依据
3. white-space:pre-wrap; 只对中文起作用，强制换行
4. white-space:nowrap; 强制不换行，都起作用 
5. white-space:nowrap; overflow:hidden; text-overflow:ellipsis;不换行，超出部分隐藏且以省略号形式出现（部分浏览器支持）
```

#### input输入框禁止显示历史记录 
在输入input时会提示原来输入过的内容，还会出现下拉的历史记录，禁止这种情况(关闭自动提示)，只需在input中加入：
autocomplete="off"

```
<input type="text"  autocomplete="off" />
```
如果所有表单元素都不想使用自动提示功能，只需在表单form上设置autocomplete=off：

```
<form autocomplete="off"> 
<input type="text" name="name">
<input type="text" name="password"> 
</form>
```

[参考博客](https://blog.csdn.net/amao_aguai/article/details/83344455)

#### 【解决方案】去掉谷歌浏览器获取焦点时默认的input、textarea的边框和背景

1、使用Chrome的都知道，当鼠标焦点在input\textarea这些元素上时，Chrome默认的会给它们加上黄色的边框。 可以使用下面的css代码去掉所有元素的边框：

```
*:focus{outline:none;}
```

2、Chrome默认用户可以控制textarea的大小，在CSS中加入下面一句就可以了：

```
textarea {resize:none;}
```

#### 浏览器记住密码的情况下，解决密码输入框自动填充密码框（input type="password" 的问题）
```
用户名：<input type='text' autocomplete='off'>
密码：<input type='password' autocomplete="new-password" style="background-color: #fff!important;" readonly onfocus="this.removeAttribute('readonly');" onblur="this.setAttribute('readonly',true);">

```

#### 解决html页面英文和数字不自动换行，但中文就可以自动换行

![处理换行](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/%E5%89%8D%E7%AB%AFCSS%E9%97%AE%E9%A2%98/huanhang.png)

###### 解决方法：添加css属性word-break: break-all;

![word-break: break-all](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/%E5%89%8D%E7%AB%AFCSS%E9%97%AE%E9%A2%98/huanhang2.png)

#### 溢出的文字隐藏

```
white-space: nowrap;
text-overflow: ellipsis;
overflow: hidden;
```

#### 溢出文字省略号显示

```
.content{
    /* display:block; */
    width:200px;
    overflow: hidden;
    white-space: nowrap;
    text-overflow: ellipsis;
}
```

> 注：如果是表格元素，需要加上display:block;

处理IE浏览器：

```
(function($) { 
    $.fn.ellipsis = function(enableUpdating){ 
        var s = document.documentElement.style; 
        if (!('textOverflow' in s || 'OTextOverflow' in s)) { 
            return this.each(function(){ 
                var el = $(this); 
                if(el.css("overflow") == "hidden"){ 
                    var originalText = el.html(); 
                    var w = el.width(); 

                  var t = $(this.cloneNode(true)).hide().css({ 
                      'position': 'absolute', 
                      'width': 'auto', 
                      'overflow': 'visible', 
                      'max-width': 'inherit' 
                  }); 
                  el.after(t); 

                  var text = originalText; 
                  while(text.length > 0 && t.width() > el.width()){ 
                         text = text.substr(0, text.length - 1); 
                         t.html(text + "..."); 
                     } 
                     el.html(t.html()); 

                     t.remove(); 

                     if(enableUpdating == true){ 
                         var oldW = el.width(); 
                         setInterval(function(){ 
                             if(el.width() != oldW){ 
                                 oldW = el.width(); 
                                 el.html(originalText); 
                                 el.ellipsis(); 
                             } 
                         }, 200); 
                     } 
                 } 
             }); 
         } else return this; 
     }; 
 })(jQuery);
```

要调整placeholder属性的样式，如果在谷歌浏览器下审核不了placeholder

解决方法：

1. F12，打开控制台
2. 在控制台右上角，选择三个点（更多选项图标），选择“Settings"
3. 将Show user agent shadow DOM勾选上



#### 文本域(textarea)的提示文字(placeholder)换行显示

```
// 在需要换行的地方加上&#13;&#10;

placeholder="请输入微信APP支付参数，便于技术查看，涉及字段如下：&#13;&#10;微信支付商户号：&#13;&#10;商户Key：&#13;&#10;微信AppID：&#13;&#10;AppSecret:"
```

#### 修改placeholder样式

```
::-webkit-input-placeholder { /* Chrome/Opera/Safari */ 
	color: #ccc;
}
::-moz-placeholder { /* Firefox 19+ */  
	color: #ccc;
}
:-ms-input-placeholder { /* IE 10+ */ 
 color: #ccc;
}
:-moz-placeholder { /* Firefox 18- */ 
 color: #ccc;
}
```

#### textarea元素的placeholder属性不显示

> textarea的placeholder属性值不显示的原因可能是`<textarea>`与`</textarea>`之间存在空格或者换行

#### [placeholder兼容浏览器的解决方案](https://blog.csdn.net/xw505501936/article/details/52815876)

> 关于placeholder的使用，众所周知它是h5的新属性，所以IE9以下就别想用它了，不支持。 那么我们必须要低版本的浏览器，做一些降级处理的兼容，原理自然就是：提示语placeholder用其他方式替代显示咯。 以下是一小段兼容处理。 

代码如下：

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>welcome to ixiewei world</title>
    <style type="text/css">
        body{font:12px/1.5 "\5FAE\8F6F\96C5\9ED1","\9ED1\4F53",Helvetica,Tahoma,arial,sans-serif; margin:0 auto; color:#333;}
        p,ul,ol,dl,dt,dd,h1,h2,h3,h4,h5,h6,form,input,select,button,textarea,iframe{margin:0; padding:0;}
        .clearfix:after{content:".";display:block;height:0;clear: both;visibility:hidden;}
        .clearfix{*zoom:1;}
        .fl{ float:left;_display: inline}
        .pr{ position:relative}
        .abs{position:absolute;}
 
        /*placeholder字体颜色*/
        ::-webkit-input-placeholder { /* WebKit browsers */
            color:    #ccc;
        }
        :-moz-placeholder { /* Mozilla Firefox 4 to 18 */
            color:    #ccc;
        }
        ::-moz-placeholder { /* Mozilla Firefox 19+ */
            color:    #ccc;opacity:1
        }
        :-ms-input-placeholder { /* Internet Explorer 10+ */
            color:    #ccc !important;
        }
        input:-webkit-autofill { /* 谷歌浏览器-文本框边框阴影遮住了背景颜色浅黄*/
            -webkit-box-shadow: 0 0 0 1000px #ffffff inset !important;
        }
        .demod{width:440px;height:auto;background:#ffffff;padding-top:35px;position:relative;font-family:microsoft yahei}
        .demod .demodin{height:40px;margin:0 37px 20px;border:1px solid #d2d6e0}
        .demod .demodin .input_d{height:30px;margin:5px 0 0 0}
        .demod .demodin .input_d input{height:30px;line-height:30px;width:280px;border:0;font-size:14px;font-family:microsoft yahei;color:#333;outline: none}
        .demod .demodin .input_d label{height:30px;line-height:30px;width:280px;border:0;font-size:14px;font-family:microsoft yahei;color:#ccc;top:0;left:0;display:none}
        .demod{width:440px;height:auto;background:#ffffff;position:relative;font-family:microsoft yahei}
        .demod .demodin{height:40px;margin:0 37px 20px;border:1px solid #d2d6e0}
        .demod .demodin p{height:16px;width:34px;border-right:1px solid #ddd;margin:13px 12px 0 0}
        .demod .demodin .input_d{height:30px;margin:5px 0 0 0}
        .demod .demodin .input_d input{height:30px;line-height:30px;width:280px;border:0;font-size:14px;font-family:microsoft yahei;color:#333;outline: none}
        .demod .demodin .input_d label{height:30px;line-height:30px;width:280px;border:0;font-size:14px;font-family:microsoft yahei;color:#ccc;top:0;left:0;display:none}
        .demod .demodin .input_d_pwd input{width:240px}
        .demod .demodin .see_pwd_btn{display:block;top:10px;right:10px;cursor:pointer;height:22px}
        .demod .demodin .see_pwd_on{color:#00AA00}
    </style>
</head>
<body>
<!--demo示例-->
<div>
    <div class="demod">
        <div class="demodin clearfix pr">
            <div class="input_d fl">
                <input type="text" placeholder="请输入手机号" autocomplete="off"/>
            </div>
        </div>
        <div class="demodin clearfix pr">
            <div class="input_d fl pr">
                <label class="abs"></label>
                <input type="password" placeholder="请输入密码" autocomplete="new-password"/>
            </div>
        </div>
        <div class="demodin clearfix pr">
            <div class="input_d input_d_pwd fl pr">
                <label class="abs"></label>
                <input type="password" placeholder="请输入密码2" autocomplete="new-password" class="ch_reg_pwd"/>
            </div>
            <div class="see_pwd_btn abs">查看密码</div>
        </div>
    </div>
</div>
<script type="text/javascript" src="/js/jquery-1.7.2.min.js"></script>
<script type="text/javascript">
    $(function () {
        //兼容不支持placeholder的浏览器[ie浏览器，并且10以下均采用替代方式处理]
        if ((navigator.appName == "Microsoft Internet Explorer") && (document.documentMode < 10 || document.documentMode == undefined)) {
            var $placeholder = $("input[placeholder]");
            for (var i = 0; i < $placeholder.length; i++) {
                if ($placeholder.eq(i).attr("type") == "password") {
                    $placeholder.eq(i).siblings("label").text($placeholder.eq(i).attr("placeholder")).show()
                } else {
                    $placeholder.eq(i).val($placeholder.eq(i).attr("placeholder")).css({"color": "#ccc"})
                }
            }
            $placeholder.focus(function () {
                if ($(this).attr("type") == "password") {
                    $(this).siblings("label").hide()
                } else {
                    if ($(this).val() == $(this).attr("placeholder")) {
                        $(this).val("").css({"color": "#333"})
                    }
                }
            }).blur(function () {
                if ($(this).attr("type") == "password") {
                    if ($(this).val() == "") {
                        $(this).siblings("label").text($(this).attr("placeholder")).show()
                    }
                } else {
                    if ($(this).val() == "") {
                        $(this).val($(this).attr("placeholder")).css({"color": "#ccc"})
                    }
                }
            });
            $(".clone_input_text").live("focus", function () {
                $(this).siblings("label").hide()
            }).live("blur", function () {
                if ($(this).val() == "") {
                    $(this).siblings("label").text($(this).attr("placeholder")).show()
                }
            });
            $placeholder.siblings("label").click(function () {
                if ($(this).parent("div").siblings(".see_pwd_btn").attr("data-flag") == "1") {
                    $(this).hide().next("input").next("input").focus()
                } else {
                    $(this).hide().next("input").focus()
                }
            })
        }
 
        //可视密码
        $(".see_pwd_btn").click(function() {
            var obj=$(this);
            var ch_reg_pwd = $(".ch_reg_pwd");
            if (obj.attr("data-flag") != 1) {
                var clone_input = '<input type="text" class="clone_input_text" placeholder="'+ ch_reg_pwd.attr("placeholder") + '" value="' + ch_reg_pwd.val() + '"/>';
                ch_reg_pwd.after(clone_input);
                ch_reg_pwd.hide();
                obj.addClass("see_pwd_on").attr("data-flag", 1);
            } else {
                ch_reg_pwd.val($(".clone_input_text").val()).show();
                $(".clone_input_text").remove();
                obj.removeClass("see_pwd_on").attr("data-flag", "");
            }
        });
    });
</script>
</body>
</html>
```

##### [HTML5 INPUT placeholder及兼容性处理](https://www.cnblogs.com/dachie/archive/2012/08/10/2632422.html)

```
HTML5对Web Form做了许多增强，比如input新增的type类型、Form Validation等。Placeholder是HTML5新增的另一个属性，当input或者textarea设置了该属性后，该值的内容将作为灰字提示显示在文本框中，当文本框获得焦点时，提示文字消失。以前要实现这效果都是用JavaScript来控制才能实现： 
请输入文字
由于placeholder是个新增属性，目前只有少数浏览器支持，如何检测浏览器是否支持它呢？(更多HTML5/CSS3特性检测可以访问)

function hasPlaceholderSupport() {
  return 'placeholder' in document.createElement('input');
}

默认提示文字是灰色的，可以通过CSS来改变文字样式：

 
/* all */
::-webkit-input-placeholder { color:#f00; }
input:-moz-placeholder { color:#f00; }
 
/* individual: webkit */
#field2::-webkit-input-placeholder { color:#00f; }
#field3::-webkit-input-placeholder { color:#090; background:lightgreen; text-transform:uppercase; }
#field4::-webkit-input-placeholder { font-style:italic; text-decoration:overline; letter-spacing:3px; color:#999; }
 
/* individual: mozilla */
#field2:-moz-placeholder { color:#00f; }
#field3:-moz-placeholder { color:#090; background:lightgreen; text-transform:uppercase; }
#field4:-moz-placeholder { font-style:italic; text-decoration:overline; letter-spacing:3px; color:#999; }
 

兼容其他不支持placeholder的浏览器：

var PlaceHolder = {
    _support: (function() {
        return 'placeholder' in document.createElement('input');
    })(),

    //提示文字的样式，需要在页面中其他位置定义
    className: 'abc',

    init: function() {
        if (!PlaceHolder._support) {
            //未对textarea处理，需要的自己加上
            var inputs = document.getElementsByTagName('input');
            PlaceHolder.create(inputs);
        }
    },

    create: function(inputs) {
        var input;
        if (!inputs.length) {
            inputs = [inputs];
        }
        for (var i = 0, length = inputs.length; i <length; i++) {
            input = inputs[i];
            if (!PlaceHolder._support && input.attributes && input.attributes.placeholder) {
                PlaceHolder._setValue(input);
                input.addEventListener('focus', function(e) {
                    if (this.value === this.attributes.placeholder.nodeValue) {
                        this.value = '';
                        this.className = '';
                    }
                }, false);
                input.addEventListener('blur', function(e) {
                    if (this.value === '') {
                        PlaceHolder._setValue(this);
                    }
                }, false);
            }
        }
    },

    _setValue: function(input) {
        input.value = input.attributes.placeholder.nodeValue;
        input.className = PlaceHolder.className;
    }
};

//页面初始化时对所有input做初始化
//PlaceHolder.init();
//或者单独设置某个元素
//PlaceHolder.create(document.getElementById('t1'));
```

#### [关于input标签和placeholder在IE8，9下的兼容问题](https://www.cnblogs.com/2010master/p/6194291.html)

```
一、input常用在表单的输入，包括text，password，H5后又新增了许多type属性值，如url, email, member等等，考虑到非现代浏览器的兼容性问题，这些新的type常用在移动端的项目中。

二、IE10+浏览器下，input标签会有一个默认的样式，比如文本框的‘×’号，密码框的小眼睛。初衷是好的，有时候很方便，但有时候我们会自己设置样式和功能。可以用伪元素方法去除： 

::-ms-clear, ::-ms-reveal{display: none;}
 
三、在低版本的IE下，input中的文字位置会改变（偏上显示），解决方法：（思路： 设置input的高度=行高）


input {
    height: 60px;
    line-height: 60px;
    margin: 0;
    padding: 0;
    outline: none;
}

四、实际中，我们会在input的前面用label标签或其他，提示input的内容信息。在IE下，在获得焦点、失去焦点时，label标签里的文字会出现抖动问题。解决方法：（设置input的显示方式为行内块）

input {
  display: inline-block;      
}

五、##placeholder是H5的一个新属性，但是在IE9以下是不支持的，为此我们会封装一个函数进行能力检测。　
参考地址：http://www.studyofnet.com/news/1022.html
###以下是代码部分：

 1 $(function() {
 2     // 如果不支持placeholder，用jQuery来完成
 3     if(!isSupportPlaceholder()) {
 4         // 遍历所有input对象, 除了密码框
 5         $('input').not("input[type='password']").each(
 6             function() {
 7                 var self = $(this);
 8                 var val = self.attr("placeholder");
 9                 input(self, val);
10             }
11         );
12 
13         /**
14          *  对password框的特殊处理
15          * 1.创建一个text框 
16          * 2.获取焦点和失去焦点的时候切换
17          */
18         $('input[type="password"]').each(
19             function() {
20                 var pwdField    = $(this);
21                 var pwdVal      = pwdField.attr('placeholder');
22                 var pwdId       = pwdField.attr('id');
23                 // 重命名该input的id为原id后跟1
24                 pwdField.after('<input id="' + pwdId +'1" type="text" value='+pwdVal+' autocomplete="off" />');
25                 var pwdPlaceholder = $('#' + pwdId + '1');
26                 pwdPlaceholder.show();
27                 pwdField.hide();
28 
29                 pwdPlaceholder.focus(function(){
30                     pwdPlaceholder.hide();
31                     pwdField.show();
32                     pwdField.focus();
33                 });
34 
35                 pwdField.blur(function(){
36                     if(pwdField.val() == '') {
37                         pwdPlaceholder.show();
38                         pwdField.hide();
39                     }
40                 });
41             }
42         );
43     }
44 });
45 
46 // 判断浏览器是否支持placeholder属性
47 function isSupportPlaceholder() {
48     var input = document.createElement('input');
49     return 'placeholder' in input;
50 }
51 
52 // jQuery替换placeholder的处理
53 function input(obj, val) {
54     var $input = obj;
55     var val = val;
56     $input.attr({value:val});
57     $input.focus(function() {
58         if ($input.val() == val) {
59             $(this).attr({value:""});
60         }
61     }).blur(function() {
62         if ($input.val() == "") {
63             $(this).attr({value:val});
64         }
65     });
66 }
```



#### 修改input type="file"按钮样式

html结构：

```
<div class="iconBtn">
	<span>上传子活动文件</span>
	<input class="inputFile" type="file" name="semfile">
</div>
```

css样式：

```
.iconBtn {
    position: relative;
    border: 1px solid #c9c9c9;
    border-radius: 3px;
    font-size: 12px;
    padding: 6px 10px 7px;
    color: #666;
    display: inline-block;
    cursor: pointer;
    background-color: #fbfbfb;
}
.inputFile {
    position: absolute;
    opacity: 0;
    filter: alpha(opacity=0);
    width: 100%;
    left: 0;
    top: 0;
    height: 100%;
    cursor: pointer;
}
```

#### 头部和底部固定定位，中间内容区滚动展示

```
<header class="head">顶部固定区域</header>

<article  class="main" id="wrapper">  
</article>

<footer class="foot">底部固定区域</footer>
```

```
.head,.foot{position:fixed;left:0;height:38px;line-height:38px;width:100%;background-color:#999;}

.head{top:0;}

.foot{bottom:0;}

.main{position:fixed;top:38px;bottom:38px;width:100%;overflow:scroll;background-color:#f2f2f2;}
```

#### 出现浮层时，禁止页面滚动

当浮层出现的时候∶

```
$('htm1').addc1ass("noscro1l');
```

当浮层隐藏的时候︰

```
$('htm1').removec1ass("noscro1l');
```

可以让一部分浏览器的窗体不能滚动，但不包括Safari等浏览器，怎么办呢?

我们可以在浮层`touchmove`的时候，阻止默认事件达到避免滚动的问题，例如︰

```
$('aside').on('touchmove', function(event){
	event.preventDefault();
});
```

这种处理兼容性强，效果最好，但是有一个问题，就是如果浮层自己也有滚动，那么这种处理会让浮层里面自己的滚动行为也无法触发，因此，我们的处理要更进一步，如下:

1. 当手指`touchstart`的元素不是滚动容器同时不失容器的子元素的时候，阻止默认行为;
2. 如果手指`touchstart`的元素是滚动容器或者容器子元素的时候，不阻止默认行为，但不包括滚动到容器边缘的时候。

根据上述原理，我自己抽象了一个简单的方法，方法名和语法如下，完整代码见这里：

```
$.smartscro11(container, selectorscro11able);
```



#### 选择倒数第n个元素

css3    :nth-last-child()选择器

规定属于其父元素的第二个子元素的每个p元素，从最后一个子元素开始计数∶

```
p:nth-last-child(2) {
	background: #fff;
}
```

#### Chrome提示框（弹窗）字体模糊

白己写的一个很简单的提示框弹窗，firefox , Safari , ie都清晰，但是chrome就惑觉很模糊

导致模糊的原因：在提示框样式中使用了transform、z-index样式有可能导致这个问题

> 例如： transform: translate(-50%, -50%); //让提示框垂直居中和水平居中
>
> 解决办法：弹窗提示框不使用transform来做垂直居中水平居中。
>
> 1，如果弹窗是大小固定的，可以使用：left:50%;top:50%; margin-left:-（弹窗宽度/2）px; margin-top:-（弹窗高度/2）px;
>
> 2，如果弹窗大小不固定；可以使用js获取弹窗高度和高度，然后按照1方法中的方式，让盒子居中

#### 取消a标签在移动端点击时的蓝色:

```
-webkit-tap-highlight-color: rgba(255,255,255, 0);
-webkit-user-select: none;
-moz-user-focus: none;
-moz-user-select: none;
```

#### 使用图片作为a标签的点击按钮时，当触发touchstart的时候，往往会有一个灰色的背景︰

```
a,a:hover,a:active,a:visited,a:link,a:focus{
	-webkit-tap-highlight-color:rgba(0,0,0,0);
	-webkit-tap-highlight-color: transparent;
	outline:none;
	background: none;
	text-decoration: none;
}
```

#### 改变选中内容的背景颜色

```
::selection {
	background: #FFF;
	color: #333;
}
::-moz-selection {
	background: #FFF;
	color: #333;
)
::-webkit-selection {
	background:#FFF;
	color: #333;
}
```

#### input 消除自动记忆功能 关闭浏览器自动填充输入框

input 的autocomplete属性默认是on：其含义代表是否让浏览器自动记录之前输入的值

```
autocomplete="off"
```

#### 去除ios input框点击时的灰色背景︰

```
-webkit-tap-highlight-color:rgba(0,0,0,0);
```

#### 区分标准模式下ie6~ie9和Firefox/Chrome的hack：

```
background-color:orange;       //all - for Firefox/Chrome
background-color:red\0;        //ie 8/9/10/Opera - for ie8/ie10/Opera
background-color:blue\9\0;     //ie 9/10 - for ie9/10
*background-color:black;       //ie 6/7 -for ie7
_background-color:green;      //ie6 - for ie6

IE6显示为：绿色，
IE7显示为：黑色，
IE8显示为：红色，
IE9显示为：蓝色，
Firefox/Chrome显示为：橘色
（本例IE10效果同IE9，Opera最新版效果同IE8）
```



#### 下划线css偏移量

[用CSS下划线距离](https://www.cnblogs.com/yeminglong/p/5481645.html)

代码一：

```
a {
    text-decoration: none; 
    background: url(underline.gif) repeat-x 100% 100%;
    padding-bottom: 4px;
    white-space: nowrap;
}
```

代码二：

```
a { 
	text-decoration: none;
	padding:0 0 6 0;
	border-bottom-color:0;
	border-bottom-width:1px;
	border-bottom-style:solid; 
}
```

代码三：

```
a{  
    text-decoration:none; 
    border-bottom:1px solid #ccc; /* #ccc换成链接的颜色 */
    display: inline-block; 
    padding-bottom:10px;  /*这里设置你要空的距离*/
}
```



#### 解决IE阴影兼容性

[ie-css3.htc](https://www.cnblogs.com/viewcozy/p/4828122.html)       [CSS3PIe]( http://css3pie.com/about/)

#### IE样式的兼容写法

```
.example{
    color:#fff;//FF,OP,IE8
    *color:#ff0;//IE7
    _color:#f00;//IE6
}
```

#### 元素在盒子中水平居中+垂直居中

[参考文章](https://blog.csdn.net/qq_27576607/article/details/78697812)

```
display: flex;//flex布局
justify-content: center;//使子项目水平居中
align-items: center;//使子项目垂直居中
```

[参考教程](https://blog.csdn.net/namechenfl/article/details/83029189)

#### KindEditor在移动端默认显示源码模式

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

但如果想要对IE8单独定义样式，可以这样：
html*~body .example{这里是针对IE8识别的样式}

针对IE9的CSS只需在相应CSS代码加入只有IE9识别的 \9\0。具体代码如下：

```
.div{ background-color:#0f0\9\0;/* ie9 */ }
```

其他浏览器写法：

```
background-color:#f00;/*all*/
background-color:#0ff\0;/* ie 8/9 */
background-color:#0f0\9\0;/* ie9 */
*background-color:#00f;/*ie7*/
_background-color:#ff0;/*ie6*/
background-color//:#090;/*非IE*/
background-color:#900\9;/*所有ie*/
```

怎么规定CSS的属性仅在IE下生效？在非IE浏览器下不生效

```
<!--[if IE]>
<style>
.test{color:red;}
</style>
<![endif]-->
```

css中判断[IE](https://www.baidu.com/s?wd=IE&tn=SE_PcZhidaonwhc_ngpagmjz&rsv_dl=gh_pc_zhidao)版本的语句

#### Koala设置scss编译后的输出路径



#### IE兼容性处理

```
<!--[if !IE]> 除IE外都可识别 <!--<![endif]-->

<!--[if IE]> 所有的IE可识别 <![endif]-->

<!--[if IE 5.0]> 只有IE5.0可以识别 <![endif]-->

<!--[if IE 5]> 仅IE5.0与IE5.5可以识别 <![endif]-->

<!--[if gt IE 5.0]> IE5.0以及IE5.0以上版本都可以识别 <![endif]-->

<!--[if IE 6]> 仅IE6可识别 <![endif]-->

<!--[if lt IE 6]> IE6以及IE6以下版本可识别 <![endif]-->

<!--[if gte IE 6]> IE6以及IE6以上版本可识别 <![endif]-->

<!--[if IE 7]> 仅IE7可识别 <![endif]-->

<!--[if lt IE 7]> IE7以及IE7以下版本可识别 <![endif]-->

<!--[if gte IE 7]> IE7以及IE7以上版本可识别 <![endif]-->
```
