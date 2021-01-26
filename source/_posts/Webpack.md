---
title: webpack起步
date: 2019-11-20 11:14:04
tags:
- webpack
categories:
- 工作笔记
- webpack
---
[webpack中文官网](https://www.webpackjs.com/)

#### 基本安装

#### 一、

1. 新建目录文件夹

   ```
   mkdir webpack-demo
   ```

2. 切换到目录

   ```
   cd webpack-demo
   ```

3. 生成package.json文件

   ```
   npm init
   ```

4. 安装webpack

   ```
   npm install --save-dev webpack
   ```

   > 执行webpack命令，如果可以执行，则安装成功
   >
   > 注意：webpack为4+版本以上，需要安装webpack-cli ,安装本地webpack-cli之前，要安装全局

5. 安装全局webpack-cli

   ```
   npm install webpack-cli –g
   ```

6. 安装本地webpack-cli

   ```
   npm install webpack-cli --save-dev
   ```

安装淘宝镜像（ 如果网速不太好的情况下，可以选择安装淘宝镜像）
```bash
npm install -g cnpm --registry=https://registry.npm.taobao.org
```

快速安装：
```bash
mkdir webpack-demo && cd webpack-demo
npm init -y
npm install webpack webpack-cli --save-dev
```

> 贯穿整个指南的是，我们将使用 diff 块，来显示我们对目录、文件和代码所做的更改。

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



------

#### 自动化构建工具webpack-学习笔记

##### 1、了解webpack相关

- 什么是webpack

  - webpack是一个核块打包器(bundLer)

  - 在webpack看来，前端的所有资源文件(js/json/css/img/Less/ ...)都会作为模块处理它将根据模块的依赖关系进行静态分析，生成对应的静态资源

- 理解Loader

  - webpack本身只能加载JS/JSON模块，如果要加载其他类型的文件(模块)，就需要使用对应的Loader进行转换/加载

  - Loader本身也是运行在node.js 环境中的Javascript模块

  - 它本身是一个函数，接受源文件作为参数，返回转换的结果

  - loader一般以xxx-Loader的方式命名，xxx代表了这个Loader要做的转换功能，比如json-Loader

- 配置文件(默认)

  - webpack.config.js ：是一个node模块，返回一个 json格式的配置信息对象

- 插件

  - 插件件可以完成一些Loader不能完成的功能。

  - 插件的使用一股是在webpack的配置信息plLugins 选项中指定。

  - cLeanlebpackPLugin：自动清除指定文件夹资源

  - HtmLlwebpackPLugin：自动生HTML文件并

  - uglifyJSPLugin ：压的s文件

> Webpack叫模块打包器，它认为所有文件都是模块，一个除外（html）
>
> 它本身只加载js和json，所以需要loader（js库）
>
> MODULES WITH DEPENDENCIES：模块之间的依赖关系
>
> Css要依赖图片，因为要引入它，也就是说，截图中，箭头指向的东西是它依赖的东西。
>
> STATIC ASSETS：静态资源

从webpack v4.0.0开始，可以不用引入一个配置文件。然而，webpack仍然还是`高度可配置的`。在开始前你需要先理解四个`核心概念`︰

- 入口(entry)
- 输出(output) 
- loader
- 插件(plugins)

##### 2、学习文档

- webpack官网: http: / /webpack.github.io/
- webpack3文档(英文): https : //webpack.js.org/
- webpack3文档(中文): https: //doc.webpack-china.org/

##### 3、开启项目

初始化项目：

- 新建目录文件夹（webpack_test）

- 生成package.json文件

- 安装webpack

  ```
  npm install webpack -g       // 全局安装
  npm install webpack --save-dev     // 局部安装
  ```

##### 4、编译打包应用

- 创建入口src/js/：entry.js

```
document.write("entry.js is work");
```

- 创建主页面: dist/index.html

```
<script type="text/javascript" src="bundle.js"></script>
```

- 编译js

  webpack src/js/entry.js dist/bundle.js

- 查看页面效果



##### webpack.config.js

```
const path = require('path');    // node内置的模块用来去设置路径的;

module.exports = {
	entry: "./src/index.js',
	output: {
		filename: "bundle.js ',
		path: path.resolve(_dirname,'dist')
	}
};
```

#### 5、打包应用

```
npm run build
```

#### 6、打包css和图片文件

- 安装样式的loader

  ```
  npm i css-loader style-loader --save-dev
  npm i file-loader url-loader --save-dev
  ```

  > 补充：url-loader是对象file-loader的上层封装，使用时需配合file-loader使用

- 配置loader

  ```
  module.exports = {
  	module: {
  		rules: [
  			{
  				test: /\.css$/,      // $是指以.css结尾的文件
  				use: ['style-loader" , "css-loader']
  			}
  		]
  	}
  }
  
  ```

#### 7、自动编译打包

- 利用webpack开发服务器工具： webpack-dev-server

- 下载

  ```
  npm install --save-dev webpack-dev-server
  ```

- webpack配置

  ```
  devserver: {
  	contentBase: './ dist'
  }
  ```

- package配置

  ```
  "start" : "webpack-dev-server --open"
  ```

- 编译打包应用并运行

#### 8、使用webpack插件

- 常见的插件

  - 使用html-webpack-plugin根据模板html生成引入script的页面

  - 使用clean-webpack-plugin清除dist文件夹

- 下载

  ```
  npm install --save-dev html-webpack-plugin clean-webpack-plugin
  ```

- webpack配置

  ```
  const HtmLwebpackPlugin = require('html-webpack-plugin'); // 自动生成htmL文件
  ```

#### 9、热加载

------

