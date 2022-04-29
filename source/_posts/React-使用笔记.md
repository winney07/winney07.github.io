---
title: React-使用笔记
date: 2021-03-02 14:15:34
tags:
- React
categories:
- 工作笔记
- React
---



[React Dom Examples](https://codesandbox.io/examples/package/react-dom)

[React Examples](https://codesandbox.io/examples/package/react)

#### VSCode扩展

##### 生成react代码片段-ES7

在VSCode中搜'ES7'，选择‘ES7 React/Redux/GraphQL/React-Native snippets’

在新建的`.jsx/.js`文件中

1. 输入`rcc`，快速生成class component：

   ```
   import React, { Component } from 'react'
   
   export default class App extends Component {
     render() {
       return (
         <div>
           
         </div>
       )
     }
   }
   
   ```

2. 输入`rfc`，快速生成function component：

   ```
   import React from 'react'
   
   export default function App() {
     return (
       <div>
         
       </div>
     )
   }
   
   ```

3. 输入`rconst`，快速生成constrctor：

   ```
   constructor(props) {
     super(props)
   
     this.state = {
        
     }
   }
   ```

4. 输入`rcredux`，快速生成redux模版：

   ```
   import React, { Component } from 'react'
   import PropTypes from 'prop-types'
   import { connect } from 'react-redux'
   
   export class test extends Component {
     static propTypes = {
       prop: PropTypes
     }
   
     render() {
       return (
         <div>
           
         </div>
       )
     }
   }
   
   const mapStateToProps = (state) => ({
     
   })
   
   const mapDispatchToProps = {
     
   }
   
   export default connect(mapStateToProps, mapDispatchToProps)(test)
   ```

   

[生产环境的配置](https://zh-hans.reactjs.org/docs/optimizing-performance.html#use-the-production-build)



[react中引入css的方式有哪几种](https://www.cnblogs.com/houxianzhou/p/15222138.html)



#### 快速注释

在vscode中，`.jsx`文件中，选中要注释的文字，按` CTRL + shift + /`

```
{/* 提取组件 */}
```

#### setState

1. 箭头函数

```
this.setState(state => ({
    isShowWarn: !state.isShowWarn
}))
```

#### 事件绑定

1. bind()

   ```
   constructor(props) {
     super(props)
   
     this.state = {
        isShowWarn: false
     }
   
     this.handleClick = this.handleClick.bind(this)
   }
   
   
   handleClick() {
       this.setState(state => ({
           isShowWarn: !state.isShowWarn
       }))
   }
   
   <button onClick={this.handleClick}>点击</button>
   ```

2. 箭头函数

   ```
   handleClick = ()=>{
       this.setState(state => ({
           isShowWarn: !state.isShowWarn
       }))
   }
   
   <button onClick={this.handleClick}>点击</button>
   ```

3. 箭头函数写在元素上

   ```
   handleClick() {
       this.setState(state => ({
           isShowWarn: !state.isShowWarn
       }))
   }
   
   <button onClick={ (e)=> this.handleClick(e) }>点击</button>
   ```

key 会传递信息给 React ，但不会传递给你的组件。如果你的组件中需要使用 `key` 属性的值，请用其他属性名显式传递这个值

```
<Post
    key={post.id}
    id={post.id}
    title={post.title} />
```

#### 组件中的return

```
return <div>内容</div>
```

返回多个html标签，换行写更清晰，使用`return()`

```
return(
	<ul>
		<li></li>
		<li></li>
		<li></li>
	</ul>
)
```



> 组件，含有return，会返回react或`null`
>
> 函数组件，可以从参数props中拿到属性
>
> class组件，可以从this.props中拿到属性
>
> props的属性名==组件传进来的属性名 
>
> `{}`中可以写JavaScript代码，如果是对象，需要`{{a:1,b:2}}`
>
> map函数，自带return
>
> key放在组件`<ListItems/>`上，而不是放在`<li><li/>`上
>
> key在某个循环中保证唯一性就好，不用在整个页面中保证唯一性
>
> 避免key使用索引index，特别是反序操作的情况。 因为会重新渲染，导致性能变差。使用id等唯一性属性



### 四、引入路由

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

#### 引入antd样式

App.css

```
@import '~antd/dist/antd.css';
```

#### [React中StrictMode严格模式](https://blog.csdn.net/wu_xianqiang/article/details/113521191)

StrictMode 是一个用来检查项目中潜在问题的工具。与 [Fragment](https://so.csdn.net/so/search?q=Fragment&spm=1001.2101.3001.7020) 一样，StrictMode 不会渲染任何可见的 UI。它为其后代元素触发额外的检查和警告。

StrictMode 目前有助于：

1、识别不安全的生命周期
2、关于使用过时字符串 ref API 的警告
3、关于使用废弃的 findDOMNode 方法的警告
4、检测意外的副作用
5、检测过时的 context API



#### React Router

[API接口](http://react-guide.github.io/react-router-cn/docs/API.html)

[词汇表](http://react-guide.github.io/react-router-cn/docs/Glossary.html)

##### [获取 URL 参数](http://react-guide.github.io/react-router-cn/docs/Introduction.html)

比如你访问 `/foo?bar=baz`，你可以通过访问 `this.props.location.query.bar` 从 Route 组件中获得 `"baz"` 的值。

```
React.render((
  <Router>
    <Route path="/" component={App}>
      <Route path="about" component={About} />
      <Route path="inbox" component={Inbox}>
        <Route path="messages/:id" component={Message} />
      </Route>
    </Route>
  </Router>
), document.body)
```

通过上面的配置，这个应用知道如何渲染下面四个 URL：

| URL                   | 组件                      |
| --------------------- | ------------------------- |
| `/`                   | `App`                     |
| `/about`              | `App -> About`            |
| `/inbox`              | `App -> Inbox`            |
| `/inbox/messages/:id` | `App -> Inbox -> Message` |



#### [createRoot](https://reactjs.org/blog/2022/03/08/react-18-upgrade-guide.html#updates-to-client-rendering-apis)

```
// Before
import { render } from 'react-dom';
const container = document.getElementById('app');
render(<App tab="home" />, container);

// After
import { createRoot } from 'react-dom/client';
const container = document.getElementById('app');
const root = createRoot(container);
root.render(<App tab="home" />);
```