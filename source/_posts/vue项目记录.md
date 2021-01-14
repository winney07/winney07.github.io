---
title: vue项目记录
date: 2020-05-26 16:35:23
tags:
- Vue.js
categories:
- 工作笔记
- Vue.js
---

### 在项目中引入阿里图库
1. 在阿里图库中，选好图标，建立好项目
2. 将整个项目的图标下载到本地解压
3. 在Vue.js项目的assets目录中，新建一个icon目录，将解压后文件夹里面的文件复制到这个目录下
4. 在main.js文件里引入iconfont.css, import '@/assets/icon/iconfont.css'
5. 在项目中引入图标的时候要加上iconfont类，然后再添加图标本身的类名

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
{% asset_img vue01.png %}
{% asset_img vue02.png %}
{% asset_img vue03.png %}
{% asset_img vue04.png %}
