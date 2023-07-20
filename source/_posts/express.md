---
title: express
date: 2020-02-06 15:10:59
tags:
- express
categories: 
- node.js
- express
---

[Express官网](http://expressjs.com/)

[Express 中文网](https://www.expressjs.com.cn/)

### express-generator

> Express-generator是Express的应用生成器，通过使用生成器工具，可以快速创建一个Express的应用骨架

[express-generator简单使用](https://www.cnblogs.com/lihuijuan/p/10821815.html)

- express-generator是一个node的自动化创建项目工具，类似于vue-cli
- 通过express --version来检查当前版本号，若能显示出来，说明安装成功
- 安装后就可以使用express命令
- express 项目名，就会在当前文件夹下生成一个项目文件夹

[express-generator](https://blog.csdn.net/wanshiwusanren/article/details/120214652)

可把[package](https://so.csdn.net/so/search?q=package&spm=1001.2101.3001.7020)脚本中的node改成nodemon，方便热启动

#### 方式一

通过 `npx` （包含在 Node.js 8.2.0 及更高版本中）命令来运行 Express 应用程序生成器

1. 新建项目文件夹（myapp)，且切换到项目目录

2. 安装Express 应用程序生成器

   ```
   npx express-generator
   ```

3. 安装依赖包

   ```
   npm i
   ```

4. 启动应用

   ```
   npm start
   ```

5. 查看

   > 浏览器中打开 `http://localhost:3000/` 





### express应用HTTPS总结

摘自：[express应用HTTPS总结](https://www.jianshu.com/p/e83186622054/)

####  1. 跨域

##### `No 'Access-Control-Allow-Origin' header is present on the requested resource`

`express`没有允许跨域访问，使用`cors`中间件解决跨域问题，安装`cors`后在`app.js`中添加下方代码

```
yarn add cors
或
npm i cors
```

```
let cors = require('cors')

let corsOptions = {
    origin: '*' //允许访问的目标站点
}

app.use(cors(corsOptions))
```

#### 2. 混入内容被阻止

##### `Mixed content blocked” when running an HTTP AJAX operation in an HTTPS page`

你在启用了https的网站上访问了通过http传输的资源，例如加载外链、获取地图瓦片等，浏览器为了安全起见拒绝了你的请求，将有关http请求更换为https或本地加载来解决该问题

#### 3. SSL协议错误

##### `net::ERR_SSL_PROTOCOL_ERROR`

启用`https`的服务器上运行了`http`服务，在申请`https`后没有将`express`应用由默认的`http`更换为`https`，将下方代码加入到`app.js`中修改一下路径即可

```
// 引入部分
const express=require('express');
const bodyParser=require('body-parser');
const cors=require("cors");
const session=require("express-session");
// const userRouter=require("./routes/user");
const fs=require('fs');
//创建web服务器
var server=express();
// server.listen(3000);
var http=require('http');
var https=require('https');

//根据项目的路径导入生成的证书文件下面的key和pem是下载证书得到的
var privateKey  = fs.readFileSync('key.key', 'utf8');
var certificate = fs.readFileSync('pem.pem', 'utf8');
var credentials = {key: privateKey, cert: certificate};
 
var httpServer = http.createServer(server);
var httpsServer = https.createServer(credentials, server);
 
//可以分别设置http、https的访问端口号
var PORT = 3000;
var SSLPORT = 8080;
 
//创建http服务器
httpServer.listen(PORT, function() {
    console.log('HTTP Server is running on: http://localhost:%s', PORT);
});
 
//创建https服务器
httpsServer.listen(SSLPORT, function() {
    console.log('HTTPS Server is running on: https://localhost:%s', SSLPORT);
});
 
//可以根据请求判断是http还是https
server.get('/', function (req, res) {
    if(req.protocol === 'https') {
        res.status(200).send('This is https visit!');
    }
    else {
        res.status(200).send('This is http visit!');
    }
});


//使用body-parser中间件
server.use(bodyParser.urlencoded({
    extended:false
}))
//托管静态目录
server.use(express.static("public"))
//解决跨域问题
server.use(cors({
    origin:["http://127.0.0.1:8081","http://localhost:8081","http://127.0.0.1:8080","http://localhost:8080"],
    credentials:true
}))
// session功能
server.use(session({
    secret:"128字符串",
    resave:true,
    saveUninitialized:true
}))
// 挂载路由
// server.use('/user',userRouter);
```

> 主要是express需要加载https模块

### 传参

[04 基于Express框架创建的Node后台获取前端传过来的参数](https://blog.51cto.com/u_11378682/4931109)

[前端开发：express的具体操作流程](https://zhuanlan.zhihu.com/p/145760258)

[前后端交互-Express框架](https://www.jianshu.com/p/a75a521921e2)

[React+Node+Express搭建一个前后端demo](https://segmentfault.com/a/1190000019608194)

#### get方法传参

`api.js`：

```
server.get('/user/:id', function (req, res, next) {
    console.log('req.params')     	
    console.log(req.params)    		//  {id: 1000}
    res.status(200).send('winney---' +  req.params.id);     //  winney---1000
})
```

前端：

```
wx.request({
  url: 'https://www.winney07.cn:8080/user/1000',  
  data: {},
  header: {
    'content-type': 'application/json' // 默认值
  },
  success (res) {
    console.log('接口返回的数据')
    console.log(res)
    // console.log(res.data)
  },
  fail(err) {
    console.log(err)
  }
})
```

#### post方法传参