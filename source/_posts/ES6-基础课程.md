---
title: ES6-基础课程
date: 2019-07-10 15:13:45
tags:
- ES6
categories: 
- 工作笔记
- ES6
---
腾讯课堂学习笔记

## ES6·历史

> 1990年底，欧洲核能研究组织(CERN) 科学家Tim Berners-Lee，在全世界最大的电脑网络——互联网的基础上，发明了万维网(World Wide Web)
>
> 1992年底，美国国家超级电脑应用中心(NCSA) 开始开发一个独立的浏览器， 叫做Mosaic。 这是人类历史上第一个浏览器，从此网页可以在图形界面的窗口浏览。
>
> 
>
> 1994年10月，NCSA的一个主要程序员Marc Andreessen联合风险投资家Jim Clark，成立了Mosaic通信公司(Mosaic Communications)，不久后改名为Netscape。这家公司的方向，就是在Mosaic的基础上，开发面向普通用户的新一 代的浏览器Netscape Navigator。
>
> 1994年12月，Navigator发布 了1.0版，市场份额一举超过90%。
>
> 
>
> 1995年
> Netscape公司雇佣了程序员Brendan Eich开发这种网页脚本语言。Brendan Eich只用了10天，就设计完成了这种语言的第一版。
> 基本语法：借鉴C语言和Java语言。
> 数据结构：借鉴Java语言， 包括将值分成原始值和对象两大类。
> 函数的用法：将函数当作第一等公民，并引入闭包。
> 原型继承模型：借鉴Self语 言。
> 正则表达式：借鉴Perl语言 。
> 字符串和数组处理：借鉴Python语言.
>
> Netscape公司的这种浏览器脚本语言，最初名字叫做Mocha, 1995年9月 改为LiveScript。12月，Netscape公 司与Sun公司(Java语 言的发明者和所有者)达成协议，后者允许将这种语言叫做JavaScript。这样一来， Netscape公 司可以借助Java语言的声势，而Sun公司则将自己的影响力扩展到了浏览器。
>
> 为了保持简单，这种脚本语言缺少一些关键的功能，比如块级作用域、模块、子类型(subtyping) 等等，但是可以利用现有功能找出解决办法。这种功能的不足，对于其他语言，你需要学习语言的各种功能，JavaScript,你需要学习各种解决问题的模式。而且由于来源多样，从一开始就注定，JavaScript的编程 风格是函数式编程和面向对象编程的一种混合体。





- 1996年3月， Navigator 2.0浏览器正式内置了JavaScript脚本语言。

- 1996年8月，微软模仿JavaScript开发了一种相近的语言，取名为JScript (JavaScript是Netscape的注册商标，微软不能用)，首先内置于IE 3.0。网景公司面临丧失浏览器脚本语言的主导权的局面。

- 1996年11月，网景公司决定将JavaScript提交给国际标准化组织ECMA，希望JavaScript能够成为国际标准，以此抵抗微软。

- 1997年7月，ECMA组织发布262号标准文件(ECMA-262) 的第一版，规定了浏览器脚本语
  言的标准，并将这种语言称为ECMAScript。这个版本就是ECMAScript 1.0版。

- 1998年6月， ECMAScript 2.0版发布。

- 1999年12月，ECMAScript 3.0版发布，成为JavaScript的通行标准， 得到了广泛支持。

- 2007年10月， ECMAScript 4.0版草案发布，被各大厂商抵制，和谐了

- 2009年12月，ECMAScript 5.0版正式发布。

- 2011年6月， ECMAscript 5.1版发布，并且成为IOS国际标准（IOS/IEC 16262：2011）。

- 2013年12月， ECMAScript 6草案发布。然后是12个月的讨论期，听取各方反馈。

- 2014年12月，ECMAScript6发布正式版本

- 浏览器支持情况：http://kangax.github.io/compat-table/es6/

  

