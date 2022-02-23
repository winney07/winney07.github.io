---
title: 工程化的Vue.js开发
date: 2019-06-24 11:34:45
tags:
- 《Vue2实践揭秘》
categories: 
- 工作笔记
- Vue2.js
---

Vue 提供一套简化开发、测试与部署的方案，不再需要花大量的时间去学习理解框架的使用概念，以及耗费大量的精力去建立复杂的自动化环境。

### 脚手架 vue-cli
这个工具可以让一个简单的命令行工具快速地构建一个足以支撑实际项目开发的Vue环境。 vue-cli的存在将项目环境的初始化工作与复杂度降到最低。
<!--more-->
##### 1、安装vue-cli
```bash
npm i vue-cli -g

(希望能在本机的任意目录下创建项目，那就得将它安装到node.js的全局运行目录下)
```
##### 2、使用vue-cli初始化项目
```bash
vue   ——   查看帮助文件
```
```bash
vue list  ——   查看有哪些官方模板可用

（这些官方模板存在的意义在于提供强大的项目构建能力，用户可以尽可能快地进行开发。）
```
------

将list指令的输出结果翻译一下,就可以清楚地了解这些官方模板应用于哪些使用场景:

- browserify—拥有高级功能的Browserify + vueify 用于正式开发;
- browserify-simple——拥有基础功能的 Browserify + vueify用于快速原型开发;
- simple—适用于单页应用开发的最小化配置;
- webpack——拥有高级功能的webpack + vue-loader用于正式开发;
- webpack-simple—拥有基础功能的webpack + vue-loader用于快速原型开发。

browserify的模板做得比较简陋，就算是用于正式开发还是会有些不足，配置的是Karma+Jasmine的单元测试框架，而browserify属于比较老旧的构建工具，估计官方提供这两个模板页是出于对经常使用browserify 的开发人员提供一个熟悉环境的考虑。到了正式的项目开发时，我们还是会走上 webpack的道路。

**所以我建议初学者可以跳过 browserify 的两个模板，直接使用webpack的两个模板。首先 webpack-simple正如其名，配置了最简单的可直接支持ES6的Vue.js编译环境**，可以应对那些要求时间短，结构相对简单的小型应用。如果对所有环境工具都非常熟悉，开发者也可以由这个模板入手，为项目底板定制更适应自身开发要求的环境。

其次，**webpack模板是一个非常赞的脚手架**，将其分析透彻之后，就会知道Vue的官方开发团队在其中花了很大的功夫，将上文所叙述的开发、测试与生产环境做了非常完善的配置，从最大程度上简化了由于工具而引入项目的复杂度，也降低了开发人员对工具的学习成本，这个模板也将是本书中讲述的重点。

------


##### 3、创建项目
```bash
vue init webpack my-project
```

查看项目
```bash
cd my-project   
npm install
npm run dev
```

### 深入vue-cli的工程模板

webpack和 webpack-simple这两个模板从文件结构上看几乎是一致的，只是一个是简化版，另一个是完全版。其实不然，webpack-simple是基于Webpack@2.1.0-beta.25进行配置的版本，而 webpack模板则是基于Webpack ^1.3.2配置的。**这两个版本暂时是互相不兼容的，而且使用的依赖包的版本也不一样，所以不要将webpack模板创建的项目文件结构复制到webpack-simple中进行直接的取代升级**,而是需要将node_modules内安装的所有的依赖包删除，然后重新安装才有可能迁移成功，这一点是需要注意的。

#### webpack-simple 模板

具体约定如下:
（1）  公共组件、指令、过滤器（多于三个文件以上的引用）将分别存放于src目录下的

- components;
- directives;
- filters 。

（2）以使用场景命名 Vue的页面文件。
（3）当页面文件具有私有组件、指令和过滤器时，则建立一个与页面同名的目录，页面文件更名为index.vue，将页面与相关的依赖文件放在一起。
（4）目录由全小写的名词、动名词或分词命名，由两个以上的词组成，以“-”进行分隔。
（5）Vue文件统一以大驼峰命名法命名，仅入口文件index.vue采用小写。
（6）测试文件一律以测试目标文件名.spec.js命名。
（7）资源文件一律以小写字符命名，由两个以上的词组成，以“-”进行分隔。

#### webpack模板
bulid——存放用于编译用的webpack配置与相关的辅助工具代码；
config——存放三大环境配置文件，用于设定环境变量和必要的路径信息；
test——存放E2E测试与单元测试文件以及相关的配置文件；
static——存放项目所需要的其他静态资源文件；
dist——存放运行npm run build 指令的生产环境输出文件，可直接部署到服务器对应的静态资源文件夹内，该文件夹只有在运行build之后才会生成。

#### 构建工具
##### 1、编译开发环境
```bash
npm run dev
```
这个指令的配置是在 package.,json 的 script属性中设置的，实质上它是由npm来引导执行入口程序dev-server.js完成以下的加载过程：

1. 加载环境变量
2. 合并webpack配置
3. 配置热加载
4. 配置代理服务
5. 配置回退支持
6. 配置静态资源
7. 加载开发服务器

###### 加载环境变量

该环节从config目录加载index.js和 dev.env.js两个模块，准备开发调试环境所必需的-些目录和全局变量。

###### 合并webpack配置

在 build目录下一共有三个webpack的配置文件:

- webpack.base.conf.js——公用的基本webpack配置;
- webpack.dev.conf.js—开发环境专用的 webpack配置项;
- webpack.prod.conf.js——生产环境专用的 webpack配置项。

