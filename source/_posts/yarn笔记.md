---
title: yarn-笔记
date: 2021-04-24 15:43:06
tags:
- 包管理器
categories:
- 学习笔记
- yarn
---

[yarn官网](https://yarnpkg.com/)

[yarn中文官网](https://www.yarnpkg.cn/)

[yarn-中文官网](http://yarnpkg.top/)

#### 全局安装yarn

```
npm install --global yarn
```

#### 查看版本

```
yarn --version
```

#### 启动开发环境服务

```
yarn start
```

#### 打包（生成静态文件）

```
yarn build
```

#### [创建React项目](https://zh-hans.reactjs.org/docs/create-a-new-react-app.html#create-react-app)

```
npx create-react-app my-app
cd my-app
yarn start
```

#### 添加React Router

```
yarn add react-router-dom@6
```





#### 使用Vite创建Vue项目

```
yarn create vite
```

```
√ Project name: ... Vue3_yarn
√ Package name: ... vue3-yarn
√ Select a framework: » vue
√ Select a variant: » vue-ts
```

```
cd Vue3_yarn
yarn
yarn dev
```



#### 新建项目

```
 yarn init
```

```
question name (yarn_test):
question version (1.0.0):
question description:
question entry point (index.js):
question repository url:
question author:
question license (MIT):
question private:
success Saved package.json
```

#### **添加依赖**

```
yarn add [package]
yarn add [package]@[version]
yarn add [package]@[tag]
```

### 将依赖项添加到不同的依赖类别中

```bash
yarn add [package] --dev  # dev dependencies
yarn add [package] --peer # peer dependencies
```

#### **更新依赖**

```
yarn upgrade [package]
yarn upgrade [package]@[version]
yarn upgrade [package]@[tag]
```

#### **删除依赖**

```
yarn remove [package]
```

#### **根据package.json文件为项目安装所有依赖**

```
yarn
```

or

```
yarn install
```

#### 更新 Yarn 本体

```bash
yarn set version latest
yarn set version from sources
```

