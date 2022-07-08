---
title: React Router笔记
date: 2022-04-12 14:34:59
tags: 
- React Router
categories:
- 学习笔记
- React Router
---

[React Router 中文文档](http://react-guide.github.io/react-router-cn/)

[react-router](https://github.com/remix-run/react-router)

[docs--installation.md](https://github.com/remix-run/react-router/blob/main/docs/getting-started/installation.md)

[react-router-dom](https://github.com/remix-run/react-router/tree/main/packages/react-router-dom)

[docs-tutorial.md](https://github.com/remix-run/react-router/blob/main/docs/getting-started/tutorial.md)

### 引入路由

依赖包分间接依赖包和直接依赖包

```
cnpm i react-router-dom
```

在pages目录中，创建路由组件

#### [React Router---看这里的最新用法](https://reactrouter.com/)

[react-router-----Github](https://github.com/remix-run/react-router)

[React Router中文文档](http://react-guide.github.io/react-router-cn/docs/API.html)

#### [react-router-dom使用指南](https://zhuanlan.zhihu.com/p/431389907)

v6文档：https://reactrouter.com

v5文档：https://v5.reactrouter.com/web/guides/quick-start

```
// 入口文件index.js
import React from "react";
import ReactDOM from "react-dom"
import { BrowserRouter } from "react-router-dom";
import App from './App'

ReactDOM.render(
    <BrowserRouter>
      <App />
    </BrowserRouter>,
    document.getElementById("root")
);
```

```
// 应用的根组件App.js
import React, {Component} from "react";
import {Routes, Route } from "react-router-dom";
import "./App.less";

import Login from "./pages/login/Login";
import Admin from "./pages/admin/Admin";

export default class App extends Component {
    render() {
        return (
            <Routes>
                <Route path="/login" element={<Login />}></Route>
                <Route path="/" element={<Admin />}></Route>
            </Routes>
        )
    }
}
```

#### 重定向

```
import { Navigate } from 'react-router-dom';
function A(){
    return (
        <Navigate to="/b" />
    )
}
```

#### 编程式重定向

navigate要在useEffect中使用

```
import React, {useEffect} from 'react'

useEffect(() => {
  if(user.isLogin) {
    navigate("/home");
  }
}, [user]);
```



[Navigation Function](https://reactrouter.com/docs/en/v6/getting-started/concepts#navigate-function)





#### 使用layout的路由配置

[参考-lazy-loading](https://github.com/remix-run/react-router/tree/main/examples/lazy-loading)

##### 关键点：Outlet

```
import React, { useEffect} from 'react'
import { useSelector} from 'react-redux'
import { useNavigate  } from "react-router-dom";

import { Routes, Route, Outlet } from "react-router-dom";

import { Layout} from 'antd';

import Top from '../../components/Top'
import Bottom from '../../components/Bottom'
import LeftNav from "../../components/LeftNav"

import Product from '../product/Product';
import AddProduct from '../product/AddProduct';
import EditProduct from '../product/EditProduct';

const { Content} = Layout;

export default function Container() {
  return (
    <Routes>
      <Route path="/" element={<DashboardLayout />}>
        <Route index element={<Product />} />
        <Route path="add" element={<AddProduct />} />
        <Route path="edit" element={<EditProduct />} />
      </Route>
    </Routes>
  );
}

function DashboardLayout() {
 
    let navigate = useNavigate();
    const stateUser = useSelector(state => state.user);
    const root = JSON.parse(localStorage.getItem('persist:root'));
    const user = JSON.parse(root.user) || stateUser;
    
    // 未登录
    useEffect(() => {
        if(!user.isLogin) {
          navigate("/login");
        }
    }, [user]);

  return (
    <Layout className='container'>
        <LeftNav/>
        <Layout>
            <Top user={user}/>
            <Content style={{ margin: '24px 16px 0' }}>
                <div className="site-layout-background content-box" style={{ padding: 24, minHeight: 850 }}>
                  <Outlet />
                <Bottom/>
                </div>
            </Content>
        </Layout>
    </Layout>
  )
}
```

