---
title: IE兼容性处理
date: 2021-01-15 15:09:48
tags:
- IE兼容
categories:
- 兼容性处理
- IE兼容
---

#### js判断浏览器是否为IE浏览器

IE6-8和IE11都适用：

```
function isIE() { //ie?
     if (!!window.ActiveXObject || "ActiveXObject" in window)
            { return true; }
     else
            { return false; }
 }
```

> window.ActiveXObject：判断浏览器是否支持ActiveX控件，只有IE浏览器里面支持ActiveX控件
> 如果浏览器支持ActiveX控件，可以利用 var xml = new ActiveXObject("Microsoft.XMLHTTP"); 创建XMLHttpRequest 对象（这是在IE7以前的版本中）；
>
> 在较新的IE版本中可以利用 var xml = new ActiveXObject("Msxml2.XMLHTTP")的形式创建XMLHttpRequest对象;
>
> 而在IE7及非IE浏览器中可以利用v ar xml=new XMLHttpRequest()创建XMLHttpRequest对象。



#### IE浏览器固定定位（fixed）的弹窗

![IE浏览器固定定位（fixed）的弹窗](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/IE%E5%85%BC%E5%AE%B9%E6%80%A7%E5%A4%84%E7%90%86/ie-fixed.png)

解决：

1. 使用相对定位（absolute），弹出蒙层
2. body使用overflow:hidden样式，让body溢出隐藏，控制页面不滚动。

#### 去除IE10中输入框和密码框的X按钮和小眼睛

![去除IE10中输入框和密码框的X按钮和小眼睛](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/IE%E5%85%BC%E5%AE%B9%E6%80%A7%E5%A4%84%E7%90%86/ie10-input.png)

```
方法：
/*去除IE输入框的X标记*/
input[type=text]::-ms-clear {display: none;}

/*去除IE输入框的小眼睛标记*/
input[type=password]::-ms-reveal {display: none;}

如果想要单独去除某个输入框的话，可以把input[type=text]改为.target-class即可。
```

#### 去掉a标签点击(active)状态的背景色

```
ie浏览器，点击a标签时，点击状态，有个背景色
想去掉这个样式：
设置：
a:active{
    -webkit-tap-highlight-color: rgba(0,0,0,0);
    -webkit-tap-highlight-color: transparent;
    outline: none;
    background: none;
    text-decoration: none;
}
```

#### 复选框 input type="check"

```
普通浏览器：
<input type="checkbox" checked="" />
在IE浏览器中checked属性的写法是大写的:
<input type="checkbox" CHECKED="" />

所以js获取checked时，要考虑ie的情况。
```

#### ie 下input输入框readonly失效,光标仍可聚焦

> ie下input输入框设置了readonly属性,但是鼠标还可以点击光标聚焦,
>
> 改为bootstrap的disable属性后,无法聚焦但是表单提交又失效,无法传递参数,
>
> 而且聚焦后,backspace按键默认触发浏览器的返回功能,
>
> 后改为增加屈性unselectable='on',可以解决.

```
$("#config_name'+index).attr("readonly", "readonly");
$("#config_name'+index ).attr("unselectable", "on");
```

```
<pre name="code" class="javascript">$('#config_name'+index) .removeAttr("unselectable");
```

#### 文件上传按钮（input type= "file"）

美化后的按钮，在在ie浏览器下要双击才能打开

![文件上传按钮-兼容性](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/IE%E5%85%BC%E5%AE%B9%E6%80%A7%E5%A4%84%E7%90%86/input-file.png)

![文件上传按钮-兼容性](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/IE%E5%85%BC%E5%AE%B9%E6%80%A7%E5%A4%84%E7%90%86/input-file2.png)

![文件上传按钮-兼容性](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/IE%E5%85%BC%E5%AE%B9%E6%80%A7%E5%A4%84%E7%90%86/input-file3.png)

> 目的是让选择文件的文字铺满该按钮，可以点击



#### a标签添加事件的注意事项

```
<a href="javascript:void(0);" class="refresh-icon"></a>
```

> 当不添加链接的时候，只是为了触发事件的时候，要加上void(0);不然在IE浏览器会报错

#### 解决IE下a标签点击有虚线边框的问题

