---
title: 在Vue项目中使用sass的配置方法
date: 2020-03-19 18:00:05
tags: 
- Vue.js
categories: 
- 工作笔记
- Vue.js
---
#### 1、安装sass的依赖包

sass-loader依赖于node-sass
```
npm install sass-loader node-sass --save-dev 
```
#### 2、在build文件夹下的webpack.base.conf.js的rules里面添加配置
```
{
 test: /\.sass$/,
 loaders: ['style', 'css', 'scss']
}
```
<!-- more -->

```
module:{
	rules:[
		...
		{
			test: /\.scss$/,
			loaders:['style','css','sass']
		}
	]
}
```

#### 3、在APP.vue中修改style标签

```
<style lang="scss">
   $blue:red;
    .common-header{
        color: $blue;
    }
</style>

```
#### 4、运行项目
```
npm run dev
```

##### 注意：
如有以下报错，是版本的问题影响的：

Module build failed: TypeError: this.getResolve is not a function at Object.loader 安装node-sass运行报错

**解决方法**： 选择更低版本的sass-loader

**卸载当前版本**：npm uninstall sass-loader
**安装指定版本**：npm install sass-loader@7.3.1 --save-dev


参考： [安装node-sass运行报错](https://blog.csdn.net/ze1024/article/details/100516650)