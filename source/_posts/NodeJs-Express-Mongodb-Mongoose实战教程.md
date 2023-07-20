---
title: NodeJs-Express-Mongodb-Mongoose实战教程
date: 2021-03-02 11:03:04
tags:
- node.js
- express
- mongodb
- mongoose
categories: 
- node.js
---

课程链接：[nodejs教程_2020年最新NodeJs+Express+Mongodb+Mongoose入门实战教程](https://www.bilibili.com/video/BV16f4y1U7oT)

#### 判断是否安装成功

```
node -v
```

#### Vscode快速生成代码块

在vscode里面安装`node-snippets`，会有node代码的相关代码提示。安装完之后，重启vscode即可生效

#### http模块-基本使用

例如，在`app.js`中输入`nodehttp`，会有`node-http-server`等语句的提示，选择`node-http-server`，会生成对应的代码块：

```
//表示引入http模块
var http = require('http');
/*
request		获取客户端传过来的信息
response	给浏览器响应信息
*/
http.createServer(function (request, response) {
  //设置响应头
  response.writeHead(200, {'Content-Type': 'text/plain'});
  //表示给我们页面上面输出一句话并且结束响应
  response.end('Hello World');
}).listen(8081); // 端口

console.log('Server running at http://127.0.0.1:8081/');
```

运行：

```
node app.js
```

在控制台显示：

```
Server running at http://127.0.0.1:8081/
```

浏览器访问http://127.0.0.1:8081/，可看到：

```
Hello World
```

> 如果修改了app.js里面的内容，需要重新运行`node app.js`

#### http模块-基本使用2

```
const http = require('http');

http.createServer((req, res) =>{
    console.log(req.url);

    // 设置响应头
    // 状态码 200， 文件类型是htm1，字符集是utf-8
    res.writeHead(200, {"Content-type": "text/html;charset='utf-8'"});  // 解决乱码

    res.write('你好  nodejs');

    res.end();   // 一定要写end
}).listen(3001)
```

浏览器访问：http://127.0.0.1:3001/，显示：

```
浣犲ソ nodejs
```

加上以下代码，解决乱码：

```
res.write('<head> <meta charset="UTF-8"></head>');  // 解决乱码
```

```
const http = require('http');

http.createServer((req, res) =>{
    console.log(req.url);

    // 设置响应头
    // 状态码 200， 文件类型是htm1，字符集是utf-8
    res.writeHead(200, {"Content-type": "text/html;charset='utf-8'"});   // 解决乱码

    res.write('<head> <meta charset="UTF-8"></head>');  // 解决乱码

    res.write('你好  nodejs');
    
    res.write('<h2>你好  nodejs</h2>');

    res.end();   // 一定要写end
}).listen(3001)
```

重新启动

```
node app.js
```



#### url模块-基本使用

> nodejs的内置模块

```
const url = require('url');

var api = 'http://www.itying.com?name=zhangsan&age=20';

var params = url.parse(api, true).query;

console.log(`姓名： ${params.name}--年龄： ${params.age}`)
```

控制台输出：

```
姓名： zhangsan--年龄： 20
```

#### http+url模块的基本使用

```
const http = require('http');
const url = require('url');

http.createServer((req, res) =>{
    console.log(req.url);

    // http://127.0.0.1:3001/?name=zhangsan&age=20  

    // 设置响应头
    // 状态码 200， 文件类型是htm1，字符集是utf-8
    res.writeHead(200, {"Content-type": "text/html;charset='utf-8'"});   // 解决乱码

    res.write('<head> <meta charset="UTF-8"></head>');  // 解决乱码

    if(req.url != '/favicon.ico') {
        var userinfo = url.parse(req.url, true).query;
        console.log(`姓名： ${userinfo.name}--年龄： ${userinfo.age}`)
    }


    res.write('你好  nodejs');

    res.write('<h2>你好  nodejs</h2>');

    res.end();   // 一定要写end
}).listen(3001)
```

在浏览器访问：http://127.0.0.1:3001/?name=zhangsan&age=20  

控制台显示：`姓名： zhangsan--年龄： 20`

#### Nodejs自启动工具supervisor

1. 安装supervisor

   ```
   npm i -g supervisor
   ```

2. 使用supervisor代替node命令启动应用

   ```
   supervisor app.js         
   ```

   `注意：`如果在vscode中，识别不了`supervisor`命令，需要重启vscode

### CommonJs 和Nodejs模块、自定义模块

#### Nodejs中的模块化

Node应用由模块组成，采用CommonJS模块规范。

在nodejs中，模块分为两类：

- 核心模块（node提供的模块，如：http模块、url模块、fs模块都是nodejs内置的核心模块，可以直接引入使用）
- 文件模块（用户编写的模块）

`module/tools.js`：

##### 自定义模块

```
/*
1.我们可以把公共的功能抽离成为一个单独的js 文件作为一个模块，默认情况下面这个模块里面的方法或者属性，外面是没法访问的。如果要让外部可以访问模块里面的方法或者属性，就必须在模块里面通过 exports或者module.exports 暴露属性或者方法。
2．在需要使用这些模块的文件中，通过require的方式引入这个模块。这个时候就可以使用模块里面暴露的属性和方法。
*/

function formatApi(api) {
    return 'http://www.itying.com/' + api
}

exports.formatApi = formatApi;
```

##### 外部引用

```
const tools = require('./module/tools')

 var api = tools.formatApi('api/focus');
 
 res.write(api);
```

在浏览器看到的输出：

```
http://www.itying.com/api/focus
```

#### exports的使用

`request.js`：

```
var obj = {
    get:function() {
        console.log('从服务器获取数据')
    },
    post: function(){
        console.log('提交数据')
    }
}

exports.xxxx = obj;
```

`app.js`：

```
const request = require('./module/request');

console.log(request);

request.xxxx.get();
```

运行：

```
node app.js

// 控制台输出：
{ xxxx: { get: [Function: get], post: [Function: post] } }
从服务器获取数据
```

#### `module.export`的使用

`request.js`：

```
var obj = {
    get:function() {
        console.log('从服务器获取数据')
    },
    post: function(){
        console.log('提交数据')
    }
}

module.exports = obj;
```

`app.js`：

```
const request = require('./module/request');

console.log(request);

request.get();
```

运行：

```
node app.js

// 控制台输出：
{ get: [Function: get], post: [Function: post] }
从服务器获取数据
```

#### exports单独导出

`request.js`：

```
// 单独导出
exports.get =  function() {
    console.log('从服务器获取数据')
}

exports.post =  function() {
    console.log('提交数据')
}
```

`app.js`：

```
const request = require('./module/request');

console.log(request);

request.get();
```

运行：

```
node app.js

// 控制台输出：
{ get: [Function: get], post: [Function: post] }
从服务器获取数据
```

#### node_modules目录的模块使用

在项目目录中，新建`node_modules`目录，创建`axios`目录，新建`index.js`文件

`node_modules\axios\index.js`：

```
exports.get =  function() {
    console.log('从服务器获取数据')
}

exports.post =  function() {
    console.log('提交数据')
}
```

`app.js`

```
const axios = require('./node_modules/axios/index.js');

console.log(axios);

axios.get();

axios.post();
```

运行：

```
node app.js

// 控制台输出：
{ get: [Function (anonymous)], post: [Function (anonymous)] }
从服务器获取数据
提交数据 
```

##### node_modules目录的模块--引用时的简写

nodejs里面，`node_modules`目录里面定义的模块，可以省略`node_modules`路径

```
const axios = require('axios/index.js');
```

`index.js`文件为默认执行文件，也可以省略写

```
const axios = require('axios');
```

##### node_modules目录的模块（非index.js文化）--引用

`node_modules\db\db.js`：

```
exports.find =  function() {
    console.log('查找数据')
}

exports.add =  function() {
    console.log('增加')
}
```

`app.js`

```
const db = require('db');
db.add();
```

运行：

```
node app.js

// 控制台输出：
  throw err;
  ^
Error: Cannot find module 'db'
```

> 因为db里面的db.js不是index.js

###### 解决方案：

切换到`node_modules\db`目录，执行以下代码：

```
npm init --yes
或
npm init -y
```

`package.json`：

```
{
  "name": "db",
  "version": "1.0.0",
  "description": "",
  "main": "db.js",      // 入口文件是db.js
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}
```

重新运行：

```
node app.js

// 控制台输出：
增加
```

### Nodejs中的包、npm 、第三方模块、package.json以及cnpm

#### 包

> Nodejs中除了它自己提供的核心模块外，我们可以自定义模块，也可以使用第三方的模块。Nodejs 中第三方模块由包组成，可以通过包来对一组具有相互依赖关系的模块进行统一管理。

![包](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/Node-js%E7%9B%B8%E5%85%B3%E7%AC%94%E8%AE%B0/%E5%8C%85.png)



##### 完全符合CommonJs规范的包目录一般包含如下这些文件。

- package.json：包描述文件。
- bin：用于存放可执行二进制文件的目录。
- lib：用于存放JavaScript代码的目录。
- doc：用于存放文档的目录。

> 在 NodeJs中通过NPM命令来下载第三方的模块（包）。

#### npm

npm是`世界上最大的开放源代码`的生态系统。我们可以通过npm下载各种各样的包，这些源代码(包）我们可以在 https://www.npmjs.com找到。

**npm是随同NodeJS一起安装的包管理工具，能解决NodeJS 代码部署上的很多问题，常见的使用场景有以下几种：**

- 允许用户从NPM服务器下载别人编写的第三方包到本地使用。(silly-datetime)
- 允许用户从NPM服务器下载并安装别人编写的命令行程序(工具)到本地使用。(supervisor)
- 允许用户将自己编写的包或命令行程序上传到NPM服务器供别人使用。

##### --save

> 安装依赖包的时候，加上`--save`，这样在`package.json`文件中的`dependencies`中就有包的相关信息，当我们将`package.json`分享给别人的时候，别人直接执行`npm i` 或`cnpm i`就可以安装项目中的依赖包。可以根据package.json来安装对应的依赖包

#### package.json

创建package.json：

```
npm init  或者  npm init -yes
```

> npm i / cnpm i表示安装dependencies对应的包   如果删掉node_modules可以通过此命令找到 package.json对应的所有的包信息

```
"dependencies" : {
    "ejs":"^2.3.4",
    "express": "^4.13.3",
    "formidable": "^1.0.17"
}
```

- `^`表示第一位版本号不变，后面两位取最新的
- `~`表示前两位不变，最后一个取最新
- `*`表示全部取最新

> 如果要指定版本安装，将版本号前面的`^/~/*`去掉即可

#### 淘宝镜像

- http://www.npmjs.org     npm包官网
- https://npm.taobao.org/   淘宝npm镜像官网

> 淘宝NPM镜像是一个完整npmjs.org镜像，你可以用此代替官方版本(只读)，同步频率目前为10分钟一次以保证尽量与官方服务同步。

我们可以使用我们定制的cnpm (gzip压缩支持)命令行工具代替默认的npm：

```
npm install -g cnpm --registry=https://registry.npm.taobao.org
```

### Nodejs中的fs模块的使用

1. fs.stat检测是文件还是目录
2. fs.mkdir创建目录
3. fs.writeFile创建写入文件
4. fs.appendFile追加文件
5. fs.readFile读取文件
6. fs.readdir读取目录
7. fs.rename重命名
8. fs.rmdir删除目录
9. fs.unlink删除文件

创建`package.json`：

```
npm init
```

```
{
  "name": "02",
  "version": "1.0.0",
  "description": "",
  "main": "app.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC"
}
```

#### 检测是文件还是目录

`app.js`：

```
const fs = require('fs');

fs.stat('./package.json', (err, data) => {
    if(err) {
        console.log(err);
        return;
    }

    console.log(`是文件：${data.isFile()}`);
    console.log(`是目录：${data.isDirectory()}`);
})
```

运行：

```
node app.js

// 控制台输出：
是文件：true
是目录：false
```

#### 创建目录

`app.js`

```
fs.mkdir('./css', err => {
    if(err) {
        console.log(err);
        return;
    }

    console.log('创建成功')
})
```

运行：

```
node app.js

// 控制台显示：
创建成功

node app.js

// 控制台显示：
[Error: EEXIST: file already exists, mkdir 'H:\Gitee\nodejs\node_demo\02\css'] {
  errno: -4075,
  code: 'EEXIST',
  syscall: 'mkdir',
  path: 'H:\\Gitee\\nodejs\\node_demo\\02\\css'
}
```

#### 创建写入文件

`如果不存在文件，就直接创建文件且写入内容；如果存在文件，就直接写入内容，替换旧的`

```
// app.js
fs.writeFile('./html/index.html', '你好nodejs', err => {
    if(err) {
        console.log(err);
        return;
    }

    console.log('创建写入文件成功');
})

node app.js
// 控制台显示：
创建写入文件成功

// app.js
fs.writeFile('./html/index.html', '你好nodejs---写入文件', err => {
    if(err) {
        console.log(err);
        return;
    }

    console.log('创建写入文件成功');
})

node app.js
// 控制台显示：
创建写入文件成功
```

参数说明：

```
filename        (String)                文件名称
data            (String | Buffer)       将要写入的内容，可以使字符串或buffer数据。
options         (object)                option数组对象，包含:
    · encoding  (String)                可选值，默认‘utf8'，当data使buffer时，该值应该为ignore
    · mode      (Number)                文件读写权限，默认值438
    · flag      (String)                默认值‘w’
 callback       {Function}              回调，传递一个异常参数err。
```

#### 追加文件

`如果不存在文件，就直接创建文件且写入内容；如果存在文件，就直接追加添加的内容到后面`

```
fs.appendFile('./css/base.css', 'body{color:red}\n', err => {
    if(err) {
        console.log(err);
        return;
    }

    console.log('追加文件成功');
})

node app.js
// 控制台显示：
追加文件成功

fs.appendFile('./css/base.css', 'h3{color:red}\n', err => {
    if(err) {
        console.log(err);
        return;
    }

    console.log('追加文件成功');
})

node app.js
// 控制台显示：
追加文件成功
```

`./css/base.css`：

```
body{color:red}
h3{color:red}

```

#### 读取文件

```
fs.readFile('./html/index.html', (err, data) => {
    if(err) {
        console.log(err);
        return;
    }

    console.log(data);
    console.log(data.toString());    // 把Buffer转化成string类型
})
```

```
node app.js
// 控制台输出：
<Buffer e4 bd a0 e5 a5 bd 6e 6f 64 65 6a 73 2d 2d 2d 2d 2d e5 86 99 e5 85 a5 e6 96 87 e4 bb b6>
你好nodejs-----写入文件
```

#### 读取目录

```
html
    │  index.html
    │  news.html
    │
    └─js
```

```
fs.readdir('./html', (err, data) => {
    if(err) {
        console.log(err);
        return;
    }

    console.log(data);
})
```

> 读取该目录下的目录以及文件

```
node app.js
// 控制台输出：
[ 'index.html', 'js', 'news.html' ]
```

#### 重命名·移动文件

`功能:1、表示重命名2、移动文件`

##### 重命名

```
fs.rename('./css/aaa.css', './css/index.css', err => {
    if(err) {
        console.log(err);
        return;
    }

    console.log('重命名成功');
})
```

##### 移动文件

```
fs.rename('./css/index.css', './html/index.css', err => {
    if(err) {
        console.log(err);
        return;
    }

    console.log('移动文件成功');
})
```

#### 删除目录

`如果目录里面有文件，直接删除目录，会删除失败`

> aaa目录里面有index.html文件

```
fs.rmdir('./aaa', err => {
    if(err) {
        console.log(err);
        return;
    }

    console.log('删除目录成功');
})
```

```
node app.js
// 控制台输出：
[Error: ENOTEMPTY: directory not empty, rmdir 'H:\Gitee\nodejs\node_demo\02\aaa'] {
  errno: -4051,
  code: 'ENOTEMPTY',
  syscall: 'rmdir',
  path: 'H:\\Gitee\\nodejs\\node_demo\\02\\aaa'
}
```

`所以要先删除该目录中的文件`

#### 删除文件

```
fs.unlink('./aaa/index.html', err => {
    if(err) {
        console.log(err);
        return;
    }

    console.log('删除文件成功');
})
```

````
node app.js
// 控制台输出：
删除文件成功
````

`然后再执行删除目录的命令`

```
fs.rmdir('./aaa', err => {
    if(err) {
        console.log(err);
        return;
    }

    console.log('删除目录成功');
})
```

```
node app.js
// 控制台输出：
删除目录成功
```

#### 案例

判断服务器上面有没有upload目录。如果没有创建这个目录，如果有的话不做操作。(图片上传)

```
const fs = require('fs');
var path = './upload';

fs.stat(path, (err, data)=> {
    if(err) {
        console.log(err);
        mkdir(path);
        return;
    }

    if(data.isDirectory()){
        console.log('目录已经存在')
    } else {
        // 如果存在upload文件，首先删除文件，再去执行创建目录
        fs.unlink(path, err =>{
            if(err) {
                console.log('请检测传入的数据是否正确');
            } else {
                mkdir(path);
            }
        })
    }
})

// 创建目录的函数
function mkdir(path) {
    fs.mkdir(path, err => {
        if(err) {
            console.log(err);
            return;
        }

        console.log('创建目录成功');
    })
}
```

#### mkdirp的使用

```
npm i mkdirp --save
```

创建目录

````
const mkdirp = require('mkdirp');
mkdirp('./uploadDir').then(made =>
    console.log(`made directories, starting with ${made}`)
)
````

一次生成多级目录

```
const mkdirp = require('mkdirp');

mkdirp('./upload/img/xxxx');
```

#### 案例2

wwwroot文件夹下面有images css js 以及index.html，找出wwwroot目录下面的所有的目录，然后放在一个数组中

```
const fs = require('fs');

fs.readdir('./wwwroot', (err, data) => {
    if(err) {
        console.log(err);
        return;
    }

    console.log(data)
})
```

```
// 结果：
[ 'css', 'images', 'index.html', 'js' ]   包含文件
```

`注意：fs里面的方法是异步的`

`fs.stat是异步方法，把fs.stat放在for循环里面执行，不起作用`

```
// 错误的写法  注意：fs里面的方法是异步的
var path = './wwwroot';
var dirArr = [];  // 所以目录的数组

fs.readdir(path, (err, data) => {
    if(err) {
        console.log(err);
        return;
    }

    for(var i = 0; i< data.length; i++) {
        fs.stat(path + '/' + data[i], (err, stats) => {
            if(stats.isDirectory()) {
                dirArr.push(data[i])
            }
        })
    }

    console.log(dirArr);
}) 
console.log(dirArr);
```

> for循环执行得比较快，100毫秒内已经执行完了这个循环

```
for(var i = 0; i<3; i++) {
	setTimeout(function(){
		console.log(i);
	},100)
}
// 控制台显示：
3
3
3
```

##### 解决方案

1. ###### 改造for循环  递归实现

   ```
   var path = './wwwroot';
   var dirArr = [];  // 所以目录的数组
   
   fs.readdir(path, (err, data) => {
       if(err) {
           console.log(err);
           return;
       }
   
       (function getDir(i) {
           if(i === data.length) {    // 执行完成
               console.log(dirArr);
               return;
           }
           fs.stat(path + '/' + data[i], (err, stats) => {
               if(stats.isDirectory()) {
                   dirArr.push(data[i])
               }
               getDir(i+1);
           })
       })(0)
   })
   ```

   ```
   // 结果：
   [ 'css', 'images', 'js' ]
   ```

2. ###### nodejs里面的新特性  async await

#### Nodejs新特性async await的使用以及使用async await处理异步

使用回调函数，获取异步的值


   ```
function getData(callback){
	// ajax
    setTimeout(function(){
        var name = '张三';
        callback(name);
    },1000);
}

getData(function(name){
    console.log(name);
})
   ```

```
node app.js
// 控制台显示：
张三
```

##### Async、Await和Promise的使用

> async是“异步”的简写,而 await可以认为是 async wait 的简写。所以应该很好理解 async用于申明一个异步的 function ,而await用于等待一个异步方法执行完成。
>
> 简单理解：
>
> async：让方法变成异步
>
> await：等待异步方法执行完成

使用promise获取异步的值

```
var p = new Promise((resolve, reject) => {
    setTimeout(function(){
        var name = '张三222';
        resolve(name);
    },1000);
})

/* p.then(function(res){
    console.log(res);
}) */

p.then((res) =>{
    console.log(res);
})

// 封装函数：
// 封装函数
function getData(resolve, reject){
    setTimeout(function(){
        var name = '张三222';
        resolve(name);
    },1000);
}

var p = new Promise(getData);
p.then(res => {
    console.log(res);
})
```

async与await

```
async function test(){
    return '学习nodejs';
}

async function main(){
    var data = await test();    // 获取异步方法里面的数据    要与async配合使用
    console.log(data);
}

main();
```

```
// 返回promise
async function test(){
    return new Promise((resolve, reject) =>{
        setTimeout(function(){
            var name = '张三333';
            resolve(name);
        },1000);
    })
}

async function main(){
    var data = await test();    // 获取异步方法里面的数据    要与async配合使用
    console.log(data);
}

main();
```

案例2使用async和await的解决

```
const fs = require('fs');
// 1、定义一个isDir的方法判断一个资源到底是目录还是文件
async function isDir(path){
    return new Promise((resolve, reject) => {
        fs.stat(path, (err, stats) => {
            if(err) {
                console.log(err);
                reject(err);
                return;
            }
            if(stats.isDirectory()){
                resolve(true);
            }else {
                resolve(false);
            }
        })
    })
}

// 2、获取wwwroot里面的所有资源循环遍历
function main(){
    var path = './wwwroot';
    var dirArr = [];
    fs.readdir(path, async (err, data) => {
        if(err) {
            console.log(err);
            return;
        }

        for(var i = 0; i< data.length; i++) {
            if(await isDir(path + '/' + data[i])){
                dirArr.push(data[i]);
            }
        }

        console.log(dirArr);
    })
}

main();
```

#### Nodejs fs中的流以及管道流

##### fs.createReadStream从文件流中读取数据

以流的方式读取

```
const fs = require('fs');

var readStream = fs.createReadStream('./input.txt');

var count = 0;
var str = '';

readStream.on('data', (chunk) => {
    console.log(`${++count} 接收到：${chunk.length}`);
    str+=chunk;
})

readStream.on('end', () => {
    console.log(str);
    console.log(count);
})

readStream.on('error', (err) => {
    console.log(err);
})
```

#### fs.createWriteStream写入文件

```
const fs = require('fs');
var str = '';
for(var i = 0; i< 500; i++) {
    str+= '我是从数据库获取的数据，要保存起来\n';
}
// 创建一个可以写入的流，写入到文件output.txt中
var writeSteam = fs.createWriteStream('./output.txt');

// 使用utf8编码写入数据
// writeSteam.write(str, 'UTF8')

writeSteam.write(str);

// 标记写入完成
writeSteam.end();
// 要执行writeSteam.end()，才可以调用finish；不执行writeSteam.end()，也会写入完成，只是finish事件监听不到
// 异步
// 处理流事件——> finish事件
writeSteam.on('finish', () => {    // finish--所有数据已被写入到底层系统时触发
    console.log('写入完成');    // 控制台后打印
})

console.log('程序执行完毕');    // 控制台先打印
```

#### 管道读写操作

复制文件，从一个流到另一个流

```
const fs = require('fs');

// 创建一个可读流
var readStream = fs.createReadStream('./aaa.jpg');
// 创建一个可写流
var writeSteam = fs.createWriteStream('./data/aaa.jpg');

// 管道读写操作
// 读取aaa.jpg文件，并写入到data中
readStream.pipe(writeSteam);     
```

还可以重命名

```
const fs = require('fs');

// 创建一个可读流
var readStream = fs.createReadStream('./app.js');
// 创建一个可写流
var writeSteam = fs.createWriteStream('./data/test.js');

// 管道读写操作
// 读取aaa.js的文件内容，并将内容写入到data/test.js文件中
readStream.pipe(writeSteam);
```

#### 利用HTTP模块Url模块Path模块Fs模块创建一个静态 WEB服务器

`tree /f`：

```
demo
│  app.js
│  package.json     
│  
└─static
    │  404.html     
    │  index.html   
    │  login.html   
    │  
    ├─css
    │      index.css
    │
    ├─images
    │      blog-head.jpg
    │      favicon.ico
    │
    ├─js
    │      index.js
    │
    └─json
            data.json
```

http模块

```
const http = require('http');
http.createServer(function (req, res) {
    res.writeHead(200, {'Content-Type': 'text/plain'});
    res.end('Hello World');
}).listen(8081);

console.log('Server running at http://127.0.0.1:8081/');
```

根据访问路径，返回对应的文件

```
const http = require('http');
const fs = require('fs');

http.createServer(function (req, res) {
    // 1.获取地址
    var pathname = req.url;
    pathname = pathname == '/' ? '/index.html' : pathname;
    // 2. 通过fs模块读取文件
    if(pathname != '/favicon.ico') {
        fs.readFile('./static' + pathname, (err, data) =>{
            if(err) {
                // console.log(err);
                res.writeHead(404, {'Content-Type': 'text/html;charset="utf-8"'});
                res.end('404');
            }

            res.writeHead(200, {'Content-Type': 'text/html;charset="utf-8"'});
            res.end(data);
        })
    }
}).listen(8081);

console.log('Server running at http://127.0.0.1:8081/');
```

存在问题，css文件访问格式不对

自定义一个模块，根据不同的文件类型（文件后缀名），返回不同的`Content-Type`

`module/common.js`：

```
exports.getMime = function(extname) {
    switch(extname) {
        case '.html':
            return 'text/html';
        case '.css':
            return 'text/css';
        case '.js':
            return 'text/javascript';
        default:
            return 'text/html';
    }

}
```

css文件访问格式不对：

`使用path.extname()获取后缀名`

```
const http = require('http');
const fs = require('fs');
const path = require('path');
const common = require('./module/common.js');

http.createServer(function (req, res) {
    // 1.获取地址
    var pathname = req.url;
    pathname = pathname == '/' ? '/index.html' : pathname;
    // path.extname()获取后缀名
    let extname = path.extname(pathname);
	// 2. 通过fs模块读取文件
    if(pathname != '/favicon.ico') {
        fs.readFile('./static' + pathname, (err, data) =>{
            if(err) {
                // console.log(err);
                res.writeHead(404, {'Content-Type': 'text/html;charset="utf-8"'});
                res.end('404');
            }
            let mime = common.getMime(extname);
            res.writeHead(200, {'Content-Type': '' + mime + ';charset="utf-8"'});
            res.end(data);
        })
    }
}).listen(8081);

console.log('Server running at http://127.0.0.1:8081/');
```

解决获取json文件时有get参数时，页面显示404

`使用url模块的url.parse()去掉get传值后的参数`

```
const http = require('http');
const fs = require('fs');
const path = require('path');
const url = require('url');
const common = require('./module/common.js');

http.createServer(function (req, res) {
    // 1.获取地址
    // var pathname = req.url;   
    var pathname = url.parse(req.url).pathname;   // 去掉get传值后的参数
    pathname = pathname == '/' ? '/index.html' : pathname;
    // path.extname()获取后缀名
    let extname = path.extname(pathname);
    // 2. 通过fs模块读取文件
    if(pathname != '/favicon.ico') {
        fs.readFile('./static' + pathname, (err, data) =>{
            if(err) {
                // console.log(err);
                res.writeHead(404, {'Content-Type': 'text/html;charset="utf-8"'});
                res.end('404,这个页面不存在');
            }
            let mime = common.getMime(extname);
            res.writeHead(200, {'Content-Type': '' + mime + ';charset="utf-8"'});
            res.end(data);
        })
    }
}).listen(8081);

console.log('Server running at http://127.0.0.1:8081/');
```

`module/common.js`：

使用mime.json动态获取content-type

```
const fs = require('fs');
exports.getFileMime = function(extname) {
    return new Promise((resolve, reject) => {
        fs.readFile('./static/data/mime.json', (err, data) => {
            if(err) {
                console.log(err);
                reject(err);
            }
            // console.log(data);   // <Buffer类型
            // console.log(data.toString());
            // console.log(JSON.parse(data.toString()));

            var mimeObj = JSON.parse(data.toString());
            console.log(mimeObj[extname])
            resolve(mimeObj[extname]);
        })
    })
}
```

`app.js`：

```
....
if(pathname != '/favicon.ico') {
    fs.readFile('./static' + pathname, async (err, data) =>{
        if(err) {
            // console.log(err);
            res.writeHead(404, {'Content-Type': 'text/html;charset="utf-8"'});
            res.end('404,这个页面不存在');
        }
        // let mime = common.getMime(extname);
        let mime =await common.getFileMime(extname);
        res.writeHead(200, {'Content-Type': '' + mime + ';charset="utf-8"'});
        res.end(data);
    })
}
    
.....
```

> 在网页中的network中，可以看到不同类型的文件请求的content-type不一样了

`module/common.js`：

使用同步的方法

```
exports.getFileMime = function(extname) {
    var data = fs.readFileSync('./static/data/mime.json');     // 同步方法

    var mimeObj = JSON.parse(data.toString());
    // console.log(mimeObj[extname]);
    return mimeObj[extname];
}
```

`app.js`：

```
....
if(pathname != '/favicon.ico') {
    fs.readFile('./static' + pathname, (err, data) =>{
        if(err) {
            // console.log(err);
            res.writeHead(404, {'Content-Type': 'text/html;charset="utf-8"'});
            res.end('404,这个页面不存在');
        }
        let mime = common.getFileMime(extname);
        res.writeHead(200, {'Content-Type': '' + mime + ';charset="utf-8"'});
        res.end(data);
    })
}
    
.....
```

#### NodeJs 封装静态WEB服务、路由、EJS模板引擎、GET、POST

`module/routes.js`：

```
const fs = require('fs');
const path = require('path');
const url = require('url');

let getFileMime = function(extname) {
    var data = fs.readFileSync('./static/data/mime.json');     // 同步方法

    var mimeObj = JSON.parse(data.toString());
    // console.log(mimeObj[extname]);
    return mimeObj[extname];
}

// 封装-创建静态web服务
exports.static = function(req, res, staticPath) {
    // 1.获取地址
    var pathname = url.parse(req.url).pathname;   // 去掉get传值后的参数
    pathname = pathname == '/' ? '/index.html' : pathname;
    // path.extname()获取后缀名
    let extname = path.extname(pathname);
    // 2. 通过fs模块读取文件
    if(pathname != '/favicon.ico') {
        fs.readFile('./' + staticPath + pathname,(err, data) =>{
            if(err) {
                // console.log(err);
                res.writeHead(404, {'Content-Type': 'text/html;charset="utf-8"'});
                res.end('404,这个页面不存在');
            }
            let mime = getFileMime(extname);
            res.writeHead(200, {'Content-Type': '' + mime + ';charset="utf-8"'});
            res.end(data);
        })
    }
}
```

`app.js`：

```
const http = require('http');
const routes = require('./module/routes.js');

http.createServer(function (req, res) {
    // 创建静态web服务
    routes.static(req, res, 'static');
}).listen(8081);

console.log('Server running at http://127.0.0.1:8081/');
```

##### 路由

> 路由（Routing〉是由一个URL(或者叫路径）和一个特定的 HTTP方法（GET、POST等）组成的，涉及到应用如何响应客户端对基个网站节点的访问。

**通俗的说：**
	路由指的就是针对不同请求的URL，处理不同的业务逻辑。

##### 访问路径，加上路由的处理：

> 【匹配不到对应文件（index.html、login.html等），继续往下匹配路由，再处理404的问题】

`因为fs.readFile是异步的，所以要改为同步的`，  不然`routes.static(req, res, 'static');`会匹配不到，就到匹配404页面了

`module/routes.js`：

```
const fs = require('fs');
const path = require('path');
const url = require('url');

let getFileMime = function(extname) {
    var data = fs.readFileSync('./static/data/mime.json');     // 同步方法

    var mimeObj = JSON.parse(data.toString());
    // console.log(mimeObj[extname]);
    return mimeObj[extname];
}

// 封装-创建静态web服务
exports.static = function(req, res, staticPath) {
    // 1.获取地址
    var pathname = url.parse(req.url).pathname;   // 去掉get传值后的参数
    pathname = pathname == '/' ? '/index.html' : pathname;
    // path.extname()获取后缀名
    let extname = path.extname(pathname);
    // 2. 通过fs模块读取文件
    // 同步的方法
    if(pathname != '/favicon.ico') {
        try {
            let data = fs.readFileSync('./' + staticPath + pathname);
            if(data) {
                let mime = getFileMime(extname);
                res.writeHead(200, {'Content-Type': '' + mime + ';charset="utf-8"'});
                res.end(data);
            }
        } catch (error) {
            
        }
    }
}
```

`app.js`：

```
const http = require('http');
const fs = require('fs');
const routes = require('./module/routes.js');
const url = require('url');

http.createServer(function (req, res) {
    // 创建静态web服务
    routes.static(req, res, 'static');     // static里面的fs.readFile要改为fs.readFileSync
    // 路由
    var pathname = url.parse(req.url).pathname; 

    if(pathname == '/login') {
        res.writeHead(200, {'Content-Type': 'text/html;charset="utf-8"'});
        res.end('执行登录');
    } else if(pathname == '/register') {
        res.writeHead(200, {'Content-Type': 'text/html;charset="utf-8"'});
        res.end('执行注册');
    } else if(pathname == '/admin') {
        res.writeHead(200, {'Content-Type': 'text/html;charset="utf-8"'});
        res.end('处理后的业务逻辑');
    } else {
        fs.readFile('./static' + pathname, (err, data) => {
            if(err) {
                // console.log(err);
                res.writeHead(404, {'Content-Type': 'text/html;charset="utf-8"'});
                res.end('404, 页面不存在');
            }
        })
    } 
    
    // 老师的代码是直接使用下面这段，但是这样，我页面访问index.html会获取不到图片，样式和js文件，访问这些文件的路径会进去else里
    // else {
    //     res.writeHead(404, {'Content-Type': 'text/html;charset="utf-8"'});
    //     res.end('页面不存在');
    // }

}).listen(8081);

console.log('Server running at http://127.0.0.1:8081/');
```

### 初识[EJS模块](https://www.npmjs.com/package/ejs)引擎

我们学的EJS是后台模板，可以把我们数据库和文件读取的数据显示到Html页面上面。它是一个第三方模块，需要通过npm安装

```
npm install ejs --save
```

`app.js`：

```
const ejs = require('ejs');
....
if(pathname == '/login') {
    let msg = '从数据库中获取到的数据';
    ejs.renderFile('./views/login.ejs', {msg:msg},(err, data) => {
        res.writeHead(200, {'Content-Type': 'text/html;charset="utf-8"'});
        res.end(data);
    })
}
....
```

`./views/login.ejs`：

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ejs模块</title>
</head>
<body>
    <h3><%= msg %></h3>
</body>
</html>
```

`app.js`：

```
if(pathname == '/news') {
    let list = [
        {id:1001, title: '新闻1111'},
        {id:1002, title: '新闻2222'},
        {id:1003, title: '新闻3333'},
        {id:1004, title: '新闻4444'},
        {id:1005, title: '新闻5555'},
    ]
    ejs.renderFile('./views/news.ejs', {newList:list}, {}, (err, data) => {
        res.writeHead(200, {'Content-Type': 'text/html;charset="utf-8"'});
        res.end(data);
    })
}
```

`./views/news.ejs`：

```
<ul>
    <%for(var i =0; i< newList.length;i++){%>
        <li><%=newList[i].title%></li>
    <%}%>
</ul>
```

> js代码写在`  <% %>`里面

### GET、POST

超文本传输协议（HTTP）的设计目的是保证客户端机器与服务器之间的通信。
在客户端和服务器之间进行请求-响应时，两种最常被用到的方法是: GET 和 POST。

GET -从指定的资源请求数据。(一般用于获取数据)
POST -向指定的资源提交要被处瑾的数据。(一般用于提交数据〉

获取请求类型：

```
req.method
```

**获取GET传值：**

```
var urlinfo = url.parse(req.url, true);
urlinfo.query
```

案例：
```
// http://127.0.0.1:8081/news?page=2&id=1
var query = url.parse(req.url, true).query;
console.log(query);

// 控制台显示：
[Object: null prototype] { page: '2', id: '1' }
```

**获取POST传值：**

```
const qs = require('qs');

var postData = '';
// 数据块接收中
req.on('data', function(postDataChunk){
    postData += postDataChunk;
});
// 数据接收完毕，执行回调函数
req.on('end', function () {
    try{
        JSON.parse(postData)
    } catch(e) {}

    req.query = postData;
    console.log(req.query);
    console.log(qs.parse(postData))      // 将获取的参数转为对象
    res.end(postData);
})
```

案例：

`./views/register.ejs`：

```
<form action="/doRegister" method="post">
    姓名：<input type="text" name="username">
    年龄：<input type="password" name="password">
    <input type="submit" value="提交">
</form>
```

`app.js`：

```
if(pathname == '/register') {
	// 注册页面
    ejs.renderFile('./views/register.ejs',{}, (err, data) => {
        res.writeHead(200, {'Content-Type': 'text/html;charset="utf-8"'});
        res.end(data);
    })
} else if(pathname == '/doRegister') {
	// 注册操作之后
    var postData = '';
    // 数据块接收中
    req.on('data', function(postDataChunk){
        postData += postDataChunk;
    });
    // 数据接收完毕，执行回调函数
    req.on('end',()=> {
        res.end(postData);
    })
}
```

#### Nodejs路由封装-封装一个类似express的路由

> 将处理路由的方法统一封装起来

`module/routes.js`：

```
const fs = require('fs');
const path = require('path');
const url = require('url');
const ejs = require('ejs');
const qs = require('qs');

let getFileMime = function(extname) {
    var data = fs.readFileSync('./static/data/mime.json');     // 同步方法

    var mimeObj = JSON.parse(data.toString());
    // console.log(mimeObj[extname]);
    return mimeObj[extname];
}

let app = {
    static: (req, res, staticPath) => {
        var pathname = url.parse(req.url).pathname;   // 去掉get传值后的参数
        pathname = pathname == '/' ? '/index.html' : pathname;
        // path.extname()获取后缀名
        let extname = path.extname(pathname);

        // 同步的方法
        if(pathname != '/favicon.ico') {
            try {
                let data = fs.readFileSync('./' + staticPath + pathname);
                if(data) {
                    let mime = getFileMime(extname);
                    res.writeHead(200, {'Content-Type': '' + mime + ';charset="utf-8"'});
                    res.end(data);
                }
                
            } catch (error) {
                
            }
        }
    },
    login: (req, res) => {
        let msg = '从数据库中获取到的数据';
        ejs.renderFile('./views/login.ejs', {msg:msg}, {}, (err, data) => {
            res.writeHead(200, {'Content-Type': 'text/html;charset="utf-8"'});
            res.end(data);
        })
    },
    news: (req, res) => {
        let list = [
            {id:1001, title: '新闻1111'},
            {id:1002, title: '新闻2222'},
            {id:1003, title: '新闻3333'},
            {id:1004, title: '新闻4444'},
            {id:1005, title: '新闻5555'},
        ];
        console.log(req.method)
        // http://127.0.0.1:8081/news?page=2&id=1
        var query = url.parse(req.url, true).query;
        console.log(query);

        ejs.renderFile('./views/news.ejs', {newList:list}, {}, (err, data) => {
            res.writeHead(200, {'Content-Type': 'text/html;charset="utf-8"'});
            res.end(data);
        })
    },
    register: (req, res) => {
        ejs.renderFile('./views/register.ejs',{}, (err, data) => {
            res.writeHead(200, {'Content-Type': 'text/html;charset="utf-8"'});
            res.end(data);
        })
    },
    doRegister: (req, res) => {
        var postData = '';
        // 数据块接收中
        req.on('data', function(postDataChunk){
            postData += postDataChunk;
        });
        // 数据接收完毕，执行回调函数
        req.on('end',()=> {
            try{
                JSON.parse(postData)
            } catch(e) {}
            
            req.query = postData;
            console.log(req.query);
            console.log(qs.parse(postData))
            res.end(postData);
        })
    },
    error: (req, res) => {
        res.end('error')
    },
}

module.exports = app;
```

`app.js`：

```
const http = require('http');
const fs = require('fs');
const url = require('url');
const app = require('./module/routes.js');

http.createServer(function (req, res) {
    // 创建静态web服务
    app.static(req, res, 'static');     // static里面的fs.readFile要改为fs.readFileSync
    // 路由
    var pathname = url.parse(req.url).pathname.replace('/','');      // replace('/','')将pathname中的/去掉
    // http://127.0.0.1:8081/login          pathname = login
    // http://127.0.0.1:8081/news           pathname = news
    // http://127.0.0.1:8081/doRegister     pathname = doRegister

    try {
        app[pathname](req, res);
    } catch (error) {
        fs.readFile('./static' + pathname, (err, data) => {
            if(err) {
                res.writeHead(404, {'Content-Type': 'text/html;charset="utf-8"'});
                res.end('404, 页面不存在');
            } else {
                app['error'](req, res);
            }
        })
    }
}).listen(8081);

console.log('Server running at http://127.0.0.1:8081/');
```

#### 封装app.get()配置路由

`module/route.js`：

```
const url = require('url');

let G = {}; 

let app = function(req, res) {
    let pathname = url.parse(req.url).pathname;

    if(G[pathname]) {
        G[pathname](req, res);   // 执行方法
    } else {
        res.writeHead(404, {'Content-Type': 'text/html;charset="utf-8"'});
        res.end('页面不存在');
    }
}

app.get = function(str, cb) {
    // 注册方法
    G[str] = cb;
}

module.exports = app;
```

`app.js`：

````
const http = require('http');
const app = require('./module/route');

// 注册web服务
http.createServer(app).listen(8081);

// 配置路由
app.get('/', function(req, res) {
    res.writeHead(200, {'Content-Type': 'text/html;charset="utf-8"'});
    res.end('首页');
})

// 配置路由
app.get('/login', function(req, res) {
    res.writeHead(200, {'Content-Type': 'text/html;charset="utf-8"'});
    res.end('login');
})

// 配置路由
app.get('/news', function(req, res) {
    res.writeHead(200, {'Content-Type': 'text/html;charset="utf-8"'});
    res.end('news');
})
````

#### 封装post以及通过req.body获取post的数据

`module/route.js`：

```
const url = require('url');

function changeRes(res){
    res.send = (data) =>{
        res.writeHead(200, {'Content-Type': 'text/html;charset="utf-8"'});
        res.end(data);
    }
}

let sever = () => {
    let G = {}; 
    // 将get和post的方法分开   避免接口名一致，后面的请求的会替换前面的方法
    G._get = {};
    G._post = {};
    
    let app = function(req, res) {
        // 扩展res的方法
        changeRes(res);

        let pathname = url.parse(req.url).pathname;
        // 获取请求类型
        let method = req.method.toLowerCase();
        if(G['_' + method][pathname]) {
            if(method == 'get') {
                G._get[pathname](req, res);   // 执行方法
            } else{
                // post 获取post的数据  把它绑定到req.body
                var postData = '';
                req.on('data', function(chunk){
                    postData += chunk;
                });
                // 数据接收完毕，执行回调函数
                req.on('end',()=> {
                    req.body = postData;
                    G._post[pathname](req, res);   // 执行方法
                })
            }
        } else {
            res.writeHead(404, {'Content-Type': 'text/html;charset="utf-8"'});
            res.end('页面不存在');
        }
    }
    
    app.get = function(str, cb) {
        // 注册方法
        G._get[str] = cb;
    }
    app.post = function(str, cb) {
        // 注册方法
        G._post[str] = cb;
    }

    return app;
}

module.exports = sever();     // 注意：要调用它
```

`app.js`：

```
const http = require('http');
const app = require('./module/route');
const ejs = require('ejs');

// 注册web服务
http.createServer(app).listen(8081);

// 配置路由
app.get('/', function(req, res) {
    res.send('首页');
})

// 配置路由
app.get('/login', function(req, res) {
    ejs.renderFile('./views/login.ejs',{}, (err, data) => {
        res.send(data);
    })
})

// 配置路由
app.get('/news', function(req, res) {
    res.send('news');
})

// login.ejs中的action="/doLogin"
// 使用这种写法（推荐）
app.post('/doLogin', function(req, res) {
    res.send(req.body)
})

// login.ejs中的action="/login"
// 虽然URL中的路径是/login跟get一样的，但渲染页面的的内容不一样。（不推荐）
app.post('/login', function(req, res) {
    res.send(req.body)
})
```

#### 封装静态web服务

> 访问静态文件，如css，js等文件

在ejs文件中引入css文件，报错

`http://127.0.0.1:8081/static/css/style.css net::ERR_ABORTED 404 (Not Found)`

`module/route.js`：

```
const fs = require('fs');
const path = require('path');
const url = require('url');

function changeRes(res){
    res.send = (data) =>{
        res.writeHead(200, {'Content-Type': 'text/html;charset="utf-8"'});
        res.end(data);
    }
}
// 根据后缀名获取文件类型
function getFileMime(extname) {
    var data = fs.readFileSync('./data/mime.json');     // 同步方法

    var mimeObj = JSON.parse(data.toString());
    // console.log(mimeObj[extname]);
    return mimeObj[extname];
}

// 静态web服务的方法
function initStatic(req, res, staticPath) {
    // 1.获取地址
    var pathname = url.parse(req.url).pathname;   // 去掉get传值后的参数
    pathname = pathname == '/' ? '/index.html' : pathname;
    // path.extname()获取后缀名
    let extname = path.extname(pathname);
    // 2. 通过fs模块读取文件
    // 同步的方法
    try {
        let data = fs.readFileSync('./' + staticPath + pathname);
        if(data) {
            let mime = getFileMime(extname);
            res.writeHead(200, {'Content-Type': '' + mime + ';charset="utf-8"'});
            res.end(data);
        }
    } catch (error) {
        
    }
}

let sever = () => {
    let G = {
        _get: {},
        _post: {},
        staticPath: 'static'     // 设置默认静态web目录
    }; 
    // 将get和post的方法分开   避免接口名一致，后面的请求的会替换前面的方法
    
    let app = function(req, res) {
        // 扩展res的方法
        changeRes(res);
        // 配置静态web服务
        initStatic(req, res, G.staticPath);

        let pathname = url.parse(req.url).pathname;
        // 获取请求类型
        let method = req.method.toLowerCase();
        if(G['_' + method][pathname]) {
            if(method == 'get') {
                G._get[pathname](req, res);   // 执行方法
            } else{
                // post 获取post的数据  把它绑定到req.body
                var postData = '';
                req.on('data', function(chunk){
                    postData += chunk;
                });
                // 数据接收完毕，执行回调函数
                req.on('end',()=> {
                    req.body = postData;
                    G._post[pathname](req, res);   // 执行方法
                })
            }
        } else {
            fs.readFile(pathname, (err, data) => {
                if(err) {
                    res.writeHead(404, {'Content-Type': 'text/html;charset="utf-8"'});
                    res.end('404, 页面不存在');
                }
            })
            // 只写这个会报错
            // res.writeHead(404, {'Content-Type': 'text/html;charset="utf-8"'});
            // res.end('页面不存在');
        }
    }
    // get 请求
    app.get = function(str, cb) {
        // 注册方法
        G._get[str] = cb;
    }
    // post 请求
    app.post = function(str, cb) {
        // 注册方法
        G._post[str] = cb;
    }
    // 配置静态Web服务目录
    app.static = function(staticPath) {
        G.staticPath = staticPath;
    }

    return app;
}

module.exports = sever();     // 注意：要调用它
```

`app.js`：

```
const http = require('http');
const app = require('./module/route');
const ejs = require('ejs');

// 注册web服务
http.createServer(app).listen(8081);

// app.static('public');      // 修改默认静态web目录

// 配置路由
app.get('/', function(req, res) {
    res.send('首页');
})

// 配置路由
app.get('/login', function(req, res) {
    ejs.renderFile('./views/login.ejs',{}, (err, data) => {
        res.send(data);
    })
})

// 配置路由
app.get('/news', function(req, res) {
    res.send('news');
})

// login.ejs中的action="/doLogin"
// 使用这种写法（推荐）
app.post('/doLogin', function(req, res) {
    res.send(req.body)
})

// login.ejs中的action="/login"
// 虽然URL中的路径是/login跟get一样的，但渲染页面的的内容不一样。（不推荐）
app.post('/login', function(req, res) {
    res.send(req.body)
})
```

`views/login.ejs`：

```
<link rel="stylesheet" href="./css/style.css">    // 配置了静态web服务，才能访问
```

### MongoDB数据库介绍、安装、使用

##### MongoDB介绍

> MongoDB是一个介于关系数据库和非关系数据库之间的产品，`是非关系数据库当中功能最丰富,最像关系数据库的NoSql数据库`。他支持的数据结构非常松散，是类似json的 bson格式，因此可以存储比较复杂的数据类型。Mongodb最大的特点是他`支持的查询语言非常强大`，其语法有点类似于面向对象的查询语言，`几乎可以实现类似关系数据库单表查询的绝大部分功能`，而且还支持对数据建立索引。它的特点是`高性能、易部署、易使用，存储数据非常方便`。



##### MongoDB安装

注意：配置db目录和log目录

配置环境变量：将安装有MongoDB的bin目录，添加到系统的环境变量中

测试是否成功：在控制台输入`mongo`、

连接数据库：

```
mongo
```

查看数据库：

```
show dbs
```

#### MongoDB数据库创建、删除、表(集合)、创建删除、数据的增、删、改、查

test(数据库)

- user
- admin
- article

表（集合）：user、admin、article

##### 1、使用数据库、创建数据库

```
user test
```

如果真的想把这个数据库创建成功，`那么必须插入一个数据`。

数据库中不能直接插入数据，只能往集合(collections)中插入数据。下面命令表示给 test数据库的user表中插入数据。

```
db.user.insert({"name":"zhangsan","age":20});
```

##### 2、查看数据库

```
show dbs
```

##### 3、显示当前的数据集合（mysql中叫表）

```
show collections
```

##### 4、删除集合，删除指定的集合   删除表

```
删除集合  db.COLLECTION_NAME.DROP()

db.user.drop();
```

##### 5、删除数据库，删除当前所在的数据库

```
db.dropDatabase();
```

##### 三、插入（增加）数据

插入数据，随着数据的插入，数据库创建成功了，集合也创建成功了

```
db.表名.insert({"name":"zhangsan","age":20});
```

##### 四、查找数据

1、查找所有记录

```
db.user.find();
```

相当于：`select * from user;`

```
> db.user.find();
{ "_id" : ObjectId("6409aade3631637f8390508f"), "name" : "zhangsan", "age" : 20 }
{ "_id" : ObjectId("6409ab7e3631637f83905090"), "name" : "zhangsan", "age" : 30 }
{ "_id" : ObjectId("6409ab883631637f83905091"), "name" : "zhangsan", "age" : 40 }
{ "_id" : ObjectId("6409ab903631637f83905092"), "name" : "zhangsan", "age" : 20 }
{ "_id" : ObjectId("6409ac5105d810a057af99e4"), "name" : "zhangsan", "age" : 22 }
```

2、查询去掉后的当前聚集集合中的某列的重复数据

```
db.user.distinct("name");
```

会过滤掉name中的相同数据

相当于：`select distinct name from user;`

```
> db.user.distinct("name");
[ "zhangsan" ]
```

3、查询`age=22`的记录

```
db.user.find({"age":22})
```

相当于：`select * from user where age = 22;`

```
> db.user.find({"age":22})
{ "_id" : ObjectId("6409ac9005d810a057af99e6"), "name" : "zhangsan", "age" : 22 }
```

4、查询`age>22`的记录

```
db.user.find({age:{$gt:22}});
```

相当于：`select * from user where age >22;`

5、查询age<22的记录

```
db.user.find({age:{$lt:22}});
```

相当于：`select * from user where age <22;`

6、查询age>=25的记录

```
db.user.find({age:{$gte:25}});
```

相当于：`select * from user where age >=25;`

7、查询age<=25的记录

```
db.user.find({age:{$lte:25}});
```

8、查询age>=23并且age <=26的记录    （注意书写格式）

```
db.user.find({age:{$gte:23,$lte:26}});
```

9、查询name中包含mongo的数据       （模糊查询用于搜索）

```
db.user.find({name:/mongo/});
```

> //相当于%%
>
> `select * from user where name like '%mongo%';`

10、查询name中以mongo开头的，  `^`符号

```
db.user.find({name:/^mongo/});
```

`select * from user where name like 'mongo%';`

查询name中以mongo结束的， ` $`符号

```
db.user.find({name:/mongo$/});
```

11、查询指定列name、age数据

```
db.user.find({},{name:1, age:1});
```

```
db.user.find({"age":{$gt:20}},{age:1});
```

```
db.user.find({"age":{$gt:20}},{name:1});
```

```
db.user.find({"age":{$gt:20}},{name:1, age:1});
```

相当于：`select name, age from user;`

当然name也可以用`true`或`false`，当用`true`的情况下和 `name:1`效果一样，如果用`false`就是排除name，显示name以外的列信息。

12、查询指定列name、age数据，`age>25`

```
db.user.find({"age":{$gt:25}},{name:1, age:1});
```

相当于：`select name, age from user where age >25;`

13、按照年龄排序   1 升序   -1  降序

升序：

```
db.user.find().sort({age:1});
```

降序：

```
db.user.find().sort({age:-1});
```

14、查询`name = zhangsan, age = 22`的数据

查询数据库的条件，可以写多个

```
db.user.find({name:'zhangsan', age:22});
```

15、查询前5条数据

```
db.user.find().limit(5);
```

相当于：`select top 5 * from user;`

新增100条数据：(类似js代码)

```
> for(var i = 1; i<100; i++) {
...
... db.admin.insert({"name":"zhang" + i, "age": i})
... };
```

```
> db.admin.find()
{ "_id" : ObjectId("640aa65d3ac7e1046e8f888c"), "name" : "zhang1", "age" : 1 }
{ "_id" : ObjectId("640aa65d3ac7e1046e8f888d"), "name" : "zhang2", "age" : 2 }
{ "_id" : ObjectId("640aa65d3ac7e1046e8f888e"), "name" : "zhang3", "age" : 3 }
{ "_id" : ObjectId("640aa65d3ac7e1046e8f888f"), "name" : "zhang4", "age" : 4 }
{ "_id" : ObjectId("640aa65d3ac7e1046e8f8890"), "name" : "zhang5", "age" : 5 }
{ "_id" : ObjectId("640aa65d3ac7e1046e8f8891"), "name" : "zhang6", "age" : 6 }
{ "_id" : ObjectId("640aa65d3ac7e1046e8f8892"), "name" : "zhang7", "age" : 7 }
{ "_id" : ObjectId("640aa65d3ac7e1046e8f8893"), "name" : "zhang8", "age" : 8 }
{ "_id" : ObjectId("640aa65d3ac7e1046e8f8894"), "name" : "zhang9", "age" : 9 }
{ "_id" : ObjectId("640aa65d3ac7e1046e8f8895"), "name" : "zhang10", "age" : 10 }
{ "_id" : ObjectId("640aa65d3ac7e1046e8f8896"), "name" : "zhang11", "age" : 11 }
{ "_id" : ObjectId("640aa65d3ac7e1046e8f8897"), "name" : "zhang12", "age" : 12 }
{ "_id" : ObjectId("640aa65d3ac7e1046e8f8898"), "name" : "zhang13", "age" : 13 }
{ "_id" : ObjectId("640aa65d3ac7e1046e8f8899"), "name" : "zhang14", "age" : 14 }
{ "_id" : ObjectId("640aa65d3ac7e1046e8f889a"), "name" : "zhang15", "age" : 15 }
{ "_id" : ObjectId("640aa65d3ac7e1046e8f889b"), "name" : "zhang16", "age" : 16 }
{ "_id" : ObjectId("640aa65d3ac7e1046e8f889c"), "name" : "zhang17", "age" : 17 }
{ "_id" : ObjectId("640aa65d3ac7e1046e8f889d"), "name" : "zhang18", "age" : 18 }
{ "_id" : ObjectId("640aa65d3ac7e1046e8f889e"), "name" : "zhang19", "age" : 19 }
{ "_id" : ObjectId("640aa65d3ac7e1046e8f889f"), "name" : "zhang20", "age" : 20 }
Type "it" for more
```

16、查询10条以后的数据

```
db.admin.find().skip(10);
```

17、查询在5~10之间的数据

```
> db.admin.find().limit(4).skip(5);
{ "_id" : ObjectId("640aa65d3ac7e1046e8f8891"), "name" : "zhang6", "age" : 6 }
{ "_id" : ObjectId("640aa65d3ac7e1046e8f8892"), "name" : "zhang7", "age" : 7 }
{ "_id" : ObjectId("640aa65d3ac7e1046e8f8893"), "name" : "zhang8", "age" : 8 }
{ "_id" : ObjectId("640aa65d3ac7e1046e8f8894"), "name" : "zhang9", "age" : 9 }
>
```

```
db.admin.find().limit(10).skip(5);
```

可用于分页，limit是pageSize，skip是第几页减1*pageSize

pageSize：每页显示的条数

```
db.admin.find().limit(10).skip(0);    		// 第一页   (n-1)*10
db.admin.find().limit(10).skip(10);		 	// 第二页
db.admin.find().limit(10).skip(20); 		// 第三页
```

18、or与查询

```
db.user.find({$or:[{age:22},{age:25}]});
```

相当于：`select * from user where age = 22 or age =25;`

19、findOne查询第一条数据

```
db.user.findOne();
```

相当于：`select top 1* from user;`

```
db.user.find().limit(1);
```

20、查询某个结果集的记录条数    统计数量

```
db.user.find().count();
```

```
db.user.find({age:{$gte:25}}).count();
```

相当于：`select count(*) from user where age >=20;`

如果要返回限制之后的记录数量，要使用`count(true)`或者`count(非0)`

```
db.user.find().skip(10).limit(5).count(true);
```

#### 四、修改数据

```
 db.student.insert({"name":"liming", "age":20, sex:"男", "score":{"shuxue":70, "yuwen":80, "yingyu":86}});
```

```
> db.student.find()                                                                      
{ "_id" : ObjectId("640acb7319e76fb47ee3df38"), "name" : "小明", "age" : 33, "score" : { "shuxue" : 70, "yuwen" : 80, "yingyu" : 86 }, "sex" : "男" }
{ "_id" : ObjectId("640acebb19e76fb47ee3df39"), "name" : "xiaoming", "age" : 20, "sex" : "男", "score" : { "shuxue" : 70, "yuwen" : 80, "yingyu" : 86 } }
{ "_id" : ObjectId("640acedf19e76fb47ee3df3a"), "name" : "Lisi", "age" : 20, "sex" : "女", "score" : { "shuxue" : 70, "yuwen" : 80, "yingyu" : 86 } }
{ "_id" : ObjectId("640aceea19e76fb47ee3df3b"), "name" : "lisa", "age" : 20, "sex" : "女", "score" : { "shuxue" : 70, "yuwen" : 80, "yingyu" : 86 } }
{ "_id" : ObjectId("640aceff19e76fb47ee3df3c"), "name" : "liming", "age" : 20, "sex" : "男", "score" : { "shuxue" : 70, "yuwen" : 80, "yingyu" : 86 } }
>
```

`注意：要加上$set，如果不加上，会直接替换整条数据`

修改里面还有查询条件。你要改谁，要告诉mongo。

查找名字叫做小明的，把年龄更改为16岁：

```
db.student.update({"name":"小明"}, {$set:{age:16}})

db.student.update({"name":"小明"}, {$set:{"sex":"男"}})
```

查找数学成绩是70，把年龄更改为33岁：

```
db.student.update({"score.shuxue":70}, {$set:{age:33}})
```

更改所有匹配项目：`{multi: true}`
By default, the update() method updates a single document. To update multiple documents, use the multi option in the update() method.

```
db.student.update({"sex":"男"},{$set:{"age":33}}, {multi: true});
```

完整替换，`不出现$set关键字了`： `注意`

```
db.student.update({"name":"小明"}, {"name":"大明","age":16}); 

// 原数据：
{ "_id" : ObjectId("640acb7319e76fb47ee3df38"), "name" : "小明", "age" : 33, "score" : { "shuxue" : 70, "yuwen" : 80, "yingyu" : 86 }, "sex" : "男" }
//  直接替换为：
{ "_id" : ObjectId("640acb7319e76fb47ee3df38"), "name" : "大明", "age" : 16 }
```

`db.users.update({name: "Lisi"},{$inc: {age: 50]}, false, true);`

相当于：` update users set age = age + 50 where name = 'Lisi';`

`db.users.update({name: 'Lisi'}, {$inc: {age: 50}, $set: {name: 'hoho'}}, false, true);`

相当于：`update users set age = age + 50, name = 'hoho' where name = 'Lisi';`

#### 五、删除数据

```
db.collectionsNames.remove({"borough":"Manhattan"});
db.users.remove({age: 132});
```

By default, the remove() method removes all documents that match the remove condition. Use the justOne option to limit the remove operation to only one of fhe matching documents.

`{justOne: true}`

```
db.restaurants.remove({"borough": "Queens"}, {justOne: true})
```

```
 db.student.remove({"sex":"男"},{justOne:true})
```

删除数据，如果不加条件，是全部都删除

```
db.admin.remove({});      // 全部删除
```

#### MongoDb大数据查询优化、MongoDB索引、复合索引、唯一索引、explain分析查询速度

##### 一、索引基础

​		索引是对数据库表中一列或多列的值进行排序的一种结构，可以让我们查询数据库变得更快。MongoDB的索引几乎与传统的关系型数据库一模一样，这其中也包括一些基本的查询优化技巧。

创建索引：

```
db.user.ensureIndex({"username":1});
```

获取当前集合的索引：

```
db.user.getIndexes();
```

删除索引的命令：

```
db.user.dropIndex({"username":1})
```

在MongoDB中，我们同样可以创建`复合索引`，如：

`数字1`表示username键的索引按升序存储，`-1`表示age键的索引按照降序方式存储

```
db.user.ensureIndex({"username":1,"age": -1});

db.user.dropIndex({"username":1,"age": -1});    // 这样删除
```

​	该索引被创建后，基于username和age 的查询将会用到该索引，或者是基于username的查询也会用到该索引，**但是只是基于age的查询将不会用到该复合索引。因此可以说，如果想用到复合索引，必须在查询条件中包含复合索引中的前N个索引列**。然而如果查询条件中的键值顺序和复合索引中的创建顺序不一致的话，MongoDB可以智能的帮助我们调整该顺序，以便使复合索引可以为查询所用。如:

```
db.user.find({"age":30, "username": "stephen"})

db.user.find({"age":10, "name": "zhang10"})
```

​		对于上面示例中的查询条件，MongoDB在检索之前将会动态的调整查询条件文档的顺序，以使该查询可以用到刚刚创建的复合索引。
​		对于上面创建的索引，MongoDB都会根据索引的 keyname和索引方向为新创建的索引自动分配一个索引名，**下面的命令可以在创建索引时为其指定索引名**，如:

```
db.user.ensureIndex({"usename": 1}, {"name": "useindex"})
```

`随着集合的增长，需要针对查询中大量的排序做索引。如果没有对索引的键调用sort,MongoDB需要将所有数据提取到内存并排序。因此在做无索引排序时，如果数据量过大以致无法在内存中进行排序，此时MongoDB将会报错。`

##### 二、唯一索引

在缺省情况下创建的索引均不是唯一索引。下面的示例将创建唯一索引，如：

```
db.user.ensureIndex({"userid":1}, {"unique": true});
```

如果再次插入userid重复的文档时，MongoDB将报错，以提示插入重复键，如：

```
db.user.insert({"userid": 5});
db.user.insert({"userid": 5});
```

`E11000 duplicate key error index: user.user.$userid_1 dup key: {: 5.0}`

如果插入的文档中不包含userid键，那么该文档中该键的值为null，如果多次插入类似的文档，MongoDB将会报出同样的错误，如：

````
db.user.insert({"age": 5});
db.user.insert({"age": 5});
````

`E11000 duplicate key error index: user.user.$userid_1 dup key: {:null }`

如果在创建唯一索引时已经存在了重复项,我们可以通过下面的命令帮助我们在创建唯一索引时消除重复文档，仅保留发现的第一个文档，如:
先删除刚刚创建的唯一索引。

##### 五、explain executionStats查询具体的执行时间

```
db.tablename.find().explain("executionStats")
```

```
db.user.find().explain("executionStats")
```

关注输出的如下数值：`explain.executionStats.executionTimeMillis`

例子：

查询6万多条数据，不加索引，查询时间500多毫秒；加上索引，10毫秒左右，再执行一次，0毫秒

#### 连接远程的数据库

```
mongo 192.168.0.8:27017
```

#### Mongodb4.x的使用以及 Mongodb账户权限配置

查看mongo版本

```
 mongo -version
```

#### Mongodb账户权限配置

1、第一步创建超级管理用户

```
use admin
db.createUser({
	user: 'admin',
	pwd: '123456',
	roles:[{role:'root', db:'admin'}]
})
```

2、第二步修改Mongodb数据库配置文件

> 查看mongodb安装路径的方法：1、win环境下，使用【win+r】快捷键打开运行窗口，输入“services.msc”指令打开服务列表，右键MongoDB服务选择“属性”查看mongodb安装路径；2、linux环境下，打开linux终端，输入“find / -name mongodb”、“locate mongodb”、“whereis mongodb”、“which mongodb”其中一个命令查看mongodb安装路径即可。

```
路径： G:\Install\WEB\mongodb\bin\mongod.cfg

配置：
security:
  authorization: enabled
```

`注：修改配置文件前，最好先备份`

3、第三步重启mongodb服务

1. `win+R` ——>` services.msc`
2. 找到MongoDB Server， 右键重启

在终端输入`mongo`连接之后，输入`show dbs`，不显示内容

4、第四步用超级管理员账户连接数据库

```
mongo admin -u 用户名 -p 密码

mongo 192.168.1.200:27017/test -u user -p password     // test:数据库名
```

```
mongo admin -u admin -p 123456      // 连接之后，再输入show dbs，会显示所有数据库
```

5、第五步给test数据库创建一个用户，  只能访问test不能访问其他数据库

```
use test

db.createUser({
	user: 'testadmin',
	pwd: '123456',
	roles:[{role:'dbOwner', db:'test'}]
})
```

```
use test

show users

db.dropUser('testadmin')     // 删除用户
```

使用testadmin账号

```
mongo test -u testadmin -p 123456
```

```
> show dbs
test  0.000GB        // 只能看到test数据库
```

#### Mongodb账户权限配置中常用的命令

1. 查看当前库下的用户

   ```
   show users
   ```

2. 删除用户

   ```
   db.dropUser('testadmin')
   ```

3. 修改用户密码

   ```
   db.updateUser('admin', {pwd: 'password'})
   ```

4. 密码认证

   ```
   db.auth('admin', 'password')
   ```

   例如：

   ```
   mongo test         // test：数据库名称
   > show dbs
   // 终端不显示内容
   
   > db.auth("testadmin", "123456")       // test数据库的用户
   1
   > show dbs
   test  0.000GB
   ```

#### Mongodb数据库角色

1. 数据库用户角色：read、readWrite;
2. 数据库管理角色：dbAdmin、`dbOwner`、userAdmin;
3. 集群管理角色：clusterAdmin、clusterManager、clusterMonitor、hostManager;
4. 备份恢复角色：backup、 restore;
5. 所有数据库角色：readAnyDatabase、readWriteAnyDatabase、userAdminAnyDatabase、dbAdminAnyDatabase
6. 超级用户角色：`root`

参考：[MongoDB 内置角色](https://www.cnblogs.com/zzw1787044/p/5773178.html)

#### 连接数据库的时候需要配置账户密码

```
const url = 'mongodb://admin:123456@localhost:27017/';
```

#### 基本操作

##### 查看mongodb的数据库存放位置/日志存放位置：

bin目录中的配置文件：`G:\Install\WEB\mongodb\bin\mongod.cfg`

```
# Where and how to store data.
storage:
  dbPath: G:\Install\WEB\mongodb\data
  journal:
    enabled: true
#  engine:
#  mmapv1:
#  wiredTiger:

# where to write logging data.
systemLog:
  destination: file
  logAppend: true
  path:  G:\Install\WEB\mongodb\log\mongod.log
```

##### 查看/修改mongodb的端口：

bin目录中的配置文件：`G:\Install\WEB\mongodb\bin\mongod.cfg`

```
# network interfaces
net:
  port: 27017
  bindIp: 127.0.0.1
```

#### 关系型数据库表（集合）与表（集合）之间的几种关系

一对一：一个身份证对应一个驾驶证

一对多：一个商品分类对应多个商品，一个班级对应多名学生

多对多：例如:一个学生可以选多门课程，而同一门课程可以被多个学生选修，彼此的对应关系即是多对多关系

一个用户可以关注多个商品，一个商品可以被多个用户关注

#### MongoDB 的高级查询aggregate聚合管道

##### 一、MongoDB聚合管道（Aggregate Pipeline）

使用聚合管道可以对集合中的文档进行变换和组合。

实际项目中：表关联查询、数据的统计。

**MongoDB**中使用`db.COLLECTION_NAME.aggregate([{<stage>},...])`方法来构建和使用聚合管道。先看下官网给的实例，感受一下聚合管道的用法。

##### 二、MongoDB Aggregation 管道操作符与表达式

| 管道操作符 | Description                                            |
| ---------- | ------------------------------------------------------ |
| `$project` | `增加、删除、重命名字段`                               |
| `$match`   | 条件匹配、只满足条件的文档才能进入下一阶段             |
| $limit     | 限制结果的数量                                         |
| $skip      | 跳过文档的数量                                         |
| $sort      | 条件排序                                               |
| $group     | 条件组合结果      统计                                 |
| $lookup    | $lookup 操作符 用以引入其它集合的数据   （表关联查询） |

##### SQL和NOSQL对比

| `WHERE`  | `$match`   |
| -------- | ---------- |
| GROUP BY | $group     |
| `HAVING` | `$match`   |
| `SELECT` | `$project` |
| ORDER BY | $sort      |
| LIMIT    | $limit     |
| SUM()    | $sum       |
| COUNT()  | $sum       |
| `join`   | `$lookup`  |

##### 三、数据模拟

```
db.order.insert({"order_id": "1", "uid": 10, "trade_no":"111", "all_price":100, "all_num": 2})
db.order.insert({"order_id": "2", "uid": 7, "trade_no":"222", "all_price":90, "all_num": 2})
db.order.insert({"order_id": "3", "uid": 9, "trade_no":"333", "all_price":20, "all_num": 6})

db.order_item.insert({"order_id": "1", "title": "商品鼠标1", "price":50, "num":1})
db.order_item.insert({"order_id": "1", "title": "商品键盘2", "price":50, "num":1})

db.order_item.insert({"order_id": "2", "title": "牛奶", "price":50, "num":1})
db.order_item.insert({"order_id": "2", "title": "酸奶", "price":40, "num":1})

db.order_item.insert({"order_id": "3", "title": "矿泉水", "price":2, "num":5})
db.order_item.insert({"order_id": "3", "title": "毛巾", "price":10, "num":1})
```

##### 四、`$project`

修改文档的结构，可以用来重命名、增加或删除文档中的字段。

要求查找order 只返回文档中trade_no和all_price字段

```
db.order.aggregate([
    {
    	$project:{trade_no: 1, all_price:1}
    }
])
```

结果：

```
{ "_id" : ObjectId("64116235c9443120dbcb913e"), "trade_no" : "111", "all_price" : 100 }
{ "_id" : ObjectId("6411623fc9443120dbcb913f"), "trade_no" : "333", "all_price" : 20 }
{ "_id" : ObjectId("641162b7c9443120dbcb9146"), "trade_no" : "222", "all_price" : 90 }
```

##### 五、`$match`

**作用**

用于过滤文档。用法类似于 `find()`方法中的参数。

```
db.order.aggregate([
    {
    	$project:{trade_no: 1, all_price:1}
    },
    {
    	$match:{"all_price": {$gte:90}}
    }
])
```

结果：

```
{ "_id" : ObjectId("64116235c9443120dbcb913e"), "trade_no" : "111", "all_price" : 100 }
{ "_id" : ObjectId("641162b7c9443120dbcb9146"), "trade_no" : "222", "all_price" : 90 }
```

##### 六、`$group`

将集合中的文档进行分组，可用于统计结果。
统计每个订单的订单数量，按照订单号分组。

```
db.order_item.aggregate([
    {
    	$group:{_id: "$order_id", total:{$sum :1}}
    }
])
```

结果：

```
{ "_id" : "2", "total" : 2 }
{ "_id" : "1", "total" : 2 }
{ "_id" : "3", "total" : 2 }
```

```
db.order_item.aggregate([
    {
    	$group:{_id: "$order_id", total:{$sum: "$num"}}
    }
])
```

结果：

```
{ "_id" : "2", "total" : 2 }
{ "_id" : "1", "total" : 2 }
{ "_id" : "3", "total" : 6 }
```

```
db.order_item.aggregate([
    {
    	$group:{_id: "$order_id", total:{$sum: "$price"}}
    }
])
```

结果：

```
{ "_id" : "3", "total" : 12 }
{ "_id" : "1", "total" : 100 }
{ "_id" : "2", "total" : 90 }
```

##### 七、`$sort`

将集合中的文档进行排序

```
db.order.aggregate([
    {
    	$project:{trade_no: 1, all_price:1}
    },
    {
    	$match:{"all_price": {$gte:90}}
    },
    {
     	$sort: {"all_price": -1}
    }
])
```

结果：

```
{ "_id" : ObjectId("64116235c9443120dbcb913e"), "trade_no" : "111", "all_price" : 100 }
{ "_id" : ObjectId("641162b7c9443120dbcb9146"), "trade_no" : "222", "all_price" : 90 }
```

八、`$limit`

```
db.order.aggregate([
    {
    	$project:{trade_no: 1, all_price:1}
    },
    {
    	$match:{"all_price": {$gte:90}}
    },
    {
     	$sort: {"all_price": -1}
    },
    {
     	$limit: 1
    }
])
```

结果：

```
{ "_id" : ObjectId("64116235c9443120dbcb913e"), "trade_no" : "111", "all_price" : 100 }
```

##### 九、`$skip`

```
db.order.aggregate([
    {
    	$project:{trade_no: 1, all_price:1}
    },
    {
    	$match:{"all_price": {$gte:90}}
    },
    {
     	$sort: {"all_price": -1}
    },
    {
     	$skip: 1
    }
])
```

结果：

```
{ "_id" : ObjectId("641162b7c9443120dbcb9146"), "trade_no" : "222", "all_price" : 90 }
```

##### 十、`$lookup`表关联

`localField: "order_id"`（order表哪个字段）与`foreignField: "order_id"`（order_item表的哪个字段关联

```
db.order.aggregate([
 	{
		$lookup:
        {
            from:"order_item",
            localField: "order_id",
            foreignField: "order_id",
            as: "items"
        }
 	}
]);
 
from:"order_item",		 	// 关联的表
localField: "order_id",		// 原表（order表）
foreignField: "order_id",	// 关联表（order_item表）
```

格式化之后的结果：

```
{
	"_id": ObjectId("64116235c9443120dbcb913e"),
	"order_id": "1",
	"uid": 10,
	"trade_no": "111",
	"all_price": 100,
	"all_num": 2,
	"items": [{
		"_id": ObjectId("64116245c9443120dbcb9140"),
		"order_id": "1",
		"title": "商品鼠标1",
		"price": 50,
		"num": 1
	}, {
		"_id": ObjectId("6411624bc9443120dbcb9141"),
		"order_id": "1",
		"title": "商品键盘2",
		"price": 50,
		"num": 1
	}]
} {
	"_id": ObjectId("6411623fc9443120dbcb913f"),
	"order_id": "3",
	"uid": 9,
	"trade_no": "333",
	"all_price": 20,
	"all_num": 6,
	"items": [{
		"_id": ObjectId("6411625dc9443120dbcb9144"),
		"order_id": "3",
		"title": "矿泉水",
		"price": 2,
		"num": 5
	}, {
		"_id": ObjectId("64116262c9443120dbcb9145"),
		"order_id": "3",
		"title": "毛巾",
		"price": 10,
		"num": 1
	}]
} {
	"_id": ObjectId("641162b7c9443120dbcb9146"),
	"order_id": "2",
	"uid": 7,
	"trade_no": "222",
	"all_price": 90,
	"all_num": 2,
	"items": [{
		"_id": ObjectId("64116251c9443120dbcb9142"),
		"order_id": "2",
		"title": "牛奶",
		"price": 50,
		"num": 1
	}, {
		"_id": ObjectId("64116256c9443120dbcb9143"),
		"order_id": "2",
		"title": "酸奶",
		"price": 40,
		"num": 1
	}]
}
```



```
db.order.aggregate([
 	{
		$lookup:
        {
            from:"order_item",
            localField: "order_id",
            foreignField: "order_id",
            as: "items"
        }
 	},
 	{
    	$project:{trade_no: 1, all_price:1, items :1}
    },
    {
    	$match:{"all_price": {$gte:90}}
    },
    {
    	$sort:{"all_price": -1}
    }
]);
```

格式化之后的结果：

```
{
	"_id": ObjectId("64116235c9443120dbcb913e"),
	"trade_no": "111",
	"all_price": 100,
	"items": [{
		"_id": ObjectId("64116245c9443120dbcb9140"),
		"order_id": "1",
		"title": "商品鼠标1",
		"price": 50,
		"num": 1
	}, {
		"_id": ObjectId("6411624bc9443120dbcb9141"),
		"order_id": "1",
		"title": "商品键盘2",
		"price": 50,
		"num": 1
	}]
} {
	"_id": ObjectId("641162b7c9443120dbcb9146"),
	"trade_no": "222",
	"all_price": 90,
	"items": [{
		"_id": ObjectId("64116251c9443120dbcb9142"),
		"order_id": "2",
		"title": "牛奶",
		"price": 50,
		"num": 1
	}, {
		"_id": ObjectId("64116256c9443120dbcb9143"),
		"order_id": "2",
		"title": "酸奶",
		"price": 40,
		"num": 1
	}]
}
```

#### Nodejs 操作MongoDB数据库

Nodejs操作mongodb数据库官方文档：

[MongoDB Node.js Driver](http://mongodb.github.io/node-mongodb-native/)

##### 一、[Create a Project Directory](https://www.mongodb.com/docs/drivers/node/current/quick-start/download-and-install/)

```
mkdir node_quickstart
```

```
cd node_quickstart
```

```
npm init -y
```

```
npm i mongodb --save
```

##### 二、[Connect to MongoDB](https://www.mongodb.com/docs/drivers/node/current/quick-start/connect-to-mongodb/)

`index.js`：

```
//引入mongodb
const { MongoClient } = require("mongodb");
//定义数据库连接的地址
const url = 'mongodb://127.0.0.1:27017';
//定义要操作的数据库
const dbName = 'test';

//实例化Mongoclient传入数据库连接地址
const client = new MongoClient(url,{useUnifiedTopology : true });
//连接数据库
client.connect((err)=>{
    if(err){
        console.log(err);
        return;
    }

    console.log('数据库连接成功');
    let db = client.db(dbName);

    // 1、查找数据
    db.collection('user').find({}).toArray((err,result)=>{
        if(err){
            console.log(err);
            return;
        }
        console.log(result);

        // 操作数据库完毕以后一定要  关闭数据库连接
        client.close();
    })

    // db.collection('user').find({"age": 13}).toArray((err,result)=>{
    //     if(err){
    //         console.log(err);
    //         return;
    //     }
    //     console.log(result);
    // })

    // 2、增加数据
    db.collection('user').insertOne({
        "name": "张三",
        "age": 13
    },(err,result)=>{
        if(err){
            console.log(err);
            return;
        }
        console.log('增加成功');
        console.log(result);

        // 操作数据库完毕以后一定要  关闭数据库连接
        client.close();
    })
    
    // 3、更新数据
    db.collection('user').updateOne({
        name: "张三",
    },{$set: {"age": 13}},(err,result)=>{
        if(err){
            console.log(err);
            return;
        }
        console.log('更新成功');
        console.log(result);
        // 操作数据库完毕以后一定要  关闭数据库连接
        client.close();
    })

    // 4、删除一条数据
    db.collection('user').deleteOne({
        name: "张三"
    },(err,result)=>{
        if(err){
            console.log(err);
            return;
        }
        console.log('删除一条数据成功');
        console.log(result);
        // 操作数据库完毕以后一定要  关闭数据库连接
        client.close();
    })
    
    // 5、删除多条数据
    db.collection('user').deleteMany({
        name: "zhangsan"
    },(err,result)=>{
        if(err){
            console.log(err);
            return;
        }
        console.log('删除多条数据成功');
        console.log(result);
        // 操作数据库完毕以后一定要  关闭数据库连接
        client.close();
    })
})
```

#### NodeJs操作MongoDb数据库查询数据通过ejs显示列表以及通过表单增加数据





#### [Express](https://www.expressjs.com.cn/)，动态路由，get传值

```
$ mkdir myapp
$ cd myapp
```

```
npm init
```

```
npm install express --save
```

`app.js`	：

```
const express = require('express')
const app = express()
const port = 5000

// 配置路由
app.get('/', (req, res) => {
  res.send('Hello World!')
})

// 监听端口
app.listen(port, () => {
  console.log(`Example app listening on port ${port}`)
})
```

```
node app.js
```

##### 配置路由、获取get传值

```
const express = require('express')
const app = express()
const port = 5000

// 配置路由
app.get('/', (req, res) => {
  res.send('首页')
})

app.get('/login', (req, res) => {
  res.send('登录')
})

app.get('/register', (req, res) => {
    res.send('注册')
})

app.get('/article', (req, res) => {     // get:获取数据（显示数据
    res.send('文章')
})

app.post('/doLogin', (req, res) => {    // post:增加数据
    console.log('执行登录')
    res.send('执行登录')
})

app.put('/editUser', (req, res) => {  // put:修改数据
    console.log('修改用户')
    res.send('修改用户')
})

app.delete('/deleteUser', (req, res) => {  // delete:删除数据
    console.log('删除用户')
    res.send('删除用户')
})

// 动态路由   配置路由的时候也要注意顺序
app.get('/article/add', (req, res) => {     
    res.send('article add')
})

app.get('/article/:id', (req, res) => {     
    var id = req.params.id;
    res.send('动态路由' + id)
})

// 如果这个路由写在后面， id就是add
// app.get('/article/add', (req, res) => {     
//     res.send('article add')
// })

// get 传值
// http://localhost:5000/product?id=125454&cid=2
app.get('/product', (req, res) => {
    var id = req.params.id;
    let query = req.query;
    console.log(query)     // { id: '125454', cid: '2' }
    res.send('product')
})
// 监听端口
app.listen(port, () => {
  console.log(`Example app listening on port ${port}`)
})
```

#### Express框架中ejs的安装使用

```
npm install ejs --save
```

```
// 2、配置模板引擎
app.set('view engine', 'ejs');
```

```
// 3、使用   默认加载模板引擎的文件夹是views
res.render('index',{     // views/index.ejs    不需要写views    {}里面是传数据，没有传空对象
	
})
```

使用`supervisor app.js`启动，就不需要每次修改了`app.js`都要重启一次

```
npm i -g supervisor 
```

##### 绑定数据

```
<%=data%>
<%=obj.name%>
```

```
<p><%-article%></p>         // 渲染包含HTML标签的内容
```

```
const express = require('express');
const app = express();
app.set('view engine', 'ejs');

app.get('/', (req, res) => {
    let title = '你好'
    res.render('index',{    
        title:title
    })
});

app.get('/news', (req, res) => {
    let userinfo = {
        name:'张三',
        age:18
    }
    let article = '<h3>内容包含HTML标签</h3>'
    res.render('news',{    
        userinfo:userinfo,
        article:article
    })
});

// 监听端口  端口号建议写成3000以上
app.listen(5000);
```

```
<p><%=title%></p>
```

```
<p><%=userinfo.name%>——————<%=userinfo.age%></p>

 <p><%-article%></p>    
```

##### 条件判断

js代码要写在`<%%>`里面

```
<%if(flag ===true){%>
    <strong>flag ===true</strong>
<%}%>   

<%if(score >=60){%>
    及格
<%}else{%>  
    不及格
<%}%>  
```

##### 循环遍历

```
<ul>
    <%for(var i = 0; i<list.length; i++){%>
        <li><%=list[i]%></li>
    <%}%>  
</ul>
```

##### 在模板中引入公共模板

```
<%- include("footer.ejs") %>
```

#### 将模板文件设置为`.html`

1. 在 app.js 定义ejs，代码如下：

   ```+
   const ejs = require('ejs');
   ```

2. 注册html模板引擎，代码如下：

   ```
   app.engine('html', ejs.__express);
   ```

3. 将模板引擎换成html，代码如下：

   ```
   app.set('view engine', 'html');
   ```

4. 修改模板文件的后缀为`.html`：`index.ejs`——>`index.html`

`app.js`：

```
const express = require('express');
const ejs = require('ejs');
const app = express();

// 1.定义ejs
app.engine('html', ejs.__express);
// 2.注册html模板引擎
app.set('view engine', 'html');

app.get('/', (req, res) => {
    let title = '你好'
    res.render('index',{    
        title:title
    })
});

app.get('/news', (req, res) => {
    let userinfo = {
        name:'张三',
        age:18
    }
    let article = '<h3>内容包含HTML标签</h3>'
    let list = [1,3,4,5,6,7,8,9,10,11,12]
    res.render('news',{    
        userinfo:userinfo,
        article:article,
        flag: true,
        score: 60,
        list:list
    })
});

// 监听端口  端口号建议写成3000以上
app.listen(5000);
```

指定模板位置，默认模板位置在`views`

```
app.set('views', __dirname + 'views');
```

#### 利用`Express.static`托管静态文件

1、如果你的静态资源存放在多个目录下面，你可以多次调用express.static中间件：

```
// 配置静态web目录
app.use(express.static('static'));
```

`重启服务`，static目录下面的文件就可以访问

[static/css/base.css](http://localhost:5000/css/base.css)

在`index.html`、`news.html`中引入样式：

```
<link rel="stylesheet" href="/css/base.css">
```

`可以配置多个静态资源存放目录`

`public/js/base.js`:

```
let a = 10;
console.log(a);
```

`app.js`：

```
// 配置第二个静态web目录
app.use(express.static('public'));
```

`重启服务`，public目录下面的文件就可以访问

在`news.html`中引入js：

```
<script src="/js/base.js"></script>
// 可以看到在控制台输出  10
```

2、如果你希望所有通过`express.static`访问的文件都存放在一个“虚拟(virtual)”目录（即目录根本不存在）下面，可以通过为静态资源目录指定一个挂载路径的方式来实现，如下所示：

```
app.use('/static', express.static('public'));
```

现在，你就可以通过带有`"/static"`前缀的地址来访问 public目录下面的文件了。

**例子：**

`app.js`：

```
// 配置虚拟目录
app.use('/static2', express.static('public'));
```

重启服务，即可访问http://localhost:5000/static2/images/logo.jpg`

`views/news.html`：

```
<img src="/static2/images/logo.jpg" alt="logo">
```

> 实际上不存在`static2`目录，是指向了`public`目录

#### Express中间件——body-paser中间件

> 通俗的讲：中间件就是匹配路由之前或者匹配路由完成做的一系列的操作。中间件中如果想往下匹配的话，那么需要写`next()`

##### Express应用可使用如下几种中间件：

- 应用级中间件
- 路由级中间件
- 错误处理中间件
- 内置中间件
- 第三方中间件

> Express中间件是一种函数，可以在HTTP请求的处理过程中进行拦截和处理，以实现某些特定的功能。中间件可以用来处理请求和响应对象，调用下一个中间件函数，终止请求-响应周期，以及执行任何其他操作。

##### 应用级中间件

> 应用级别的中间件使用app.use()方法来注册，可以匹配任何路由，也可以设置在路由之前或之后执行

`app.js`：

```
// 应用级中间件            
app.use((req, res, next) => {       // 在请求路由之前就执行
    console.log(new Date());        // 访问http://localhost:5000/在控制台输出当前时间
    next();
})

app.get('/', (req, res) => {
    let title = '你好'
    res.render('index',{    
        title:title
    })
});
```

##### 路由级中间件

> 路由级别的中间件使用app.METHOD()方法来注册，其中METHOD表示HTTP请求方法（如GET、POST等），可以针对特定的路由进行匹配

```
// 路由中间件（用得比较少）
app.get('/news/add', (req, res, next) => {
   console.log('执行增加新闻');      // 在控制台输出 执行增加新闻
   next();                         // 继续向下匹配路由
});

app.get('/news/:id', (req, res) => {
    res.send('新闻动态路由')           // 在页面输出  新闻动态路由
});
```

##### 错误处理中间件

> 错误处理中间件通常用于处理在请求处理过程中发生的错误

```
//  3. 错误处理中间件
app.use(( req, res, next) => {
    res.status(404).send('404')
})
```

示例：

```
app.use((err, req, res, next) => {
    console.log(new Date());
    console.log(err);
    res.status(500).send('服务器错误')
})
```

##### 内置中间件

```
// 4. 内置中间件
app.use(express.static('static'))
```

```
<link rel="stylesheet" href="/css/base.css">
```

##### 第三方中间件

`body-parser`中间件

> body-parser是一个处理HTTP请求体的中间件，可以解析JSON、Raw、文本（Text）、URL-encoded格式的请求体。在Express框架中，使用body-parser做为请求体解析中间件[[3](https://blog.csdn.net/fuhanghang/article/details/116986474)]。使用body-parser可以把请求主体解析为req.body属性下可用的对象形式，方便后续处理[[1](https://zhuanlan.zhihu.com/p/405704013)]

1. 安装

   ```
   npm i body-parser --save
   ```

2. 引入

   ```
   const bodyParser = require('body-parser');
   ```

3. 设置中间件

   ```
   app.use(bodyParser.json());
   app.use(bodyParser.urlencoded({ extended: false }));
   ```

   > 处理form表单的中间件     form表单提交的数据

4. 接收post数据：`req.body`    示例：

   ```
   app.get('/login', (req, res) => {
       res.render('login',{})
   })
   
   app.post('/doLogin', (req, res) => {
       var body = req.body;
       console.log(body);          // 控制台输出：{ username: 'admin', password: '123456' }
       res.send(body.username + ' ' + body.password);
   })
   ```

   `index.ejs`：

   ```
   <form action="/doLogin" method="post">
       <div class="form-group">
           <label for="username">用户名</label>
           <input type="text" class="form-control" id="username" name="username">
       </div>
   
       <div class="form-group">
           <label for="password">密码</label>
           <input type="password" class="form-control" id="password" name="password">
       </div>
   
       <div>
           <input type="submit" value="提交">
       </div>
   </form>
   ```

### Express中间件  cookie的基本使用

- cookie是存储于访问者的计算机中的变量。可以让我们用同一个浏览器访问同一个域名的时候共享数据。

- HTTP是无状态协议。简单地说，当你浏览了一个页面，然后转到同一个网站的另一个页面，服务器无法认识到这是同一个浏览器在访问同一个网站。每一次的访问，都是没有任何关系的。
- Cookie是一个简单到爆的想法：当访问一个页面的时候，服务器在下行HTTP报文中，命令浏览器存储一个字符串；浏览器再访问同一个域的时候，将把这个字符串携带到上行HTTP请求中。第一次访问一个服务器，不可能携带cookie。必须是服务器得到这次请求，在下行响应报头中，携带cookie 信息，此后每一次浏览器往这个服务器发出的请求，都会携带这个cookie。

> 要加密，不允许修改，不加密，在客户端可以直接修改

1. 安装

   ```
   npm i cookie-parser --save
   ```

2. 引入

   ```
   const cookieParser = require('cookie-parser');
   ```

3. 设置中间件

   ```
   app.use(cookieParser());
   ```

4. 设置cookie

   `res.cookie('name','test', {maxAge: 1000*60*60});`

   ```
   app.get('/', (req, res) => {
       // 设置cookie，如果cookie没有过期的话，关闭浏览器后重新打开cookie，cookie不会销毁
       res.cookie('name','test', {maxAge: 1000*60*60});
   
       res.send('Cookie的使用');
   });
   ```

5. 获取cookie

   `let name = req.cookies.name;`

   ```
   app.get('/article', (req, res) => {
       // 获取cookie
       let name = req.cookies.name;
       res.send('文章页面----' + name);
   });
   
   app.get('/user', (req, res) => {
       // 获取cookie
       let name = req.cookies.name;
       res.send('用户页面----' + name);
   })
   ```

   > 在访问`/`时设置了cookie，在这个域（Domain）下不同的页面之间可以共享这个cookie

##### 指定 cookie 的路径

`path`：指定 cookie 的路径，默认为当前路径。

```
// 指定cookie路径
res.cookie('name','test', {maxAge: 1000*60*60, path: '/article'});
```

> 设置了之后，在文章页面可以获取到该cookie，在用户页面获取不了该cookie

##### 指定 cookie 的域名

`domain`：指定 cookie 的域名，默认为当前域名

1. 在host中添加两个域

   ```
   127.0.0.1 aaa.test.com
   127.0.0.1 bbb.test.com
   ```

2. `http://localhost:5000/`的访问，可以使用`http://aaa.test.com:5000/`和`http://bbb.test.com:5000/`访问

3. 在`aaa.test.com`中设置的cookie，在`bbb.test.com`中无法获取——【默认为当前域名】

   ```
   app.get('/', (req, res) => {
       res.cookie('name','test', {maxAge: 1000*60*60});
       res.send('Cookie的使用');
   });
   ```

   1. 先访问`http://aaa.test.com:5000/`进行设置cookie        
   2. 访问`http://aaa.test.com:5000/user`，可以获取到cookie
   3. 访问`http://bbb.test.com:5000/user`，无法获取到cookie

4. 设置多个域名共享cookie

   ```
   // 设置多个域名共享cookie， aaa.test.com   bbb.test.com
   res.cookie('name','test22', {maxAge: 1000*60*60, domain: '.test.com'});
   ```

   > aaa.test.com和bbb.test.com共享cookie       test.com二级域名都可以获取cookie

##### 中文cookie

```
res.cookie('name','张三', {maxAge: 1000*60*60});
```

> cookie可以在客户端修改，如果像这种中文编码后的值被修改后，就会乱码。所以要对cookie进行加密

##### 加密cookie

`防止cookie被恶意篡改`

1. 在初始化 cookie-parser 中间件时，需要传入一个 secret 参数，这个参数就是用来对 cookie 进行签名的密钥。

   ```
   // 1. 配置中间件的时候需要传入加密的参数
   app.use(cookieParser('test'));
   ```

2. 将 signed 参数设置为 true

   ```
   // 2.将 signed 参数设置为 true
   res.cookie('name','test33', {maxAge: 1000*60*60, signed: true});
   ```

3. 获取签名后的cookie值

   ```
    let signedName = req.signedCookies.name; 
   ```

`加了签名后的cookie，如果被修改了，无法获取到cookie的值，会默认返回false/undefined`



### Express Session的基本使用

##### 一、Session的简单介绍

​		**session是另一种记录客户状态的机制,不同的是Cookie保存在客户端浏览器中，而session保存在服务器上。**

​		Cookie数据存放在客户的浏览器上，Session数据放在服务器上。Session相比 Cookie要更安全一些。由于Session保存到服务器上，所以当访问量增多的时候，会比较占用服务器的性能。单个cookie保存的数据大小不能超过4K，很多浏览器都限制一个站点最多保存20个cookie。Session没有这方面的限制。Session是基于Cookie进行工作的。



##### 二、Session的工作流程

​		当浏览器访问服务器并发送第一次请求时，服务器端会创建一个session对象，生成一个类似于key, value的键值对，然后将key (cookie)返回到浏览器(客户)端，浏览器下次再访问时，携带key (cookie)，找到对应的session(value)。



##### 三、express-session的使用

https://www.npmjs.com/package/express-session

1. 安装

   ```
    npm i express-session --save
   ```

2. 引入

   ```
   const session = require('express-session');
   ```

3. 配置session的中间件

   ```
   // 配置session的中间件
   app.use(session({
       secret: 'keyboard cat',     // 服务器端生成session的签名
       resave: false,              // 强制保存 session  即使它并没有变化
       saveUninitialized: true,    // 强制将未初始化的session存储
       cookie: { 
           maxAge: 1000*60,
           secure: false            // true表示只有https协议才能访问cookie
       },
       rolling: true         // 在每次请求时强行设置cookie，这将重置cookie过期时间（默认是false)
   }))
   ```

4. 设置session

   ```
   app.get('/login', (req, res) => {
       // 设置session
       req.session.username = '张三';
       req.session.age =  28;
       res.send('执行登录!');
   });
   ```

5. 获取session

   ```
   app.get('/', (req, res) => {
       // 获取session
       if(req.session.username || req.session.age) {
           res.send('欢迎--'+ req.session.username + ' '+  req.session.age +'--!');
       }else {
           res.send('请先登录!');
       }
   });
   ```

6. 销毁session

   ```
   app.get('/loginOut', (req, res) => {
       // 删除session
       // 1.设置session的过期时间为0(它会把所有的session值都销毁)
       // req.session.cookie.maxAge = 0;
       // 2. 销毁指定session
       // req.session.username = '';
       // 3. 销毁session
       req.session.destroy();   // 全部销毁
   	
   	 //	req.session.destroy(function(err){
   	 //	
   	 //	});
       res.send('退出登录!');
   });
   ```

   

#### 负载均衡配置session，把session保存到数据库

多服务器负载均衡

1. 安装

   ```
   npm i express-session connect-mongo --save
   ```

2. 引入模块

   [connect-mongo](https://www.npmjs.com/package/connect-mongo)

   ```
   const express = require('express');
   const session = require('express-session');
   const MongoStore = require('connect-mongo');
   const app = express();
   ```

3. 配置session中间件

   ```
   // 配置session的中间件
   app.use(session({
       secret: 'keyboard cat',     // 服务器端生成session的签名
       name:'test',                // 修改session对应cookie的名称
       resave: false,              // 强制保存 session  即使它并没有变化
       saveUninitialized: true,    // 强制将未初始化的session存储
       store: MongoStore.create({    
           mongoUrl:'mongodb://localhost:27017/sessionDB', // 数据库连接地址
           touchAfter: 24 * 3600 // session自动更新时间（不管发出了多少次请求，在24小时内只更新一次session，除非你改变了）
       }),
       cookie: { 
           maxAge: 1000*60,         // session过期时间
           secure: false            // true表示只有https协议才能访问cookie
       },
       rolling: true                // 在每次请求时强行设置cookie，这将重置cookie过期时间（默认是false)  
   }))
   ```

4. 在mongoDB中查看数据

   ```
   > use sessionDB
   switched to db sessionDB
   > show collections
   sessions
   > db.sessions.find()
   { "_id" : "e0DHVlNpyZoixD7MT-A_Kr1EqMQno6My", "expires" : ISODate("2023-03-29T06:19:29.579Z"), "lastModified" : ISODate("2023-03-29T06:18:29.579Z"), "session" : "{\"cookie\":{\"originalMaxAge\":60000,\"expires\":\"2023-03-29T06:19:29.579Z\",\"secure\":false,\"httpOnly\":true,\"path\":\"/\"},\"username\":\"张三\",\"age\":28}" }
   >
   ```

##### 其他存储方式的插件

##### [connect-redis](https://www.npmjs.com/package/connect-redis)

##### [connect-mysql](https://www.npmjs.com/package/connect-mysql)



### Express路由模块化以及 Express应用程序生成器

http://expressjs.com/en/guide/routing.html 中的`express.Router`

Express中允许我们通过`express.Router`创建模块化的、可挂载的路由处理程序。

1. 新建login.js；将登录相关模块的api都写在login.js中，便于管理，也便于多人同时协作开发

2. 在app.js中

   ```
   // 1.引入login模块
   const login = require('./routes/login');
   // 2.挂载login模块
   app.use('/login', login);
   ```

3. 访问`http://localhost:5000/login/*`，即可正常访问

`routes/login.js`：

```
const express = require('express');
const router = express.Router();

router.get('/', function(req, res) {
    res.render('login',{});
})

router.post('/doLogin', function(req, res) {
    var body = req.body
    console.log(body);
    res.send('执行提交' + body.username);
})

module.exports = router;
```

`login.html`：

```
<form action="/login/doLogin" method="post">
    <div class="form-group">
        <label for="username">用户名</label>
        <input type="text" class="form-control" id="username" name="username">
    </div>
    <div class="form-group">
        <label for="password">密码</label>
        <input type="password" class="form-control" id="password" name="password">
    </div>
    <div class="form-group">
        <input type="submit" value="提交">
    </div>
</form>
```

`app.js`：

```
const express = require('express');
const ejs = require('ejs');
const bodyParser = require('body-parser');
const app = express();

// 引入外部login模块
const login = require('./routes/login');

// 配置模板引擎
app.engine('html', ejs.__express)
app.set('view engine', 'html');

// 配置静态资源目录
app.use(express.static('public'));

// 配置第三方中间件
app.use(bodyParser.urlencoded({ extended:false}));
app.use(bodyParser.json());

// 挂载login模块
app.use('/login', login);

app.get('/', (req, res) => {
  res.send('首页!');
});

app.listen(5000, () => {
  console.log('Example app listening on port 5000!');
});

```

##### 新建user.js模块

```
const express = require('express');
const router = express.Router();

router.get('/', function(req, res) {
    res.send('用户列表');
});
router.get('/add', function(req, res) {
    res.send('添加用户');
});
router.get('/edit', function(req, res) {
    res.send('编辑用户');
});

module.exports = router;
```

##### 挂载user模块

```
const user = require('./routes/user')

// 挂载user模块
app.use('/user', user);
```

访问`http://localhost:5000/user/*`即可

#### Express应用程序生成器-[express-generator](http://expressjs.com/en/starter/generator.html#express-application-generator)

安装

```
npm install -g express-generator
```

验证是否安装成功

```
 express -h
```

创建项目

```
express --view=ejs myapp
```

```
// 执行以上命令，会创建myapp目录，在里面自动生成以下目录及文件：
myapp
│  app.js
│  package.json
│
├─bin
│      www
│
├─public
│  ├─images
│  ├─javascripts
│  └─stylesheets
│          style.css
│
├─routes
│      index.js
│      users.js
│
└─views
        error.ejs
        index.ejs
```

```
cd myapp
npm i
npm start  或  node ./bin/www
```

##### 根据不同模块创建路由

1. 路由分模块：

   ```
   routes
   │  admin.js
   │  api.js
   │  index.js
   │
   └─admin
           login.js    
           nav.js      
           user.js
   ```

2. 页面分模块：

   ```
   views
   │  error.ejs
   │  index.ejs
   │
   └─admin
       ├─login
       │      index.ejs
       │
       ├─nav
       │      add.ejs
       │
       └─user
               add.ejs
   ```

3. 路由配置

   `routes/index.js`：

   ```
   var express = require('express');
   var router = express.Router();
   
   /* GET home page. */
   router.get('/', function(req, res, next) {
     res.render('index', { title: 'Express' });
   });
   
   module.exports = router;
   ```

   `routes/api.js`：

   ```
   var express = require('express');
   var router = express.Router();
   
   /* GET API listing. */
   router.get('/', function(req, res, next) {
     res.send('API');
   });
   
   module.exports = router;
   ```

   `routes/admin.js`：

   ```
   var express = require('express');
   var router = express.Router();
   
   // 引入模块
   const user = require('./admin/user');
   const login = require('./admin/login');
   const nav = require('./admin/nav');
   
   /* GET Admin listing. 管理后台相关的*/
   router.get('/', function(req, res, next) {
     res.send('后台管理中心');
   });
   
   // 挂载路由
   router.use('/user', user);
   router.use('/login', login);
   router.use('/nav', nav);
   
   module.exports = router;
   ```

   `routes/admin/user.js`：

   ```
   const express = require('express');
   const router = express.Router();
   
   router.get('/', function(req, res) {
       res.send('用户列表');
   });
   router.get('/add', function(req, res) {
       res.render('admin/user/add');
   });
   router.get('/edit', function(req, res) {
       res.send('编辑用户');
   });
   
   router.post('/doAdd', function(req, res) {
       var body = req.body;
       res.send(body);
   });
   
   router.post('/doEdit', function(req, res) {
       res.send('执行编辑');
   });
   
   module.exports = router;
   ```

   `routes/admin/nav.js`：

   ```
   const express = require('express');
   const router = express.Router();
   
   router.get('/', function(req, res) {
       res.send('导航列表');
   });
   router.get('/add', function(req, res) {
       res.render('admin/nav/add');
   });
   router.get('/edit', function(req, res) {
       res.send('编辑用户');
   });
   
   router.post('/doAdd', function(req, res) {
       var body = req.body;
       res.send(body);
   });
   
   router.post('/doEdit', function(req, res) {
       res.send('执行编辑');
   });
   
   module.exports = router;
   ```

   `routes/admin/login.js`：

   ```
   const express = require('express');
   const router = express.Router();
   
   router.get('/', function(req, res) {
       res.render('admin/login/index',{});
   })
   
   router.post('/doLogin', function(req, res) {
       var body = req.body
       console.log(body);
       res.send('执行提交' + body.username);
   })
   
   module.exports = router;
   ```

4. 页面

   `views/admin/user.ejs`：

   ```
   <form action="/admin/user/doAdd" method="post">
       <input type="text" name="username" placeholder="用户名">   <br/> <br/>
       <input type="password" name="password" id="password"placeholder="密码"> <br/> <br/>
       <input type="submit" value="提交">
   </form>
   ```

5. app.js配置

   ```
   const admin = require('./routes/admin');
   const index = require('./routes/index');
   const api = require('./routes/api');
   
   app.use('/admin', admin);
   app.use('/api', api);
   app.use('/', index);
   ```

### Express结合multer 上传图片

Multer是一个node.js中间件，用于处理multipart/form-data类型的表单数据，它主要用于上传文件。它是写在 busboy 之上非常高效。

**注意**: Multer不会处理任何非`multipart/form-data`类型的表单数据。

1. 安装依赖

   ```
   npm i express ejs multer --save
   ```

2. 在根目录新建`static/uploads`目录， 上传之前目录必须存在

3. `app.js`：

   ```
   const express = require('express');
   var path = require('path');
   const multer = require('multer');
   const upload =  multer({ dest: 'static/uploads'}); // uploads这个目录必须要在上传文件前存在
   const app = express();
   
   app.set('views', path.join(__dirname, 'views'));
   app.set('view engine', 'ejs');
   
   app.get('/', (req, res) =>{
       res.send('hello world');
   });
   
   app.get('/upload', (req, res) =>{
       res.render('upload');
   });
   
   // pic是文件框的name值
   app.post('/doUpload', upload.single('pic'), (req, res) => {
       console.log(req.file);
       res.send(req.file);
   });
   
   app.listen(5000, () => {
       console.log('server is running at port 5000');
   });
   ```

4. `views/upload.ejs`：

   `注意`：form 要一定加上` enctype="multipart/form-data"`属性

   ```
   <form action="/doUpload" method="post" enctype="multipart/form-data">
       <input type="file" name="pic">
       <input type="submit" value="上传">
   </form>
   ```

5. 上传一张图片之后，可以在`static/uploads`下多了一个文件名随机生成的文件，但是`没有后缀名，打开不了`

##### 自定义上传后的文件名以及设置文件后缀名

`app.js`中将`const upload =  multer({ dest: 'static/uploads'});`替换为以下代码：

```
const storage = multer.diskStorage({
    // 配置上传的目录
    destination: function (req, file, cb) {
        cb(null, 'static/uploads')     // 上传之前目录必须存在
    },
    // 修改上传后的文件名
    filename: function (req, file, cb) {
        // 1. 获取后缀名
        const extname = path.extname(file.originalname);
        // 2. 获取文件名
        const basename = path.basename(file.originalname, extname);
        // 3. 生成新的文件名
        cb(null, basename + Date.now() + extname)

        // cb(null, file.originalname)
    }
})
const upload = multer({ storage: storage })
```

##### 将文件上传的这个功能封装到`tools.js`中

`model/tools.js`：

```
const path = require('path');
const multer = require('multer');

let tools = {
    multer(){
        const storage = multer.diskStorage({
            // 配置上传的目录
            destination: function (req, file, cb) {
                cb(null, 'static/uploads')     // 上传之前目录必须存在
            },
            // 修改上传后的文件名
            filename: function (req, file, cb) {
                // 1. 获取后缀名
                const extname = path.extname(file.originalname);
                // 2. 获取文件名
                const basename = path.basename(file.originalname, extname);
                // 3. 生成新的文件名
                cb(null, basename + Date.now() + extname)
        
                // cb(null, file.originalname)
            }
        })
        const upload = multer({ storage: storage })

        return upload;
    }
}

module.exports = tools;
```

`app.js`：

```
const tools = require('./model/tools');


// pic是文件框的name值
app.post('/doUpload', tools.multer().single('pic'), (req, res) => {
    console.log(req.file);
    res.send(req.file);
});
```

#### Express按照日期生成上传文件目录

- [mkdirp](https://www.npmjs.com/package/mkdirp)——创建目录
- [silly-datetime](https://www.npmjs.com/package/silly-datetime)——格式化日期

安装依赖

```
npm i silly-datetime --save
```

`model/tools.js`:

```
const path = require('path');
const multer = require('multer');
const { mkdirp } = require('mkdirp');
var sd = require('silly-datetime');
let tools = {
    multer(){
        const storage = multer.diskStorage({
            // 配置上传的目录
            destination: async (req, file, cb)=>{
                // 1. 获取当前日期 20200703
                const day = sd.format(new Date(), 'YYYYMMDD');
                // 2. 拼接目录：static/upload/20200703
                let dir = path.join('static/uploads', day);
                // 3. 按照日期生成图片存储目录   mkdirp是一个异步方法  要使用 async 和 await
                await mkdirp(dir);
                // 4. 生成新的文件名
                cb(null, dir)     // 上传之前目录必须存在
            },
            // 修改上传后的文件名
            filename: function (req, file, cb) {
                // 1. 获取后缀名
                const extname = path.extname(file.originalname);
                // 2. 获取文件名
                const basename = path.basename(file.originalname, extname);
                // 3. 生成新的文件名
                // 原文件名
                cb(null, basename + extname);
                
                // 带日期
                // const day = sd.format(new Date(), 'YYYYMMDD');
                // cb(null, basename + '_' + day + extname)
            }
        })
        const upload = multer({ storage: storage })

        return upload;
    }
}

module.exports = tools;
```

#### 多文件上传

`app.js`：

```
// 这里tools.multer() == upload
var cpUpload = tools.multer().fields([
    { name: 'pic1', maxCount: 1 },
    { name: 'pic2', maxCount: 1 },
])

// pic是文件框的name值
app.post('/doUpload', cpUpload, (req, res) => {
    // console.log(req.file);
    // res.send(req.file);
    res.send(req.files);   // 多文件上传,要用files
});
```

#### 上传文件的文件名为中文的处理

[解决multer上传文件乱码 文件上传](https://blog.csdn.net/samllucky/article/details/126962435)

[fileFilter](https://github.com/expressjs/multer#filefilter)（Function）——Multer的option

```
fileFilter(req, file, callback) {
    // 解决中文名乱码的问题 latin1 是一种编码格式
    file.originalname = Buffer.from(file.originalname, "latin1").toString("utf8");
    callback(null, true);
},
```



```
const path = require('path');
const multer = require('multer');
const { mkdirp } = require('mkdirp');
var sd = require('silly-datetime');
let tools = {
    multer(){
        const storage = multer.diskStorage({
            // 配置上传的目录
            destination: async (req, file, cb)=>{
                // 1. 获取当前日期 20200703
                const day = sd.format(new Date(), 'YYYYMMDD');
                // 2. 拼接目录：static/upload/20200703
                let dir = path.join('static/uploads', day);
                // 3. 按照日期生成图片存储目录   mkdirp是一个异步方法  要使用 async 和 await
                await mkdirp(dir);
                // 4. 生成新的文件名
                cb(null, dir)     // 上传之前目录必须存在
            },
            // 修改上传后的文件名
            filename: function (req, file, cb) {
                // // 1. 获取后缀名
                // const extname = path.extname(file.originalname);
                // // 2. 获取文件名
                // const basename = path.basename(file.originalname, extname);
                // 3. 生成新的文件名
                // 原文件名
                // cb(null, decodeURI(file.originalname));
                cb(null, file.originalname);

                // 带日期
                // const day = sd.format(new Date(), 'YYYYMMDD');
                // cb(null, basename + '_' + day + extname)
            }
        })
        const upload = multer({
            fileFilter(req, file, callback) {
                // 解决中文名乱码的问题 latin1 是一种编码格式
                file.originalname = Buffer.from(file.originalname, "latin1").toString("utf8");
                callback(null, true);
            },
            storage: storage
         })

        return upload;
    }
}

module.exports = tools;
```

#### 一个文件选择框进行多选——可以使用`upload.array()`

```
 <input type="file" name="pic1" multiple>
```

```
app.post('/doUpload', upload.array('pic1', 2), (req, res) => {
  console.log(req.files);
  res.send('Files uploaded successfully.');
});
```

#### 多个文件上传框，每个文件上传框多选的报错处理

报错信息：`MulterError: Unexpected field`

原来代码：

```
// upload.ejs:
<form action="/doUpload" method="post" enctype="multipart/form-data">
    <input type="file" name="pic1" multiple>
    <input type="file" name="pic2" multiple>
    <input type="submit" value="上传">
</form>

// app.js:
var cpUpload = tools.multer().fields([
    { name: 'pic1', maxCount: 2 },
    { name: 'pic2', maxCount: 8 },
])

app.post('/doUpload', cpUpload, (req, res) => {
    res.send(req.files);   // 多文件上传,要用files
});
```

在[Node Multer unexpected field](https://stackoverflow.com/questions/31530200/node-multer-unexpected-field)中看到以下解答：

###### **2022-2023 Answer**

When using FormData and working with arrays, the multer variable name must also include the '**[]**', this did not use to be the case.

Old code:

```js
const multerConfig = upload.fields([
    {name: 'photos', maxCount: 20}
])
```

**2022+** code:

```js
const multerConfig = upload.fields([
    {name: 'photos[]', maxCount: 20}
])
```

修改后的代码：

`将name值修改为[]形式，可解决`

```
<input type="file" name="pic1[]" multiple>
<input type="file" name="pic2[]" multiple>
```

```
var cpUpload = tools.multer().fields([
    { name: 'pic1[]', maxCount: 2 },
    { name: 'pic2[]', maxCount: 8 },
])
```

### mongoose 入门以及mongoose 实现数据的增、删、改、查

> Mongoose是在node.js异步环境下对mongodb进行便捷操作的对象模型工具。Mongoose是NodeS的驱动，不能作为其他语言的驱动。

[Mongoose](https://mongoosejs.com/)有两个特点：

1、通过关系型数据库的思想来设计非关系型数据库
2、基于mongodb驱动，简化操作

#### 使用

1. 安装

   ```
   npm i mongoose --save
   ```

2. 引入

   ```
   const mongoose = require('mongoose');
   ```

3. 连接数据库

   ```
   mongoose.connect('mongodb://127.0.0.1:27017/test');     // test是数据库名
   ```

   如果有账户密码需要采用下面的连接方式：

   ```
   mongoose.connect('mongodb://admin:123456@127.0.0.1:27017/test');   //账号:密码@
   ```

4. 定义Schema， `字段名称必须要与数据库保持一致`

   > 数据库中的Schema，为数据库对象的集合。schema是 mongoose里会用到的一种数据模式,可以理解为表结构的定义;每个schema 会映射到mongodb中的一个collection，它不具备操作数据库的能力

   ```
   const { Schema } = mongoose;
   
   var UserSchema = new Schema({
       name: String,
       age: Number,
       sex: String
   });
   ```

5. 定义Model(创建数据模型)

   > 定义好了Schema，接下就是生成Model。model是由schema生成的模型，可以对数据库的操作。
   > 注意：mongoose.model里面可以传入两个参数也可以传入三个参数

   mongoose.model（参数1：模型名称（`首字母大写`)，参数2：Schema，参数3:数据库集合名称)
   **如果传入2个参数的话：**这个模型会和`模型名称相同的复数的数据库建立连接`：如通过下面方法创建模型，那么这个模型将会操作users这个集合。
   **如果传入3个参数的话：**模型默认操作第三个参数定义的集合名称

   ```
   var User = mongoose.model('User', UserSchema);      // 操作users表——User则对应users表
   ```

   ```
   var User = mongoose.model('User', UserSchema, 'user');  // 操作user表
   ```

6. 查询数据

   ```
User.find({}, function (err, users) {
       if (err) {
           console.log(err);
       } else {
           console.log(users);
       }
   });
   ```
   
   报错处理`throw new MongooseError('Model.find() no longer accepts a callback');`

   因为在Mongoose 6.0版本中，Model.find()方法不再接受回调函数，而是返回一个Promise。如果你在Mongoose 6.0或更高版本中继续使用回调函数调用Model.find()，就会出现这个错误。

   修改后：

   ```
   User.find({})
       .then((users) => {
           console.log(users);
       })
       .catch((error) => {
           console.log(error);
       });
   ```

7. 增加数据（插入数据）

   `Model.save()方法不再接受回调函数`

   ```
   var user = new User({
       name: '张三AAAAAA',
       age: 18,
       sex: '男'
   });
   
   user.save()
   .then((users) => {
       console.log(users);
   })
   .catch((error) => {
       console.log(error);
   });
   ```

8. 更新数据

   ```
   User.updateOne({
       name: '张三AAAAAA'
   }, {
       $set: {
           name: '张三333',
           age: 28,
           sex: '女'
       }
   })
   .then((users) => {
       console.log(users);
   })
   .catch((error) => {
       console.log(error);
   });
   ```

9. 删除数据

   ```
   User.deleteOne({'_id':'642538f4a1e6c5b49ac14d57'}) // id直接写字符串就行，mongoose会处理
   .then((res) => {
       console.log(res);
   })
   .catch((error) => {
       console.log(error);
   });
   ```

   控制台输出：

   ```
   { acknowledged: true, deletedCount: 1 }
   ```

#### mongoose默认参数、mongoose模块化、mongoose性能疑问

mongoose 默认参数：增加数据的时候，如果不传入数据会使用默认配置的数据





mongoose 预定义模式修饰符`Getters`与 `Setters`修饰符









https://www.bilibili.com/video/av38925557

https://www.bilibili.com/video/av41033371