参考：[解决IE下a标签点击有虚线边框的问题](https://blog.csdn.net/zhangxianya1/article/details/47128007)

```
a:focus{outline:none;}
```

#### IE上设置input type = file文件上传区域的光标不闪烁

我们使用文件上传时,时常自定义图标,这时候通常会把input的透明度设置为0,然后覆盖在一个按钮上实现自定义图标，但是在IE上使用时会出现光标闪烁问题

解决办法: css设置font-size为0

#### js判断浏览器是否为IE浏览器

IE6-8和IE11都适用:

```
function isIE() {
	if (!!window.Activexobject || "Activexobject" in window)
 		return true;
 	}
	else{
 		return false;
 	}
}
```

> window.ActiveXObject：判断浏览器是否支持ActiveX控件，只有IE浏览器里面支持ActiveX控件 如果浏览器支持ActiveX控件，可以利用 var xml = new ActiveXObject("Microsoft.XMLHTTP"); 创建XMLHttpRequest 对象（这是在IE7以前的版本中）；
>
> 在较新的IE版本中可以利用 var xml = new ActiveXObject("Msxml2.XMLHTTP")的形式创建XMLHttpRequest对象;
>
> 而在IE7及非IE浏览器中可以利用v ar xml=new XMLHttpRequest()创建XMLHttpRequest对象。

#### IE不支持remove()方法。

[ie浏览器的不能使用remove()方法去删除](https://blog.csdn.net/mengtianqq/article/details/79744394)

> 1.因为ie浏览器没有remove()方法，可以使用 removeChild()方法去删除;
>
> 注意removeChild()的使用者是当前节点上一级，比如像删除节点node，使用的方法是：node.parentNode.removeChild(）；

```
function deleteRow(node){
	 node.parentNode.removeChild(node);
}
```

#### [IE对于域名带下划线访问问题]( http://www.360doc.com/content/14/0826/17/432969_404801617.shtml)

[ie 浏览器无法保存cookie,且与域名包含了下划线(_)有关系的问题](https://blog.csdn.net/qidizi/article/details/44494169)

https://datatracker.ietf.org/doc/html/rfc3696#section-2

> 项目中用到cookie传递参数到服务器端，用ip localhost等访问均正常，由于项目以后要用域名访问，果断修改hosts文件，添加k_test.com进行域名映射测试，当再次通过IE浏览器打开项目后，悲剧的事情发生了，居然无法登陆，再次用ip 、 localhost访问，都正常，百思不得其解，这个问题正正纠结了一下午，试了各种测试，都没有结果，第二天一大早，灵机—动，换了个google浏览器，奇迹发生了，居然可以登陆了，然后再试IE，问题依旧，盯着域名看了半天，想起应该换个域名了，果断去掉下划线，IE能正常访问了，纠结差不多一天的问题终于得到了解决，百度了一下域名下划线，果然IE浏览器确实存在这方面的问题，虽然是一个小小的问题，但纠结了一天，确实很郁闷，谨以此告诫自己以后的人生中多注重细节。

#### IE7局部滚动区域下绝对定位或相对定位元素不随滚动条滚动的bug

解决方法： 

如果.scrollArea{}是滚动区域，那么在样式里面加上ie7的hack：

```
.scrollArea{*position:relative;*left:0;*top:0;}
```

#### 文件上传按钮的美化

> input框，type为file  
>
> （兼容性）页面中的上传，在ie浏览器下要双击才能打开

![文件上传按钮的美化](https://raw.githubusercontent.com/winney07/Images/main/Note/%E4%B8%8A%E4%BC%A0%E6%8C%89%E9%92%AE%E7%BE%8E%E5%8C%96%E6%A0%B7%E5%BC%8F.png)

![解决方法](https://raw.githubusercontent.com/winney07/Images/main/Note/%E4%B8%8A%E4%BC%A0%E6%8C%89%E9%92%AE%E7%BE%8E%E5%8C%96-%E8%A7%A3%E5%86%B3%E6%96%B9%E6%B3%95.png)

![按钮放大](https://raw.githubusercontent.com/winney07/Images/main/Note/%E4%B8%8A%E4%BC%A0%E6%8C%89%E9%92%AE-IE%E6%94%BE%E5%A4%A7.png)

![大小问题](https://raw.githubusercontent.com/winney07/Images/main/Note/%E4%B8%8A%E4%BC%A0%E6%8C%89%E9%92%AE-IE%E5%A4%A7%E5%B0%8F%E9%97%AE%E9%A2%98.png)



目的是让选择文件的文字铺满该按钮，可以点击：

![不铺满](https://raw.githubusercontent.com/winney07/Images/main/Note/%E4%B8%8A%E4%BC%A0%E6%8C%89%E9%92%AE-IE%E4%B8%8D%E9%93%BA%E6%BB%A1.png)

![font-size导致](https://raw.githubusercontent.com/winney07/Images/main/Note/%E4%B8%8A%E4%BC%A0%E6%8C%89%E9%92%AE-IE-font-size%E5%AF%BC%E8%87%B4.png)