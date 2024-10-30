---
title: vue项目记录
date: 2020-05-26 16:35:23
tags:
- Vue.js
categories:
- 前端开发框架
- Vue.js
---

### 在项目中引入阿里图库
1. 在阿里图库中，选好图标，建立好项目
2. 将整个项目的图标下载到本地解压
3. 在`Vue.js`项目的`assets`目录中，新建一个icon目录，将解压后文件夹里面的文件复制到这个目录下
4. 在`main.js`文件里引入`iconfont.css`, `import '@/assets/icon/iconfont.css'`
5. 在项目中引入图标的时候要加上`iconfont`类，然后再添加图标本身的类名

### 链接文字的写法(路由跳转)
##### 不传参
```
声明式：<router-link :to="{name:'index'}}">    或者    <router-link to='/index'>

编程式：router.push(...)
方法一: this.$router.push({path:'路径')};
方法二：this.$router.push({name:'组件名')};
```

##### 传参
```
声明式：<router-link :to="{name:'index',query:{id:'xxx',name:'xxx'}}">
编程式：router.push(...)

方法一：this.$router.push({path:'xxx',query:{aa:xx, bb: xx}});   //带查询参数，类似于 “？” 的形式传值

方法二：this.$router.push({path:'xxx',params:{aa:xx, bb: xx}}); 

注：以上两种方法的query跳转路径也可以写成name:'组件名'的形式

在query中放入需要传递的参数即可，多个参数之间用逗号隔开；

取值：this.$route.query.xx   (可在跳转的页面取得所传递的值)；
```

### 路由
```
component: () => import('@/views/dashboard/console/index.vue'),
可以简写为：
component: () => import('@/views/dashboard/console'),
```

### Vue.js 组件中绑定点击事件不生效的解决方法
在使用组件（比如 element UI）的过程中，会发现无法通过 @click 绑定标签的点击事件。

因为 Vue.js 使用的是一套自己的事件传递机制，所以我们需要添加 @click.native 来绑定 DOM 原生事件。
```
<el-dropdown-item icon="el-icon-unlock" @click.native="resetPass"></el-dropdown-item>
```

### Vuex的store的使用
注意：改变store值，要使用mutations，不要直接改变
store.js文件：
```
export default new Vuex.Store({
  state: {
    isCollapse: false,
    isMobile: false
  },
  mutations: {
    toggleCollapse(state) {
      state.isCollapse =  !state.isCollapse;
    }
  },
})
```
#### 在页面中的使用：
```
在页面中引入：
import { mapState , mapMutations } from 'vuex';

引入state：
computed: {
  ...mapState(['isCollapse','isMobile'])
},

引入方法：
methods: {
  ...mapMutations(['toggleCollapse'])
}

页面结构中，直接使用：
:class="{'sider-collapse':isCollapse}"

在事件中直接使用：
this.toggleCollapse();

如果要传参：
this.toggleCollapse({
  param: this.isCollapse
});

```

### $emit的使用
通过 Event Bus 进行组件间通信，来折叠侧边栏

bus.js:
```
import Vue from 'vue';

// 使用 Event Bus
const bus = new Vue();

export default bus;
```
```
在点击事件的组件中：
引入：
import bus from '../public/bus';

页面结构中：
@click="collapseChage"
v-show="!isCollapse"

数据，方法：
data() { 
  return {
      isCollapse: false,
  }
},
methods: {
  // 侧边栏折叠
  collapseChage() {
      this.isCollapse = !this.isCollapse;
      bus.$emit('toggleCollapse', this.isCollapse);
  },
}

在需要用到这个状态的组件中：
引入：
import bus from '../public/bus';
数据：
data() { 
  return {
      isCollapse: false,
  }
},

页面结构：
:class="{'content-collapse':isCollapse}"

监听toggleCollapse事件：
created() {
  bus.$on('toggleCollapse', msg => {
      this.isCollapse = msg;
  });
}

```
### 如何将element-ui中的表格和分页器连接起来

```
<el-table 
    :data="tableData.slice((query.pageIndex - 1)*query.pageSize, query.pageIndex * query.pageSize)"
    border
    class="table"
    ref="multipleTable"
    header-cell-class-name="table-header"
    @selection-change="handleSelectionChange"
>
	<el-table-column type="selection" width="55" align="center"></el-table-column>
    <el-table-column prop="id" label="ID" width="55" align="center"></el-table-column>
    <el-table-column prop="name" label="用户名" ></el-table-column>
    <el-table-column label="账户余额" >
    	<template slot-scope="scope">￥{{scope.row.money}}</template>
    </el-table-column>
</el-table>

<div class="pagination" >
    <el-pagination
        background
        @size-change="handleSizeChange"
        @current-change="handleCurrentchange"
        :current-page="query.pageIndex"
        :page-sizes="[10, 15, 20, 30]"
        :page-size="query.pageSize
        layout="total, sizes, prev, pager, next, jumper"
        :total="pageTotal">
    </el-pagination>
</div> 


export default{
	name :'basetable',
    data() {
        return (
            query:{
                address:'',
                name:'',
                pageIndex:1,   // 当前页
                pageSize: 10,	// 每页显示条数
                tableData: [],
             }
        }
     },
     // 分页导航
     handleCurrentChange(val) {
        this.$set(this.query,'pageIndex', val);
        this.getData();
     },
     handleSizeChange(val) {
        this.$set(this.query,'pageSize', val);
        this.getData();
     }
}
```

#### 在vue项目中使用sass的配置方法

##### 1、安装sass的依赖包

`sass-loader依赖于node-sass`

```
npm install sass-loader node-sass --save-dev
```

##### 2、在build文件夹下的webpack.base.conf.js的rules里面添加配置

```
{
 test: /\.sass$/,
 loaders: ['style', 'css', 'scss']
}
```

如下图所示：



##### 3、在APP.vue中修改style标签

```
<style lang="scss">
   $blue:red;
    .common-header{
        color: $blue;
    }
</style>
```

##### 4、运行项目

```
npm run dev
```

##### `注意：`

如有以下报错，是版本的问题影响的：

`Module build failed: TypeError: this.getResolve is not a function at Object.loader 安装node-sass运行报错`

- **解决方法**： 选择更低版本的sass-loader
- **卸载当前版本**：npm uninstall sass-loader
- **安装指定版本**：npm install sass-loader[@7.3.1 ]() --save-dev 

参考： [安装node-sass运行报错](https://blog.csdn.net/ze1024/article/details/100516650)

#### Vue项目设置每个页面的title

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

##### 4、在每个vue页面中加入 

```
 <div class="content content-box">
      <div v-wechat-title="$route.meta.title"></div>
</div>
```

###### 【参考】： [vue项目设置每个页面的title](https://www.cnblogs.com/itgezhu/p/10817502.html)

#### Vue.js + ElementUI导航写法

##### 方法一（基本的）：

> ElementUI导航通常会和vue-router一起使用，所以与官网的示例的写法不太一样。具体写法如下:

```plain
<el-menu :default-active="$route.path" class="el-menu-vertical-demo" router>
   <el-menu-item v-for="item in items" :index="item.src">{{item.name}}            
   </el-menu-item>
 </el-menu>
```

**data里则是正常的数据即可：**

```plain
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

【参考】： [VUE elementUi导航写法](https://blog.csdn.net/weixin_42488404/article/details/83414761)

##### 方法二(加上图标的)：

```plain
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

```plain
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