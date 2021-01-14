---
title: webpack起步
date: 2019-11-20 11:14:04
tags:
- webpack
categories:
- 工作笔记
- webpack
---
## 基本安装
#### 一、
首先我们创建一个目录，初始化 npm(生成package.json文件），然后 在本地安装 webpack，接着安装 webpack-cli（此工具用于在命令行中运行 webpack）：

注意：webpack为4+版本以上，需要安装webpack-cli ,安装本地webpack-cli之前，要安装全局

安装淘宝镜像 *如果网速不太好的情况下，可以选择安装淘宝镜像*
```bash
npm install -g cnpm --registry=https://registry.npm.taobao.org
```
```bash
mkdir webpack-demo && cd webpack-demo
npm init -y
npm install webpack webpack-cli --save-dev
```

*<div style="background:#DCF2FD;color:#618ca0;padding:6px;">贯穿整个指南的是，我们将使用 diff 块，来显示我们对目录、文件和代码所做的更改。</div>*

#### 二、
现在我们将创建以下目录结构、文件和内容：
###### project
```bash
  webpack-demo
  |- package.json
+ |- index.html
+ |- /src
+   |- index.js
```
###### src/index.js
```bash
function component() {
  var element = document.createElement('div');

  // Lodash（目前通过一个 script 脚本引入）对于执行这一行是必需的
  element.innerHTML = _.join(['Hello', 'webpack'], ' ');

  return element;
}

document.body.appendChild(component());
```
###### index.html
```bash
<!doctype html>
<html>
  <head>
    <title>起步</title>
    <script src="https://unpkg.com/lodash@4.16.6"></script>
  </head>
  <body>
    <script src="./src/index.js"></script>
  </body>
</html>
```
> 我们还需要调整 package.json 文件，以便确保我们安装包是私有的(private)，并且移除 main 入口。这可以防止意外发布你的代码。

*<div style="background:#DCF2FD;color:#618ca0;padding:6px;">如果你想要了解 package.json 内在机制的更多信息，我们推荐阅读 {% link npm 文档 https://docs.npmjs.com/files/package.json %}。</div>*

###### package.json
```bash
 {
    "name": "webpack-demo",
    "version": "1.0.0",
    "description": "",
+   "private": true,
-   "main": "index.js",
    "scripts": {
      "test": "echo \"Error: no test specified\" && exit 1"
    },
    "keywords": [],
    "author": "",
    "license": "ISC",
    "devDependencies": {
      "webpack": "^4.0.1",
      "webpack-cli": "^2.0.9"
    },
    "dependencies": {}
  }
```
> 在此示例中，`<script>` 标签之间存在隐式依赖关系。`index.js` 文件执行之前，还依赖于页面中引入的 `lodash`。之所以说是隐式的是因为 `index.js` 并未显式声明需要引入 `lodash`，只是假定推测已经存在一个全局变量 `_`。

使用这种方式去管理 JavaScript 项目会有一些问题：
> * 无法立即体现，脚本的执行依赖于外部扩展库(external library)。
> * 如果依赖不存在，或者引入顺序错误，应用程序将无法正常运行。
> * 如果依赖被引入但是并没有使用，浏览器将被迫下载无用代码。

让我们使用 webpack 来管理这些脚本。

#### 关于webpack使用CleanWebpackPlugin插件时报错
<div style="color:red;">CleanWebpackPlugin is not a constructor</div>
错误写法：
```bash
const CleanWebpackPlugin = require("clean-webpack-plugin");
 
...
 
plugins: [
    new CleanWebpackPlugin(['dist'])
]
```
正确写法：
```bash
const { CleanWebpackPlugin } = require("clean-webpack-plugin");
 
...
 
plugins: [
    new CleanWebpackPlugin()
]
```