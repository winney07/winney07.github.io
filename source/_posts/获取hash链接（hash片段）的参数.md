---
title: 获取hash链接（hash片段）的参数
date: 2022-08-10 11:25:26
tags:
- JavaScript
categories: 
- JavaScript
---

**URL 结构**：URL 由多个部分组成，包括协议（如 `http` 或 `https`）、主机名（如 `www.example.com`）、端口号（可选，默认为 80 或 443）、路径（如 `/path/to/page`）、查询字符串（如 `?id=123&name=John`）以及哈希片段（如 `#section2`）。

#### `window.location.hash`

通过 `window.location.hash` 属性来访问当前 URL 的哈希片段。这个属性返回包括 `#` 符号的哈希部分，例如 `#section2`。

#### 获取hash片段中的参数的方法

```
function getHashParams() {
    const hash = window.location.hash.substr(1); // 去掉开头的 #
    const params = {};

    if (hash) {
        const parts = hash.split('?'); // 以 ? 分割
        const path = parts[0]; // 获取路径部分
        params.path = path; // 存储路径

        if (parts.length > 1) {
            const queryString = parts[1]; // 获取查询参数部分
            const paramPairs = queryString.split('&');

            paramPairs.forEach(pair => {
                const [key, value] = pair.split('=');
                params[key] = decodeURIComponent(value || ''); // 解码参数值
            });
        }
    }

    return params;
}

const params = getHashParams();
console.log(window.location.hash); //URL 中的哈希链接
console.log(params.path); // 输出路径
console.log(params.id); // 输出 id 参数的值
console.log(params.name); // 输出 name 参数的值
```

#### 例子

1. 链接1：

   ```
   http://127.0.0.1:5500/hash.html#?id=2&name=winney
   ```

   输出结果：

   ```
   #?id=2&name=winney
   
   2
   winney
   ```

2. 链接2：

   ```
   http://127.0.0.1:5500/hash.html#/?id=2&name=winney
   ```

   输出结果：

   ```
   #/?id=2&name=winney
   /
   2
   winney
   ```

3. 链接3：

   ```
   http://127.0.0.1:5500/hash.html#/test/text.html?id=2&name=winney
   ```

   输出结果：

   ```
   #/test/text.html?id=2&name=winney
   /test/text.html
   2
   winney
   ```

> 注意：查询参数前需要加上`?`号

`getHashParams()`方法适合以上3种情况的hash链接获取参数

如果不使用`params.id`这种方法获取参数对应的值，也可以使用解构赋值获取需要的参数：

```
const { id, name } = params;
```

#### 根据参数名获取对应的值

`getHashParams()`方法是一次性返回全部参数。如果想通过传参数名来获取参数对应的值，可以给`getHashParams()`方法添加参数

```
/*
** @param paramName{string}    // 参数名
*/
function getHashParams(paramName) {
    const hash = window.location.hash.substr(1); // 去掉开头的 #
    const params = {};

    if (hash) {
        const parts = hash.split('?'); // 以 ? 分割
        const path = parts[0]; // 获取路径部分
        params.path = path; // 存储路径

        if (parts.length > 1) {
            const queryString = parts[1]; // 获取查询参数部分
            const paramPairs = queryString.split('&');

            paramPairs.forEach(pair => {
                const [key, value] = pair.split('=');
                params[key] = decodeURIComponent(value || ''); // 解码参数值
            });
        }
    }

    // 如果提供了参数名称，返回特定参数的值；否则返回所有参数
    if (paramName) {
        return params[paramName] || null; // 返回特定参数的值或 null（如果参数不存在）
    } else {
        return params;
    }
}

const id = getHashParams('id');
console.log(id); // 输出 id 参数的值
var params_all = getHashParams();
console.log(params_all); // 输出所有参数
const age = getHashParams('age');
console.log(age); // 输出 age 参数的值
```

链接：

```
http://127.0.0.1:5500/hash.html#/test/text.html?id=2&name=winney
```

结果：

```
2
{path: '/test/text.html', id: '2', name: 'winney'}
null
```

