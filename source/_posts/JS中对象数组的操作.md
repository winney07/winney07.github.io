---
title: JS中对象数组的操作
date: 2019-08-09 11:47:26
tags:
- JavaScript
categories: 
- JavaScript
---
#### 判断一个对象数组的某个对象是否具体某个属性，如果没有就追加对象

```
// records是对象数组
if (!records.some(obj => obj.username === value.username)) {
    records.push(value);
}
```

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
