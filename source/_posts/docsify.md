---
title: docsify
date: 2020-08-24 17:54:50
tags:
- docsify
categories: 
- 文档网站生成工具
- docsify
---

#### [官网文档](https://docsify.js.org/#/zh-cn/quickstart)

[docsify中文文档](https://docsify.js.org/#/zh-cn/)

摘自[视觉派pie](https://www.jianshu.com/p/4883e95aa903) 、[Docsify快速搭建个人博客](https://www.imooc.com/article/287154)

> 文档网站生成工具、快速搭建个人博客

> docsify 是一个动态生成文档网站的工具。不同于 GitBook、Hexo 的地方是它不会将 `.md` 转成 `.html` 文件，所有转换工作都是在运行时进行。
>
> 这将非常实用，如果只是需要快速的搭建一个小型的文档网站，或者不想因为生成的一堆 `.html` 文件“污染” commit 记录，只需要创建一个 `index.html` 就可以开始写文档而且直接部署在[GitHub Pages](https://links.jianshu.com/go?to=https%3A%2F%2Fdocsify.js.org%2F%23%2Fzh-cn%2Fdeploy)。

#### 特性

- 无需构建，写完文档直接发布
- 容易使用并且轻量 (~19kB gzipped)
- 智能的全文搜索
- 提供多套主题
- 丰富的 API
- 支持 Emoji
- 兼容 IE10+
- 支持 SSR ([example](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2Fdocsifyjs%2Fdocsify-ssr-demo))

#### 生成文档的工具：

阿里的语雀、DokuWiki、MDwiki、HDwiki

[使用Typora+docsify+GitHub Pages搭建团队知识库](https://www.jianshu.com/p/84b46b67031d)

##### 文档案例

[使用Vue全家桶+Node.js搭建的小型全栈项目](https://hanxueqing.github.io/Douban-Movie/#/?id=使用vue全家桶nodejs搭建的小型全栈项目)

#### 安装

全局安装`docsify-cli`工具，可以方便地创建及在本地预览生成的文档。

```
npm i docsify-cli -g
```

#### 初始化项目

如果想在项目的 `./docs` 目录里写文档，直接通过 `init` 初始化项目。

```
docsify init ./docs
```

#### 本地预览

通过运行 `docsify serve` 启动一个本地服务器，可以方便地实时预览效果。默认访问地址 [http://localhost:3000](http://localhost:3000/) 

```
docsify serve docs
```

#### 添加左侧导航栏-loadSidebar: true

1. 修改docs/index.html，配置 `loadSidebar` 选项

   ```
   window.$docsify = {
     loadSidebar: true,  // 开启左侧导航栏
     name: '',
     repo: ''
   }
   ```

2. 在根目录(docs)（与index.html同目录）中，新建`_sidebar.md`文件

   ```
   * 常用网址     // 分组名
   
     * [Vue](website/vue.md)   // 链接到对应文件
   * 收藏博客
   
     * [javascript](blogs/javascript.md)
   * 常用软件
   
     * [web前端](software/web.md)
   * 笔记
   
     [web前端](software/web.md)
   ```

3. 配置 `alias` 避免不必要的回退过程 （即访问非根目录的页面时，会报`_sidebar.md`文件是404)

   ```
   window.$docsify = {
       loadSidebar: true,
       alias: {
         '/.*/_sidebar.md': '/_sidebar.md'
       }
   }
   ```

4. 新建对应的文件（如：`website/vue.md` 【新建website目录，新建vue.md】）

#### [docsify 侧边栏目录扩展](https://www.cnblogs.com/baby123/p/14361402.html)

官方文档没有介绍左侧目录的折叠问题，可以使用这个开源：

git地址 https://github.com/iPeng6/docsify-sidebar-collapse

代码如下：

```
<link rel="stylesheet" href="//cdn.jsdelivr.net/npm/docsify-sidebar-collapse/dist/sidebar.min.css" />
<link rel="stylesheet" href="//cdn.jsdelivr.net/npm/docsify-sidebar-collapse/dist/sidebar-folder.min.css" />

<script src="//cdn.jsdelivr.net/npm/docsify-sidebar-collapse/dist/docsify-sidebar-collapse.min.js"></script>
```

使用sidebarDisplayLevel设置默认折叠的层级：

```
window.$docsify = {
      sidebarDisplayLevel: 1,   // 如果想收起的是第一层级，设置为0
}
```

然后根据自己需求修改样式。

#### 侧边栏三层级配置

参考[docsify侧边栏折叠](https://cpury.com/1408.html)

_sidebar.md：

```
* 项目
    * [管理后台](project/manage.md)
        * [新广告后台](project/ad_admin.md)
        * [纳米盒应用后台2.0](project/AppManage2.0.md)
        * [纳米盒管理后台](project/manage_new.md)
        * [黄豆芽办公系统](project/ai.huangdouya.com.md)
        * [黄豆芽sdk运营后台](project/hanteng-manage.vxinyou.com.md)
        * [切支付](project/check_pay.md)
```

manage.md：（里面写什么都可以）

```
## 新广告后台
## 纳米盒应用后台2.0
## 纳米盒管理后台
## 黄豆芽办公系统
## 黄豆芽sdk运营后台
## 切支付
```

#### 添加代码高亮

引入js文件：

```
<script src="//cdn.jsdelivr.net/npm/prismjs@1/components/prism-bash.min.js"></script>
```

参考[代码高亮](https://docsify.js.org/#/zh-cn/language-highlight)

写代码的时候要加上bash

```
​```bash
echo "hello"
​```
```



#### 添加搜索功能

1. 修改`window.$docsify`（在`docs/index.html`）

   ```
   window.$docsify = {
       loadSidebar: true,
       name: '',
       repo: '',
       search: {   // 添加
           noData: {
             '/': '无匹配结果'
           },
           paths: 'auto',
           placeholder: {
             '/': '搜索'
           }
       }
     }
   ```

2. 添加`search.min.js`插件（在`docs/index.html`）

   ```
   <script src="//cdn.jsdelivr.net/npm/docsify/lib/plugins/search.min.js"></script>
   ```

   ```
   <link rel="stylesheet" href="//cdn.jsdelivr.net/npm/docsify-sidebar-collapse/dist/sidebar.min.css" />
   ```




#### 部署到服务器

[如何把 Docsify 文档部署到服务器?](https://blog.csdn.net/weixin_34568812/article/details/112002961)

[使用Typora+docsify+GitHub Pages搭建团队知识库](https://www.jianshu.com/p/84b46b67031d)

[使用docsify 写开源文档+部署到云服务器](https://juejin.cn/post/6844904115466682375)



#### 配置参考

```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>工作文档</title>
  <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1" />
  <meta name="description" content="Description">
  <link rel="shortcut icon" href="./favicon.ico" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0, minimum-scale=1.0">
  <link rel="stylesheet" href="//cdn.jsdelivr.net/npm/docsify@4/lib/themes/vue.css">
  <link rel="stylesheet" href="//cdn.jsdelivr.net/npm/docsify-sidebar-collapse/dist/sidebar.min.css" />
  <link rel="stylesheet" href="//cdn.jsdelivr.net/npm/docsify-sidebar-collapse/dist/sidebar-folder.min.css" />
  <style>
    a{
      text-decoration: none;
    }
    a:hover{
      text-decoration: underline;
    }
    .sidebar ul li a{
      /* color: #0088CC !important; */
      font-weight: normal;
    }
    .content td a, .content p a{
      font-weight: normal;
    }
    .markdown-section blockquote p{
      font-weight: normal;
    }
    .markdown-section h5{
      font-size: 1.05rem;
      margin-top: 0.5rem;
      margin-bottom: 1rem;
    }
    .markdown-section hr{
      margin: 2em 0 0.5rem;
    }
    .sidebar-nav ul:not(.app-sub-sidebar)>li.folder::before{
      display: none;
    }
    .sidebar-nav ul:not(.app-sub-sidebar)>li.file::before{
      background: none;
    }
    .sidebar-nav ul:not(.app-sub-sidebar)>li::before{
      content: "-";
      top: -1px;
      left: -10px;
      width: 10px;
      height: 10px;
    }
    .sidebar-nav ul:not(.app-sub-sidebar)>li.open::before{
      transform: none;
    }
    .markdown-section p{
      margin: 0;
    }
    .markdown-section th{
      background-color: #f8f8f8;
      color: #909399;
    }
    .markdown-section pre{
      padding: 0 0.6rem;
      margin: 0.6em 0;
    }
    .markdown-section pre>code{
      padding: 0.4rem 5px;
    }
    .markdown-section code, .markdown-section output:after, .markdown-section pre{
      font-family: 'Source Sans Pro,Helvetica Neue,Arial,sans-serif';
    }
    /* .sidebar{
      width: 200px;
    }
    .sidebar-toggle{
      width: 184px;
    }
    .content{
      left: 200px;
    }
    .markdown-section{
      max-width: 90%;
    } */
  </style>
</head>
<body>
  <div id="app"></div>
  <script>
    window.$docsify = {
      // name: '工作文档',
      auto2top: true,
      repo: '',
      loadSidebar: true,
      sidebarDisplayLevel: 0,
      // subMaxLevel: 2,
      alias: {
        '/.*/_sidebar.md': '/_sidebar.md'
      },
      search: {
          noData: {
            '/': '无匹配结果'
          },
          paths: 'auto',
          placeholder: {
            '/': '搜索'
          }
      }
    }
  </script>
  <!-- Docsify v4 -->
  <script src="//cdn.jsdelivr.net/npm/docsify@4"></script>
  <script src="//cdn.jsdelivr.net/npm/docsify/lib/plugins/search.min.js"></script>
  <script src="//cdn.jsdelivr.net/npm/docsify-sidebar-collapse/dist/docsify-sidebar-collapse.min.js"></script>
  <script src="//cdn.jsdelivr.net/npm/prismjs@1/components/prism-bash.min.js"></script>
</body>
</html>
```