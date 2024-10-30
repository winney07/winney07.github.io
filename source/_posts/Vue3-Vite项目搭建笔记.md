---
title: Vue3-Vite项目搭建笔记
date: 2020-07-29 10:53:07
tags:
- Vue3
- Vite
categories:
- 前端开发框架
- Vue.js
---

[Vite官网](https://vitejs.dev/)

[Vite中文官网](https://vitejs.cn/)

安装Vuter，有代码提示

> Vite requires [Node.js](https://nodejs.org/en/) version 14.18+, 16+

```
node -v
```

#### [创建项目](https://vitejs.dev/guide/#scaffolding-your-first-vite-project)

```
npm create vite@latest
```

```
Ok to proceed? (y) y
√ Project name: ... Vue3_mobile
√ Package name: ... vue3-mobile
√ Select a framework: » vue
√ Select a variant: » vue-ts
```

```
cd Vue3_mobile
npm install   
npm run dev
```

或

```
npm init vite@latest
```

```
√ Project name: ... vue_mobile
√ Select a framework: » vue
√ Select a variant: » vue-ts
```

```
cd vue_mobile
npm install
npm run dev
```



#### [几款实用的VUE移动端UI框架](https://wenku.baidu.com/view/c4b466ee5cbfc77da26925c52cc58bd6318693d5.html)

- [Vant](https://vant-contrib.gitee.io/vant/#/zh-CN) （有赞）
- [NutUI](https://nutui.jd.com/#/)   (京东)
- [Mint-ui](http://mint-ui.github.io/docs/#/)
- [Vux](https://doc.vux.li/zh-CN/vux-loader/plugins.html)  （微信风格）
- [vonic](https://vonic.ai/#features)

#### [vue3+vite的项目如何将打包后的绝对路径改为相对路径](https://blog.csdn.net/zy21131437/article/details/125861170)

在vue3+vite的项目中，配置文件名为 **`vite.config.js`**，如果没有就在[根目录](https://so.csdn.net/so/search?q=根目录&spm=1001.2101.3001.7020)下新建一个，文件名固定为：**`vite.config.js`**，然后在里面加上base属性，设置值为 `"./"`，如下：

```
import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [vue()],
  base: './'
})
```

如果不是用Vite的，[vue cli3.x打包后如何修改生成的静态资源的目录和路径](https://www.jb51.net/article/243243.htm)



### 移动端1px的问题

1px可以不转换为rem



### 移动端vm与rem适配

1. 将根元素的`font-size`设置为`font-size: 0.13333333vw;`
2. 这样就是1rem = 1px；写样式的时候，多少px就写多少rem

参考博客：

[最简单的移动端适配方案（vw/rem）](https://blog.csdn.net/qq_38990451/article/details/107382146?app_version=5.6.1&csdn_share_tail={"type"%3A"blog"%2C"rType"%3A"article"%2C"rId"%3A"107382146"%2C"source"%3A"winney07"}&ctrtid=M0aIM&utm_source=app)

[最简单的移动端适配方案(rem+vw)](https://blog.csdn.net/sky2714/article/details/80849863?app_version=5.6.1&csdn_share_tail={"type"%3A"blog"%2C"rType"%3A"article"%2C"rId"%3A"80849863"%2C"source"%3A"winney07"}&ctrtid=keW0g&utm_source=app)



#### 关于字体的适配-[文本字号不建议使用`rem`](https://github.com/amfe/article/issues/17)

> 现在绝大多数的字体文件都自带一些点阵尺寸，通常是`16px`和`24px`，所以我们**不希望出现`13px`和`15px`这样的奇葩尺寸**。

所以可以使用媒体查询，根据不同的dpr，设置不一样的字体大小

```
p {
    font-size: 12px; 
    line-height: 1.5;
}
@media(-webkit-min-device-pixel-ratio:2),(min-device-pixel-ratio:2){
   p {
      font-size: 24px;
  }
}

@media(-webkit-min-device-pixel-ratio:3),(min-device-pixel-ratio:3){
   p {
      font-size: 36px;
  }
}
```

github上使用下面这种，但好像不起作用

```
[data-dpr="2"] p {
    font-size: 24px;
}
[data-dpr="3"] p {
    font-size: 36px;
}
```

### svg的使用

```
<link rel="icon" type="image/svg+xml" href="/vite.svg" />
```

