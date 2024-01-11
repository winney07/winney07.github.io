---
title: Vue项目设置每个页面的title
date: 2020-03-19 17:59:33
tags: 
- Vue.js
categories:
- 前端开发框架
- Vue.js
---
##### 1、在项目目录下安装vue-wechat-title
```
cnpm i vue-wechat-title --save-dev
```
##### 2、在main.js中 使用vue-wechat-title
```
Vue.use(require('vue-wechat-title'))     //实例化参数
```
##### 3、在router的配置中设置
```
{
      path: '/home',
      name: 'Home',
      component: Home,
      meta: {
        title: '主页'       //页面标题
      }
 }
```
##### 4、在每个vue页面中加入 `<div v-wechat-title="$route.meta.title"></div>`
```
 <div class="content content-box">
      <div v-wechat-title="$route.meta.title"></div>
</div>
```


###### 【参考】： [vue项目设置每个页面的title](https://www.cnblogs.com/itgezhu/p/10817502.html)

