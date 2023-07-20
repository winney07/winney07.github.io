---
title: 使用cmd命令删除文件夹
date: 2019-12-06 11:48:43
tags:
- 常用命令
categories: 
- 常用命令
---
###### 1、删除空文件夹
```bash
rmdir 空文件夹名
```
###### 2、删除文件夹以及文件夹内所有内容（/s是删除所有子目录以及其中的内容；/q是在删除时，不提示yes or no）
```bash
rmdir /s/q 文件夹名
```
###### 3、删除指定盘符的文件夹(删除D盘multify文件夹下的my-multify文件夹以及子内容，并且不提示)
```bash
rmdir /s/q d:\multify\my-multify
```