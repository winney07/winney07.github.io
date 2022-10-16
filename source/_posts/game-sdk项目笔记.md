---
title: game_sdk项目笔记
date: 2021-10-13 16:08:14
tags:
- React
- SDK
---

```
yarn create react-app game_sdk
```

```
cd game_sdk
yarn start
```

#### 添加路由

```
yarn add react-router-dom
```

1. `index.js`

```
import { HashRouter } from 'react-router-dom';

<HashRouter>
    <App/>
</HashRouter>
```

> 注意事项：使用HashRouter，直接访问http://localhost:3003/login是页面空白的，要注意HashRouter与BrowserRouter的区别

> http://localhost:3003/#/login

项目中改为BrowserRouter，正式环境再改为HashRouter

```
import { BrowserRouter } from 'react-router-dom';

<BrowserRouter>
    <App/>
</BrowserRouter>
```

2. `router/index.js`

```
import { Routes, Route } from 'react-router-dom';

import Login from '../pages/user/Login';
import Service from '../pages/service/Service';
import MyCenter from '../pages/mycenter/MyCenter';
import Register from '../pages/user/Register';

function RootRouter() {
  return (
    <>
       <Routes>
        <Route path="/login" element={<Login />} />
        <Route path="/register" element={<Register />} />
        <Route path="/service" element={<Service />} />
        <Route path="/mycenter" element={<MyCenter />} />
      </Routes>
    </>
  );
}

export default RootRouter;
```

3. `App.js`

```
import RootRouter from "./router";

function App() {
  return (
    <>
       <RootRouter/>
    </>
  );
}

export default App;
```

#### 使用[antd](https://ant.design/docs/react/use-with-create-react-app-cn)（项目中使用antd)

```
yarn add antd
```

修改 `src/App.css`，在文件顶部引入 `antd/dist/antd.css`。

```css
@import '~antd/dist/antd.css';
```

##### [高级配置](https://ant.design/docs/react/use-with-create-react-app-cn#高级配置)——使用less

安装 craco 

```
yarn add @craco/craco
```

修改 `package.json` 里的 `scripts` 属性。

```diff
/* package.json */
"scripts": {
-   "start": "react-scripts start",
-   "build": "react-scripts build",
-   "test": "react-scripts test",
+   "start": "craco start",
+   "build": "craco build",
+   "test": "craco test",
}
```

在项目根目录创建一个 `craco.config.js` 用于修改默认配置。

```
/* craco.config.js */
module.exports = {
  // ...
};
```

引入 [craco-less](https://github.com/DocSpring/craco-less) 来帮助加载 less 样式和修改变量

`src/App.css` 文件修改为 `src/App.less`，然后修改样式引用为 less 文件。

```diff
/* src/App.js */
- import './App.css';
+ import './App.less';
/* src/App.less */
- @import '~antd/dist/antd.css';
+ @import '~antd/dist/antd.less';
```

安装 `craco-less` 

```
yarn add craco-less
```

修改 `craco.config.js` 文件

```
const CracoLessPlugin = require('craco-less');

module.exports = {
  plugins: [
    {
      plugin: CracoLessPlugin,
      options: {
        lessLoaderOptions: {
          lessOptions: {
            modifyVars: { '@primary-color': '#f6c700' },
            javascriptEnabled: true,
          },
        },
      },
    },
  ],
};
```

`注意：配置完，要重启项目`

这里是配置主题颜色，不改变主题颜色，可不加

```
 modifyVars: { '@primary-color': '#f6c700' },
```





也可以使用[Ant Design Mobile](https://antd-mobile.gitee.io/zh/guide/quick-start)

```
yarn add antd-mobile
```

