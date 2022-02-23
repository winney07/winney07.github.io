---
title: Vue.js + Element-UI导航写法
date: 2020-03-19 17:28:29
tags: 
- Vue.js
- Element-ui
categories:
- 工作笔记
- Vue.js
---
#### 方法一（基本的）：

> elementUi导航通常会和vue-router一起使用，所以与官网的示例的写法不太一样。具体写法如下:

```
<el-menu :default-active="$route.path" class="el-menu-vertical-demo" router>
   <el-menu-item v-for="item in items" :index="item.src">{{item.name}}            
   </el-menu-item>
 </el-menu>
```
**data里则是正常的数据即可：**

```
data(){
      return{
        items:[
          {src:'/gameinfo/index',name:'基本信息'},
          {src:'/gameversion/index',name:'版本管理'},
          {src:'/gameplatform/index',name:'渠道管理'},
          {src:'/gameproduct/index',name:'充值产品'},
          {src:'/gameplugin/index',name:'插件管理'}
        ]
      }
    }
```
<!-- more -->
**效果如图所示：**

![路由](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/Vue-js-Element-UI%E5%AF%BC%E8%88%AA%E5%86%99%E6%B3%95/nav1.png)

【参考】： [VUE elementUi导航写法](https://blog.csdn.net/weixin_42488404/article/details/83414761)

#### 方法二(加上图标的)：

```
<el-menu :default-active="$route.path" class="el-menu-vertical-demo" router>
    <el-menu-item v-for="(item, i) in items" :key="i" :index="item.path">
        <template>
            <i :class="item.icon"></i>
            <span slot="title"> {{ item.title }}</span>
        </template>          
    </el-menu-item>
</el-menu>
```
**data里面**：

```
items:[
    { 
        path:'/gameinfo/index',
        title:'基本信息',
        icon:'iconfont icon-info'
    },
    { 
        path:'/gameversion/index',
        title:'版本管理',
        icon:'iconfont icon-version'
    },
    { 
        path:'/gameplatform/index',
        title:'渠道管理',
        icon:'iconfont icon-channel'
    },
    { 
        path:'/gameproduct/index',
        title:'充值产品',
        icon:'iconfont icon-recharge'
    },
    { 
        path:'/gameplugin/index',
        title:'插件管理',
        icon:'el-icon-cpu'
    },
    { 
        path:'/package/index',
        title:'打包管理',
        icon:'iconfont icon-packageKit'
    },
    { 
        path:'/order/index',
        title:'订单查询',
        icon:'iconfont icon-orderQuery'
    },
    { 
        path:'/gameinfo/index',
        title:'切换至ios',
        icon:'iconfont icon-android'
    },
]
```
**效果如图所示：**
![导航栏跳转路由](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/Vue-js-Element-UI%E5%AF%BC%E8%88%AA%E5%86%99%E6%B3%95/nav2.png)

【参考】： [Vue框架Element UI教程-导航栏跳转路由（五）](https://www.jianshu.com/p/e24c37fb9e64)

#### 方法三（当前目录下的多个子页面选中时的高亮问题）：

![当前目录下的多个子页面选中时的高亮问题](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/Vue-js-Element-UI%E5%AF%BC%E8%88%AA%E5%86%99%E6%B3%95/nav3.png)
![当前目录下的多个子页面选中时的高亮问题](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/Vue-js-Element-UI%E5%AF%BC%E8%88%AA%E5%86%99%E6%B3%95/nav4.png)

**router/index.js文件的路由配置（特别关注activeMenu、apiActiveMenu的配置）：**

```
    {
      path: '/gameinfo/edit',
      name: 'GameEdit',
      component: GameEdit,
      meta: {
        title: '修改信息',
        activeMenu: '/gameinfo/index', // 主菜单 的 接口文档 高亮
        apiActiveMenu: '/gameinfo/edit' // 接口文档的子菜单高亮
      }
    },
```
**关键代码（在导航栏组件内写）：**

```
computed: {
    activeMenu() {
      const route = this.$route
      const { meta, path } = route
      // if set path, the sidebar will highlight the path you set
      if (meta.apiActiveMenu) { // 注意这里很重要
        return meta.activeMenu
      }
      return path
    }
}
```
【参考】： [elementui中NavMenu 导航菜单高亮问题——解决多种情况](https://blog.csdn.net/m0_38134431/article/details/94755527)