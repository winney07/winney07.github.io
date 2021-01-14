---
title: TypeScript 简介
date: 2020-11-04 15:43:11
tags:
-  TypeScript
categories: 
- 工作笔记
- TypeScript
---
[【技术胖博客】](https://jspang.com/detailed?id=63)

###### Demo1.ts

```
function jspang() 
{ 
    let web: string = "Hello world" 
    console.log (web)
}
jspang()
```



##### 初步运行

```
node Demo.ts

会出现报错：
SyntaxError: Unexpected token ':'
表示异常，不支持这个东西。
```

输入以下语句来转ts为js：
```
tsc Demo1.ts
```
如果出现：
 无法将“tsc”项识别为 cmdlet、函数、脚本文件或可运行程序的名称。请检查名称的拼写，如果包括路径，请确保路径正确，然后再试一次。

[参考](https://www.cnblogs.com/vickylinj/p/12228773.html)  则：
```
npm install typescript -g
cnpm install typescript -g

再次运行即可：
tsc Demo1.ts
node Demo1.js
```
每次都这样的操作比较麻烦，可以全局安装ts-node
```
cnpm install -g ts-node 
```
即可直接输入以下语句执行：
```
ts-node Demo1.ts
```