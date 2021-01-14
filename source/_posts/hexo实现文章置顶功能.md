---
title: hexo实现文章置顶功能
date: 2020-05-25 14:39:52
tags:
- 常用命令
categories: 
- 工作笔记
- 常用命令
---
### 修改generator.js
```
找到node_modules/hexo-generator-index/lib/generator.js这个文件。
```
在
```
var posts = locals.posts.sort(config.index_generator.order_by);
```
下面添加：
```
posts.data = posts.data.sort(function(a, b) {
    if(a.top && b.top) { // 两篇文章top都有定义
        if(a.top == b.top) return b.date - a.date; // 若top值一样则按照文章日期降序排
        else return b.top - a.top; // 否则按照top值降序排
    }
    else if(a.top && !b.top) { // 以下是只有一篇文章top有定义，那么将有top的排在前面（这里用异或操作居然不行233）
        return -1;
    }
    else if(!a.top && b.top) {
        return 1;
    }
    else return b.date - a.date; // 都没定义按照文章日期降序排
});
```
完整代码:
```
'use strict';

var pagination = require('hexo-pagination');

module.exports = function(locals) {
  var config = this.config;
  var posts = locals.posts.sort(config.index_generator.order_by);
  posts.data = posts.data.sort(function(a, b) {
      if(a.top && b.top) { // 两篇文章top都有定义
          if(a.top == b.top) return b.date - a.date; // 若top值一样则按照文章日期降序排
          else return b.top - a.top; // 否则按照top值降序排
      }
      else if(a.top && !b.top) { // 以下是只有一篇文章top有定义，那么将有top的排在前面（这里用异或操作居然不行233）
          return -1;
      }
      else if(!a.top && b.top) {
          return 1;
      }
      else return b.date - a.date; // 都没定义按照文章日期降序排
  });
  var paginationDir = config.pagination_dir || 'page';
  var path = config.index_generator.path || '';

  return pagination(path, posts, {
    perPage: config.index_generator.per_page,
    layout: ['index', 'archive'],
    format: paginationDir + '/%d/',
    data: {
      __index: true
    }
  });
};

```