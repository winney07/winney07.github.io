---
title: Javascript方法
date: 2020-04-07 14:23:17
tags:
- Javascript
categories: 
- 工作笔记
- Javascript
---

## js:判断某变量的值是否等于某数组中的一个元素

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

## js高效修改对象数组里的对象属性名

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

### 数组相减
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