---
title: 日期对象Date的常用方法
date: 2020-08-10 11:22:26
tags:
- JavaScript
categories: 
- JavaScript
---

### 创建Date实例

```
let date = new Date();		// Fri Jul 14 2023 15:23:52 GMT+0800 (中国标准时间)
```

```
let date = new Date(1689321710307);		// Fri Jul 14 2023 16:01:50 GMT+0800 (中国标准时间)
```

```
let date = new Date('2023-07-14 16:10:40');	 // Fri Jul 14 2023 16:10:40 GMT+0800 (中国标准时间)
```

```
let date = new Date(2023, 6, 14, 15, 23, 52);  // Fri Jul 14 2023 15:23:52 GMT+0800 (中国标准时间)
```

### 格式化

#### 1. Date对象方法

```
let LDS = date.toLocaleDateString();	// 2023/7/14
```

```
let LS = date.toLocaleString();			// 2023/7/14 15:23:52
```

```
let LTS = date.toLocaleTimeString(); 	// 15:23:52
```

#### 2. 封装方法

格式：`2023-07-14`

```
function formatDate(date) {
    const year = date.getFullYear();
    const month = String(date.getMonth() + 1).padStart(2, '0');
    const day = String(date.getDate()).padStart(2, '0');

    return `${year}-${month}-${day}`;
}

const date = new Date();
const formattedDate = formatDate(date);
console.log(formattedDate); 	//	2023-07-14
```

格式：`2023-07-14 15:30:45`：

```
function formatDate(date, format) {
    const year = date.getFullYear();
    const month = String(date.getMonth() + 1).padStart(2, '0');
    const day = String(date.getDate()).padStart(2, '0');
    const hours = String(date.getHours()).padStart(2, '0');
    const minutes = String(date.getMinutes()).padStart(2, '0');
    const seconds = String(date.getSeconds()).padStart(2, '0');

    return format
        .replace('YYYY', year)
        .replace('MM', month)
        .replace('DD', day)
        .replace('HH', hours)
        .replace('mm', minutes)
        .replace('ss', seconds);
}

const date = new Date();
const formattedDate = formatDate(date, 'YYYY-MM-DD HH:mm:ss');
console.log(formattedDate); // 2023-07-14 15:30:45
```

格式：`2023-07-14 15:30:45`

```
function formatDate(date, separator = '-') {
    const year = date.getFullYear();
    const month = String(date.getMonth() + 1).padStart(2, '0');
    const day = String(date.getDate()).padStart(2, '0');
    const hours = String(date.getHours()).padStart(2, '0');
    const minutes = String(date.getMinutes()).padStart(2, '0');
    const seconds = String(date.getSeconds()).padStart(2, '0');

    const formattedDate = [year, month, day].join(separator);
    const formattedTime = [hours, minutes, seconds].join(':');

    return formattedDate + ' ' + formattedTime;
}

const date = new Date();
const formattedDate = formatDate(date, '-');
console.log(formattedDate); // 2023-07-14 15:30:45
```

> 后面两种方法，传参方式不一样，实现效果一样。

> **`padStart()`** 方法用另一个字符串填充当前字符串（如果需要的话，会重复多次），以便产生的字符串达到给定的长度。从当前字符串的左侧开始填充。
>
> 参数：`targetLength`：当前字符串需要填充到的目标长度；`padString`：填充字符串。默认值为 " "（空格）

### 获取时间戳（当前时间的毫秒数）

```
let t = date.getTime();		// 1689319432759
```

```
let now = Date.now();    	// 1689319432759
```

> 1. `Date.now()`: 静态方法，直接通过 `Date.now()` 调用，返回的是当前时间的毫秒数，不需要创建 `Date` 对象实例。
> 2. `Date.getTime()`:  `Date` 对象的实例方法，需要先创建一个 `Date` 对象，然后通过该对象调用 `getTime()` 方法，返回的是该日期对象表示的时间的毫秒数。
>
> 总结来说，`Date.now()` 更方便和直接，可以直接获取当前时间的毫秒数，而 `date.getTime()` 则是通过 `date` 对象获取该对象表示的时间的毫秒数。

### 获取年份

```
let y = date.getFullYear();		// 2023
```

### 获取月份

```
let m = date.getMonth() + 1;	// 7
```

### 获取月中的哪一日

```
let d = date.getDate();		// 14
```

### 获取小时

```
let h = date.getHours();	// 15
```

### 获取分钟

```
let min = date.getMinutes();   // 23
```

### 获取秒数

```
let s = date.getSeconds();		// 52
```

### 获取星期几

```
let day = date.getDay();		// 5
```

### 时间戳转换格式

```
//时间戳转换格式
function formatDateTime(timeStamp) { 
    var date = new Date();
    date.setTime(timeStamp * 1000);
    var y = date.getFullYear();    
    var m = date.getMonth() + 1;    
    m = m < 10 ? ('0' + m) : m;    
    var d = date.getDate();    
    d = d < 10 ? ('0' + d) : d;    
    var h = date.getHours();  
    h = h < 10 ? ('0' + h) : h;  
    var minute = date.getMinutes();  
    var second = date.getSeconds();  
    minute = minute < 10 ? ('0' + minute) : minute;    
    second = second < 10 ? ('0' + second) : second;   
    return y + '-' + m + '-' + d+' '+h+':'+minute+':'+second;    
};
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
new Date().toLocaleDateString()
2020/3/2
new Date().toLocaleTimeString()
17:50:21
new Date().toLocaleString();
2020/3/2 17:46:52
new Date().toTimeString()
17:50:59 GMT+0800 (中国标准时间)
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
