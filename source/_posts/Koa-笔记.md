---
title: Koa-笔记
date: 2021-01-20 15:17:06
tags:
- Koa
categories: 
- 工作笔记
- Koa
---

[技术胖-koa2教程](https://www.bilibili.com/video/BV1Pt41127sj?from=search&seid=17378531192218366513)    [技术胖博客笔记](http://www.jspang.com/detailed?id=34)

#### 第01节：Koa开发环境搭建

1、npminit -y (-y可选)  ————生成package.json文件

2、npm install --save koa ————在开发环境安装koa

3、编写测试程序：

```
const Koa = require('koa');
const app = new Koa();

app.use(async (ctx) => {
  ctx.body = 'Hello Winney'  
})

app.listen(3000)
```

4、运行node index.js  （因为是基于node的，所以直接node **.js）

5、然后在浏览器中输入：http://127.0.0.1:3000

#### 第02节：async/await的使用方法

```
async function testAsync() {
	return 'Hello async'
}
```

> 加上async，就把这个方法变成了异步的
>
> 启用了async，返回的不是一个普通字符串，而是一个promise

```
function getSomething() {
    return 'something';
}

async function testAsync() {
    return 'Helllo Async';
}

const result = testAsync();
console.log(result);
getSomething();
```

#### await：async wait 

```
function getSomething() {
    return 'something';
}

async function testAsync() {
    return 'Helllo Async';
}

async function test() {
    const v1 = await getSomething();
    const v2 = await testAsync();
    console.log(v1, v2);
    console.log(`${v1} ${v2}`);
}

test();
```

> await不仅可以接收promise对象也可以接收普通返回值。

#### setTimeout延迟处理

```
function takeLongTime() {
    return new Promise(resolve => {
        setTimeout(() => resolve('long_time_value'), 1000)
    })
}

async function test() {
    const v = await takeLongTime();
    console.log(v);
}

test();
```

> node demo.js     输入命令后，3秒后出现结果

#### 第03节：Get请求的接收

监听端口

```
app.listen();
```

query和querystring区别

- query：返回的是格式化好的参数对象。

- querystring：返回的是请求字符串

> 在koa2中GET请求通过request接收，但是接受的方法有两种：query和querystring。

```
const Koa = require('koa');
const app = new Koa();

app.use(async(ctx) => {
    let url = ctx.url;

    //从request中获取GET请求
    let request = ctx.request;
    let req_query = request.query;
    let req_querystring = request.querystring;

    //从上下文中直接获取
    let ctx_query = ctx.query;
    let ctx_querystring = ctx.querystring;

    ctx.body = {
        url,
        req_query,
        req_querystring,
        ctx_query,
        ctx_querystring
    }
});

app.listen(3000, ()=>{
    console.log('demo server is starting at port 3000');
});
```

访问http://localhost:3000/在页面中显示：

```
"url": "/" , "req_query": {}, "reg_querystring":""}
```

访问http://localhost:3000/?user=winney&age=26在页面中显示：

```
"url" :"/?user=winney&age=26" , "req_query": {"user":"winney, "age": "26"},'req_querystring ": "user=winney&age=26"}

```

> 我们可以使用浏览器插件-iFormatTool，让内容更清晰。图片中我们可以清楚看到query是一个对象，而querystring就是一个普通的字符串。

下载地址：http://www.pc6.com/soft/FireFox_579049.html

> 将解压后里面的.crx文件拖拽到谷歌浏览器的扩展程序中，选择"添加"

#### 添加扩展程序成功后，在页面中可以看到json格式的数据

{% asset_img note1.png %}



#### 