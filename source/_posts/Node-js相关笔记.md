---
title: Node.js相关笔记
date: 2020-08-24 12:18:15
tags:
- node.js
categories: 
- node.js
---

[Node.js官网](https://nodejs.org/zh-cn/)

[Cnode社区](https://cnodejs.org/)

[Node.js中文网](http://nodejs.cn/)

[Node.js 中文文档 | Node.js 中文网](https://www.nodeapp.cn/)

[淘宝NPM镜像](https://npm.taobao.org/)

Node.js&HTML5论坛

[npmmirror 镜像站](https://npmmirror.com/)   或 npm.taobao.org

**后端处理分页数据的接口**   [参考博客](https://www.cnblogs.com/fm060/p/8144758.html)

[element+express+mongoose实现分页查询](https://www.axis-studio.org/2017/12/29/element-express-mongoose实现分页查询/index.html)



[MongoDB With Node.js | MongoDB](https://www.mongodb.com/languages/mongodb-with-nodejs)











#### 后端接口代码：

```javascript
app.get('/api/getSources',async(req, res)=>{
    let currentPage = parseInt(req.query.currentPage) // 转换前端传入当前页码
    let pageSize = parseInt(req.query.pageSize) // 转换前端传入的每页大小
    let skip = (currentPage-1)*pageSize // 实现分割查询的skip
    let params = {}

    // 所有数据
    var allSources = await Sources.find();
    var allCount = allSources.length;
    var allPage = Math.ceil(allCount/pageSize);
    
    // 根据页码和每页显示条数筛选数据
    const sources = await Sources.find(params).skip(skip).limit(pageSize)

    var object ={
        allCount: allCount,
        allPage: allPage,
        page: currentPage,
        data: sources
    }
    res.send(object)
})
```

#### 前端请求接口代码：

```javascript
/**
 * 获取素材列表
 */
export const getSources = (param) => {
  return request({
    method: 'GET',
    url: '/getSources',
    params: param
  })
}
```

.vue页面：

```javascript
<el-pagination
  @size-change="handleSizeChange"
  @current-change="handleCurrentChange"
  :current-page="currentPage"
  :page-sizes="[10, 15, 20, 25, 30]"
  :page-size="pageSize"
  layout="total, sizes, prev, pager, next, jumper"
  :total="allCount">
</el-pagination>


sourceList: [],
allCount: 0,
pageSize: 10,
currentPage: 1,
  
created () {
  // 渲染第一页的数据
  this.initData(this.currentPage)
},
  
initData (thisPage) {
  let param = {
    currentPage: thisPage,
    pageSize: this.pageSize,
  }
  getSources(param).then(res => {
    console.log(res)
    this.sourceList = res.data.data
    this.allCount = res.data.allCount
  })
},
  
handleCurrentChange(val) {
  // console.log(`当前页: ${val}`);  
  // 渲染相应页码的数据
  this.initData(val)
}
```

#### 创建package.json：

```javascript
npm init
```

[npm模块管理器](http://javascript.ruanyifeng.com/nodejs/npm.html)

[我们安装了Nodejs是安装了什么](https://jingyan.baidu.com/article/91f5db1b3e1f991c7f05e395.html)

[安装 Node 和 gulp](https://github.com/nimoc/gulp-book/blob/master/chapter1.md)

### 安装

[node安装包下载地址](https://nodejs.org/zh-cn/download/)

1. 下载.msi文件
2. 按"下一步"，"下一步"装好
3. 双击安装好的目录里面的"node.exe"，文件，输入node  （这一步好像不需要）
4. 创建一个app.js文件

```javascript
const http = require("http");
const hostname = "127.0.0.1";
const port = 3000;
const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('He1lo world\n');
});

server.listen(port, hostname, ()=> {
	console.log(`Server running at http://${hostname}:${port}/`)
});
```

1. 运行app.js：

```javascript
node app.js
```

1. 在浏览器中预览

```javascript
http://localhost:3000/ 
或者
http://127.0.0.1:3000/
```

使用淘宝NPM镜像

```javascript
npm install -g cnpm --registry=https://registry.npm.taobao.org
```

清屏命令（清掉历史操作记录）

```javascript
cls
```

取消命令继续执行

```javascript
Ctrl +  C 
```

[window下通过nvm-windows来安装多版本node](https://blog.csdn.net/qq_36423639/article/details/70230571)

[全栈最后一公里 - Scott 带你学习 Node.js 线上服务器部署与发布](http://www.imooc.com/article/17554 Scott)

[七天学会NodeJS](http://nqdeng.github.io/7-days-nodejs/)



[Handlebars-轻量的语义化模板](https://www.handlebarsjs.cn/)



**什么是异步I/O？**

就是我们读取/写入文件或者操作数据库的时候，此时应该是异步的读取。CPU命令磁盘驱动器读取文件，CPU此时不能死等磁盘返回结果，如果死等CPU自己就被阻塞了，性能是极大的浪费。比如：PHP读取文件，性能就不高，因为被阻塞了。



### Node.js创建第一个应用

如果我们使用PHP来编写后端的代码时，需要Apache 或者Nginx 的 HTTP服务器，来处理客户端的请求相应。不过对Node.js 来说，概念完全不一样了。使用 Node.js时，我们不仅仅在实现一个应用，同时还实现了整个HTTP服务器。

1. 引入http模块

```javascript
var http= require("http");
```

1. 创建服务器

接下来我们使用http.createServer()方法创建服务器，并使用listen方法绑定8888端口。函数通过request, response参数来接收和响应数据。

```javascript
var http = require('http');

http.createServer(functio (request, response){
	// 发送HTTP头部
	// HTTP状态值: 200 : oK
  // 设置HTTP头部，状态码是200，文件类型是html，字符集是utf8
  response.writeHead(200,{"Content-Type":"text/html;charset=UTF-8"});

  // 发送响应数据“Hello World"
  res.end("哈哈哈哈，我买了一个iPhone" +(1+2+3)+"s"");
          
}).listen(8888);

// 终端打印如下信息
console.log("Server running at http://127.0.0.1:8888/");
```

结束响应：

```javascript
res.end();
```

### node.js查询数据，倒序排序：sort('-字段名')

```
let currentPage = parseInt(req.query.currentPage) // 转换前端传入当前页码
let pageSize = parseInt(req.query.pageSize) // 转换前端传入的每页大小
let skip = (currentPage-1)*pageSize // 实现分割查询的skip
let params = {'delete_time': "0"};

// 根据页码和每页显示条数筛选数据
const sources = await Sources.find(params).sort('-create_time').skip(skip).limit(pageSize)
```

#### [常用的Nodejs开发工具](http://www.bjpowernode.com/hot/2981.html)

- Express.js
- Socket.io
- Meteor
- Keystone
- Koa.js
- PM2.5
- Electrode.js
- Babel
- Broccoli
- Webpack



#### [JSON Server](https://www.npmjs.com/package/json-server)——模拟服务端接口数据

> 一般用在前后端分离后，前端人员可以不依赖 `API`开发，而在本地搭建一个 `JSON`服务，自己产生测试数据。

> 一个在本地运行，可以存储 `json`数据的 `server`。

1. 安装

   ```
   npm install -g json-server
   ```

2. 通过查看版本号，来测试是否安装成功

   ```
   json-server -v
   ```

3. 创建json数据 --` db.json`

   ```
   {
     "posts": [
       {
         "title": "title",
         "id": 1
       },
     ],
     "comments": [
       {
         "id": 1,
         "body": "some comment",
         "postId": 1
       }
     ],
     "profile": {
       "name": "typicode"
     }
   }
   ```

4. 开始服务——进入到` db.json`文件所在的目录，执行以下代码

   ```
   json-server --watch db.json
   ```

   `json-server `默认是 3000端口，我们也可以自己指定端口，指令如下：

   ```
   json-server --watch db.json --port 5000(端口号)
   ```

5. 查看接口返回数据

   ```
   http://localhost:5000/posts
   ```

6. 增删改查相关操作，[看语雀中的笔记](https://www.yuque.com/winney07/vp9xtm/ppi9zu#d8Beu)



#### 截屏保存图片插件

[casperjs](https://www.npmjs.com/package/casperjs)

phantomjs

[capture-phantomjs](https://www.npmjs.com/package/capture-phantomjs)