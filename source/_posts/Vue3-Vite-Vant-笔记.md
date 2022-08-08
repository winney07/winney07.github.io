---
title: Vue3-Vite-Vant-笔记
date: 2022-08-03 16:50:58
tags:
- Vue3
- Vite
- Vant
---

[vue3使用vite2移动端项目](https://zhuanlan.zhihu.com/p/351888882)

[vite px转rem (vite+vant+vue3 demo)](https://zhuanlan.zhihu.com/p/442732586)

注：如果是ts项目，postcss.config.js需重命名为postcss.config.cjs



[vite+vue3+ts+eslint编写移动端rem自适应](https://www.proyy.com/6956431101141352485.html#toc_3)



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



#### [Rem适配](https://vant-contrib.gitee.io/vant/#/zh-CN/advanced-usage#liu-lan-qi-gua-pei)

```
npm install postcss postcss-pxtorem --save-dev
```

```
npm i -S amfe-flexible
```

https://github.com/amfe/lib-flexible

> 由于`viewport`单位得到众多浏览器的兼容，`lib-flexible`这个过渡方案已经可以放弃使用，不管是现在的版本还是以前的版本，都存有一定的问题。建议大家开始使用`viewport`来替代此方。

#### [Viewport 布局](https://vant-contrib.gitee.io/vant/#/zh-CN/advanced-usage#viewport-bu-ju)—推荐

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

报错：

```
This file is being treated as an ES module because it has 
a '.js' file extension and 'H:\Gitee\Vue3_demo\vue3-vite-vant\package.json' contains "type": "module". To treat it as a CommonJS script, rename it to use the '.cjs' file extension.
```

解决：1.将`postcss.config.js`改为`postcss.config.cjs` ;  2.重启服务



### mock数据

[mockjs介绍](https://www.jianshu.com/p/d812ce349265)

https://github.com/nuysoft/Mock/wiki/Getting-Started

[mock官网](http://mockjs.com/)

[mock示例](http://mockjs.com/examples.html)

```
npm install mockjs --save-dev
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

   电脑的“设置”——“网络和共享中心”——“Windows Defender 防火墙”（左下角）——“启用或关闭Windows Defender 防火墙”（左侧）——选择“关闭”（专用网络和公用网络都关闭）

   注意：使用完，最好重新“启用”防火墙。

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



[活动规则背景图](http://136pic.com/muban/16118575.html)