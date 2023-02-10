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
mkdir webpack-demo && cd webpack-demo    //  要再git bash中运行 && 
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

`<div style="background:#DCF2FD;color:#618ca0;padding:6px;">如果你想要了解 package.json 内在机制的更多信息，我们推荐阅读 {% link npm 文档 https://docs.npmjs.com/files/package.json %}。</div>`

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

#### 打包压缩js文件-步骤

1. 全局安装`webpack-cli`

   ```
   npm install webpack-cli –g
   ```

2. 创建项目目录 + 切换到项目目录

   ```
   mkdir webpack_demo && cd webpack_demo     //  && 符号，要在git bash中才能运行
   ```

3. 初始化`package.json`文件

   ```
   npm init -y
   ```

4. 安装依赖包

   ```
   npm install webpack webpack-cli --save-dev
   ```

5. 修改`package.json`文件

   ```
   "scripts": {
       "test": "echo \"Error: no test specified\" && exit 1",
    +  "build": "webpack"       // 添加这个命令  
   },
   ```

   > 在命令行，直接输入`webpack`，进行打包。   没有添加该命令前，输入`npm run build`，进行打包

6. 在根目录创建`src/index.js`

   ```
   function component() {
       var element = document.createElement('div');
   
       // Lodash（目前通过一个 script 脚本引入）对于执行这一行是必需的
       element.innerHTML = _.join(['Hello', 'webpack'], ' ');
   
       return element;
   }
   
   document.body.appendChild(component());
   ```

7. 在根目录创建`webpack.config.js`

   ```
   const path = require('path');
   
   module.exports = {
     entry: './src/index.js',     // 配置输入路径
     mode: 'production',
     output: {          // 配置输出路径
       filename: 'bundle.js',
       path: path.resolve(__dirname, 'dist')
     }
   };
   ```

8. 执行打包命令

   ```
   webpack     
   ```

   或

   ```
   npm run build
   ```

9. 查看打包后文件

   在根目录会生成`dist/bundle.js`

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





#### 与gulp的比较

- gulp比较灵活  未封装
- webpack 封装好的



1. 创建目录（webpack-vue）
2. 切换到目录

```javascript
cd webpack-vue
```

3. 生成package.json文件

```javascript
cnpm init

// 将 entry point: (index.js)   改为main.js    // 这个是入口文件
```

4. 修改package.json文件

```javascript
// 将script修改为下面这样
"scripts": {
	"dev": "webpack-dev-server --open --hot --port 8888"
}
```

5. 安装vue等相关模板

```javascript
cnpm install vue --save  
或
cnpm i vue -S
```

6. 安装wepack和webpack-dev-server

```javascript
cnpm i -D webpack webpack-dev-server
```

7. 安装其他依赖包

```javascript
cnpm i -D vue-loader vue-html-loader vue-style-loader vue-template-compiler
cnpm i -D css-loader file-loader style-loader
cnpm i -D babel-loader babel-core babel-preset-env
```

8. 配置webpack

`webpack.config.js：`

```javascript
module.exports={       			// 模块
	entry: './main.js',  			// 入口文件

	output:{              		// 将VUE文件编译输出
		path: __dirname, 				// 项目根路径 是node.js中的一个全局变量,它指向当前执行脚本所在的目录
		filename: 'build.js'    // 所有的JS放入build.js
	},

	module:{
		rules:[{                  // 加载规则
			test:/\.vue$/,         // vue文件
			loader:'vue-loader'    // 加载器
		},{
			test:/\.js$/,
			loader:'babel-loader',       // ES6转换，所有的ES6文件加载及转换
			exclude: /node_modules/     // 排除这个目录
		}]
	}
}
```

