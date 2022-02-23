---
title: Hexo + NexT主题博客相关设置
date: 2018-08-02 14:28:04
tags:
- Hexo
categories: 
- 工作笔记
- Hexo
---
## 一、添加文章版权声明功能
打开博客目录下的主题配置文件（/themes/next/_config.yml），找到Declare license on posts 标签，进行配置：
```bash
# Declare license on posts
post_copyright:
  enable: true    #激活版权声明模块
  license: CC BY-NC-SA 3.0     #版权许可协议
  license_url: https://winney07.github.io/      #声明的文章的可点击链接（域名）
  ```
配置完后，执行以下命令，在浏览器中访问，效果如图所示：
![版本声明设置](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/Hexo-NexT%E4%B8%BB%E9%A2%98%E5%8D%9A%E5%AE%A2%E7%9B%B8%E5%85%B3%E8%AE%BE%E7%BD%AE/next-set1.png)
<!--more-->
## 二、设置favicon图标
1、选择一个favicon制作网站完成制作，例如：{% link 比特虫  http://www.bitbug.net/ %} ，制作一个16*16，一个32*32的；
2、两个不同尺寸大小的文件，重名为favicon-16x16-next.png和favicon-32x32-next.png；
2、将重命名的两个图片文件放到博客目录下的themes/next/source/images中（覆盖原来的两个默认的）
如图所示：
![设置favicon图标](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/Hexo-NexT%E4%B8%BB%E9%A2%98%E5%8D%9A%E5%AE%A2%E7%9B%B8%E5%85%B3%E8%AE%BE%E7%BD%AE/favicon.png)
## 三、添加头像
1、把想要设置的头像图片放到hexo/themes/next/source/images目录下;
2、在hexo/themes/next/layout/_macro目录中找到sidebar.swig文件;
3、在sidebar.swig文件中找到类名为：site-overview-wrap sidebar-panel sidebar-panel-active的section标签，进行如图所示的修改：
![添加头像](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/Hexo-NexT%E4%B8%BB%E9%A2%98%E5%8D%9A%E5%AE%A2%E7%9B%B8%E5%85%B3%E8%AE%BE%E7%BD%AE/user-head.png)
效果如图所示：(若想去掉边框，可以根据头像标签的类名，全局搜索，找到对应的样式进行修改)
![修改头像样式](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/Hexo-NexT%E4%B8%BB%E9%A2%98%E5%8D%9A%E5%AE%A2%E7%9B%B8%E5%85%B3%E8%AE%BE%E7%BD%AE/user-header.png)
## 四、添加友情链接
打开主题配置文件（/themes/next/_config.yml），找到以下内容进行修改：
```bash
# Blog rolls
links_icon: link
links_title: 友情链接 
# links_layout: block   //块状显示（选择了行内显示，这个要注释掉，不然会报错）
links_layout: inline    //行内显示
links:
  小超: https://www.xiaochao.me/
  Github: https://www.github.com
```
如图所示：
![添加友情链接](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/Hexo-NexT%E4%B8%BB%E9%A2%98%E5%8D%9A%E5%AE%A2%E7%9B%B8%E5%85%B3%E8%AE%BE%E7%BD%AE/friend-link.png)

## 五、调整hexo页面宽度
博客在浏览器上的留白太多，因此想增加文章的宽度。

打开/Hexo/themes/hexo-theme-next/source//css/_variables/custom.styl 添加两行代码即可：
```
$main-desktop = 1400px 
$content-desktop = 1100px
```