---
title: Node.js相关笔记
date: 2020-08-24 12:18:15
tags:
- Node.js
- 工作笔记
---

### node.js查询数据，倒序排序：sort('-字段名')

```
let currentPage = parseInt(req.query.currentPage) // 转换前端传入当前页码
let pageSize = parseInt(req.query.pageSize) // 转换前端传入的每页大小
let skip = (currentPage-1)*pageSize // 实现分割查询的skip
let params = {'delete_time': "0"};

// 根据页码和每页显示条数筛选数据
const sources = await Sources.find(params).sort('-create_time').skip(skip).limit(pageSize)
```

