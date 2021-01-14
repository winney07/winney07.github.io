---
title: 工程化的Vue.js开发
date: 2019-06-24 11:34:45
tags:
- 《Vue2实践揭秘》
categories: 
- 工作笔记
- Vue2.js
---
#####  Vue 提供一套简化开发、测试与部署的方案，不再需要花大量的时间去学习理解框架的使用概念，以及耗费大量的精力去建立复杂的自动化环境。

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
{% asset_img vue-list.png %}
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
{% asset_img webpack.png %}

#### webpack-simple 模板
{% asset_img webpack-simple.png %}

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
{% asset_img npmrundev1.png %}
{% asset_img npmrundev2.png %}
##### 2、编译生产环境
```bash
npm run build
```
### Vue工程化的webpack配置与基本用法
{% asset_img webpack2.png %}
### webpack的特点
{% asset_img webpack3.png %}
{% asset_img webpack4.png %}

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
{% asset_img bieming.png %}
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
