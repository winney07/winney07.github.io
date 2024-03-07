---
title: webpack笔记
date: 2024-02-28 14:58:53
tags:
- webpack
---

#### 将多个js文件合并成一个js文件的同时，不进行压缩

```
const path = require("path");

module.exports = {  
  entry: "./src/wanka/index.js",  // 入口文件
  output: {
    path: path.resolve(__dirname, "dist"),
    filename: "bundle.js", // 输出的文件名
  },
  mode: 'development',
  devtool: 'source-map' // 设置为生成source map
};

```

