---
title: JS中操作URL的相关方法
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




#### 参数对应的值带`=`号

如果动态传参时，参数对应的值含有`=`号，避免浏览器自动处理等号，使用`encodeURIComponent`方法

发送端：

```
const key = "BANXB1cAPFcEAGwFZgk=";
const encodedValue = encodeURIComponent(key);
const url = `edit.html?key=${encodedValue}`;
window.location.href = url;
```

接收端：

```
const queryString = window.location.search;
const urlParams = new URLSearchParams(queryString);
const encodedValue = urlParams.get("key");
const decodedValue = decodeURIComponent(encodedValue);
```

> 因在项目中使用`$.form.href("{:url('xy/test/group')}" + "?id=" + id + '&key='+key);`这样跳转到页面2。其中`key`的值最后可能带有`=`号，跳转到页面2的时候，在页面2中获取到的key参数少了最后的`=`号

> 如果大家使用`window.location.href`进行页面跳转时，在链接上传参，没有问题，可以忽略这个问题。

### [将网址url中的参数转化为JSON格式的两种方法](https://www.cnblogs.com/wangshucheng/p/11203097.html)

#### 第一种： for 循环方式

```
// 第一种： for循环
var GetQueryJson1 = function () {
  let url = location.href; // 获取当前浏览器的URL
  let arr = []; // 存储参数的数组
  let res = {}; // 存储最终JSON结果对象
  arr = url.split('?')[1].split('&'); // 获取浏览器地址栏中的参数
   
  for (let i = 0; i < arr.length; i++) { // 遍历参数
    if (arr[i].indexOf('=') != -1){ // 如果参数中有值
      let str = arr[i].split('=');
      res[str[0]] = str[1];
    } else { // 如果参数中无值
      res[arr[i]] = '';
    }
  }
  return res;
}
console.log(GetQueryJson1());
```

#### 第二种：正则表达式方式

```
// 第二种：正则表达式
var GetQueryJson2 = function () {
  let url = location.href; // 获取当前浏览器的URL
  let param = {}; // 存储最终JSON结果对象
  url.replace(/([^?&]+)=([^?&]+)/g, function(s, v, k) {
    param[v] = decodeURIComponent(k);//解析字符为中文
    return k + '=' +  v;
  });
  return param;
}
 
console.log(GetQueryJson2());
```

#### URL参数改为json格式

```修改url参数
var data = $(formEl).serialize()                // 表单数据（筛选条件)
    ,arr = decodeURIComponent(data).split("&")  // 对数据拆分处理
    ,formData = {}                              // 需要缓存的数据对象
// 转为JSON对象
arr.map(function(item) {
    formData[item.split('=')[0]] =  item.split('=')[1];
})
```

#### 修改url参数

```
function changeURLArg(url,arg,arg_val){ 
    var pattern=arg+'=([^&]*)'; 
    var replaceText=arg+'='+arg_val; 
    if(url.match(pattern)){ 
        var tmp='/('+ arg+'=)([^&]*)/gi'; 
        tmp=url.replace(eval(tmp),replaceText); 
        return tmp; 
    }else{ 
        if(url.match('[\?]')){ 
            return url+'&'+replaceText; 
        }else{ 
            return url+'?'+replaceText; 
        } 
    } 
    return url+'\n'+arg+'\n'+arg_val; 
}
```

#### 改变hash值

```
//改变hash值
function changeHash(key, val) {
    location.hash= location.hash.match(key+"=([^&]*)") ? location.hash.replace(eval('/('+ key+'=)([^&]*)/gi'), key+"="+val) : location.hash + "&"+key+"="+val
}
```

