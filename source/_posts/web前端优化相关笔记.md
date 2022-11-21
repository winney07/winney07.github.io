---
title: web前端优化相关笔记
date: 2020-11-21 14:52:22
tags:
---

#### SEO网页优化

- 在页面内容中，尽量不用空格`&nbsp;`，使用padding或margin或缩进

- 在a标签的外部链接中，加入rel="nofollow"，不然小蜘蛛爬走了。

``` 
<a id="qzone" href="链接" target="_blank" rel="nofollow" title="标题">标题</a>
```

- a标签尽量加上title属性，有利于SEO

- 使用语义化代码
- br用于文本换行，不要用于标签后换行
- table可以加上caption
- `<title>`：网页标题
- `<meta keywords>`：关键词
- `<meta description>`：网页描述



#### 浏览器基本工作原理

- DNS解析(多级缓存)
- 请求(TCP建连、HTTP报文)
- 解析（解压、缓存处理、引用资源)
- 构建：DOM树（节点显隐、层次结构)
- 构建：CSSOM树(CSS优先级)
- 构建：Render树(CSS匹配规则)
- 脚本：文档状态(阻塞和延迟、内联和外联)