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

#### [Viewport 布局](https://vant-contrib.gitee.io/vant/#/zh-CN/advanced-usage#viewport-bu-ju)

```
npm install postcss-px-to-viewport --save-dev
```

#### viewport布局的相关配置

在根目录添加`postcss.config.js`

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

