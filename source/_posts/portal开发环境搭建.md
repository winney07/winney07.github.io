---
title: portal开发环境搭建
date: 2021-02-19 11:41:30
tags:
- portal
categories: 
- 工作笔记
- portal
---

#### 1.1环境

**运行环境n**odejs

使用gulp自动化编译scss，js等

使用bower管理依赖插件

使用requirejs作为模块加载器

使用bootstrap css作为样式框架

依赖jquery，jquery-ui两个库

#### 1.2项目目录

node_modules为依赖模块文件

.bowerrc 为bower配置文件,包含模块安装目录配置

bower.json为bower配置文件,包含依赖模块等

gulpfile.js为gulp任务配置文件

package.json为程序配置文件,包含npm依赖模块等

Lib为bower.json  dependencies中的依赖文件

node.js开发环境搭建

1、进入官网https://nodejs.org/en/download/

2、下载文件后，双击(.msi)安装

3、安装相关环境 

打开C:\Program Files\nodejs目录你会发现里面自带了npm,直接用npm安装相环境即可

#### npm介绍

1、说明：npm（node package manager）nodejs的包管理器，用于node插件管理（包括安装、卸载、管理依赖等）；

2、使用npm安装插件：命令提示符执行**npm install <name> [-g] [--save-dev]**；

2.1、<name>：node插件名称。例：**npm install gulp --save-dev**

2.2、**-g**：全局安装。将会安装在C:\Users\Administrator\AppData\Roaming\npm，并且写入系统环境变量；  非全局安装：将会安装在当前定位目录；  全局安装可以通过命令行在任何地方调用它

