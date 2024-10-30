---
title: React Native相关笔记
date: 2021-09-28 10:35:24
tags:
- React Native
categories:
- 前端开发框架
- React Native
---

[React Native官网](https://reactnative.dev/)

[React Native 中文网](https://www.reactnative.cn/)

#### 移动App的开发模式

- 原生开发
- 原生App
- Android | iOS | Windows



- 混合开发
- 混合App
- React Native | Weex | Flutter



- H5开发
- Web App
- HTML、CSS、JavaScript

#### 跨平台框架的比较

| 框架     | React Native        | Weex              | Flutter               |
| -------- | ------------------- | ----------------- | --------------------- |
| 所属公司 | Facebook            | Alibaba           | Google                |
| 编程语言 | JavaScript（React） | JavaScript（Vue） | Dart                  |
| 引擎     | JSCore              | V8                | Flutter engine        |
| 支持系统 | Android、iOS        | Android、iOS、Web | Android、iOS、Fuchsia |
| 性能     | 一般                | 较快              | 较快                  |
| 使用场景 | 整体App             | 单页面            | 整体App               |
| 学习成本 | 难                  | 易                | 一般                  |

[移动端跨平台框架对比](https://www.jianshu.com/p/8717e1e614a9)

#### 移动App的开发模式

| 开发模式 | 原生开发          | 混合开发         | Web开发               |
| -------- | ----------------- | ---------------- | --------------------- |
| 运行环境 | Android、iOS      | Android、iOS     | 浏览器、WebView       |
| 编程语言 | Java、Objective-C | JavaScript、Dart | HTML、CSS、JavaScript |
| 可移植性 | 差                | 一般             | 好                    |
| 开发速度 | 慢                | 一般             | 快                    |
| 性能     | 快                | 较慢             | 慢                    |
| 学习成本 | 高                | 一般             | 低                    |

React Native的优点

- 开发体验好
  - 用统一的代码规范开发移动端程序，不用关注移动端的差异
- 开发成本低
  - 开发一次，可以生成Android和iOs两个系统上的App- Learn once, write anywhere
- 学习成本低
  - 只要掌握JavaScript和React，就可以进行移动端开发了





React Native的不足

- 不成熟;
  - 项目版本更新维护较频繁，学习成本高;
  - 试错成本高，有些问题较少解决方案，易耽误开发进度。
- 性能差
  - 整体性能仍不如原生
- 兼容性差
  - 涉及底层的功能，需要针对Android和iOs双端单独开发;

#### 基础环境搭建

- 安装Node.js

  - Node.js的版本应>=12(推荐安装LTS版本)
  - ` npm config set registry https://registry.npm.taobao.org`

- 安装Yarn

  ```
  npm install -g yarn
  ```

- 安装 React Native脚手架

  ```
   npm install -g react-native-cli
  ```

  

需要安装Android开发环境、iOS开发环境

Window下只能安装Android开发环境

Mac下可以安装Android开发环境、iOS开发环境



Android环境

- 安装JDK
- 安装Android Studio
- 安装Android SDK
- 配置环境变量





·下载JDK(Java SE Development Kit)
 https:/www.oracle.com/jiava/technologies/iavase/javase-jdk8-downloads.html·JDK的版本必须是1.8(1.8版本，官方也直接称8版本)
·目前不支持高于1.8的JDK版本
·下载时要求登陆(请先注册Oracle账号)
·或者直接找老师，获取上面的安装包
·安装JDK(一直“下一步”)
·命令行中，输入java -version，验证安装是否成功
L, A, G，。u———



·下载Android Studio
https://developer.android.com/studio/index.html·安装Android Studio (一直“下一步")·启动Android Studio
·初次启动，需要安装组件（组件约2GB，安装后占用空间约8GB)·安装组件的过程巨长巨长巨长，要有耐心





. What
·Android SDK是针对安卓开发的套件. Why
·虽然Android Studio默认会安装最新版本的Android SDK
·但是，目前编译React Native应用需要的是Android 10(Q)版本的SDK
· How
·打开Android Studio，在菜单Tools下找到"SDK Manager"





·配置ANDROID_HOME环境变量
·`打开Android Studio，点击菜单Tools → SDK Manager，找到Appearance &Behavior → System Settings → Android SDK`



·跟ANDROID_HOME相关的环境变量
·`%ANDROID_HOME%\platform-tools%ANDROID_HOME%\emulator`
·`%ANDROID_HOME%\tools·%ANDROID_HOME%\tools\bin`
—L，A,G，。u



react native 进阶

react native 高级

ECMAScript新功能

