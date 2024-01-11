---
title: React-使用笔记
date: 2021-03-02 14:15:34
tags:
- React
categories:
- 前端开发框架
- React
---



#### [疫情实时大数据报告](https://voice.baidu.com/act/newpneumonia/newpneumonia/?from=osari_wangmeng#tab4)—React项目

[React Dom Examples](https://codesandbox.io/examples/package/react-dom)

[React Examples](https://codesandbox.io/examples/package/react)

[Create React App 中文文档](https://create-react-app.bootcss.com/)

[Create React App](https://create-react-app.dev/)

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

> 在 `map()` 方法中的元素需要设置 key 属性
>

key 会传递信息给 React ，但不会传递给你的组件。如果你的组件中需要使用 `key` 属性的值，请用其他属性名显式传递这个值：

```
const content = posts.map((post) =>
  <Post
    key={post.id}
    id={post.id}
    title={post.title} />
);
```

上面例子中，`Post` 组件可以读出 `props.id`，但是不能读出 `props.key`。

### 

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

#### [轮播图-swiper](https://swiperjs.com/get-started)

```
npm install swiper


// import Swiper JS
import Swiper from 'swiper';
// import Swiper styles
import 'swiper/css';

const swiper = new Swiper(...);
```

[Swiper React Components](https://swiperjs.com/react)



### react移动端

### [Ant Design Mobile](https://mobile.ant.design/zh)

[ant-design-mobile——GitHub](https://github.com/ant-design/ant-design-mobile)

```
npm install --save antd-mobile
```

#### [国际化](https://mobile.ant.design/zh/guide/i18n)



#### textarea 标签

而在 React 中，`<textarea>` 使用 `value` 属性代替。这样，可以使得使用 `<textarea>` 的表单和使用单行 input 的表单非常类似：

```
<textarea value={this.state.value} onChange={this.handleChange} />
```

#### select 标签

由于 `selected` 属性的缘故，椰子选项默认被选中。React 并不会使用 `selected` 属性，而是在根 `select` 标签上使用 `value` 属性。这在受控组件中更便捷，因为您只需要在根标签中更新它。例如：



#### react打包正式环境-相对路径

```
npm run build
```

> 打包后，会有静态资源获取不到的报错

解决：

在`package.json`文件中，加入`homepage`属性

```
"homepage": "."
```

[react 项目打包路径问题](https://blog.csdn.net/qq_40259641/article/details/114988659)

#### create-react-app打包上线页面空白的问题

1.项目用的是 BrowserRouter ， BrowserRouter 一般是用于服务端渲染，所以服务端也需要相应的配置。要不然 网关不知道你有哪些路由，怎么给你转发。

解决：

1. `BrowserRouter 换成 HashRouter`
   打包后，发现在本地开启web服务器预览后，正常，但是放在服务器上后，依然为空白，提示静态资源找不到。
2. 解决：
   配置 package.json 中的` homepage:'./'`
   这样可以使打包后的静态资源，采用相对路径。



[react根据不同环境配置不同接口](https://blog.csdn.net/weixin_40302777/article/details/94579132)

[三分钟教你搞定 React 项目多环境配置](https://www.ltonus.com/React/react-project-config.html)



#### [React实现复制功能](https://blog.csdn.net/yasuifi/article/details/119648390)

```
npm i --save copy-to-clipboard
```

```
import copy from 'copy-to-clipboard';


handleClick = (e) => {
  copy(e.target.value)
}


<input placeholder='请输入' onClick={this.handleClick}/> 
```

#### Lazy和Suspense

1、`React.lazy`

`React.lazy`函数能让你像渲染常规组件一样处理动态引入（的组件）。

什么意思呢？其实就是懒加载。

（1）为什么代码要分割

当你的程序越来越大，代码量越来越多。一个页面上堆积了很多功能，也许有些功能很可能都用不到，但是一样下载加载到页面上，所以这里面肯定有优化空间。就如图片懒加载的理论。

（2）实现原理

当Webpack 解析到该语法时，它会自动地开始进行代码分割(Code Splitting)，分割成一个文件，当使用到这个文件的时候会这段代码才会被异步加载。

（3）解决方案

在`React.lazy`和常用的三方包`react-loadable`，都是使用了这个原理，然后配合webpack进行代码打包拆分达到异步加载，这样首屏渲染的速度将大大的提高。

由于`React.lazy`不支持服务端渲染，所以这时候`react-loadable`就是不错的选择。

2、如何使用`React.lazy`

下面示例代码使用`create-react-app`脚手架搭建



#### 富文本编辑器

[react-draft-wysiwyg](https://github.com/jpuri/react-draft-wysiwyg)——GitHub

```
npm install --save react-draft-wysiwyg draft-js
```

```
import { Editor } from "react-draft-wysiwyg";
import "react-draft-wysiwyg/dist/react-draft-wysiwyg.css";
<Editor
  editorState={editorState}
  toolbarClassName="toolbarClassName"
  wrapperClassName="wrapperClassName"
  editorClassName="editorClassName"
  onEditorStateChange={this.onEditorStateChange}
/>;
```

[react-draft-wysiwyg-文档](https://jpuri.github.io/react-draft-wysiwyg/#/docs?_k=jjqinp)



#### [enzyme](https://github.com/enzymejs/enzyme)——GitHub

用于 React 的 JS 测试工具

[React测试框架之enzyme](https://blog.csdn.net/weixin_33860553/article/details/88004644)

[Enzyme学习笔记](https://blog.csdn.net/weixin_37972723/article/details/102076907)

[React 测试利器之 Enzyme](https://blog.csdn.net/chenzhizhuo/article/details/104196969)

[全网最细：Jest+Enzyme测试React组件（包含交互、DOM、样式测试）](https://blog.csdn.net/m0_46995864/article/details/125365202)