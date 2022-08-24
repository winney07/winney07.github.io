---
title: CSS笔记
date: 2022-08-21 17:29:52
tags:
- CSS
- 工作笔记
---



#### CSS选择器

1. id选择器
2. 类选择器
3. 标签选择器
4. 相邻选择器（+）
5. 子选择器（>）
6. 后代选择器（li a)
7. 通配符选择器（*）
8. 属性选择器（







#### Sass报错

如果按照了sass，使用`<style lang="scss" scoped>`时报错，原因可能是安装的sass版本是最新的，版本太高的原因，安装以下两个版本，再使用sass就不会报错。

```
"node-sass": "^4.12.0",
"sass-loader": "^8.0.2",
```

#### 引入字体图标

1. 使用cdn链接，在public目录下的`index.html`中引入`iconfont字体图标链接`

   ```
   <link rel="stylesheet" href="//at.alicdn.com/t/font_907707_neo27xdny5.css">
   ```

   > 登录账号——资源管理——我的项目——选中项目——选中“Font class”——复制链接——放到`public/index.html`	

2. 在页面中调用，要加上iconfont

   ```
   <i class="iconfont icon-IOS"></i>
   ```

   
