---
title: 前端CSS问题
date: 2020-06-30 17:35:17
tags:
- css问题
categories: 
- 工作笔记
- css问题
---
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
{% asset_img css1.png %}

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
{% asset_img css2.png %}
##### 鼠标上移，换行显示全部内容：
{% asset_img css3.png %}

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

#### 浏览器记住密码的情况下，解决密码输入框自动填充密码框（input type="password" 的问题）
```
用户名：<input type='text' autocomplete='off'>
密码：<input type='password' autocomplete="new-password" style="background-color: #fff!important;" readonly onfocus="this.removeAttribute('readonly');" onblur="this.setAttribute('readonly',true);">

```

#### 解决html页面英文和数字不自动换行，但中文就可以自动换行

{% asset_img huanhang.png %}

###### 解决方法：添加css属性word-break: break-all;

{% asset_img huanhang2.png %}

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

#### 选择倒数第n个元素

css3    :nth-last-child()选择器

规定属于其父元素的第二个子元素的每个p元素，从最后一个子元素开始计数∶

```
p:nth-last-child(2) {
	background: #fff;
}
```

#### chrome提示框（弹窗）字体模糊

白己写的一个很简单的提示框，firefox , Safari , ie都清晰，但是chrome就惑觉很模糊

 transform，z-index有可能导致这个问题

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

![Koala设置输出路径](https://raw.githubusercontent.com/winney07/Images/main/Note/Koala-%E8%BE%93%E5%87%BA%E8%B7%AF%E5%BE%84.png)

> 1. <!--[if !IE]> 除IE外都可识别 <!--<![endif]-->
>
> 2. <!--[if IE]> 所有的IE可识别 <![endif]-->
>
> 3. <!--[if IE 5.0]> 只有IE5.0可以识别 <![endif]-->
>
> 4. <!--[if IE 5]> 仅IE5.0与IE5.5可以识别 <![endif]-->
>
> 5. <!--[if gt IE 5.0]> IE5.0以及IE5.0以上版本都可以识别 <![endif]-->
>
> 6. <!--[if IE 6]> 仅IE6可识别 <![endif]-->
>
> 7. <!--[if lt IE 6]> IE6以及IE6以下版本可识别 <![endif]-->
>
> 8. <!--[if gte IE 6]> IE6以及IE6以上版本可识别 <![endif]-->
>
> 9. <!--[if IE 7]> 仅IE7可识别 <![endif]-->
>
> 10. <!--[if lt IE 7]> IE7以及IE7以下版本可识别 <![endif]-->
>
> 11. <!--[if gte IE 7]> IE7以及IE7以上版本可识别 <![endif]-->