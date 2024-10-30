---
title: HTML页面之间传参-iframe父子页面传参
date: 2021-08-25 11:12:23
tags:
- JavaScript
categories: 
- JavaScript
---

#### A域名下的参数传给B域名下的页面

场景1：推广页面要求一定要使用A域名，而推广页面的网页内容是在B域名下，而B域名推广页需要从A域名的推广链接上获取参数。

> 这里是填写的推广链接是A域名下的，但是实际用户访问的页面是B域名下的`game.html`页面

例如：

A域名的推广链接：http://A.com/iframeParentPage.html?app_id=70116&user=admin&age=18

B域名推广页面：http://B.com/game.html?game_id=10002&platform_id=205&type=game

> A、B域名在不同的主体下，不能把B域名下的页面放到A域名的服务器上。
>
> B域名需要拿到`app_id`等参数。

1. A域名下`iframeParentPage.html`中获取参数：`window.location.search`

   ```
    console.log(window.location.search);	// ?app_id=70116&user=admin&age=18
   ```

2. 携带A域名下`iframeParentPage.html`中的参数，进行页面跳转

   ```
   window.location.href = "http://B.com/game.html?game_id=10002&platform_id=205&type=game&" + window.location.search.substring(1);
   ```

   > 备注：
   >
   > 1. 使用`window.location.search.substring(1);`是要把`?`去掉
   >
   > 2. 要在`type=game`后面加上`&`

3. 在B域名下的`game.html`页面中获取参数

   ```
   const queryParams = new URLSearchParams(window.location.search);
   console.log('queryParams');
   console.log(queryParams);
   console.log(queryParams.get('app_id'));
   console.log(queryParams.get('user'));
   console.log(queryParams.get('age'));
   ```

### `iframe`嵌套页面-父子页面传参

#### 查询字符串（URL 参数）

场景2：推广页面要求一定要使用A域名，而推广页面的网页内容是在B域名下，而B域名推广页需要从A域名的推广链接上获取参数。

> 这里是填写的推广链接是A域名下的，但是实际用户访问的页面是A域名下`iframe`嵌套了B域名下的`game.html`的页面，也就是URL中显示的是A域名

A域名下的页面：

```
<iframe title="游戏页面" src="" frameborder="0"></iframe>
```

```
document.querySelector('iframe').src= "http://A.com/iframeParentPage.html?app_id=70116&user=admin&age=18&" + window.location.search.substring(1);
```

B域名下的页面：

```
const queryParams = new URLSearchParams(window.location.search);
console.log('queryParams');
console.log(queryParams);
console.log(queryParams.get('app_id'));
console.log(queryParams.get('user'));
console.log(queryParams.get('age'));
```

#### 同域名下-使用缓存

A页面：

```
localStorage.setItem('params', window.location.search.substring(1));
```

B页面：

```
var params = localStorage.getItem('params');
console.log(params);
const queryParams = new URLSearchParams(params);
console.log(queryParams.get('app_id'));
console.log(queryParams.get('user'));
console.log(queryParams.get('age'));
```

> 注意：不同域名，使用这个方法不可以。
>
> 根据需要，使用`localStorage`或`sessionStorage`
