---
title: gulp学习笔记
date: 2019-07-11 11:50:39
tags:
- Gulp
categories: 
- 工作笔记
- Gulp
---
[前端自动化构建工具 Gulp 视频教程](https://www.bilibili.com/video/av64407974?from=search&seid=17812780048673997573)

[旧版官网](https://v3.gulpjs.com.cn)   |  [旧版API](https://v3.gulpjs.com.cn/docs/api/)   |  [新版官网](https://www.gulpjs.com.cn/docs/getting-started/quick-start/)     |    [新版API](https://www.gulpjs.com.cn/docs/api/concepts/)

{% link Gulp中文网 https://www.gulpjs.com.cn/%}

{% link Gulp https://gulpjs.com/%}
{% link Gulp插件 https://gulpjs.com/plugins/%}
gulp是与grunt功能类似的<b>**前端项目构建**</b>，工具，也是基于nodejs的自动<b>任务运行器</b>
能自动化地完成JavaScript/coffee/sass/less/html/image/css等文件的合并、压缩、检查、监听文件变化、浏览器自动刷新、测试等任务。
gulp更高效（异步多任务）、更易于使用，插件高质量
特点：
1、任务化
2、基于流（数据流，输入流I 输出流O）
<!--more-->

```bash
|- dist 
|- src
    |- js
    |- css
    |- less
|- index.html
|- gulpfile.js
|- package.json

```
使用淘宝镜像
```bash
npm install -g cnpm --registry=https://registry.npm.taobao.org
```
- 脚手架工具：套用代码（模板代码）

- 依赖管理工具：依赖代码（库、依赖）

- 构建工具：预处理代码（自己写的JavaScript，CSS，HTML）  检查代码、编译、打包

- 构建工具的配置一般保存在构建配置文件（build file）里

用脚手架工具yemoman搭建项目，用依赖管理工具bower来搜索、安装依赖，用构建工具gulp来处理文件。Yemoman作为一个脚手架工具，可以初始化gulp(构建配置文件)和bower（项目基本的依赖）。Gulp还可以使用bower所提供的信息把依赖添加到项目的主要文件中。

- JavaScript引擎，提供了编译和运行JavaScript的环境

脚手架工具的作用是搭建项目，让项目顺利跑起来。脚手架工具可以创建一个项目必需的目录，并且初始文件（比如构建代码）、模板代码复制过去，最后安装依赖。在整个开发过程中，脚手架工具的定位是创建项目的基础架构。

Generator是可以被命令行工具yo执行的JavaScript应用，它所做的事情只不过是创建新目录和复制文件。不过，它也没有那么简单。它还可监听参数来修改文件。

- Yeoman的唯一任务就是运行generator。

依赖是独立完整的模块，它是一个应用的一部分或者扩展。依赖可以是像jQuery或angular这样的库，可以是一些UI组件，也可以是像bootstrap这样完整的UI框架。依赖的另一种叫法是包。使用依赖或者包的好处在于：你不用花时间去开发那些已经有的功能，只要用现成的就行了。

依赖管理工具的主要功能是在社区和公司的仓库中搜索依赖，并且下载到本地的项目中。

只要一个模块是由Git托管的，并且拥有bower.json文件，就可以用bower来安装。

有了bower，你就可以用工具来管理所有的第三方模块和组件了。

- Gulp流式构建系统

构建系统是整个工具链的核心。它会处理所有的源文件，把它们变成可部署的代码。它还可以 检查代码质量，自动执行重复的操作。

构建工具首先会读取一个构建配置（或者构建文件），然后定义三个东西：源文件、处理流程和输出文件的目录。源代码经过处理的流程后，最后会被输出到目录中。

用脚手架工具创建应用，用依赖管理工具下载需要的依赖，然后使用构建工具来执行代码编译工具。这三个工具都是基于Node.js的版本。Gulp是整个项目的核心，也是最主要的工具。

#### 全局安装gulp

```bash
cnpm i gulp -g
```
#### 局部安装gulp
```bash
cnpm i gulp --save-dev
```
#### 配置gulpfile.js


#### 使用gulp插件
##### 相关插件：
```bash
gulp-concat: 合并文件（js/css）
gulp-uglify：压缩js文件
gulp-rename：文件重命名
gulp-less：编译less
gulp-clean-css：压缩css
gulp-livereload：实时自动编译刷新
```

###重要API
##### gulp.src(filePath/pathArr)
指向指定路径的所有文件，返回文件流对象
用于读取文件

##### gulp.dest(dirPath/pathArr)
指向指定的所有文件夹

##### gulp.task(name, [deps], fn)
定义一个任务

##### gulp.watch()
监视文件的变化

### 处理js(合并/压缩js文件)
 创建js文件
   src/js/test1.js
   src/js/test2.js
##### 下载插件：
```bash
cnpm install gulp-concat gulp-uglify gulp-rename --save-dev
```
##### 配置编码
```bash
var concat = require('gulp-concat');
var uglify = require('gulp-uglify');
var rename = require('gulp-rename');
```

##### gulpfile.js
```bash
var gulp = require('gulp');
var concat = require('gulp-concat');
var uglify = require('gulp-uglify');
var rename = require('gulp-rename');

//注册任务
// gulp.task('任务名', function() {
//     //配置任务的操作
// })

//注册合并压缩js的任务
gulp.task('js', function() {
    //如果js目录（包括子目录）的所有js文件，需要加上/**/，
    //不加，只代表js目录下的所有js文件
    // gulp.src("src/js/**/*.js") 
    
    return gulp.src("src/js/*.js")             //找到目标原文件，将数据读取到gulp的内存中
               .pipe(concat('build.js'))       //临时合并文件
               .pipe(gulp.dest('dist/js/'))    // 临时输出文件到本地
               .pipe(uglify())                 //压缩文件
               .pipe(rename({suffix: '.min'}))  //重命名
               .pipe(gulp.dest('dist/js/'))     //输出压缩文件
});
// 如果执行每个人物都要gulp ***敲一次命令行，是不方便的，所以把任务放到默认任务里面
//注册默认任务
// gulp.task('default', ['js'])
```
![报错信息](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/gulp%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B0/1.png)
gulp4中创建的任务是一个异步的javascript函数——一个接受错误第一次回调或返回stream, promise, event emitter, child process, 或 observable观察的函数。
{% link gulp运行报错：Task function must be specified必须指定任务函数 http://www.xinran001.com/frontend/47.html %}


##### 执行任务
```bash
gulp js
```
在dist目录下生成  js文件夹和build.js和build.min.js

### 处理css
 创建css文件
   src/css/test1.css
   src/css/test2.css
   src/less/test3.less
 ##### 下载插件
 ```bash
 cnpm install gulp-less gulp-clean-css --save-dev
 ```
 ##### 配置编码
 var less = require('gulp-less');
 var cleanCSS = require('gulp-clean-css');
 ##### less处理任务
```bash
gulp.task('less', function() {
    return gulp.src("src/less/*.less")
               .pipe(less())            //编译less文件为css文件
               .pipe(gulp.dest('src/css/'))
});
```
##### 执行命令
```bash
gulp less
```
在src/css目录下生成test3.css文件（先将less编译为css文件，
放到src/css目录下，然后再跟其他css文件一起压缩处理等）
##### 合并压缩css文件
```bash
gulp.task('css', function() {
    return gulp.src("src/css/*.css")
               .pipe(concat('build.css'))
               .pipe(rename({suffix: '.min'}))
               .pipe(cssClean({compatibility: 'ie8'}))
               .pipe(gulp.dest('dist/css/'))
});
```
##### 执行命令
```bash
gulp css
```
在dist目录下生成css目录，css目录里面有文件build.min.css
##### 执行任务异步，任务之间解决依赖关系
使用gulp.task('default', ['js', 'less', 'css']);
报错：
![报错信息](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/gulp%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B0/2.png)
原因：
gulp.task 移除了三参数语法，现在不能使用数组来指定一个任务的依赖。gulp 4.0 加入了 gulp.series 和 gulp.parallel 来实现任务的串行化和并行化。
不要用Gulp3的方式指定依赖任务，你需要使用gulp.series和gulp.parallel，因为gulp任务现在只有两个参数。
```bash
gulp.series：按照顺序执行
gulp.paralle：可以并行计算
```
{% link 参考博客 https://www.jianshu.com/p/c30ff8592421%}
存在异步问题：
```bash
gulp.task('default', gulp.parallel('js', 'less', 'css', function () {
    // Build the website.
}));
```
报错：
![报错信息](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/gulp%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B0/3.png)
{% link 参考gulp4 Sample gulpfile.js https://www.npmjs.com/package/gulp4%}
最终将任务改为：
```bash
var build = gulp.series(gulp.parallel('js', 'less', 'css'));
gulp.task('default', build);
```
将已生成的dist目录删除，执行任务
```bash
gulp 
```
![运行gulp](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/gulp%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B0/4.png)
在目录中生成dist目录，里面有这3个任务生成的文件。
注：如果gulp任务中，去掉return，也可以完成任务，但是任务变成同步执行。
return能保证任务是异步执行的，在任务执行完成后，会在gulp中释放掉。效率高

less执行的任务比较多，也许less还没执行完，就执行到css任务了。
![less还没执行完，就执行到css任务](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/gulp%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B0/5.png)
所以要保证执行css任务时，less任务已经执行完了。（添加一个任务数组参数）
3.0**这样写：
```bash
gulp.task('css', ['less'], function() {
    return gulp.src("src/css/*.css")
               .pipe(concat('build.css'))
               .pipe(rename({suffix: '.min'}))
               .pipe(cssClean({compatibility: 'ie8'}))
               .pipe(gulp.dest('dist/css/'))
});
```
4.0**这样写：
```bash
var build = gulp.series('less', gulp.parallel('js', 'css', 'html'));
gulp.task('default', build);
```
结果：（css任务在less任务完成之后再执行）
![css任务在less任务完成之后再执行](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/gulp%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B0/6.png)
### 压缩html
```bash
cnpm install gulp-htmlmin --save-dev
```
##### 配置编码
```bash
var htmlMin = require('gulp-htmlmin');
```
##### 压缩html任务
```bash
gulp.task('html', function() {
    return gulp.src('index.html')
               .pipe(htmlMin({collapseWhitespace: true}))
               .pipe(gulp.dest('dist/'))
})
```
src/index.html:
![运行结果](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/gulp%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B0/7.png)
压缩之后dist/index.html:
![运行结果](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/gulp%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B0/8.png)
原因：
原html文件引入的css文件路径不对：
```bash
<link rel="stylesheet" href="dist/css/build.min.css">
```
改为：
```bash
<link rel="stylesheet" href="css/build.min.css">
```
#### 半自动进行项目构建（把gulp的版本换为3.9.1，4.0以上版本处理起来不熟练）
##### 下载插件
```bash
cnpm install gulp-livereload --save-dev
```
##### 配置编码
```bash
var livereload = require('gulp-livereload');

//所有需要实时监听的任务，后面加上：
.pipe(livereload())  

```
```bash
gulp.task('watch',['default'], function() {
    //开启监听
    livereload.listen();

    //确认监听的目标以及绑定相应的任务
    gulp.watch('src/js/*.js', ['js']);
    gulp.watch(['src/css/*.css', 'src/less/*.less'], ['css']);
    gulp.watch('*.html',  ['html']);
})
```
执行任务
```bash
gulp watch 
```
当src里面的文件有修改时，直接手动刷新浏览器，则可以看到变化，不需要再输入一次执行任务的命令
### 全自动进行项目构建
#### 热加载（实时加载）
##### 下载插件：gulp-connect
```bash
cnpm install gulp-connect --save-dev
```
##### 配置编码
```bash
var connect = require('gulp-connect');

gulp.task('server', ['default'],function() {
    //配置服务器的选项
    connect.server({
        root: 'dist/',
        livereload: true,     //实时刷新
        port: 5000
    })

    //确认监听的目标以及绑定相应的任务
    gulp.watch('src/js/*.js', ['js']);
    gulp.watch(['src/css/*.css', 'src/less/*.less'], ['css']);
    gulp.watch('*.html',  ['html']);
});

//所有需要实时监听的任务，后面加上：
 .pipe(connect.reload())
```
##### 执行任务
```bash
gulp server
```
### 自动开启链接
##### 下载插件
```bash
cnpm install open --save-dev
```
##### 配置编码
```bash
var open = require('open');
```
```bash
在server任务中，加入：
//open可以自动打开指定的链接
open('http://localhost:5000/');
```
### --扩展--
打包加载gulp插件
<b>前提：将插件下载好</b>
下载打包插件：gulp-load-plugins
```bash
cnpm install gulp-load-plugins --save-dev

引入： var $ = require('gulp-load-plugins')();
```
($就是函数执行后返回的对象，其他插件的方法都在$这个对象里面。)
神来之笔：其他的插件不用再引入了
使用方法：
所有的插件用$引出，其他插件的方法名统一为插件的名字(即插件)
使用：
在每个方法前面加上$.来调用该方法。
```bash
gulp.task('css', ['less'],function() {
    return gulp.src("src/css/*.css")
               .pipe($.concat('build.css'))
               .pipe($.rename({suffix: '.min'}))
               .pipe($.cssClean({compatibility: 'ie8'}))
               .pipe(gulp.dest('dist/css/'))
               .pipe($.livereload())              //实时刷新
               .pipe($.connect.reload())
});

gulp.task('html', function() {
    return gulp.src('index.html')
               .pipe($.htmlMin({collapseWhitespace: true}))
               .pipe(gulp.dest('dist/'))
               .pipe($.livereload())              //实时刷新
               .pipe($.connect.reload())
});
```
###### $.后面跟的是gulp插件，gulp-后面的名称。
报错：
```bash
$.htmlMin is not a function
```
因为一开始是：var htmlMin = require('gulp-htmlmin');
将htmlMin改为htmlmin即可
报错：
```bash
$.cssClean is not a function
```
因为一开始是：var cssClean = require('gulp-clean-css');
将cssClean改为cleanCss即可(驼峰命名法)

注：如果使用gulp-load-plugins这个插件，就不用每个插件一个一个引入。
gulpfile.js：
```bash
var gulp = require('gulp');
var $ = require('gulp-load-plugins')();

// var concat = require('gulp-concat');
// var uglify = require('gulp-uglify');
// var rename = require('gulp-rename');
// var less = require('gulp-less');
// var cssClean = require('gulp-clean-css');
// var htmlMin = require('gulp-htmlmin');
// var livereload = require('gulp-livereload');
// var connect = require('gulp-connect');

var open = require('open');
//注册任务
// gulp.task('任务名', function() {
//     //配置任务的操作
// })

//注册合并压缩js的任务
gulp.task('js', function() {
    //如果js目录（包括子目录）的所有js文件，需要加上/**/，
    //不加，只代表js目录下的所有js文件
    // gulp.src("src/js/**/*.js") 
    
    return gulp.src("src/js/*.js") //找到目标原文件，将数据读取到gulp的内存中
               .pipe($.concat('build.js'))       //临时合并文件
               .pipe(gulp.dest('dist/js/'))    // 临时输出文件到本地
               .pipe($.uglify())                 //压缩文件
               .pipe($.rename({suffix: '.min'}))  //重命名
               .pipe(gulp.dest('dist/js/'))     //输出压缩文件
               .pipe($.livereload())              //实时刷新
               .pipe($.connect.reload())
});

//注册转换less的任务
gulp.task('less', function() {
    return gulp.src("src/less/*.less")
               .pipe($.less())            //编译less文件为css文件
               .pipe(gulp.dest('src/css/'))
               .pipe($.livereload())              //实时刷新
               .pipe($.connect.reload())
});

//注册合并压缩css文件
gulp.task('css', ['less'],function() {
    return gulp.src("src/css/*.css")
               .pipe($.concat('build.css'))
               .pipe($.rename({suffix: '.min'}))
               .pipe($.cleanCss({compatibility: 'ie8'}))
               .pipe(gulp.dest('dist/css/'))
               .pipe($.livereload())              //实时刷新
               .pipe($.connect.reload())
});
//注册压缩html任务
gulp.task('html', function() {
    return gulp.src('index.html')
               .pipe($.htmlmin({collapseWhitespace: true}))
               .pipe(gulp.dest('dist/'))
               .pipe($.livereload())              //实时刷新
               .pipe($.connect.reload())
});

//注册监视任务(半自动)
gulp.task('watch', ['default'], function() {
    //开启监听
    livereload.listen();

    //确认监听的目标以及绑定相应的任务
    gulp.watch('src/js/*.js', ['js']);
    gulp.watch(['src/css/*.css', 'src/less/*.less'], ['css']);
    gulp.watch('*.html',  ['html']);
})

//注册监视任务（全自动）
gulp.task('server', ['default'],function() {
    //配置服务器的选项
    $.connect.server({
        root: 'dist/',
        livereload: true,     //实时刷新
        port: 5000
    })
    
    //open可以自动打开指定的链接
    open('http://localhost:5000/');

    //确认监听的目标以及绑定相应的任务
    gulp.watch('src/js/*.js', ['js']);
    gulp.watch(['src/css/*.css', 'src/less/*.less'], ['css']);
    gulp.watch('*.html',  ['html']);
});

// 如果执行每个任务都要gulp *敲一次命令行，是不方便的，所以把任务放到默认任务里面
//注册默认任务
// gulp 4.0.2不能这样写：
// gulp.task('default', ['js', 'less', 'css']);

// gulp4可以这样写：
// var build = gulp.series('less', gulp.parallel('js', 'css', 'html'));
// gulp.task('default', build);

gulp.task('default', ['js', 'less', 'css', 'html']);

```

[JsLint 的安装和使用](https://www.cnblogs.com/CyLee/p/6368629.html)

 JSLint 是一款Javascript验证工具，在定位错误并确保基本指南得以遵循时，非常有用。如果你正在编写专业级的javascript，应该使用 JSLint 或者类似的验证工具（JSHint）。它帮助我们避免了许多种bug，极大缩短了开发时间。如果你安装了Node.js，像这样即可安装：

安装：

```
npm install -g jslint
```

使用 JSlint：

```
jslint spa.js
```

如果出现以下效果，说明安装并且验证成功

```
spa.js is OK.
```

[JSCS：验证JavaScript代码](https://www.w3cschool.cn/intellij_idea_doc/intellij_idea_doc-cpvt2z2y.html)