{% link 查看浏览器支持ES6的情况 http://kangax.github.io/compat-table/es6/ %}

#### 编译ES6

例如，文件目录如下：
```bash
- code 
-- dist
-- src
--- index.js
--- index.html
```
将src里使用es6写的index.js编译成es5的js文件，放置到dist目录中。

(因为本机使用npm安装gulp有问题，所以改为使用cnpm安装)

#### [检查浏览器对ES6的支持情况](http://ruanyf.github.io/es-checker/index.cn.html)

##### 0、使用淘宝镜像安装
{% link 使用淘宝镜像安装 https://www.xiaochao.me/seo/118.html %}
```bash
npm install -g cnpm --registry=https://registry.npm.taobao.org
```
##### 1、项目初始化
```bash
cnpm init -y
```
##### 2、全局安装babel-cli
```bash
cnpm install -g babel-cli
```
##### 3、安装将代码转为ESCMA script 的模块（安装转换包）
```bash
cnpm install --save-dev babel-preset-es2015 babel-cli
```
##### 4、新建.babelrc文件
```bash
1)在当前项目目录下创建：
cd.>.babelrc

2).babelrc文件内容：
{
    "presets": [
        "es2015",
    ],
    "plugins": []
}
```
编译前的src/index.js ：
```bash
let a  = 3;
console.log(a);
```
##### 5、编译
```bash
babel src/index.js -o dist/index.js
```
编译后的dist/index.js：
```bash
"use strict";

var a = 3;
console.log(a);
```
##### 6、命令的简化方式
1) 修改package.json文件
```bash
"scripts": {
    "build": "babel src/index.js -o dist/index.js"
}
```
2) 在命令行中 输入下面的简化命令来代替 babel src/index.js -o dist/index.js
```bash
cnpm run build
```



#### gulp

{% link Gulp中文网 https://www.gulpjs.com.cn/ %}
##### 安装gulp
```bash
cnpm install gulp --save-dev
```
(这里安装后是gulp4,因为gulp4和gulp3的执行有差别，这里安装3.9.1版本的，暂不对gulp4做学习处理，这里主要学习es6)
##### 安装browser-sync
```bash
cnpm install browser-sync --save-dev
```
##### 安装gulp-babel
```bash
cnpm install gulp-babel --save-dev
```
##### 新建gulpfile.js
```bash
var gulp        = require("gulp")
var browserSync = require("browser-sync").create()
var babel       = require("gulp-babel")
//修改完之后，刷新页面
var reload       = browserSync.reload

gulp.task('change', function(){
    gulp.src('./src/index.js')
        .pipe(babel({
            presets:['es2015']
        }))
        .pipe(gulp.dest('./dist/'))
        .pipe(reload({stream:true}))
})

gulp.task("default", function() {
    browserSync.init({
        server:{
            baseDir: './'
        },
        port:'8089'
    });
    gulp.watch('src/*.js',['js'])
})
```
参考 {% link 简单利用gulp-babel搭建es6转es5环境 https://www.cnblogs.com/liangcheng11/p/6909387.html%}

gulpfile.js:
```bash
var gulp = require('gulp'),
    $ = require('gulp-load-plugins')();
 
var app = {
    srcPath: 'src/',
    devPath: 'dist/'
};
 
gulp.task('js',function(){
    return gulp.src(app.srcPath + '/*.js',{base:app.srcPath})
        .pipe($.plumber())
        .pipe($.babel({
            　presets: ['es2015']
        }))
        .pipe(gulp.dest(app.devPath));
});
gulp.task('html',function(){
    return gulp.src(app.srcPath + '/*.html',{base:app.srcPath})
        .pipe(gulp.dest(app.devPath));
});
 
gulp.task('clean',function(){
    return gulp.src(app.devPath)
        .pipe($.clean());
});
 
//浏览器同步
gulp.task('webserve',function(){
    return gulp.src(app.devPath)
        .pipe($.webserver({
            livereload: true, //开启gulp-livereload
            open: true,
            port: 2333 //浏览器端口
        }));
});
 
// 监听
gulp.task('watch',function(){
    gulp.watch(app.srcPath + '/*.js', ['js']);
    gulp.watch(app.srcPath + '**/*.html', ['html']);
});

gulp.task('build',['js', 'html']);

//定义gulp默认任务
gulp.task('default',['build','watch'], function () {
    return gulp.src(app.devPath)
        .pipe($.webserver({
            livereload: true, //开启gulp-livereload
            open: true,
            port: 2333 //浏览器端口
        }));
});
```
#### 利用转码器让ES6在浏览器运行(不推荐)
###### Traceur转码器
Google公司的Traceur转码器，可以将ES6代码转为ES5代码。这意味着，你可以用ES6的方式编写程序，又不用担心浏览器是否支持。
它有多种使用方式。
###### 直接插入网页
Traceur允许将ES6代码直接插入网页。
首先，必须在网页头部加载Traceur库文件。
{% link 利用转码器让ES6在浏览器运行 https://blog.gaoqixhb.com/p/55783789cef7e0a008d5d6ef%}



> 低版本的浏览器对es6的兼容性不太好，所以需要把es6编译成es5

#### 实时监听代码

安装 live-server，在控制台输入live-server运行代码

```
npm install –g live-server
```