这里使用了一个叫 webpack-merge的包来进行两个 webpack配置之间的合并，这个环节就是通过这个包将webpack.base.conf.js和 webpack.dev.conf.js合并成最终的webpack配置。
请记住这几个配置文件，在下面的章节中我们会对这些配置的内容进行调整。

###### 配置热加载

热加载是一个非常棒的功能，这个功能启用后的效果就是:当开发环境被启动并进入调试模式后，一旦我们修改了任意地方的源代码，浏览器中对应的内容就会被自动刷新，而无须手工对浏览器进行刷新的操作，这个配置将是我们做页面布局或者功能调整时的一大臂助。

###### 配置代理服务器

这个环境是为我们的代码增加一个模拟的服务端做准备，有了它的存在，我们就可以在没有后端程序支持的情况下，直接模拟远程服务器执行的一些请求的效果。例如，向服务器发出一个 HTTP GET /api/books/的请求,那么我们就可以利用代理服务器将这一请求截获下来，然后返回一组这个 API应该执行成功的返回结果，这样我们的前端程序运行起来的效果就与接入了服务端后的效果是一致的了。我们将这一技术称为服务模拟，在后面的章节中会具体介绍这一技术。

###### 加载开发服务器

启动一个Express的 Web服务器，将上述各个环境中配置好的模块进行加载，并使程序能通过浏览器进行访问。
以上就是npm run dev的完整执行思路。

##### 2、编译生产环境
```bash
npm run build
```
### Vue工程化的webpack配置与基本用法

webpack是一个模块打包的工具，它的作用是把互相依赖的模块处理成静态资源，如下图所示。

[模块依赖----->静态资源](https://webpack.docschina.org/)

### webpack的特点

#### 代码分割

在 webpack的依赖树里有两种类型的依赖:同步依赖和异步依赖。异步依赖会成为一个代码分割点，并且组成一个新的代码块。在代码块组成的树被优化之后，每个代码块都会保存在一个单独的文件里。

#### 加载器

webpack原生是只能处理JavaScript的，而加载器的作用是把其他的代码转换成JavaScript代码，这样一来所有种类的代码都能组成一个模块，也就是说，我们可以在代码内通过import将 webpack打包的资源以模块的方式引入到程序中。

以下是Vue项目中常用到的加载器（它们都是以NPM库形式提供的)：

- vue-loader——用于加载与编译*.vue文件;
- vue-style-loader——用于加载.vue文件中的样式;
- style-loader——用于将样式直接插入到页面的`<style>`内;
- css-loader——用于加载*.css样式表文件;*
- less-loader——用于编译与加载.less文件(需要依赖于less库);
- babel-loader—用于将ES6编译成为浏览器兼容的ES5;
- file-loader——用于直接加载文件;
- url-loader—用于加载URL指定的文件，多用于字体与图片的加载;
- json-loader——用于加载*.json文件为JS 实例。

#### 智能解析

webpack的智能解析器能处理几乎所有的第三方库，它甚至允许依赖里出现这样的表达式：

```
require("./components/"+ name + ".vue")
```

> 这一点恰恰是browserify不能做到的。

它能处理大多数的模块系统，比如说CommonJS和AMD。

#### 插件系统

webpack有丰富的插件系统，大多数内部的功能都是基于这个插件系统的。这也使得我们可以定制 webpack，把它打造成能满足我们需求的工具，并且把自己做的插件开源出去。



### 基本用法
（webpack的打包依赖于它的一个重要配置文件webpack.config.js）
##### 样式表引用
某些页面或者组件可能具有特定的样式定义，这些样式对于其他页面说是冗余的，我们只希望这些组件在应用时才自动加载这些特定的样式、
```bash
import Vue form 'vue'
//...省略
//引用指定的样式源文件
import './app/assets/less/dark.less'
export default {
    // ...省略
}
```
(需要在webpack的配置中加入less-loader)
##### 字体的引用
#### 用别名取代路径引用

在项目开发过程中有可能有许多包是没有放在npm 上的，有一些较老的可能还依然只存在于bower 上，某些甚至在 bower与 npm上都找不到，而不得不通过下载的方式在项目内引用，这样一来我们的代码可能通过require就得在代码内引用一段很长的文件路径，如下所示。

```
import Selector from '../ ../bower_components/bootstrap-select/dist/js/select'
```

这种包的引用方式明显违反了CommonJS的编程规范，对于这些长路径，甚至还具有“...”"这些相对路径搜索的定义,我们可以通过webpack 的resolve配置项来解决.就以select这个组件为例，在 webpack.base.config.js中加入以下的这个别名的定义：

```
module.exports ={
    entry:{ ... },
    output: { ﹒. . },
    module:{ ...},
    resolve: {
        extensions:['','·js'],
        alias:{
            'bs-select':'bower_components/bootstrap-select/dist/js/select.js'
        }
    }
}
```

有了这个定义以后，我们就可以将上面那个长引用改为下面的写法：

```
import Selector from 'bs-select';
```

绝对不要让路径引用进入到我们的代码，因为这是代码的“癌症”,一旦开始植入并生长起来，以前的代码将难以维护！

#### 配置多入口程序
不单只有一个入口，例如：前台提供最终用户使用（http://domain.com/index),后台提供给登录用户使用（http://domain.com/admin/)，那么自然需要多个与main.js类似的程序入口。
```bash
首先在build/webpack.base.conf.js配置文件中的entry配置属性上加上新的入口文件：
module.exports = {
    entry: {
        app: './src/main.js',
        admin: './src/admin-main.js'
    },
    // ...
}

```
（其他相关设置，需要用到时参考书上内容)
#### 基于Karma + Phantom + Mocha + Sinon + Chai的单元测试环境
#### 基于Nightwatch的端到端测试环境
