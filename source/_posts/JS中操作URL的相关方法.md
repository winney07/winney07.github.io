---
title: JS中对象数组的操作
date: 2019-08-09 11:47:26
tags:
- JavaScript
categories: 
- JavaScript
---
### 获取URL中的参数：

```
/*
** @param name{string}    // 参数名
*/
function getURLParam(name) {
    // 获取完整的查询参数字符串
    const queryString = window.location.search;

    // 创建URLSearchParams对象来解析查询参数
    const params = new URLSearchParams(queryString);

    // 使用get方法获取指定名称的参数值
    return params.get(name);
}
```
`http://127.0.0.1:5500/URL.html?username=test&age=18`

```
const username = getURLParam('username');
console.log(username); // "test"

const age = getURLParam('age');
console.log(age); // "18"
```

### 解析URL

```
const urlString = 'https://www.test.com:8080/path/url.html?username=test&age=18';
const url = new URL(urlString);

console.log(url.protocol);  // "https:"
console.log(url.host);      // "www.test.com:8080"
console.log(url.pathname);  // "/path/url.html"
console.log(url.search);    // "?username=test&age=18"
console.log(url.hostname);  // www.test.com
console.log(url.href);      // https://www.test.com:8080/path/url.html?username=test&age=18
console.log(url.origin);    // https://www.test.com:8080
console.log(url.port);      // 8080

// 解析查询参数
const searchParams = new URLSearchParams(url.search);
console.log(searchParams.get('username')); // "test"
console.log(searchParams.get('age')); // "18"
```

### 构建URL

> 在页面之间传参，不想手动把参数使用`&`符号一个一个拼起来时

1. 使用URL构造函数构建URL

   ```
   const url = new URL('https://www.test.com');
   url.pathname = '/path';
   url.searchParams.set('username', 'test');
   url.searchParams.set('age', '18');
   console.log(url.toString()); // "https://www.test.com/path?username=test&age=18"
   ```

2. 使用字符串拼接构建URL

   ```
   const baseUrl = 'https://www.test.com';
   const path = '/path';
   const params = new URLSearchParams({ username: 'test', age: '18' });
   const constructedUrl = `${baseUrl}${path}?${params.toString()}`;
   console.log(constructedUrl); // "https://www.test.com/path?username=test&age=18"
   ```

   

