---
title: Vue3-Vite-Vant-笔记
date: 2021-11-03 16:50:58
tags:
- Vue3
- Vite
- Vant
categories:
- 前端开发框架
- Vue.js
---

[vue3使用vite2移动端项目](https://zhuanlan.zhihu.com/p/351888882)

[vite px转rem (vite+vant+vue3 demo)](https://zhuanlan.zhihu.com/p/442732586)

注：如果是ts项目，postcss.config.js需重命名为postcss.config.cjs



[vite+vue3+ts+eslint编写移动端rem自适应](https://www.proyy.com/6956431101141352485.html#toc_3)

[flex布局: 一行显示固定个数，换行展示](https://blog.csdn.net/weixin_52827704/article/details/123914911)

#### 创建项目

```
npm create vite@latest
```

```
√ Project name: ... vue3-vite-vant
√ Select a framework: » vue
√ Select a variant: » vue-ts
```

```
cd vue3-vite-vant
npm install
npm run dev
```

#### 使用vant

```
npm i vant
```

#### [按需引入组件（推荐）](https://vant-contrib.gitee.io/vant/#/zh-CN/quickstart#an-xu-yin-ru-zu-jian-tui-jian)

```
npm i unplugin-vue-components -D
```

##### 配置vite.config.ts

```
import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'
import Components from 'unplugin-vue-components/vite';
import { VantResolver } from 'unplugin-vue-components/resolvers';

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [
    vue(),
    Components({
      resolvers: [VantResolver()],
    }),
  ]
})

```

#### 引入vant的样式

```
import 'vant/lib/index.css';
```

##### 引入函数组件的样式

Vant 中有个别组件是以函数的形式提供的，包括 `Toast`，`Dialog`，`Notify` 和 `ImagePreview` 组件。在使用函数组件时，`unplugin-vue-components` 无法自动引入对应的样式，因此需要手动引入样式。

#### 使用方法1

##### 在 `<script setup>` 中可以直接使用 Vant 组件，不需要进行组件注册。

```
<script setup>
  import { Button } from 'vant';
</script>

<template>
  <Button />
</template>
```

#### 使用方法2

```
<script setup lang="ts">
</script>

<template>
  <div>
    <van-button type="primary">主要按钮</van-button>
    <van-button disabled type="primary">禁用状态</van-button>
  </div>
</template>
```

#### 移动端适配写法-设计稿尺寸（750*1624px）

[移动端设计规范和方法汇总](https://www.zcool.com.cn/article/ZODQ2Mzg0.html)

##### 一、rem写法

1.

```
html, body{
    font-size: 0.13333333vw;
}
```

2.元素在750宽的设计稿中，多少px，就写多少rem

##### 二、viewport插件的写法

元素在750宽的设计稿中，`*px`，就写`*/2px`  (要除以2)



#### [Rem适配](https://vant-contrib.gitee.io/vant/#/zh-CN/advanced-usage#liu-lan-qi-gua-pei)

```
npm install postcss postcss-pxtorem --save-dev
```

```
npm i -S amfe-flexible
```

https://github.com/amfe/lib-flexible

> 由于`viewport`单位得到众多浏览器的兼容，`lib-flexible`这个过渡方案已经可以放弃使用，不管是现在的版本还是以前的版本，都存有一定的问题。建议大家开始使用`viewport`来替代此方。

#### [Viewport 布局](https://vant-contrib.gitee.io/vant/#/zh-CN/advanced-usage#viewport-bu-ju)—推荐—本项目使用

```
npm install postcss-px-to-viewport --save-dev
```

#### viewport布局的相关配置

在项目根目录添加`postcss.config.cjs`

```
// postcss.config.js
module.exports = {
  plugins: {
    'postcss-px-to-viewport': {
      viewportWidth: 375,
    },
  },
};
```

`注意：添加完文件之后，要重启项目`

报错：

```
This file is being treated as an ES module because it has 
a '.js' file extension and 'H:\Gitee\Vue3_demo\vue3-vite-vant\package.json' contains "type": "module". To treat it as a CommonJS script, rename it to use the '.cjs' file extension.
```

解决：1.将`postcss.config.js`改为`postcss.config.cjs` ;  2.重启服务

#### 使用less

```
cnpm i less less-loader -D
```

##### 使用

```
<style lang='less' scoped>

</style>
```



#### 在main.ts中引入reset.less

```
import './assets/css/reset.less'
```

#### reset.less

```
/* http://meyerweb.com/eric/tools/css/reset/ 
   v2.0 | 20110126
   License: none (public domain)
*/

html, body, div, span, applet, object, iframe,
h1, h2, h3, h4, h5, h6, p, blockquote, pre,
a, abbr, acronym, address, big, cite, code,
del, dfn, em, img, ins, kbd, q, s, samp,
small, strike, strong, sub, sup, tt, var,
b, u, i, center,
dl, dt, dd, ol, ul, li,
fieldset, form, label, legend,
table, caption, tbody, tfoot, thead, tr, th, td,
article, aside, canvas, details, embed, 
figure, figcaption, footer, header, hgroup, 
menu, nav, output, ruby, section, summary,
time, mark, audio, video {
	margin: 0;
	padding: 0;
	border: 0;
	// font-size: 100%;
	// font: inherit;
	vertical-align: baseline;
}
/* HTML5 display-role reset for older browsers */
article, aside, details, figcaption, figure, 
footer, header, hgroup, menu, nav, section {
	display: block;
}
body {
	line-height: 1;
}
ol, ul {
	list-style: none;
}
blockquote, q {
	quotes: none;
}
blockquote:before, blockquote:after,
q:before, q:after {
	content: '';
	content: none;
}
table {
	border-collapse: collapse;
	border-spacing: 0;
}
```

#### 配置手机可访问本地电脑项目

[Vite 使用本地ip+localhost访问服务](http://www.manongjc.com/detail/29-saiyfskdbsqqcmz.html)

使用vite新建的项目默认访问链接：http://127.0.0.1:5173/

1. 修改`vite.config.js`文件，添加`server`配置

   ```
   server: {
       host: '0.0.0.0',
       port: 8888,
       open: true
   },
   ```

   ```
   export default defineConfig({
     plugins: [vue()],
     base:'./',    // 处理打包后放正式环境的相对路径的问题
     server: {		// 处理使用本地ip访问页面
       host: '0.0.0.0',
       port: 8888,
       open: true
     },
   })
   ```

2. 若使用手机访问本地ip页面，访问不成功（显示“服务器已停用”）。即要将本地电脑的防火墙“关闭”即可。[手机和电脑连接同一wifi,手机访问不了电脑起的项目](https://blog.csdn.net/zoepriselife316/article/details/117957732)

   2.1电脑的“设置”——“网络和共享中心”——“Windows Defender 防火墙”（左下角）——“启用或关闭Windows Defender 防火墙”（左侧）——选择“关闭”（专用网络和公用网络都关闭）

   `注意：使用完，最好重新“启用”防火墙。`
   
   2.2 如果手机连接的当前wifi那里的`HTTP代理`-`配置代理`是开启的，将其关闭

[vite.config.js之resolve.alias配置](https://www.jianshu.com/p/dd26cae7d7b2)





#### [vue实现动态改变title](https://www.dianjilingqu.com/161326.html)



#### [自定义主题颜色](https://vant-contrib.gitee.io/vant/#/zh-CN/config-provider#zi-ding-yi-css-bian-liang)

1.

```
 import { ConfigProvider } from 'vant';
```

2.

```
<van-config-provider :theme-vars="themeVars">
    <van-nav-bar
    title="红包活动"
    left-arrow
    @click-left="onClickLeft"
    />
</van-config-provider>
```

3.

```
const themeVars = {
    navBarBackgroundColor: '#555',
    navBarTitleTextColor: '#fff',
    navBarIconColor: '#fff',
};
```

> 原来：background: var(--van-nav-bar-background-color);
>
> 自定义写法：navBarBackgroundColor，会转换成--van-nav-bar-background-color



#### [样式覆盖报错处理](https://blog.csdn.net/m0_51431448/article/details/123003864)

```
[@vue/compiler-sfc] the >>> and /deep/ combinators have been deprecated. Use :deep() instead.
```

在Vue2中 我们经常使用 **>>>** 或 **/deep/** 样式穿透 修改[elementui](https://so.csdn.net/so/search?q=elementui&spm=1001.2101.3001.7020)里面的样式

但是Vue3中 弃用了 **>>>** 和 **/deep/** 使用 **:deep()** 代替

```
/deep/ .van-cell__title{
    span{
        font-weight: bold;
    }
}
 /deep/ .van-cell__left-icon{
    color: red;
    font-size: 30px;
}
```

改为：

```
:deep(.van-cell__title){
    span{
        font-weight: bold;
    }
}
:deep(.van-cell__left-icon){
    color: red;
    font-size: 30px;
}
```

#### [路由配置](https://router.vuejs.org/installation.html)

1.安装

```
npm install vue-router@4
```

2.src目录中新建router目录，新建index.ts

```
import {createRouter, createWebHashHistory} from 'vue-router'
import RedPacket from '../pages/redPacket/index.vue';
import Withdraw from '../pages/Withdraw/index.vue'

const routes = [
    { 
        path: '/',
        component: RedPacket,
        meta: {
            title: '红包活动'
        }
    },
    { 
        path: '/withdraw',
        component: Withdraw,
        meta: {
            title: '提现'
        }
    },
]

const router = createRouter({
    history: createWebHashHistory(),
    routes, 
})

export default router;
```

3.修改mian.ts

```
import router from './router';

app.use(router);
```

4.App.vue

```
<template>
   <router-view></router-view>
</template>
```

#### 动态修改页面Title

```
router.beforeEach((to, from) => {
    // 动态修改页面title
    if (to.meta.title) {
        document.title = to.meta.title  as string;
    }
})
```

#### 页面跳转组件-router-link

```
<router-link to="/withdraw">
    <van-button color="#fe8124" plain size="small"> 
    提现
    </van-button>
</router-link> 
```

#### 自定义主题放在App.vue

```
<script setup lang="ts">
import { ConfigProvider } from 'vant';
// 自定义主题颜色
  const themeVars = {
      navBarBackgroundColor: '#555',
      navBarTitleTextColor: '#fff',
      navBarIconColor: '#fff',
      cellHorizontalPadding: '8px'
  };
</script>

<template>
  <div>
    <van-config-provider :theme-vars="themeVars">
      <router-view></router-view>
    </van-config-provider>
  </div>
</template>

<style  scoped>

</style>
```

#### 父子组件传值-defineProps

参考：[vue3：语法糖内的defineProps及defineEmits、defineExpose](https://blog.csdn.net/skyblacktoday/article/details/120879677)

属性：

1.

```
const props =  defineProps({
    title: String,
})
```

2. 采用ts专有声明，无默认值

```
const props =  defineProps<{ // 采用ts专有声明，无默认值
    title: string,
}>()
```

3. 采用ts专有声明，有默认值

```
interface Props {
    title?: string
}
const props = withDefaults(defineProps<Props>(), {
    title: '首页',
})
```



##### 子组件：

```
<van-nav-bar
    :title="props.title"
    left-arrow
    @click-left="onClickLeft"
/>

const props =  defineProps({
    title: String,
})
或带默认值
const props =  defineProps({
    title: {
        type: String,
        default: '红包活动'
    }
})
```

##### 父组件：

```
<!-- 顶部导航 -->
<TopNav :title="'提现'"/>


<!-- 顶部导航 -->
<TopNav :title="'红包活动'"/>
```

`注意：如果传值是字符串要加上单引号(:title="'红包活动'")，否则不生效`

##### 或使用变量：

```
import { ref } from 'vue';
const title = ref('红包活动')

<!-- 顶部导航 -->
<TopNav :title="title"/>
```

#### 子组件传父组件-defineEmits

##### 子组件：

```
<van-nav-bar
    left-arrow
    :right-text="props.rightText"
    @click-right="onClickRight"
/>
const $emit = defineEmits(['navRightClick'])
// 导航栏右侧按钮点击
const onClickRight = () => {
    $emit('navRightClick')
};

const props =  defineProps({
    rightText: String
})
```

##### 父组件：

```
 <TopNav :title="'提现'" :rightText="'提现明细'" @navRightClick="handleRightClick"/>
```

```
const handleRightClick = () => {
    console.log("点击右侧按钮")
}
```

#### 编程式路由跳转

```
import { useRouter } from 'vue-router'

const router = useRouter()
const handleRightClick = () => {
     router.push('/')
}
```

#### 导航栏父子传值-也可改为插槽的用法

##### 子组件：

```
<van-nav-bar
    :title="props.title"
    left-arrow
    @click-left="onClickLeft"
>
   <template #right>
        <slot></slot>
    </template>
</van-nav-bar>
```

不能写：

```
<van-nav-bar
    :title="props.title"
    left-arrow
    @click-left="onClickLeft"
>
    <slot></slot>      // 这样写不起作用
</van-nav-bar>
```

##### 父组件：

```
<TopNav :title="'提现'">
   <router-link to="/withdraw/detail">红包明细</router-link>
</TopNav>
```

或：

```
<TopNav :title="'提现'">
   <span @click="handleRightClick">红包明细</span>
</TopNav>


const router = useRouter()
const handleRightClick = () => {
    console.log('跳转')
     router.push('/withdraw/detail')
}
```





#### Vite热更新的开启

vite.config.ts：

```
server: {
    hmr: true,    // 开启热更新
}
```

参考：[vite热更新（vue3）](https://blog.csdn.net/weixin_45369499/article/details/125158995)   | [Vite 是如何做热更新的](https://blog.csdn.net/wanglaotou88/article/details/124708297)

`项目的热更新存在延迟，每次都要重启项目`

做了以上配置还是不起作用：

原因：组件引入的路径大小写写错

```
import Withdraw from '../pages/Withdraw/index.vue';
```

解决：将`Withdraw`改为`withdraw`即可

```
import Withdraw from '../pages/withdraw/index.vue';
```

参考：[Vue Vite热更新不起作用的正确解决办法](https://www.jb51.net/article/240873.htm)

> 提示：文件夹名称严格注意大小写
>
> router 路由中名称 和文件夹(目录), 文件名需要保证大小写一致

#### [‘v-model’ directives require no argument](https://blog.csdn.net/weixin_48952990/article/details/125387578)

解决方法：
解决方法：
在VScode中，打开 “文件>首选项>设置” 找到右侧用户设置
搜索vetur.validation,找到下面这句

```
"vetur.validation.template": true  
```


将true改成false

//如果没有可以直接添加该句 （将检查关闭）

```
"vetur.validation.template": false
```

#### [vue3：复制功能（vue-clipboard3）](https://blog.csdn.net/qq_40745143/article/details/123688798)

```
npm install --save vue-clipboard3
```

```
import useClipboard from 'vue-clipboard3'
import { Toast } from 'vant';
import 'vant/es/toast/style';

// 复制绑定码
const { toClipboard } = useClipboard()
const copy = async (val:string) => {
   try {
      await toClipboard(val)
      console.log('Copied to clipboard')
      Toast.success('复制成功');
   } catch (e) {
      console.error(e)
   }
   show.value = false;  // 关闭弹窗
}
```

```
 <van-button color="#fe7c1a" @click="copy('bcJcB9')">复制并前往绑定</van-button>
```

#### 

#### [页面布局](https://vant-contrib.gitee.io/vant/#/zh-CN/col)

![layout布局](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/Vue3-Vite-Vant-%E7%AC%94%E8%AE%B0/note1.png)



左右有padding，元素之间间距相等（加`gutter="15"`），元素宽度一样(`span="6"`)，换行（每行相加够24）

```
<van-row justify="space-between" gutter="15">
    <van-col span="6" class="active">
        <van-button type="primary" size="small">2元</van-button>
    </van-col>
    <van-col span="6">
        <van-button type="primary" size="small">5元</van-button>
    </van-col>
    <van-col span="6">
        <van-button type="primary" size="small">10元</van-button>
    </van-col>
    <van-col span="6">
        <van-button type="primary" size="small">2元</van-button>
    </van-col>

    <van-col span="6">
        <van-button type="primary" size="small">2元</van-button>
    </van-col>
    <van-col span="6">
        <van-button type="primary" size="small">2元</van-button>
    </van-col>
    <van-col span="6">
        <van-button type="primary" size="small">2元</van-button>
    </van-col>
    <van-col span="6">
        <van-button type="primary" size="small">2元</van-button>
    </van-col>
</van-row>
```

`注：这样写，按钮看起来还是不平均配分,因没有给按钮设置宽度（width: 100%;`

```
.van-button{
    width: 100%;
    border-radius: 5px;
    margin-bottom: 18px;
    background-color: #ffd898;
    border-color: #ffd898;
}
.active{
    .van-button{
        background-color: #ffab22;
        border-color: #ffab22;
    }
}
```

#### 动态绑定class

`:class`

```
:class="{active: amount === i.amount}
```

### mock数据

1. vite-plugin-mock
2. mockjs
3. axios

[mockjs介绍](https://www.jianshu.com/p/d812ce349265)

https://github.com/nuysoft/Mock/wiki/Getting-Started

[mock官网](http://mockjs.com/)

[mock示例](http://mockjs.com/examples.html)

#### 步骤：

##### 1.安装

```
npm i vite-plugin-mock mockjs  -D
```

**[vite-plugin-mock](https://github.com/vbenjs/vite-plugin-mock)**

[使用](https://github.com/vbenjs/vite-plugin-mock#usage)

##### 2.在vite.config.ts中引入

```
import { viteMockServe } from 'vite-plugin-mock'

plugins: [
  vue(),
  viteMockServe({
    // default
    mockPath: 'mock',
  }),
],
```

##### 3.在项目根目录新建mock目录-mock/index.ts：

[示例](https://github.com/vbenjs/vite-plugin-mock#mock-file-example)

```
// test.ts
import { MockMethod } from 'vite-plugin-mock'
export default [
  {
    url: '/api/get',
    method: 'get',
    response: ({ query }) => {
      return {
        code: 0,
        data: {
          name: 'vben',
        },
      }
    },
  },
  {
    url: '/api/post',
    method: 'post',
    timeout: 2000,
    response: {
      code: 0,
      data: {
        name: 'vben',
      },
    },
  },
  {
    url: '/api/text',
    method: 'post',
    rawResponse: async (req, res) => {
      let reqbody = ''
      await new Promise((resolve) => {
        req.on('data', (chunk) => {
          reqbody += chunk
        })
        req.on('end', () => resolve(undefined))
      })
      res.setHeader('Content-Type', 'text/plain')
      res.statusCode = 200
      res.end(`hello, ${reqbody}`)
    },
  },
] as MockMethod[]
```

##### 4.安装axios

```
npm i axios
```

##### 5.使用

```
import axios from 'axios'

async function fn() {
  const { data } = await axios.get('/api/get')
  console.log(data);
}
fn()
```

##### 6.使用mock来模拟更多数据

##### 7.将mock模拟的数据放到接口返回中

mock/index.ts：

```
// test.ts
import { MockMethod } from 'vite-plugin-mock'
import Mock from 'mockjs'
var list = Mock.mock({
  // 20条数据
  "data|20": [{
    // 商品种类
    "goodsClass": "女装",
    // 商品Id
    "goodsId|+1": 1,
    //商品名称
    "goodsName": "@ctitle(10)",
    //商品地址
    "goodsAddress": "@county(true)",
    //商品等级评价★
    "goodsStar|1-5": "★",
    //商品图片
    "goodsImg": "@Image('100x100','@color','小甜甜')",
    //商品售价
    "goodsSale|30-500": 30

  }]
})
export default [
  {
    url: '/api/get',
    method: 'get',
    response: ({ query }) => {
      return {
        code: 0,
        data: list
      }
    },
  },
  },
] as MockMethod[]
```

使用示例：

```
import Mock from 'mockjs'

// 定义数据类型
var data = Mock.mock({
  // 20条数据
  "data|20": [{
    // 商品种类
    "goodsClass": "女装",
    // 商品Id
    "goodsId|+1": 1,
    //商品名称
    "goodsName": "@ctitle(10)",
    //商品地址
    "goodsAddress": "@county(true)",
    //商品等级评价★
    "goodsStar|1-5": "★",
    //商品图片
    "goodsImg": "@Image('100x100','@color','小甜甜')",
    //商品售价
    "goodsSale|30-500": 30

  }]
})
// 输出结果随机生成的数据（node index.js）
 console.log(data);
```

[vue项目，svn提交代码时忽略node_modules文件夹提交](https://www.jianshu.com/p/d8ca41e9bce4)

##### 8.将数据和接口方法分开

mock/data.ts：

```
import Mock from 'mockjs'

// mock的数据
// 金额列表
export const amountList = Mock.mock({
    // 20条数据
    "amountList": [{
      "amount": 2,
      "amountId": 0,
    },
]
})
```

mock/index.ts：

```
import { MockMethod } from 'vite-plugin-mock'
import { amountList } from './data.js'

export default [
    {
      url: '/api/getAmountList',
      method: 'get',
      response: ({ query }) => {
        return {
          code: 0,
          data: amountList,
        }
      },
    },
] as MockMethod[]
```

#### reactive的做法

```
// reactive的做法
import { reactive, toRefs } from 'vue';
const userinfo = reactive({
    name: '',
    level: 0,
    server_area: ''
})
const {name, level, server_area} = toRefs(userinfo)
axios.get('/api/getUserInfo').then(res => {
    const { name, level, server_area } =  res.data.data.userInfo
    userinfo.name = name;
    userinfo.level = level;
    userinfo.server_area = server_area;
})
```

#### ref的做法

```
import { ref } from 'vue';
// ref的做法
const name = ref('');
const server_area = ref('');
const level = ref(0)
axios.get('/api/getUserInfo').then(res => {
    const userinfo = res.data.data.userInfo;
    name.value = userinfo.name;
    level.value = userinfo.level;
    server_area.value = userinfo.server_area;
})
```

#### 枚举的使用-enum

```
// 枚举
enum HbType {
    '等级红包' = 1,
    '充值红包' ,
    '高级红包' ,
}
enum HbIcon {
    'src/assets/images/hb_level.png' = 1,
    'src/assets/images/hb_charge.png' ,
    'src/assets/images/hb_senior.png' ,
}
```

##### 数据

```
// 红包数据
// type:1 --等级红包
// type:2 --充值红包
// type:3 --高级红包
export const hbData = Mock.mock({
    hbData: {
        total: 300.00,
        list: [{
            id: 10001,
            type: 1,
            amount: 50,
        },{
            id: 10001,
            type: 2,
            amount: 100,
        },{
            id: 10001,
            type: 3,
            amount: 150,
        }]
    }
})
```

##### 页面

```
import axios from 'axios';
import { ref } from 'vue'

const hbList = ref([]);
axios.get('/api/getHbData').then(res => {
    hbList.value.push(...res.data.data.hbData.list);
    console.log(hbList)
})

// 结构
<van-cell 
    class="withdraw-li"
    :title="'+ ' + i.amount +'元'"
    :label="HbType[i.type]"
    center 
    v-for="i in hbList"
    :key="i.id"
>  
    <template #icon>
        <img :src="HbIcon[i.type]" class="red-packet" alt="">
    </template>
    <template #value>
        <router-link to="/withdraw">提现 &gt;</router-link>
    </template>
</van-cell>
```



#### 解决报错信息

控制台报以下警告信息：

```
Added non-passive event listener to a scroll-blocking ‘touchstart‘ event. Consider marking event...
```

解决：

```
// 安装插件
npm install -S default-passive-events
// 在main.js引入
import 'default-passive-events'
```

[参考](https://blog.csdn.net/yjl13598765406/article/details/125496865)



#### 打包报错

`注意： 写v-for循环时，要对循环的列表进行判断，以免数据还没有返回就进行渲染，获取不到值`

```
 <div class="content" v-if="list.length > 0">
 </div>
```

`Property 'id' does not exist on type 'never'.`

解决：加上类型限制

```
 interface List {
    amount: number;
    date: string
    id: number
    type: number
 }
 const list = ref<List[]>([])
```

