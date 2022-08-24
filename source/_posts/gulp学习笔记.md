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

在百度网盘，Gulp-master、gulp-demo-master、gulp-book-master中有相关使用教程。

[gulp-官网](https://www.gulpjs.com.cn/)

[gulp-github](https://github.com/gulpjs/gulp)

[gulp-book](https://github.com/winney07/gulp-book)

[gulp-book](https://github.com/nimoc/gulp-book)

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





[gulp 入门指南](https://github.com/nimoc/gulp-book)

[Gulp编译、合并、压缩，以及Browsersync实时刷新教程](https://blog.csdn.net/beverley__/article/details/55213235)



https://www.xiaochao.me/seo/118.html

https://www.xiaochao.me/seo/119.html

https://www.xiaochao.me/seo/120.html



小超的博客复制过来的：

### gulp的安装

gulp是依赖于node.js的开放，安装前，请先去node.js官网下载，安装完成后，就开始了以下的操作

安装全局的npm (因为npm是国外的，在这，由于公司的网速，特别卡，坑了我几天了，安装一个npm需要2天，电脑还是不关机的情况下，后来放弃了，就选择了淘宝镜像的。

cnpm，安装方法，可参考一下淘宝的镜像https://npm.taobao.org/ )，在接下来的文章中，我会与淘宝镜像的命令进行说明



使用淘宝镜像安装：npm，可直接安装gulp,node.js自动安装有npm，不需要引用

```javascript
npm install -g cnpm --registry=https://registry.npm.taobao.org
```

gulp安装：如果是npm，—下请不要再开头加c ，加了就不关我的事了，在这里-g代表全局变量声明

```javascript
cnpm install -g gulp
```



安装完全局后，接下来，就开始了gulp的使用了，先创建自己的项目文件，在这里，因为我是用window的，如果是linux我也不做过多的讲解了，等有机会在服务器上折腾一个gulp的时候

进入E盘，在选中的项目中创建一个文件，window用户用md , linux用户用mkdir，在命令行上输入

```javascript
md gulp-xiaochao
```

cd,进入目录后，在开始前，我们先创建一个叫package.json文件的文件，先位置好相关的依赖，在这里也可以直接输入

```javascript
cnpm init
```

进行相关的配置，在这里面会问我们—些问题，版本号和说明什么的，如果喜欢折腾可以填写，全部回车也可以，没有太大的影响，在填写完后，会自动的在文件夹下看见一个叫package.json，当打开文件就会看见，刚刚配置好的说明。回到命令行工具，开始安装gulp，在这里注意—下，前面是全局，要加-g说明，现在是安装在局部，就不需要加上，但是要加上的是--save-dev,这表示写入刚刚创建的

package.json的文件夹里，如下：

```javascript
cnpm install gulp --save-dev
```

当创建好了gulp，目录文件上，会多出了一个node_modules文件夹，打开package,json文件，可以看到上面写着相应的版本号，为了测试他是遵循我的依赖文件走的，我就删除了这个node_modules,然后再从新安装了一下，这次，我不加gulp

```javascript
cnpm install --save-dev
```

安装后，会发现目录里面被删除的node_modules文件又回来了，解释一下，因为在配置文件package.json已经写入了gulp，所以在安装的时候，这里是可以自动安装回来的，说到这，aulp的安装就结束了



#### gulpfile.js：

```javascript
// 获取gulp
var gulp = require('gulp');
// 获取gulp-uglify模块(用于压缩js文件)
var uglify = require('gulp-uglify');
// 压缩js
// 在命令使用gulp script启动此任务
	gulp.task('script', function(){
 		// 1.我到文件
		gulp.src('js/*.js')
    		// 2.压缩js
				.pipe(uglify())
    		// 3.另存压缩后的文件
				.pipe(gulp.dest('dist/js'))
})


// 注意：1.要加"task"；2.连写，后面不加分号；3.pipe的英文不要写错
```



### 环境搭建

#### 1.1 环境运行环境nodejs

- 使用gulp 自动化编译scss. js 等
- 使用bower管理依赖插件,
- 使用requirejs 作为模块加载器,
- 使用bootstrap css 作为样式框架
- 依赖jquery,jquery-ui 两个库



#### 1.2 项目目录

- node_rodules 为依赖模块文件
- .bowerrc 为 bower配置文件，包含模块安装目录配置
- bower. json 为 bower配置文件，包含依赖模块等
- gulpfile.js 为 gulp 任务配置文件
- package.json为程序配置文件，包含npm 依赖模块等
- Lib 为 bower.json  dependencies 中的依赖文件



node.js开发环境搭建

[node.js官网](https: //nodejs.org/en/download/)



### bower的使用

使用了bower的项目都会在目录下有一个bowex..ison.文件。在该文件同级目录下，使用如下命令即可安装相关依赖库。

```javascript
bower install
```

注：bower下载安装依赖库实际上是使用git进行下载。对于linux系统，由于默认都有安装git，所以一般没问题。但是windows系统一般没有git。在 windows系统下需要确定安装了git客户端，建议使用同捆的git bash 命令什来执行bowerinstall命令。或者把git目录加入windows的环境变量中,再在命令行中执行bowerinstall命令。（）

使用 bower安装某个特定类库，例如： jquery 



#### 1. 安装

先装全局，然后在对应文件夹中打开git CMD，做以下操作：

1. 在对应的文件夹中，查看是否安装了bower
2. 生成.bowerrc文件
3. 在.bowerrc文件中写出安装bower的文件夹目录

```javascript
{
	“directory”: "lib"
}
```

#### 2.生成bower.json文件

在window下的CMD命令窗口，以管理员的身份，去到对应的目录，运行  bower init    其他需要输入的信息，可以选择都是默认也可以选择自己写

#### 3.安装其他依赖插件

```javascript
bower install jquery bootstrap require jquery-ui --save-dev
```

加上--save-dev，在bower.json文件中会写入相关信息：

```javascript
"devDependencies": {
  "jquery": "^3.3.1",
  "bootstrap": "^4.0.0",
	"requirejs": "^2.3.5",
	"jquery-ui": "^1.12.1"
}
```

### gulp-自动化操作

#### 全局安装gulp

Gulpjs是一个自动化构建工具，开发者可以使用它在项目开发过程中自动执行常见任务，gulp,js 是基于node.js构建的，利用node.js 的威力，可以快速构建项目

1. 说明：全局安装gulp 目的是为了通过她执行gulp 任务 ;
2. 安装：命令提示符执行cnpm install gulp -g; 

#### 生成package.json

先写好gulpfile.js文件再执行cnpm init命令：

```javascript
cnpm init
```

#### 本地安装gulp

```javascript
cnpm install gulp-connect --save-dev

cnpm install gulp --save-dev
```

#### 运行

```javascript
gulp
```

#### Sass文件处理

```javascript
gulp sass
```

#### 把gulp-connect改为gulp-webserver

```javascript
cnpm install gulp-webserver --save-dev
```



报错：

```javascript
Uncaught Error: Script error for "popper.js", needed by: bootstrap
// 不知道什么原因导致的
```

#### 解决报错

在project\lib\bootstrap\assets\js\vendor中复制一份popper.min.js改名为popper.js，放在project目录下



[Javascript模块化编程（三）：require.js的用法](http://www.ruanyifeng.com/blog/2012/11/require_js.html)



### AMD与CMD的区别

- AMD：requirejs     先加载所有的依赖      加载完才能使用
- CMD：seajs		延迟加载			   需要谁，加载谁

#### AMD

```javascript
define(['a', 'b', 'c'], function(a, b, c){
		....
})
```

#### CMD

```javascript
define(function (){
var a= require('a');
    a.info();
var b = require('b');
    b.info2();
})
```



#### gulpfile.js的配置

```
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
var gulp        = require("gulp")
var browserSync = require("browser-sync").create()
var babel       = require("gulp-babel")
//修改完之后，刷新页面
var reload       = browserSync.reload

gulp.task('js', function(){
    return gulp.src('src/index.js')
               .pipe(gulp.dest('dist'))
               .pipe(babel({
                　presets: ['es2015']
                }))
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
var gulp = require('gulp');
// 调用 .create() 意味着你得到一个唯一的实例并允许您创建多个服务器或代理。
var browserSync = require('browser-sync').create();
// 定义一个任务，任务的名字，该任务所要执行的一些操作
gulp.task('watch', function() {
// 启动Browsersync服务。这将启动一个服务器，代理服务器（proxy）或静态服务器（server）
browserSync.init({
    // 设置监听的文件，以gulpfile.js所在的根目录为起点，如果不在根目录要加上路径，单个文件就用字符串，多个文件就用数组
    files: ["*.html", "css/*.css", "src/*.js", "dist/*.js"],
    // 启动静态服务器，默认监听3000端口，设置启动时打开的index.html的路径
    server: {
        baseDir: "./"
    },
    // 在不同浏览器上镜像点击、滚动和表单，即所有浏览器都会同步
    ghostMode: {
        clicks: true,
        scroll: true
    },
    // 更改控制台日志前缀
    logPrefix: "learning browser-sync in gulp",
    // 设置监听时打开的浏览器，下面的设置会同时打开chrome, firefox和IE
    // browser: ["chrome", "firefox", "iexplore"],
    // 设置服务器监听的端口号
    port: 8089
  });
});

gulp.task("default", function() {
    browserSync.init({
        server:{
            baseDir: './'
        },
        port:'8089'
    });
    
})
```





#### Gulp-demo

```
│  gulpfile.js      
│  index.html       
│  package.json     
│  
├─dist
│  │  index.html    
│  │
│  ├─css
│  │      build.min.css
│  │
│  └─js
│          build.js
│          build.min.js
│
└─src
    ├─css
    │      test1.css
    │      test2.css
    │      test3.css
    │
    ├─js
    │      test1.js
    │      test2.js
    │
    └─less
            test3.less
gulpfile.js
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
    
    return gulp.src("src/js/*.js")             //找到目标原文件，将数据读取到gulp的内存中
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

// 如果执行每个任务都要gulp ***敲一次命令行，是不方便的，所以把任务放到默认任务里面
//注册默认任务
// gulp 4.0.2不能这样写
// gulp.task('default', ['js', 'less', 'css']);

// gulp.task('default', gulp.parallel('js', 'less', 'css', function () {
//     // Build the website.
// }));

// var build = gulp.series('less', gulp.parallel('js', 'css', 'html'));
// gulp.task('default', build);
gulp.task('default', ['js', 'less', 'css', 'html']);
```

