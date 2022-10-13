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



使用[Ant Design Mobile](https://antd-mobile.gitee.io/zh/guide/quick-start)

```
yarn add antd-mobile
```

