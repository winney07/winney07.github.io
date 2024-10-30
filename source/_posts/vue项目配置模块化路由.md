---
title: vue项目配置模块化路由
date: 2020-05-25 14:09:42
tags:
- Vue.js
categories:
- 前端开发框架
- Vue.js
---
### 目录结构
```
├── src
|    ├── assets         // 静态资源img、css、js
|    ├── components     // 小组件
|    ├── views          // 页面(视图)组件
|    ├── App.vue        // 根组件
|    ├── main.js        // 全局脚本文件（项目的入口）
|    ├── router
|    |    ├── index.js       // 路由脚本文件
|    |    ├── modules       // 模块
|    |    |    ├── user.js         // 用户模块
|    |    |    ├── other.js        // 其他模块


```
### 模块文件的配置 (以用户模块为例，其他模块也是一样的)
```
export default [
    {
        name: 'login',
        path: '/login',
        meta: {
            title: '登录页面'
        },
        component: () => import('@/views/account/login/index.vue') 
    },
    {
        name: 'register',
        path: '/register',
        meta: {
            title: '注册页面'
        },
        component: () => import('@/views/account/register/index.vue')
    },
    {
        name: 'result',
        path: '/result',
        meta: {
            title: '注册结果'
        },
        component: () => import('@/views/account/register/result/index.vue')
    }
]

//因为这里配置了页面title，所以加meta属性，如果不需要配置，可以不加
```

### index.js (router目录下的index.js)
```
import Vue from 'vue'
import VueRouter from 'vue-router'

import accoutRouter from './modules/user'
import otherRouter from './modules/other'

Vue.use(VueRouter)

export default new VueRouter({
  routes: [
    ...accoutRouter,
    ...otherRouter,
  ]
})

```

### main.js
```
import Vue from 'vue'
import App from './App.vue'
import router from './router'
import store from './store'

Vue.config.productionTip = false

new Vue({
  router,
  store,
  render: h => h(App)
}).$mount('#app')

```

### 根据路由动态修改title 
在main中加入以下代码：
```
/* 路由发生变化修改页面title */
router.beforeEach((to, from, next) => {
  if (to.meta.title) {
      document.title = to.meta.title || '首页'
  }
  next()
})
```
main.js最终代码：
```
import Vue from 'vue'
import App from './App.vue'
import router from './router'
import store from './store'

Vue.config.productionTip = false

/* 路由发生变化修改页面title */
router.beforeEach((to, from, next) => {
  if (to.meta.title) {
      document.title = to.meta.title || '首页'
  }
  next()
})

new Vue({
  router,
  store,
  render: h => h(App)
}).$mount('#app')


```
