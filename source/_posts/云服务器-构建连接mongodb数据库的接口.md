---
title: 云服务器-构建连接mongodb数据库的接口
date: 2022-10-22 11:12:23
tags:
- 云服务器
categories: 
- 云服务器
---

### 云服务器数据库

1. 进入`mongo`

   ```
   mongo
   ```

2. 查看已有数据库

   ```
   > show dbs
   admin      0.078GB
   local      0.078GB
   myFirstDB  0.078GB
   shopping   0.078GB
   test       0.078GB
   ```

3. 查看当前数据库

   ```
   > db
   test
   ```

4. 查看当前数据库的所有集合

   ```
   > show collections
   system.indexes
   users
   ```

5. 查找某个集合的所有数据

   ```
   > db.users.find()
   { "_id" : ObjectId("64255dec03b14a5ae59ad213"), "name" : "zhangsan", "age" : 20 }
   { "_id" : ObjectId("642650ee5d48a1118feb04d1"), "name" : "张三AAAAAA", "age" : 18, "sex" : "男", "__v" : 0 }
   { "_id" : ObjectId("6426aa7de101e51497b40037"), "name" : "张三BBBBBB", "age" : 26, "sex" : "女", "__v" : 0 }
   ```

6. 创建数据库

   ```
   > use wedding
   switched to db wedding
   > db
   wedding
   ```

7. 创建集合

   ```
   > db.createCollection('blessing')
   { "ok" : 1 }
   ```

8. 向集合中插入文档

   ```
   > db.blessing.insert({"name":"张三", "bless": "快乐快乐快乐快乐"})
   WriteResult({ "nInserted" : 1 })
   ```

9. 查看集合中插入的文档：

   ```
   > db.blessing.find()
   { "_id" : ObjectId("64dc9dcfc7acd67531cafb17"), "name" : "张三", "bless" : "快乐快乐快乐快乐" }
   ```

   



### express接口搭建

接口所在目录：`/usr/local/src/webCode/wx`

接口文件所在位置：`/usr/local/src/webCode/wx/server/wedding/blessing.js`

##### node命令使用之前

```
nvm  use 16.13.0
```

#### 运行接口

```
node api.js
```

#### 解决跨域问题

`Access to XMLHttpRequest at 'https://www.winney07.cn:8080/wedding/blessing/getBlessingList' from origin 'http://192.168.1.15:5500' has been blocked by CORS policy: Response to preflight request doesn't pass access control check: No 'Access-Control-Allow-Origin' header is present on the requested resource.`

使用的是`https`协议，在微信开发者中，请求`https://www.winney07.cn:8080/wedding/blessing/getBlessingList`接口，是可以得到数据的。

#### 解决方法：

1. 服务端——接口响应前加上

```
res.header("Access-Control-Allow-Origin", "*");              	// 允许任意外源访问
res.header("Access-Control-Allow-Headers", "Content-Type");		// 自定义请求首部字段
res.header("Access-Control-Allow-Methods", "*");    		 	// 允许所有请求方法
res.header("Content-Type", "application/json;charset=utf-8");	// 设置数据返回类型为json，字符集为utf8
```

2. 前端——使用Fetch请求

```
fetch("https://www.winney07.cn:8080/wedding/blessing/getBlessingList",{
   method:'GET'
}).then(response => {
    if (!response.ok) {
        throw new Error('Network response was not ok');
    }
    return response.json(); // 解析响应数据为 JSON 格式
})
.then(data => {
    console.log('Response data:', data);
    // 在这里处理获取到的响应数据
})
.catch(error => {
    console.error('Fetch error:', error);
});
```

> `fetch` 规范主要在三个方面与 `jQuery.ajax()` 不同：
>
> - 从 `fetch()` 返回的 Promise **不会因 HTTP 的错误状态而被拒绝**，即使响应是 HTTP `404` 或 `500`。相反，它将正常兑现（`ok` 状态会被设置为 `false`），并且只有在网络故障或者有任何阻止请求完成时，才拒绝。

[Fetch API](https://developer.mozilla.org/zh-CN/docs/Web/API/Fetch_API)



#### 接口一直保持运行状态

要保持云服务器上的 Express 接口一直运行，使其在服务器启动后保持运行状态，而不需要手动运行 `node api.js`。

**使用进程管理工具**

在服务器上安装 `pm2`：

```
npm install -g pm2
```

然后，在项目文件夹中运行：

```
pm2 start api.js
```

