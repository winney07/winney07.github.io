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

