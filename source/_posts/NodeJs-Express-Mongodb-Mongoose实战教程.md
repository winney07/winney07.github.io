---
title: NodeJs+Express+Mongodb+Mongoose实战教程
date: 2021-03-02 11:03:04
tags:
- nodejs
- express
- mongodb
- mongoose
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



查询6万多条数据，不加索引，查询时间500多毫秒，加上索引，10毫秒左右