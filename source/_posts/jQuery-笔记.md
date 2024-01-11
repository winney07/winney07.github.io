---
title: jQuery-笔记
date: 2019-03-07 15:01:55
tags:
- jQuery
categories: 
- JavaScript
- jQuery
---

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

[jQuery UI](https://www.jqueryui.org.cn/)

#### 监听输入框的值变化事件

```
$(".search-input").bind('input porpertychange',function(){
	.....
});
```

不足：输入中文时，每输入一个字母，都会触发

#### 监听输入框的值变化-优化

改为使用compositionstart和compositionend

```
// 搜索框
var flag = true;
$(".optionList .searchIpt").on("compositionstart", function() {
    flag = false;
});
$(".optionList .searchIpt").on("compositionend", function() {
    flag = true;
});
$(".optionList .searchIpt").on("keyup", function() {
    if(flag) {
        var text = $(this).val().trim();
        // 匹配查询结果
        searchCheck(text, ".searchIpt");
    }
});
```

#### 回到页面顶部

```
window.onscroll = function(){
    if (document.documentElement.scrollTop || document.body.scrollTop > 0) {
        document.getElementById("test").style.display='block';
    }else{
        document.getElementById("test").style.display='none';
    }
}
test.onclick = function(){
    document.body.scrollTop = document.documentElement.scrollTop = 0;
    document.getElementById("test").style.display = "none";
}
```

#### 过滤选择器

[jQuery 学习之路（2）：选择器与过滤器](https://www.lmlphp.com/user/58650/article/item/808868/)

一、基本选择器

```
标签选择器：　　$('button')

ID选择器：　　$('#id1')

类选择器：　　$('.class1')

多重选择器：　　$('#id1,.class1,button')

全体选择器：　　$('*') 
```

基本选择器完全根据 CSS 选择器的规范而来，对于了解 CSS 的用户非常容易掌握。

**二、层次选择器**

```
子选择器：　　$('parent > child')　　　　　　　　
后代选择器：　　$('ancester descendant')
单一兄弟选择器：　　$('prev + next')
所有兄弟选择器：　　$('prev ~ siblings')
```

　　子选择器和后代选择器的区别：子选择器是后代选择器的子集，前者只筛选出符合条件的直接子元素，后者筛选出符合条件的所有子孙元素。
　　单一兄弟选择器与所有兄弟选择器类似，前者只筛选出符合条件的下一个同辈元素，后者筛选出符合条件的后面的所有的同辈元素。

**三、属性选择器**

　　属性选择器可以筛选出包含特定属性的元素，或者根据属性的值的格式来筛选出元素。

```
属性包含：　　　　　　　　[attr]
属性值为指定字符串：　　　　[attr = "value"]
属性值不为指定字符串：　　　　[attr != "value"]
属性值以指定字符串开始：　　　　[attr ^= "value"]
属性值以指定字符串结束：　　　　[attr $= "value"]
属性值包含指定字符串：　　　　[attr *= "value"]
多属性筛选：　　　　　　　　[attr1 *= "value1"][attr2 = "value2"]
```

　　其中，[name != "value"] 的实现效率较低，可以使用 :not([attr = 'value']) 的形式

**四、基本过滤器**

　　有些过滤器的实现并不高效，原因参见官网，对于这部分过滤器，建议使用 .filter(selector) 来调用，如 $('div').filter(':hidden') ，后面所有的这类过滤器都以红色特殊标出。

```
:animated　　　　    当前执行动画的元素
:eq(index)　　　　    取出指定索引的元素（jQuery 对象是集合，索引从0开始）
:gt(index)　　　　　　取出索引大于指定值的元素
:lt(index)　　　　　　　　取出索引小于指定值的元素
:first 　　　　　 取出第一个元素，即索引为0的元素
:last　　　　　　取出最后一个元素，即索引为 size()-1 的元素
:even　　　　　　取出索引为偶数的元素
:odd　　　　　　取出索引为奇数的元素
:header　　　　　取出所有标题元素，如 h1,h2,h3 等
:root　　　　　　取出根元素
:not(selector)　　取出所有不匹配指定过滤器的元素　
:focus　　　　　　　　　　当前得到焦点的元素
```

**五、子元素过滤器**

```
:first-child　　　　　　　　是其父元素的第一个子元素
:last-child　　　　　　　　是其父元素的最后一个元素
:first-of-type　　　　　　　　是同辈同类元素中的第一个元素
:last-of-type　　　　　　　　是同辈同类元素中的最后一个元素
:only-child　　　　　　　　是其父元素的唯一子元素
:only-of-type　　　　　　在同辈元素中，没有同类元素的元素，即此元素是同辈元素中唯一的该类型元素
:nth-child(index)　　　　其父元素的第 index 元素，该 index 从 1 开始
:nth-last-child(index)　　　　其父元素的倒数第 index 元素，该 index 从 1 开始
:nth-of-type(index)　　　　　　是同辈的同类元素中的第 index 元素，该 index 从 1 开始
:nth-last-of-type(index)　　　　是同辈的同类元素中倒数第 index 元素，该 index 从 1 开始
```

**六、内容过滤器**

```
:contains(text)　　　　　　包含指定字符串的元素
:empty　　　　　　　　　　没有子元素的元素
:has(selector)　　　　　　 包含至少一个指定的选择器匹配的元素
:parent　　　　　　　　　　包含至少一个子节点的（一个元素或文本）元素
```

**七、表单过滤器**

```
:input
:text
:password
:button
:reset
:submit
:radio
:checkbox
:checked
:selected
:file
:image
:focus
:enabled
:disabled
```

**八、可见性过滤器**

```
:hidden　　　　当前隐藏的元素
:visible　　　　当前显示的元素
```



#### Tabs切换内容

```
$(".tab li").click(function(){
    $(".tab li").eq($(this).index()).addClass("active").siblings().removeClass("active");
    $(".tabContent div").hide().eq($(this).index()).show();
})
```







#### jQuery自定义扩展



#### 插件

- jquery-ui
- jquery-lazyload
- jquery-color



#### jquery获取name属性为数组的值

```
<input type="text" name="nameArr[]" value="1" title="标题1">
<input type="text" name="nameArr[]" value="2" title="标题2">

var inputs = $('input[name^="nameArr"]');
```



![需求](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/jQuery-%E7%AC%94%E8%AE%B0/1.png)

##### 新增按钮事件

```
$("#hb-setting").on("click", "#drawCard-add", function () {
    var i = $(this).data('index') + 1;  // name值的下标
    var li = '<div class="layui-form-item gear-item">'+
                '<label class="layui-form-label"></label>'+
                '<div class="layui-input-block">'+
                    '<div class="layui-input-inline">'+
                        '<input type="number" name="gear7['+ i +']" min="0" lay-verify="required" lay-reqText="..." placeholder="请输入..." class="layui-input">'+
                    '</div>'+
                    '<div class="layui-input-inline">'+
                        '<input type="number" name="reg_day7['+ i +']" min="0" lay-verify="required" lay-reqText="..." placeholder="请输入..." class="layui-input">'+
                    '</div>'+
                    '<div class="layui-input-inline">'+
                        '<input type="number" name="draw_card_times7['+ i +']" min="0" lay-verify="draw_card_times" placeholder="请输入..." class="layui-input">'+
                    '</div>'+
                    '<div class="layui-input-inline">'+
                        '<input type="text" name="money7['+ i +']" lay-verify="drawCard_money" placeholder="请输入..." class="layui-input">'+
                    '</div>'+
                    '<div class="layui-input-inline w154">'+
                        '<input type="text" name="frontend_money7['+ i +']" placeholder="请输入前端展示金额" class="layui-input">'+
                    '</div>'+
                    '<div class="layui-input-inline w154">'+
                        '<input type="text" name="describe7['+ i +']" lay-verify="required" lay-reqText="..." placeholder="请输入..." class="layui-input">'+
                    '</div>'+
                    '<div class="layui-inline">'+
                        '<i class="layui-icon layui-icon-add-circle" id="drawCard-add" data-index="'+ i +'"></i> '+
                    ' </div>'+
                '</div>'+
            '</div>';

    $(this).removeAttr("id");
    $(this).removeClass("layui-icon-add-circle");
    $(this).addClass("layui-icon-reduce-circle");
    $(this).addClass("drawCard-del");

    // 在前面追加元素
    $("#drawCard_hb_tr").before(li);

    form.render(); //更新全部

    // 活动状态为“关闭”时——不强制要求输入档位内容
    var name_arr = ['gear7', 'reg_day7', 'describe7', 'cash_notice7'];
    updateVerify($('[name="reward_7"]').val(), name_arr);
})
```

##### 更新表单的验证条件函数

开启状态，必填，关闭状态，不必填

```
// 更新表单的验证条件
 function updateVerify(status, name_arr) {
    for(var i in name_arr) {
        // 关闭状态，不强制要求输入档位内容
        if(status === "0") {
            $('[name^="' + name_arr[i]+ '"]').removeAttr("lay-verify");
        } else {
            $('[name^="' + name_arr[i]+ '"]').attr("lay-verify", "required");
        }
    }

    form.render(); // 更新表单元素
 }
```

##### 减去按钮事件

```
// 删除按钮
$("#hb-setting").on("click", ".drawCard-del", function () {
    var idx = $(this).data('index');  // 当前被删除的index
    $(this).parent(".layui-inline").parent(".layui-input-block").parent(".layui-form-item").remove();   // 删除当前列的元素

    updateGearIndex(idx, "#drawCard-add");      
});


// 更新档位中的name值/减号/加号的下标
function updateGearIndex(idx, add_btn) {
    var gear_items = $('.layui-show').find(".gear-item");  // 档位配置的所有列
    var gear_len = gear_items.length;  // 档位的列数
    // 更新下标
    for(var j = idx; j < gear_len; j++) {
        var inputs = $(gear_items[j]).find('.layui-input-block').children().find('input');   // 当前横列的所有input
        $(gear_items[j]).find('.layui-icon-reduce-circle').attr('data-index', j);    // 修改减号的index——都减1

        for(var k = 0; k < inputs.length; k++) {
            var name = $(inputs[k]).attr('name');
            $(inputs[k]).attr("name", setCharOnIndex(name, name.length - 2, j));    // 修改name值的下标-减1
        }
    }
    form.render(); //更新全部

     // 修改加号的data-index属性
    $(add_btn).attr('data-index', gear_len -1);
}
```

##### 切换状态事件

```
 // 监听活动状态-等级红包
 form.on('select(reward_1)', function(data){
    var name_arr = ['gear1', 'reg_day1', 'level1', 'describe1', 'cash_notice1'];

    updateVerify(data.value, name_arr);

    upateLabelIcon(data.value, ['cash_level1', 'cash_notice1']);
}); 

// 更新表单元素是否必填的 * 图标
function upateLabelIcon(status, name_arr2) {
    for(var i in name_arr2) {
        if(status === "0") {
            $('[name="' + name_arr2[i] + '"]').parent(".layui-input-block").siblings(".layui-form-label").removeClass("required");
        } else {
            $('[name="' + name_arr2[i] + '"]').parent(".layui-input-block").siblings(".layui-form-label").addClass("required");
        }
    }
}
```

[jquery获取name属性为数组的值（天王老子来了我也这样写）...](https://blog.csdn.net/Lucky_Freedom/article/details/110231690)

```

//补充一下知识
$("input[name^='news']")         选择所有的name属性以'news'开头的input元素 
$("input[name$='news']")         选择所有的name属性以'news'结尾的input元素 
$("input[name*='man']")          选择所有的name属性包含'news'的input元素

//下面是代码
var jurisdiction={};//创建一个空对象
$('input[name^="jurisdiction"]:checked').each(function(index,element){	//index下标 element 当前选中的元素
  jurisdiction[index] = $(this).val();//压入对象数组
});

```

[jquery js 获取input name为数组或者属性相同的值](https://blog.csdn.net/lfbin5566/article/details/115966302)

```
<input type="text" name="nameArr[]" value="1" title="标题1">
<input type="text" name="nameArr[]" value="2" title="标题2">
 
<input type="text" id="video_url0" value="0" name="nameArr0" class="video_url" placeholder="请上传活动视频">
<input type="text" id="video_url1" value="1" name="nameArr1" class="video_url" placeholder="请上传活动视频">
<input type="text" id="video_url2" value="2" name="nameArr2" class="video_url"
placeholder="请上传活动视频">
 
$("input[name^='nameArr']")//获取所有的name属性以'nameArr'开头的input元素 
$("input[name$='nameArr']")//获取所有的name属性以'nameArr'结尾的input元素 
$("input[name*='nameArr']")//获取所有的name属性包含'nameArr'的input元素
 
//创建一个空数组
var data_arr = [];
//index下标 element 当前选中的元素
$('input[name^="nameArr"]').each(function(index,element){
    //压入数组	
    data_arr[index] = $(this).val();
});
console.log(data_arr);
 
 
```

