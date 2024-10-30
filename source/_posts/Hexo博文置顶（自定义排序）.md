---
title: Hexo博文置顶（自定义排序）
date: 2021-01-14 11:55:19
tags: 
- Hexo
- Element-ui
categories:
- 文档网站生成工具
- Hexo
---

#### Hexo博文置顶（自定义排序）

> 使用的是`top`属性，`top`值越高，排序越在前，不设置`top`值得博文按照时间顺序排序。
> 修改Hexo文件夹下的node_modules/hexo-generator-index/lib/generator.js

原来代码：

```
const config = this.config;
const posts = locals.posts.sort(config.index_ generator.order by);

sort(posts.data, (a， b) => (b.sticky || 0) - (a.sticky || 0));

const paginationDir.config.pagination_ dir || 'page';
const path.config.index_ generator.path || '';

return pagination(path, posts, {
	perPage: config.index_ generator.per_page,
	layout: ['index', 'archive'],
	format: paginationDir + '/%d/',
	data: {
    	_index: true
    }
});
```

改为：

```
'use strict';

const pagination = require('hexo-pagination');
const { sort } = require('timsort');

module.exports = function(locals) {
  const config = this.config;
  const posts = locals.posts.sort(config.index_generator.order_by);

  // sort(posts.data, (a, b) => (b.sticky || 0) - (a.sticky || 0));

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
  const paginationDir = config.pagination_dir || 'page';
  const path = config.index_generator.path || '';

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

1、即在`const posts = locals.posts.sort(config.index_generator.order_by);`下面添加如下`javascript`代码：

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

2、在对应的md文件中添加top属性：

```
---
title: 网站素材
date: 2021-01-08 11:23:25
tags:
- 网站素材
categories: 
- 工作笔记
- 网站素材
top: 102
---
```

[参考文献](https://blog.csdn.net/qq_32454537/article/details/79482920)

