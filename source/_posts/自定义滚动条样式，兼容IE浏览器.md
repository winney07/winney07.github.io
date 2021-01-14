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
{% asset_img ie-scrollar.png %}
{% asset_img ie-scrollar2.png %}

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