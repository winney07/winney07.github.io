---
title: JavaScript对象的相关操作
date: 2022-07-09 14:44:34
tags:
- JavaScript
categories: 
- JavaScript
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

#### js拷贝对象，不改变原来对象

```
var obj = {a:1,b:2}  
var newObj = JSON.parse(JSON.stringify(obj)); 
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

#### [如果动态设置json对象的key](https://www.cnblogs.com/strangerqt/p/4465114.html)

项目中要求动态设置json的key属性，如果按照一般的json设置方法是不行的。假如你把一个key设置为一个变量的话，那么最后js解析出来的就是key为这个变量名而不是这个变量的值。

解决：通过使用

`var o = {};`

`o[变量名] = 变量值`

再把这个变量赋值给json即可

#### 计算对象属性个数

```
var obj = {
  p1: 123,
  p2: 456
};

Object.keys(obj).length // 2
Object.getOwnPropertyNames(obj).length // 2
```

多字词语来作为属性名，必须给它们加上引号：

```
let user = {
  name: "John",
  age: 30,
  "likes birds": true  // 多词属性名必须加引号
};
```

列表中的最后一个属性应以逗号结尾：

```javascript
let user = {
  name: "John",
  age: 30,
}
```

这叫做尾随（trailing）或悬挂（hanging）逗号。这样便于我们添加、删除和移动属性，因为所有的行都是相似的。

当创建一个对象时，我们可以在对象字面量中使用方括号。这叫做 **计算属性**。

例如：

```javascript
let fruit = prompt("Which fruit to buy?", "apple");

let bag = {
  [fruit]: 5, // 属性名是从 fruit 变量中得到的
};

alert( bag.apple ); // 5 如果 fruit="apple"
```

计算属性的含义很简单：`[fruit]` 含义是属性名应该从 `fruit` 变量中获取。

所以，如果一个用户输入 `"apple"`，`bag` 将变为 `{apple: 5}`。

本质上，这跟下面的语法效果相同：

```javascript
let fruit = prompt("Which fruit to buy?", "apple");
let bag = {};

// 从 fruit 变量中获取值
bag[fruit] = 5;
```

……但是看起来更好。

我们可以在方括号中使用更复杂的表达式：

```javascript
let fruit = 'apple';
let bag = {
  [fruit + 'Computers']: 5 // bag.appleComputers = 5
};
```

方括号比点符号更强大。它允许任何属性名和变量，但写起来也更加麻烦。

所以，大部分时间里，当属性名是已知且简单的时候，就使用点符号。如果我们需要一些更复杂的内容，那么就用方括号。

#### [克隆与合并，Object.assign](https://zh.javascript.info/object-copy#cloning-and-merging-object-assign)

#### 在html中显示JSON数据的方法

其实JSON.stringify本身就可以将JSON格式化，具体的用法是：

```
JSON.stringify(res, null, 2);	// res是要JSON化的对象，2是spacing
```

[在html中显示JSON数据的方法](https://www.jb51.net/web/553898.html)

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

[JavaScript 深拷贝性能分析](https://segmentfault.com/a/1190000013107871)

[深入 js 深拷贝对象](https://www.cnblogs.com/makai/p/11249986.html)

日常深拷贝，建议序列化反序列化方法。
