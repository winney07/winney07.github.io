---
title: AntDesignUI相关笔记
date: 2020-05-24 16:19:49
tags:
- AntDesignUI
- 工作笔记
---

[文字滚动，轮播效果](https://ant.design/components/alert-cn/)

[轮播的公告](https://ant.design/components/alert-cn/#components-alert-demo-loop-banner)

配合 [react-text-loop-next](https://npmjs.com/package/react-text-loop-next) 或 [react-fast-marquee](https://npmjs.com/package/react-fast-marquee) 实现消息轮播通知栏。

```
cnpm i --save react-text-loop-next react-fast-marquee
```

#### key报错

[antd key报错 Each child in a list should have a unique “key“ prop.](https://blog.csdn.net/AS_TS/article/details/107981367)

Table表格，Select选择器中的Option，`map()` 遍历渲染，Modal 对话框    需要添加key