2.3、**--save**：将保存配置信息至package.json（package.json是[nodejs项目配置文件](http://www.ydcss.com/archives/18#lesson6)）；

2.4、**-dev**：保存至package.json的devDependencies节点，不指定-dev将保存至dependencies节点；一般保存在dependencies的像这些express/ejs/body-parser等等。

2.5、为什么要保存至package.json？因为node插件包相对来说非常庞大，所以不加入版本管理，将配置信息写入package.json并将其加入版本管理，其他开发者对应下载即可（命令提示符执行**npm install**，则会根据package.json下载所有需要的包，**npm install --production**只下载dependencies节点的包）。

#### 选装cnpm

1、说明：因为npm安装插件是从国外服务器下载，受网络影响大，可能出现异常，如果npm的服务器在中国就好了，所以我们乐于分享的淘宝团队干了这事。！来自官网：**“这是一个完整 npmjs.org 镜像，你可以用此代替官方版本(只读)，同步频率目前为 10分钟 一次以保证尽量与官方服务同步。”**；

2、官方网址：[http://npm.taobao.org](http://npm.taobao.org/)；

3、安装：命令提示符执行`**npm install cnpm -g --registry=https://registry.npm.taobao.org**`；  注意：安装完后最好查看其版本号**cnpm -v**或关闭命令提示符重新打开，安装完直接使用有可能会出现错误；

注：cnpm跟npm用法完全一致，只是在执行命令时将npm改为cnpm（以下操作将以cnpm代替npm）。

```
npm install -g cnpm --registry=http://registry.npm.taobao.org
```

Bower使用（为什么使用bower，因为它可以节省掉你去git或是网上找js的时间;）

注：选Git CMD

#### bower的安装

1、首先在我的系统安装 **nodejs**。因为我的系统是windows，还需要安装**msysgit**，注意图二中的选项

2、之后就可以用npm包管理工具下载并**全局安装bower**:  

```
npm install -g bower
```

全局安装bower 后，可以查看Bower的帮助信息，使用命令：

```
bower help
```

3、初始化当前工程的bower，此操作会在当前目录下生成bower.json文件：

```
bower init
```

#### bower的使用

使用了bower的项目都会在目录下有一个bower.json文件。在该文件同级目录下，使用如下命令即可安装相关依赖库。

```
bower install  
```

> 注：bower下载安装依赖库实际上是使用git进行下载。对于linux系统，由于默认都有安装git，所以一般没问题。但是windows系统一般没有git。在windows系统下需要确定安装了git客户端，建议使用同捆的git bash命令行来执行bower install命令。或者把git目录加入windows的环境变量中，再在命令行中执行bower install命令。()

使用bower安装某个特定类库，例如jquery:

```
bower install jquery
```

使用bower更新某个特定类库，例如jquery:

```
bower update jquery
```

删除包,例如jquery (如果包已经被依赖，则不能删除)

```
bower uninstall jquery
```

试着在项目文件夹下，下载jquery 和 underscore

```
bower install jquery underscore
```

然后就可以看到项目文件夹下多了bower_components（默认目录）,再就是两个插件包了（jquery和underscore）

初步这样也就行了，但是/bower_components这个目录有点让人不习惯，我想把东西下载到我习惯的目录里。需要加一个**.bowerrc文件**。注意，*不需要名字什么的*，只要新增一个.bowerrc就行了。

提示：**用cmd命令创建文件**如下:

```
$ type null >.bowerrc
bash: type: null: not found
```

#### .bowerrc配置

```
{
    "directory" : "js/jslib",
    "json":"",
    "endpoint" : "",
    "searchpath": "",
    "shorthand_resolver" : ""
}

```

里面可以定义下载目录：

```
{
"directory": "app/vendor"
}
```

同样的cmd命令再执行一遍，这次可以看到文件下载到app/vendor中了。

```
bower install jquery underscore
```

由于在实际安装过程中，没有运行命令 >bower init 现在重新运行该命令 生成bower.json

遇到了问题，bower init 失败

```
$ bower initbower ENOINT
Register requires an interactive she11
Additional error details:
Note that you can manua1ly force an interactive she1l with --config.interactive
```

**解决办法：**在 windows cmd（管理者） 里面使用 bower init,而不是在 git bash 里面使用 bower init.

使用bower install jquery **--save**才会把jquery依赖记入到bower.json。

要安装某个版本使用#，如安装juqery1.9.1，可以使用bower install jquery#1.9.1。

除了用包名安装，也可以指定git地址，进行安装，如bower install https://github.com/jquery/jquery。



bower install --save handlebars 后就会看到handlebar 在bower.json的dependencies里，如果不加--save就不会有。

接下来删了app/vendor下的所有内容，然后bower install，他会把bower.json中的dependencies重新下载。

#### 全局安装gulp

Gulp.js是一个自动化构建工具，开发者可以使用它在项目开发过程中自动执行常见任务，gulp.js是基于node.js构建的，利用node.js流的威力，可以快速构建项目

1、说明：全局安装gulp目的是为了通过她执行gulp任务；

2、安装：命令提示符执行**cnpm install gulp -g**；

3、查看是否正确安装：命令提示符执行**gulp -v**，出现版本号即为正确安装。

#### 新建package.json文件

2.1、说明：package.json是基于nodejs项目必不可少的配置文件，它是存放在项目根目录的普通json文件；

2.2、它是这样一个json文件**（注意：json文件内是不能写注释的，复制下列内容请删除注释）**： 

```
{
  "name": "test",   //项目名称（必须）
  "version": "1.0.0",   //项目版本（必须）
  "description": "This is for study gulp project !",   //项目描述（必须）
  "homepage": "",   //项目主页
  "repository": {    //项目资源库
    "type": "git",
    "url": "https://git.oschina.net/xxxx"
  },
  "author": {    //项目作者信息
    "name": "surging",
    "email": "surging2@qq.com"
  },
  "license": "ISC",    //项目许可协议
  "devDependencies": {    //项目依赖的插件
    "gulp": "^3.8.11",
    "gulp-less": "^3.0.0"
  }
}
```

2.3、当然我们可以手动新建这个配置文件，但是作为一名有志青年，我们应该使用更为效率的方法：命令提示符执行**cnpm init**

![手动新建这个配置文件](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/portal%E5%BC%80%E5%8F%91%E7%8E%AF%E5%A2%83%E6%90%AD%E5%BB%BA/note1.png)

2.4、查看package.json帮助文档，命令提示符执行**cnpm help package.json**

特别注意：package.json是一个普通json文件，所以不能添加任何注释。参看 http://www.zhihu.com/question/23004511

#### 本地安装gulp插件

3.1、安装：定位目录命令后提示符执行`**cnpm install --save-dev**`；

3.2、本示例以gulp-less为例（编译less文件），命令提示符执行`**cnpm install gulp-less --save-dev**`；

![编译less文件](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/portal%E5%BC%80%E5%8F%91%E7%8E%AF%E5%A2%83%E6%90%AD%E5%BB%BA/note2.png)

3.3、将会安装在node_modules的gulp-less目录下，该目录下有一个gulp-less的使用帮助文档README.md；

3.4、为了能正常使用，我们还得本地安装gulp：`**cnpm install gulp --save-dev**`；

PS：细心的你可能会发现，我们全局安装了gulp，项目也安装了gulp，全局安装gulp是为了执行gulp任务，本地安装gulp则是为了调用gulp插件的功能。

#### 新建gulpfile.js文件（重要）

4.1、说明：gulpfile.js是gulp项目的配置文件，是位于项目根目录的普通js文件（其实将gulpfile.js放入其他文件夹下亦可）。

4.2、它大概是这样一个js文件（更多插件配置请[查看这里](http://www.ydcss.com/archives/tag/gulp)）：

```
// 导入工具包 require('node_modules里对应模块')
var gulp = require('gulp'), //本地安装gulp所用到的地方
    less = require('gulp-less');
 
// 定义一个testLess任务（自定义任务名称）
gulp.task('testLess', function () {
    gulp.src('src/less/index.less') // 该任务针对的文件
        .pipe(less()) //该任务调用的模块
        .pipe(gulp.dest('src/css')); // 将会在src/css下生成index.css
});
 
gulp.task('default',['testLess', 'elseTask']); // 定义默认任务 elseTask为其他任务，该示例没有定义elseTask任务
 
// gulp.task(name[, deps], fn) 定义任务  name：任务名称 deps：依赖任务名称 fn：回调函数
// gulp.src(globs[, options]) 执行任务处理的文件  globs：处理的文件路径(字符串或者字符串数组) 
// gulp.dest(path[, options]) 处理完后文件生成路径

```

bower install  表示安装bower.json中的依赖文件到lib

npm install 表示安装package.json中的外挂到node_modules

#### gulp环境下安装sass

1、首先全局环境下配置淘宝镜像(**注意:这里是全局环境，不是项目根目录)
执行语句: 

```
npm install -g cnpm --registry=https://registry.npm.taobao.org
```

2、进入项目根目录，安装
执行语句:

```
cnpm install --save-dev node-sass
```

3、仍然是项目根目录，安装
执行语句: 

```
npm install --save-dev gulp-sass
```

#### gulp运行

输入 gulp

#### Require.js使用

1、为什么要用require.js

最早的时候，所有Javascript代码都写在一个文件里面，只要加载这一个文件就够了。后来，代码越来越多，一个文件不够了，必须分成多个文件，依次加载。

```
<script src="1.js"></script>
<script src="2.js"></script>
<script src="3.js"></script>
<script src="4.js"></script>
<script src="5.js"></script>
<script src="6.js"></script>
```

这段代码依次加载多个js文件。

这样的写法有很大的缺点。首先，加载的时候，浏览器会停止网页渲染，加载文件越多，网页失去响应的时间就会越长；其次，由于js文件之间存在依赖关 系，因此必须严格保证加载顺序（比如上例的1.js要在2.js的前面），依赖性最大的模块一定要放到最后加载，当依赖关系很复杂的时候，代码的编写和维 护都会变得困难。

require.js的诞生，就是为了解决这两个问题：

​    （1）实现js文件的异步加载，避免网页失去响应；

​    （2）管理模块之间的依赖性，便于代码的编写和维护。

2、require.js的加载

```
<script src="js/require.js"></script>
```

加载require.js以后，下一步就要加载自己的代码了。假定自己的代码文件是main.js，也放在js目录下面。那么，只需要写成下面这样就行了：

```
<script src="js/require.js" data-main="js/main"></script>
```

3、模块的加载

1）main.js

```
require.config({
  //baseUrl: "../lib",
  shim: {
    'underscore': {
     exports: '_'
    },
  },
  paths: {
    "jquery": "../lib/jquery/dist/jquery.min",
    "underscore": "../lib/underscore/underscore-min",
    "selector":"selector"
  }
});

require(['jquery', 'underscore','selector'], function($, _,selector){
  alert(selector.add(1,1));
});
```

2）模块的写法 selector.js

```
define(function() {
    var add = function(x,y) {
        return x+y;
    }

    return {
        add:add
    };
});
```

