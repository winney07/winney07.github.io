---
title: CSS样式Demo
date: 2019-08-22 10:57:59
tags:
- CSS
categories: 
- CSS
---

#### 使用flex布局实现上下布局，整屏背景图设置—图片会变形

优点：铺满

缺点：图片变形

| 值      | 描述                                                         |
| ------- | ------------------------------------------------------------ |
| contain | 此时会保持图像的纵横比并将图像缩放成将适合背景定位区域的最大大小。 |
| cover   | 此时会保持图像的纵横比并将图像缩放成将完全覆盖背景定位区域的最小大小。 |

`注：使用 background-size: cover;  ，背景图会根据屏幕高度铺满，图片会发生变形`

![背景图设置](https://raw.githubusercontent.com/winney07/Images/main/Note/%E4%B8%8A%E4%B8%8B%E5%B8%83%E5%B1%80%EF%BC%8C%E8%83%8C%E6%99%AF%E5%9B%BE%E8%AE%BE%E7%BD%AE1.png)



```
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, minimum-scale=1">

// 结构
<body>
    <header>
        <h1>上下布局，背景图设置</h1>
    </header>
    <div class="content">
       <div class="form-box">
       </div>     
    </div>
</body>
```

```
// 样式
<style>
*{
    padding: 0;
    margin: 0;
}
html, body{
    font-size: 0.13333333vw;
    height: 100vh;
    font-family: 'Microsoft YaHei';
}
body{
    background-color: #f1f1f1;
    display: flex;
    flex-direction: column;
}
header{
    height: 88rem;
    line-height: 88rem;
    text-align: center;
    font-size: 18em;
}
.content{
    flex: 1;
    background: url(./images/pubuliu/24.jpg) center center no-repeat;
    background-size: cover;
}
.form-box{
    width: 90%;
    margin: 200rem auto 0;
    min-height: 600rem;
    background-color: #fff;
    border-radius: 5rem;
}
</style>
```

#### 使用img和定位，设置背景图--图片不变形

优点：图片不 变形

缺点：不铺满

![设置背景图](https://raw.githubusercontent.com/winney07/Images/main/Note/%E4%B8%8A%E4%B8%8B%E5%B8%83%E5%B1%80%EF%BC%8C%E8%83%8C%E6%99%AF%E5%9B%BE%E8%AE%BE%E7%BD%AE2.png)

```
// 结构
<body>
    <header>
        <h1>使用img和定位，设置背景图--图片不变形</h1>
    </header>
    <img src="./images/pubuliu/24.jpg" alt="" class="bg">
    <div class="content">
       <div class="form-box">
       </div>     
    </div>
</body>
```

```
// 样式
<style>
*{
    padding: 0;
    margin: 0;
}
html, body{
    font-size: 0.13333333vw;
    height: 100vh;
    font-family: 'Microsoft YaHei';
}
body{
    background-color: #f1f1f1;
}
header{
    height: 88rem;
    line-height: 88rem;
    text-align: center;
    font-size: 18em;
}
.bg{
    width: 100%;
}
.content{
    position: absolute;
    top: 200rem;
    left: 5%;
    z-index: 100;
    width: 90%;
    min-height: 600rem;
    background-color: #fff;
    border-radius: 5rem;
}
</style>
```

#### 直接给body设置背景图--图片会变形

优点：铺满

缺点：图片变形

![设置背景](https://raw.githubusercontent.com/winney07/Images/main/Note/%E4%B8%8A%E4%B8%8B%E5%B8%83%E5%B1%80%EF%BC%8C%E8%83%8C%E6%99%AF%E5%9B%BE%E8%AE%BE%E7%BD%AE3.png)

```
// 结构
<body>
    <header>
        <h1>直接给body设置背景图--图片会变形</h1>
    </header>
    <div class="content">
       <div class="form-box">
       </div>     
    </div>
</body>
```

```
// 样式
<style>
*{
    padding: 0;
    margin: 0;
}
html, body{
    font-size: 0.13333333vw;
    height: 100vh;
    font-family: 'Microsoft YaHei';
}
body{
    background-color: #f1f1f1;
    background: url(./images/pubuliu/24.jpg) center center no-repeat;
    background-size: cover;
    padding-top: 88rem;
    box-sizing: border-box;
}
header{
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 88rem;
    line-height: 88rem;
    text-align: center;
    font-size: 18em;
    background-color: #fff;
}
.content{
    margin: 200rem auto 0;
    width: 90%;
    min-height: 600rem;
    background-color: #fff;
    border-radius: 5rem;
}
</style>
```

