---
title: MangoDB
date: 2021-01-20 11:22:42
tags:
- MangoDB
categories: 
- 工作笔记
- MangoDB
---

[mongoDB官网](https://www.mongodb.com/)    [mongoDB中文官网](https://www.mongodb.org.cn/)  

#### 安装

参考教程：[安装mongodb3.6之Installing MongoDB Compass...](https://blog.csdn.net/mar_ljh/article/details/79286913)

![安装教程](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/MangoDB/note2.png)

#### 环境变量配置

环境变量加在“系统变量”中

![环境变量加在“系统变量”中](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/MangoDB/note3.png)

##### [安装compass](https://docs.mongodb.com/manual/reference/program/install_compass/index.html)

#### 备份与删除

备份：

```
mongodump -h 127.0.0.1 -d company -o D:\software\MangoDB\backup\123
```

恢复：

```
mongorestore -h 127.0.0.1 -d testDemo D:\software\MangoDB\backup\123\company
```



  [【尚硅谷】前端视频_MongoDB夯实基础视频](https://www.bilibili.com/video/av21989676?from=search&seid=13644841351714946278)

- 基本概念

  数据库（database）

  集合（collection）

  文档（documen）
  	-在MongoDB中，数据庳和集合都不需要手动创建，
  		当我们创建文档时，如果文档所在的集合或数据库不存在会自动创建数据庳和集合

- 基本指令

  - show dbs
  - show databases
    -显示当前的所有数据库
  - use 数据库名
    -进入到指定的数据库中
  - db
    -db表示的是当前所处的数据库
  - show collections
    -显示数据库中所有的集合

#### 数据库（Database）

- 数据库是按照数据结构来组织、存储和管理数据的仓库。
- 我们的程序都是在内存中运行的，一旦程序运行结束或者计算机断电，程序运行中的数据都会丢失。
- 所以我们就需要将一些程序运行的数据持久化到硬盘之中，以确保数据的安全性。而数据库就是数据持久化的最佳选择。
- 说白了，数据库就是存储数据的仓库。



#### 数据库分类

数据库主要分成两种:

- 关系型数据库(RDBMS)

  - MySQL、Oracle、DB2、SQL Server .....

  - 关系数据库中全都是表

- 非关系型数据库(NoSQL Not Only SQL)
  
   - MongoDB、Redis......
   - 键值对数据库
   - 文档数据库MongoDB

#### 数据库(database)

- 数据库的服务器

  - 服务器用来保存数据

  - mongod用来启动服务器

- 数据库的客户端

  - 客户端用来操作服务器，对数据进行增删剧改查的操作

  - mongo用来启动客户端

#### MongoDB简介

- MongoDB是为快速开发互联网Web应用而设计的数据库系统。
- MongoDB的设计目标是极简、灵活、作为Web应用栈的一部分。
- MongoDB的数据模型是面向文档的，所谓文档是一种类似于JSON的结构，简单理解MongoDB这个数据库中存的是各种各样的JSON。(BSON )



#### 三个概念

- 数据库( database )
  – 数据库是一个仓库，在仓库中可以存放集合。

- 集合( collection )
  – 集合类似于数组，在集合中可以存放文档。

- 文档( document )

  – 文档数据库中的最小单位，我们存储和操作的内容都是文档。

#### 下载MongoDB

- 下载地址

   https://www.mongodb.org/dl/win32/

- MongoDB的版本偶数版本为稳定版，奇数版本为开发版。

- MongoDB对于32位系统支持不佳，所以3.2版本以后没有再对32位系统的支持。

##### SQL

- 结构化查询语言
- 关系数据库全都同SQL来操作

1.安装MongoDB

- 安装
- 配置环境交量
  C: \Program Files\MongoDB\Server\3.2\bin
- 在c盘根日录
  - 创建一个文件夹data
  - 在data中创建一个文件夹db
- 打开cmd命令行窗口
  - 输入mongod启动mongodb服务器
  - 32位注意：
    启动服务器时，需要输入如下内容：
    mongod --storageEngine=mmapv1
- 在打开一个cmd窗口
  输入mongo连接mongodb ，出现  >

#### 启动MongoDB

- 在C盘根目录下创建data文件夹，在data下创建db文件夹

- 打开CMD命令行窗口，输入mongod

- 32位系统第一次启动∶

  mongod --storageEngine=mmapv1

> 端口号最大不要超过65535
>
> mongod --dbpath 数据库路径 
>
> 如果不想使用默认的端口号， 可以 mongod --dbpath 数据库路径 --port 端口号

**注：先开数据库，再开客户端  先 mongod 再mongo**



将MongoDB设置为系统服务，可以白动在后台启动，不需要每次都手动启动

1. 在c盘根目录创建data
   在data 下创建db和log文件夹

2. 创建配置文件
   在目录C: \Program Files\MongoDB\Server\3.2下添加一个配置文件mongod.cfg

3. 以管理员的身份打开命令行窗口

4. 执行如下的命令

   ```
   sc.exe  create MongoDB binPath="\"C:\Program Files mongoDB\Server\3.2\bin\mongod.exo\" --service --config=\"C:Program Files\MongoDB\Server\3.2\mongod.cfg\"" DisplayName= "MongoDB" start= "auto"
   
   sc.exe create MongoDB binPath="\"mongod的bin目录\mongod.exe\"--service --config=\"mongo的安装目录\mongod.cfg\"" DisplayName="MongoDB" start= “auto"
   ```

5. 启动mongodb服务

6. 如果启动失败，证明上边的操作有误,
   在控制台输入sc delete MongoDB别除之前配置的服务然后从第—步再来一次

[增删改查](https://docs.mongodb.com/manual/crud/)

#### 数据库服务器—mongoDB

![数据库服务器—mongoDB](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/MangoDB/note1.png)

#### 安装mongodb以及设置为windows服务 详细步骤

[参考教程](https://blog.csdn.net/u010874036/article/details/51921206)

[Install MongoDB Community Edition on Windows](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-windows/)