9. 编写入口文件(main.js）

```javascript
import Vue from 'vue'
import App from './App.vue'

new Vue({
  el:'#app',
  render:h => h(App)

  // h相当于创建一个element
  // 相当于下面： 渲染这个App
  // render:function(createElement) {
  //     return createElement(App)
  // }
})
```



[Webpack手册介绍-源宝](http://www.ybao.org/book/webpack/webpack-2889.html)

### Webpack是什么?

1. 模块化
2. 自定义文件或npm install
3. 静态文件模块化
4. 借助于插件和加载器



### Webpack的优势

主要体现在以下几点：

1. 代码分离
2. 装载器(css , sass ，jsx等等)
3. 智能解析(require("./templatel/" + names + ".ejs"))



### 安装流程

```javascript
npm install -g webpack
npm install webpack-dev-server
```

### 创建项目步骤

1. 安装webpack

```javascript
cnpm install -g webpack
```

1. 新建一个文件夹webpack-my-app (切换到这个目录）

```javascript
...>cd 目录\webpack-my-app
```

1. 生成package.json

```javascript
> cnpm init

package name:(webpack-my-app)
version: (1.0.0)
description：应用于webpackentry 
point：(index.js)
test command:
git repository:
keywords: webpack打包工具  webpack-dev-serve
author: winney
1icense: (ISC)
```

1. 新建一个入口文件(app.js）：

```javascript
alert("我是入口文件,打包输出bundle.js");
```

1. 执行打包命令：

```javascript
webpack  app.js  bundle.js
```

（提示需要安装 webpack-cli, 在当前目录，命令：cnpm install webpack-cli -D）

在页面中引用bundle.js：(会生成一个bundle.js）

如果期间报错，查看webpack的版本

```javascript
webpack -v
```

结果报错：

```javascript
The CLI moved into a separate package: webpack-c1i. .. ,..6
please insta11'webpack-cli' in addition to webpack itself to use the CLI.
-> when using npm: npm insta11 webpack-cli-D
->when using yarn: yarn add webpack-cli -D
```

执行了cnpm insta11 webpack-cli-D，输入webpack -v，还是报一样的错。

**【解决方案】**

[webpack4.0.1安装问题及解决方法](https://www.cnblogs.com/cythia/p/8495341.html)

**全局安装一下webpack-cli**

```javascript
npm install webpack-cli -g
```

当安装完之后,就能显示版本号了,

注意点:安装好之后,打包文件的时候必须在webpack.config.js文件里面配置入口出口文件来打包,不然的话会报错.使用的时候尽量还是不要在生产环境使用.官网上也说了一句话:安装这些最新体验版本时要小心！它们可能仍然包含 bug，因此不应该用于生产环境。

**在项目目录下要本地安装webpack-cli -D**

```javascript
npm install webpack-cli -D
```

1. app.js引入people.js（如果引入的是自己创建的文件，必须使用./，即使是在同一个目录下，也要使用./）

people.js：

```javascript
// module.exports = "Hello EveryBody ! ! ! ! !";

function getHello( ) {
	return "Hello Everyone welcome to Lanou Class"
}
module.exports = getHello( );
```

app.js：

```javascript
let people = require('./people.js');
let $ = require("jquery");

// $("body").append("<h1>" + people[0].name + "</h1>");

$.each(people, function(key, value){
	$("body").append("<h1>" + people [key].name + "</h1>");
});
console.log(people[1].name);
```

### 如何将js文件进行模块化

- module.exports     require( )
- 自定义文件，引入时需要使用./
- npm下载的文件，不需要./

### 如何使用第三方

1. 在npm服务器中下载第三方
2. require()第三方

### 如何将静态文件模块化

1. 创建css文件
2. 下载对应的加载器
3. 修饰我们的css文件   !css-loader

### 如何配置webpack.config.js

- 出口文件
- 入口文件
- 模块
- 加载器

### 如何使用package.json启动项目

```javascript
scripts "build" "start"
```

### 如何将es6转换为es5

```javascript
babel babel-core babel-loader. . .
```

1. 全局安装 ：

```javascript
cnpm install -g webpack@3.8.1
```

查看版本：

```javascript
webpack -v
```

1. 生成package.json：

```javascript
cnpm init 
```

1. 局部安装

```javascript
cnpm install --save-devwebpack@3.8.1
```

1. 新建一个文件夹 src，里面放app.js（入口文件）
2. 新建一个dist文件夹，存放输出的文件
3. 在开发环境中，总是要一边改，一边看转化效果吧，webpack 也能办到，多加一个参数就好。

```javascript
webpack --watch ./src/app.js ./dist/app.bundle.js（实时监听）
```

1. 在生产环境，或线上，我们肯定不希望这么大的体积，毕竟体积越大，带宽浪费就越多呀，下载也越慢。

```javascript
webpack -p ./src/app.js ./dist/app.bundle.js 【压缩】
```

如果要发布到线上环境，我们要把它压缩一下的。

而 webpack 本来就有这样的功能，也只是一个参数 -p

------

### 配置文件的设置

#### 创建配置文件 webpack.config.js

```javascript
// entry 表示源文件，output 这边表示的是输出的目标文件。
module.exports = { 
  entry: './src/app.js',
  output: {
    filename: './dist/app.bundle.js'
  }
};
```

直接在终端上输入 webpack 就可以了。webpack 命令会去找 webpack.config.js 文件，并读取它的内容（源文件和目标文件），最后进行相应的处理。

#### 改造 package.json 的 scripts 部分

就是可以放一些常用的命令行脚本，比如我们可以把我们经常要用的 webpack 命令放到这里来。

我把它改了一下，变成类似下面这样：

```javascript
{
  "name": "hello-wepback",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "dev": "webpack -d --watch",
    "prod": "webpack -p"
  },
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "webpack": "^3.8.1"
  }
}
```

改动的内容主要是增加了下面几行：

```javascript
 "scripts": {
    "dev": "webpack -d --watch",
    "prod": "webpack -p"
  },
```

怎么用呢？

很简单，分别是

```javascript
npm run dev 
```

和

```javascript
npm run prod 
```

------

因为 index.html 文件太死了，连 js 文件都写死了，有时候引用的 js 文件是动态变化的呢？

打个比方，类似下面这种例子：

而且还不确定有多少个。

还有一种情况，有时候为了更好的 cache 处理，文件名还带着 hash，例如下面这样：

```javascript
main.9046fe2bf8166cbe16d7.js
```

这个 hash 是文件的 md5 值，随着文件的内容而变化，你总不能每变化一次，就改一下 index.html 文件吧？

效率太低！

下面我们要使用一个 webpack 的插件 [html-webpack-plugin](https://github.com/jantimon/html-webpack-plugin)  来更好的处理这个问题。

####  html-webpack-plugin

```javascript
cnpm install html-webpack-plugin --save-dev
var HtmlWebpackPlugin = require('html-webpack-plugin');
```

webpack.config.js 文件改一下：

```javascript
module.exports = {
  entry: './src/app.js',
  output: {
    path: __dirname + '/dist',
    filename: 'app.bundle.js'
  },
  plugins: [new HtmlWebpackPlugin()]
};
```

最后，运行一下上文所说的 npm run dev 命令，你会发现在 dist 目录生成了 index.html 文件

要改变 title 很简单，上文提到 HtmlWebpackPlugin 这个方法可以传入很多参数的，下面这样就可以解决这个问题。

```javascript
var HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {
  entry: './src/app.js',
  output: {
    path: __dirname + '/dist',
    filename: 'app.bundle.js'
  },
  plugins: [new HtmlWebpackPlugin({
    title: "hello world"
  })]
};
```

配置文件修改了，配置文件是不会自动构建的，要重新运行 npm run dev

#### 制作一个新模板

新建 src/index.html 文件

把 webpack.config.js 更改如下：

```javascript
var HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {
  entry: './src/app.js',
  output: {
    path: __dirname + '/dist',
    filename: 'app.bundle.js'
  },
  plugins: [new HtmlWebpackPlugin({
    template: './src/index.html',
  })]
};
```

------

loader 用于对模块的源代码进行转换。loader 可以使你在 import 或"加载"模块时预处理文件。因此，loader 类似于其他构建工具中“任务(task)”，并提供了处理前端构建步骤的强大方法。loader 可以将文件从不同的语言（如 TypeScript）转换为 JavaScript，或将内联图像转换为 data URL。loader 甚至允许你直接在 JavaScript 模块中 import CSS文件！

说白了，就是 loader 类似于 task，能够处理文件，比如把 Scss 转成 CSS，TypeScript 转成 JavaScript 等。

再不明白的话，还是用实例来说明吧。（其实它的概念并不重要，你会用就行）

#### 用 css-loader 和 style-loader 处理 CSS

```javascript
cnpm install --save-dev css-loader style-loader
var HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {
  entry: './src/app.js',
  output: {
    path: __dirname + '/dist',
    filename: 'app.bundle.js'
  },
  plugins: [new HtmlWebpackPlugin({
    template: './src/index.html',
    filename: 'index.html',
    minify: {
      collapseWhitespace: true,
    },
    hash: true,
  })],
  module: {
    rules: [
      {
        test: /\.css$/,
        use: [ 'style-loader', 'css-loader' ]
      }
    ]
  }
};
```

#### 用 sass-loader 把 SASS 编译成 CSS

```javascript
cnpm install sass-loader node-sass --save-dev
var HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {
  entry: './src/app.js',
  output: {
    path: __dirname + '/dist',
    filename: 'app.bundle.js'
  },
  plugins: [new HtmlWebpackPlugin({
    template: './src/index.html',
    filename: 'index.html',
    minify: {
      collapseWhitespace: true,
    },
    hash: true,
  })],
  module: {
    rules: [
      {
        test: /\.scss$/,
        use: [ 'style-loader', 'css-loader', 'sass-loader' ]
      }
    ]
  }
};
```

#### 用 extract-text-webpack-plugin 把 CSS 分离成文件

```javascript
cnpm install --save-dev extract-text-webpack-plugin 
var HtmlWebpackPlugin = require('html-webpack-plugin');
const ExtractTextPlugin = require('extract-text-webpack-plugin');

module.exports = {
  entry: './src/app.js',
  output: {
    path: __dirname + '/dist',
    filename: 'app.bundle.js'
  },
  plugins: [new HtmlWebpackPlugin({
      template: './src/index.html',
      filename: 'index.html',
      minify: {
        collapseWhitespace: true,
      },
      hash: true,
    }),
    new ExtractTextPlugin('style.css')
  ],
  module: {
    rules: [
      {
        test: /\.scss$/,
        use: ExtractTextPlugin.extract({
          fallback: 'style-loader',
          //resolve-url-loader may be chained before sass-loader if necessary
          use: ['css-loader', 'sass-loader']
        })
      }
    ]
  }
};
```

### webpack-dev-server

```javascript
// 先全局安装 
npm install -g webpack-dev-server
npm install --save-dev webpack-dev-server

// 安装@2.11.1版本的
```

### 配置 react 开发环境（babel）

#### 1. 安装 react

要使用 react，就必须装下面两个包的。

```javascript
npm install --save react react-dom
```

#### 2. 建立 babel

可能你不懂 babel 是什么，你可以把它理解为编译器，它能把 react 代码转成一般浏览器可读可执行的代码，通常可以用它来转化 react 或 vue 这样的前端代码，或者把 es6 代码转成普通的 javascript 代码等等。

如果还不理解的话，可以看我这篇文章 [babel 入门指南](https://www.rails365.net/articles/babel-ru-men-zhi-nan)。

要让 babel 很好的转化 react 代码，首先要安装好 babel，再装 babel 转化 react 的包。

运行下面的命令。

```javascript
npm install --save-dev babel-core babel-preset-react babel-preset-env
```

创建 .babelrc 文件。

```javascript
{
  "presets": ["env", "react"]
}
```

#### 3. 在 webpack 使用 babel-loader

最后我们需要在 webpack 中使用一个 loader 来转化 react 的代码。

首先，安装。

```javascript
npm install --save-dev babel-loader
```

**webpack.config.js**

```javascript
var HtmlWebpackPlugin = require('html-webpack-plugin');
const ExtractTextPlugin = require('extract-text-webpack-plugin');

module.exports = {
  entry: './src/app.js',
  ...
  module: {
    rules: [
      {
        test: /\.scss$/,
        use: ExtractTextPlugin.extract({
          fallback: 'style-loader',
          //resolve-url-loader may be chained before sass-loader if necessary
          use: ['css-loader', 'sass-loader']
        })
      },
      // 这两行是处理 react 相关的内容
      { test: /\.js$/, loader: 'babel-loader', exclude: /node_modules/ },
      { test: /\.jsx$/, loader: 'babel-loader', exclude: /node_modules/ }
    ]
  }
};
```

**4. 写 react 组件**

**src/index.html**

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Hello World</title>
</head>
<body>
  <div id="root"></div>
</body>
</html>
```

**src/app.js**

```javascript
import css from './app.scss';

import React from 'react';
import ReactDOM from 'react-dom';
import Root from './Root';

ReactDOM.render(
  <Root></Root>,
  document.getElementById('root')
);
```

**src/Root.js**

```javascript
import React from 'react';

export default class Root extends React.Component {
  render() {
    return (
      <div style={{textAlign: 'center'}}>
        <h1>Hello World</h1>
      </div>);
  }
};
```

手动创建.babelrc文件时，报以下错误，创建失败：

![img](https://cdn.nlark.com/yuque/0/2021/png/5378426/1626407672490-e7c25db5-8e5b-4d49-9ede-c3ff38e8d543.png)

创建.babelrc文件命令：

```javascript
echo >.babelrc 
```

### clean-webpack-plugin 清除文件

一般这个插件是配合 webpack -p 这条命令来使用，就是说在为生产环境编译文件的时候，先把 build或dist (就是放生产环境用的文件) 目录里的文件先清除干净，再生成新的。

把 src/app.js 改改内容，然后再执行 npm run prod。

再多运行几次，生成的带 hash 的 app.bundle.js 文件就会很多。

```javascript
dist
├── app.bundle.0e380cea371d050137cd.js
├── app.bundle.259c34c1603489ef3572.js
├── app.bundle.e56abf8d6e5742c78c4b.js
├── index.html
└── style.css
```

这些带 hash 的 app.bundle.js 只有最新的才有用，其他的都没用，我们要在 build 之前把它们全清空，这真是 clean-webpack-plugin 发挥的作用。

#### 使用 clean-webpack-plugin

```javascript
cnpm i clean-webpack-plugin --save-dev
```

**webpack.config.js：**

```javascript
const path = require('path')
...
const CleanWebpackPlugin = require('clean-webpack-plugin');

let pathsToClean = [
  'dist',
]

module.exports = {
  entry: {
    "app.bundle": './src/app.js'
  },
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: '[name].[chunkhash].js'
  },
  ...
  plugins: [
    new CleanWebpackPlugin(pathsToClean),
    ...
    new ExtractTextPlugin('style.css')
  ],
  ...
};
```

重新运行npm run prod

会删除dist这个目录，然后重新再生成一个。

![img](https://cdn.nlark.com/yuque/0/2021/png/5378426/1626407672515-a1a87d46-d623-4cfa-8668-3d06f270ec59.png)

### 配置多个 HTML 文件

有个问题，**contact.html 使用的 js 和 css 跟 index.html 是一模一样的**

如果我要让 contact.html 使用跟 index.html 不同的 js，如何做呢？（只要保证 js 不同，css 也会不同的，因为 css 也是由 js 里 import 的嘛)

```javascript
module.exports = {
  entry: {
    "app.bundle": './src/app.js',
    // 这行是新增的。
    "contact": './src/contact.js'
  },
  ...
  plugins: [
    new CleanWebpackPlugin(pathsToClean),
    new HtmlWebpackPlugin({
      template: './src/index.html',
      filename: 'index.html',
      minify: {
        collapseWhitespace: true,
      },
      hash: true,
      // 这行是新增的。
      excludeChunks: ['contact']
    }),
    new HtmlWebpackPlugin({
      template: './src/contact.html',
      filename: 'contact.html',
      minify: {
        collapseWhitespace: true,
      },
      hash: true,
      // 这行是新增的。
      chunks: ['contact']
    }),
    new ExtractTextPlugin('style.css')
  ],
  ...
};
```

上面的 excludeChunks 指的是不包含， chunks 代表的是包含。

**src/contact.js**

```javascript
console.log('hi from contact js')
```

**生产环境和开发环境： 【修改package.json文件】**

分别是开发环境使用的 npm run dev 命令和生产环境使用的 npm run prod 命令。

我们把它改成下面这样：

```javascript
"scripts": {
  "dev": "webpack-dev-server",
  "prod": "NODE_ENV=production webpack -p"
},
```

**【window环境，需要加set 和 &】**

![img](https://cdn.nlark.com/yuque/0/2021/png/5378426/1626407672454-5d1aa245-88fb-4fc9-ac80-5310bc090380.png)

### Bootstrap 框架

![img](https://cdn.nlark.com/yuque/0/2021/png/5378426/1626407672698-8f1e9d77-8ee9-4aec-95d7-5a2762257594.png)

还要装bootstrap-sass 

```javascript
cnpm bootstrap-sass@3.3.7 --save-dev
```

#### webpack.config.js

```
const webpack = require('webpack');
const config = {
  entry: './src/js/app.js',
  output: {
    path: __dirname + '/dist',
    filename: 'bundle.js'
  },
  module:{
    rules: [
      {
        test: /\.js$/,
        exclude: /node_modules/,
        use: [ 'babel-loader' ]
      },
      {
        test: /\.css$/,
        use: [ 'style-loader', 'css-loader' ]
      }
    ]
  }
}

module.exports = config;
```

```
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');
const { CleanWebpackPlugin } = require('clean-webpack-plugin');

module.exports = {
    // entry: './src/index.js',
    entry: {
        app: './src/index.js',
        print: './src/print.js',
    },
    devtool: 'inline-source-map',
    devServer: {
        contentBase: './dist'
    },
    plugins: [
        new CleanWebpackPlugin(),
        new HtmlWebpackPlugin({
            title: 'Out Management'
        })
    ],
    output: {
        // filename: 'bundle.js',
        filename: '[name].bundle.js',
        path: path.resolve(__dirname, 'dist')
    },
};
```



### webpack-app

```plain
│  .babelrc
│  .bootstraprc
│  package.json
│  webpack.bootstrap.config.js
│  webpack.common.js
│  webpack.config.js
│  webpack.config.js.bak
│  webpack.dev.js
│  webpack.prod.js
│
|——node_modules
|
├─dist
│  │  app.bundle.23080236a288b553e71f.js
│  │  app.bundle.e107dfebe8e36080c12b86a23bcd7955.css
│  │  bootstrap.2f405ecd1f1909206470.js
│  │  bootstrap.55cebd1d76656dacbe76ac17ea3f37bf.css 
│  │  contact.c35a6e89d395e9e9d252.js
│  │  contact.html
│  │  index.html
│  │
│  ├─fonts
│  │      glyphicons-halflings-regular.eot
│  │      glyphicons-halflings-regular.ttf
│  │      glyphicons-halflings-regular.woff
│  │      glyphicons-halflings-regular.woff2
│  │
│  └─images
│          glyphicons-halflings-regular.svg
│          money-bag.svg
│
└─src
    │  app.css
    │  app.js
    │  app.scss
    │  app2.js
    │  contact.html
    │  contact.js
    │  index.html
    │  index.pug
    │  jquery.changeStyle.js
    │  Root.js
    │
    ├─images
    │      logo.png
    │      money-bag.svg
    │      true.jpg
    │
    └─includes
            header.pug
```

### webpack.prod.js

```plain
const merge = require('webpack-merge');
const common = require('./webpack.common.js');
const bootstrapEntryPoints = require('./webpack.bootstrap.config')
const webpack = require('webpack');

module.exports = merge(common, {
  entry: {
    "app.bundle": './src/app.js',
    "contact": './src/contact.js',
    "bootstrap": bootstrapEntryPoints.prod
  },
  plugins: [
    new webpack.DefinePlugin({
      'process.env': {
        'NODE_ENV': JSON.stringify('production')
      }
    })
  ]
});
```

### webpack.dev.js

```plain
const merge = require('webpack-merge');
const common = require('./webpack.common.js');
const bootstrapEntryPoints = require('./webpack.bootstrap.config')

module.exports = merge(common, {
  entry: {
    "app.bundle": './src/app.js',
    "contact": './src/contact.js',
    "bootstrap": bootstrapEntryPoints.dev
  },
  devtool: 'inline-source-map',
  devServer: {
    contentBase: './dist',
    inline: true,
    port: 9000,
    open: true,
  }
});
```

### webpack.config.js

```plain
const webpack = require('webpack');
const bootstrapEntryPoints = require('./webpack.bootstrap.config')
var HtmlWebpackPlugin = require('html-webpack-plugin');
const ExtractTextPlugin = require('extract-text-webpack-plugin');
const path = require('path');
const CleanWebpackPlugin = require('clean-webpack-plugin');
var isProd = process.env.NODE_ENV === 'production'; // true or false

var bootstrapConfig = isProd ? bootstrapEntryPoints.prod : bootstrapEntryPoints.dev;

var cssDev = ['style-loader', 'css-loader?sourceMap', 'sass-loader?sourceMap'];
var cssProd = ExtractTextPlugin.extract({
  fallback: 'style-loader',
  //resolve-url-loader may be chained before sass-loader if necessary
  use: ['css-loader', 'sass-loader']
})

var cssConfig = isProd ? cssProd : cssDev;

let pathsToClean = [
  'dist',
]
module.exports = {
  devtool: 'source-map',
  entry: {
    "app.bundle": './src/app2.js',
    // 这行是新增的。
    "contact": './src/contact.js',
    "bootstrap": bootstrapConfig
  },
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: '[name].[hash].js'
  },
  devServer: {
    port: 9000,
    open: true,
    hot: true
  },
  plugins: [new CleanWebpackPlugin(pathsToClean),
    new HtmlWebpackPlugin({
      template: './src/index.html',
      filename: 'index.html',
      minify: {
        collapseWhitespace: true,
      },
      hash: true,
      // 这行是新增的。
      excludeChunks: ['contact']
    }),
    new HtmlWebpackPlugin({
      template: './src/contact.html',
      filename: 'contact.html',
      minify: {
        collapseWhitespace: true,
      },
      hash: true,
      // 这行是新增的。
      chunks: ['contact']
    }),
    // css 文件放到 css 目录中
    new ExtractTextPlugin({
      filename: '[name].css',
      disable: !isProd,
      publicPath: 'css/'
    }),
    // 这两行是新增的
    new webpack.NamedModulesPlugin(),
    new webpack.HotModuleReplacementPlugin(),
    new webpack.ProvidePlugin({
      $: 'jquery',
      jQuery: 'jquery'
    }),
  ],
  module: {
    rules: [
      {
        test: /\.scss$/,
        use: cssConfig
      },
      // 这两行是处理 react 相关的内容
      { test: /\.js$/, loader: 'babel-loader', exclude: /node_modules/ },
      { test: /\.jsx$/, loader: 'babel-loader', exclude: /node_modules/ },
      { test: /\.pug$/, loader: ['raw-loader', 'pug-html-loader'] },
      { test: /\.(gif|png|jpe?g|svg)$/i,
        use: [
          {
            loader: 'file-loader',
            options: {
              name: '[name].[ext]',
              outputPath: 'images/'
            }
          },
          {
            loader: 'image-webpack-loader',
            options: {
              bypassOnDebug: true,
            }
          }
        ]
      },
      // 下面几行才是 html-loader 的配置内容
      {
        test: /\.html$/,
        use: [ {
          loader: 'html-loader',
          options: {
            minimize: true
          }
        }],
      },
      
      { test:/bootstrap-sass[\/\\]assets[\/\\]javascripts[\/\\]/, loader: 'imports-loader?jQuery=jquery' },
      // 字体文件都放到 fonts 目录中
      { test: /\.(woff2?|svg)$/, loader: 'url-loader?limit=10000&name=[name].[ext]&outputPath=fonts/' },
      { test: /\.(ttf|eot)$/, loader: 'file-loader?name=[name].[ext]&outputPath=fonts/' },
    ]
  }
};
```

### webpack.common.js

```plain
const path = require('path')
const HtmlWebpackPlugin = require('html-webpack-plugin');
const ExtractTextPlugin = require('extract-text-webpack-plugin');
const CleanWebpackPlugin = require('clean-webpack-plugin');
const webpack = require('webpack');

module.exports = {
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: '[name].[chunkhash].js'
  },
  plugins: [
    new webpack.ProvidePlugin({
      $: 'jquery',
      jQuery: 'jquery'
    }),
    new CleanWebpackPlugin(['dist']),
    new HtmlWebpackPlugin({
      template: './src/index.html',
      filename: 'index.html',
      minify: false,
      hash: process.env.NODE_ENV === 'production',
      excludeChunks: ['contact']
    }),
    new HtmlWebpackPlugin({
      template: './src/contact.html',
      filename: 'contact.html',
      minify: false,
      hash: process.env.NODE_ENV === 'production',
      chunks: ['contact']
    }),
    new ExtractTextPlugin({
      filename: '[name].[contenthash].css',
      disable: false,
    }),
  ],
  module: {
    rules: [
      {
        test: /\.scss$/,
        use: ExtractTextPlugin.extract({
          fallback: 'style-loader',
          use: ['css-loader?sourceMap', 'sass-loader?sourceMap']
        })
      },
      { test: /\.js$/, loader: 'babel-loader', exclude: /node_modules/ },
      { test: /\.jsx$/, loader: 'babel-loader', exclude: /node_modules/ },
      { test: /\.pug$/, loader: ['raw-loader', 'pug-html-loader'] },
      {
        test: /\.(gif|png|jpe?g|svg)$/i,
        use: [
          {
            loader: 'file-loader',
            options: {
              name: '[name].[ext]',
              outputPath: 'images/'
            }
          },
          {
            loader: 'image-webpack-loader',
            options: {
              bypassOnDebug: true,
            }
          }
        ]
      },
      {
        test: /\.html$/,
        use: [{
          loader: 'html-loader',
        }]
      },
      { test: /\.woff2?$/, loader: 'url-loader?limit=10000&name=[name].[ext]&outputPath=fonts/' },
      { test: /\.(ttf|eot)$/, loader: 'file-loader?name=[name].[ext]&outputPath=fonts/' },
      { test:/bootstrap-sass[\/\\]assets[\/\\]javascripts[\/\\]/, loader: 'imports-loader?jQuery=jquery' },
    ]
  }
};
```

### webpack.bootstrap.config.js

```plain
const fs = require('fs');

function getBootstraprcCustomLocation() {
  return process.env.BOOTSTRAPRC_LOCATION;
}

const bootstraprcCustomLocation = getBootstraprcCustomLocation();

let defaultBootstraprcFileExists;

try {
  fs.statSync('./.bootstraprc');
  defaultBootstraprcFileExists = true;
} catch (e) {
  defaultBootstraprcFileExists = false;
}

if (!bootstraprcCustomLocation && !defaultBootstraprcFileExists) {
  /* eslint no-console: 0 */
  console.log('You did not specify a \'bootstraprc-location\' ' +
    'arg or a ./.bootstraprc file in the root.');
  console.log('Using the bootstrap-loader default configuration.');
}

// DEV and PROD have slightly different configurations
let bootstrapDevEntryPoint;
if (bootstraprcCustomLocation) {
  bootstrapDevEntryPoint = 'bootstrap-loader/lib/bootstrap.loader?' +
    `configFilePath=${__dirname}/${bootstraprcCustomLocation}` +
    '!bootstrap-loader/no-op.js';
} else {
  bootstrapDevEntryPoint = 'bootstrap-loader';
}

let bootstrapProdEntryPoint;
if (bootstraprcCustomLocation) {
  bootstrapProdEntryPoint = 'bootstrap-loader/lib/bootstrap.loader?extractStyles' +
    `&configFilePath=${__dirname}/${bootstraprcCustomLocation}` +
    '!bootstrap-loader/no-op.js';
} else {
  bootstrapProdEntryPoint = 'bootstrap-loader/extractStyles';
}

module.exports = {
  dev: bootstrapDevEntryPoint,
  prod: bootstrapProdEntryPoint,
};
```

### .babelrc

```plain
{
  "presets": ["env", "react"]
}
```
