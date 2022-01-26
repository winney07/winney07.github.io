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

{% asset_img 1.png %}
<!--more-->
{% asset_img 2.png %}
{% asset_img 3.png %}
{% asset_img 4.png %}
{% asset_img 5.png %}

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

