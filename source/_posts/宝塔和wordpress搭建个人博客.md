---
title: 宝塔和wordpress搭建个人博客
date: 2022-08-04 16:48:21
tags:
- 云服务器
categories:
- 云服务器
---



## 使用宝塔和wordpress搭建个人博客



### 1.宝塔的安装

#### 1.1安装方式

1. [编程导航](https://www.code-nav.cn/) 搜”宝塔“
2. 选择"**Linux面板**"（[选择安装](https://www.bt.cn/new/download.html) ）
3. 选“安装脚本”
4. 复制 “**Centos安装脚本**” 的代码
5. 粘贴命令，直接安装【在git上登录服务器，切换到opt目录（cd /opt）】
6. 把面板地址和用户名密码记住



#### 1.2 8888端口不可以访问-要做以下两个配置

1. ##### 在腾讯云控制台，配置安全组

   ![配置安全组](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/%E6%9C%8D%E5%8A%A1%E5%99%A8%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2/image.png)

2. ##### 在腾讯云控制台，配置防火墙

   ![配置防火墙](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/%E6%9C%8D%E5%8A%A1%E5%99%A8%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2/image2.png)



### 2.登录面板地址后

#### 2.1注册宝塔账号

#### 2.2安装推荐套件（使用默认推荐即可）

`备注：安装LNMP(推荐)`

![配置防火墙](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/%E6%9C%8D%E5%8A%A1%E5%99%A8%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2/image3.png)



### 3.网站-添加站点



### 4. WordPress安装

`备注：1.先把刚建的站点删除，以免冲突； `

4.1[wordpress官网](https://wordpress.org/download/)下载安装包（ .tar.gz格式的）

4.2将 .tar.gz文件上传到站点根目录

4.3鼠标放上 .tar.gz文件，选择“解压”

4.4进入解压后的文件夹，将里面的文件全部复制到站点根目录

4.5安装包和解压后的文件夹可以删掉了



[宝塔wordpress安装及使用（宝塔wordpress建站教程）](https://blog.csdn.net/qq_33468857/article/details/124652515)

[宝塔面板安装wordpress详细教程](https://blog.csdn.net/JunyouYH/article/details/123448276)



#### 添加子域名

在阿里云-控制台-域名解析-解析设置，添加记录值

`注：需要等10分钟，才生效`





#### [VuePress](https://vuepress.vuejs.org/zh/)

[极简静态网站生成器](https://github.com/vuejs/vuepress/tree/master/packages/%40vuepress/core)



可以直接 云开发

https://github.com/Tencent/cloudbase-framework?site=vuepress#%E9%A1%B9%E7%9B%AE%E7%A4%BA%E4%BE%8B