---
title: 自定义滚动条样式，兼容IE浏览器
date: 2019-12-17 17:43:16
tags: 兼容性处理
categories: 
- 工作笔记
- 兼容性处理
---
经常写页面的同学都知道，浏览器一般自带的滚动条样式很丑，和页面风格格格不入，于是就想着是否能够改变原有滚动条样式？但实际中，其他浏览器又和IE浏览器不一样，导致兼容性不好。

#### Chrome浏览器滚动条自定义样式修改
```bash
div{
  /*滚动条滑块按钮的颜色*/
  scrollbar-face-color: #134187;
  /*滚动条整体颜色*/
  scrollbar-highlight-color: #134187;
  /*滚动条轨道颜色*/
  scrollbar-track-color: #011433;
}
/*滚动条整体部分,必须要设置*/
::-webkit-scrollbar{
  background-color: #011433;
  width:10px;
  height:10px;
}
/*滚动条的轨道*/
::-webkit-scrollbar-track{
  background-color: #011433;
  border-radius: 10px;
}
/*滚动条的滑块按钮*/
::-webkit-scrollbar-thumb{
  border-radius: 10px;
  background-color: #134087;
}

```

#### IE浏览器滚动条自定义样式修改

在写样式之前，我们看一下IE浏览器滚动条样式设置位置参考图：
![IE浏览器滚动条样式设置位置参考图](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/%E8%87%AA%E5%AE%9A%E4%B9%89%E6%BB%9A%E5%8A%A8%E6%9D%A1%E6%A0%B7%E5%BC%8F%EF%BC%8C%E5%85%BC%E5%AE%B9IE%E6%B5%8F%E8%A7%88%E5%99%A8/ie-scrollar.png)

| 滚动条样式                  | 支持情况   | 支持浏览器版本 | 可否继承 | 描述                                   |
| --------------------------- | ---------- | -------------- | -------- | -------------------------------------- |
| scrollbar-3dlight-color     | IE特有属性 | IE5.5+         | y        | 设置滚动框的和滚动条箭头左上边缘的颜色 |
| scrollbar-highlight-color   | IE特有属性 | IE5.5+         | y        | 设置滚动框的和滚动条箭头左上边缘的颜色 |
| scrollbar-face-color        | IE特有属性 | IE5.5+         | y        | 设置滚动框和滚动条箭头的颜色           |
| scrollbar-arrow-color       | IE特有属性 | IE5.5+         | y        | 设置i滚动条箭头的颜色                  |
| scrollbar-shadow-color      | IE特有属性 | IE5.5+         | y        | 设置滚动框的和滚动条箭头右下边缘的颜色 |
| scrollbar-dark-shadow-color | IE特有属性 | IE5.5+         | y        | 设置滚动条槽的颜色                     |
| scrollbar-base-color        | IE特有属性 | IE5.5+         | y        | 设置滚动条主要构成部分的颜色           |
| scrollbar-track-color       | IE特有属性 | IE5.5+         | y        | 设置滚动条轨迹组成部分的颜色           |

```bash
//Ie下滚动条样式
HTML {
  scrollbar-base-color: #134087;
  //scrollbar-base-color: #134087;
  scrollbar-3dlight-color:#134087;
  scrollbar-highlight-color: #134087;
  scrollbar-track-color: #011433;
  scrollbar-arrow-color: #011433;
  scrollbar-shadow-color:#011433;
  //scrollbar-dark-shadow-color: #011433;
}
```

摘抄自：https://blog.csdn.net/qq_36727756/article/details/92795170