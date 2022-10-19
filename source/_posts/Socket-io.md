---
title: Socket.io
date: 2021-08-17 11:30:39
tags:
- Node.js
- Socket.io
---

[Socket.io-官网](https://socket.io/)

[socket.io官方文档-w3cschool](https://www.w3cschool.cn/socket/)

[socket.io官方文档中文版](https://zhuanlan.zhihu.com/p/29148869)——知乎博客

[Socket.io入门（简单使用socket）](https://www.jianshu.com/p/099056f9785c)

[Socket.io进阶（简单使用广播、命名空间）](https://www.jianshu.com/p/1aa181662a07)

[什么是socketIO？](https://www.easemob.com/news/3674)



[socket.io 快速入门教程——聊天应用](https://www.w3cschool.cn/socket/socket-ulbj2eii.html)

#### WebSockets

#### Socket.io

- Javascript库
- 面向实时Web应用
- 服务器和客户端的双向通信
- 主要使用WebSocket协议（基于WebSocket的库）
- 事件驱动





#### 测试

[debug](https://github.com/visionmedia/debug)

- [mocha](https://socket.io/zh-CN/docs/v4/testing/#example-with-mocha)
- [jest](https://socket.io/zh-CN/docs/v4/testing/#example-with-jest)
- [tape](https://socket.io/zh-CN/docs/v4/testing/#example-with-tape)

Socket.IO 客户端不是 WebSocket 实现，因此无法与 WebSocket 服务器建立连接，即使`transports: ["websocket"]`

[ws](https://www.npmjs.com/package/ws)

#### 服务器

##### 1.安装

```
yarn add socket.io
```

使用 `µWebSockets.js {#usage-with-µwebsocketsjs}`

```
yarn add uWebSockets.js@uNetworking/uWebSockets.js#v20.4.0
```

##### 初始化

[https.createServer](https://nodejs.org/api/https.html#https_https_createserver_options_requestlistener)

Konva（基于canvas的绘图库）

https://gitee.com/jepsonpp/draw-and-guess





socket发送一个connection，io收到了一个socket，就创立了连接（connected）



socket发送一个disconnection，就失去了连接



当socket发送一个input事件，携带着message数据，当io接收到之后，可能对message做相应的处理，然后返回data数据，当socket接收到data数据，可以对视图做更新处理。



CDN

https://cdnjs.com/libraries/socket.io



#### 博客文章

[Vue 使用 Vue-socket.io 实现即时聊天应用（Vue3连接原理分析）](https://blog.csdn.net/weixin_47746452/article/details/126827806?spm=1001.2014.3001.5501)

[Vue 使用 Apache Echarts 绘制地图（省市、地区）](https://blog.csdn.net/weixin_47746452/article/details/125600385?spm=1001.2014.3001.5501)

[WebSocket协议理解-数据包格式解析](http://t.zoukankan.com/zhangmingda-p-12678630.html)

[ping/pong模式_PING的完整形式是什么？](ping/pong模式_PING的完整形式是什么？)

[socket.io中的pingtimeout和pingInterval](https://qa.1r1g.com/sf/ask/3490608271/#)