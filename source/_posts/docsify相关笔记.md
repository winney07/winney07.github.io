---
title: docsify相关笔记
date: 2020-08-24 20:47:32
tags:
- docsify
- 工作笔记
---

#### [官网文档](https://docsify.js.org/#/zh-cn/quickstart)

#### 安装

```
npm i docsify-cli -g
```

#### 初始化项目

```
docsify init ./docs
```

#### 本地预览

```
docsify serve docs
```

#### 添加左侧导航栏-loadSidebar: true

1. 修改docs/index.html

   ```
   window.$docsify = {
     loadSidebar: true,  // 开启左侧导航栏
     name: '',
     repo: ''
   }
   ```

2. 在根目录(docs)中，新建`_sidebar.md`文件

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

3. 新建对应的文件（如：`website/vue.md` 【新建website目录，新建vue.md】）



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

