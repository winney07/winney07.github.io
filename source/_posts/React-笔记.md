---
title: React-笔记
date: 2021-03-02 12:00:41
tags:
- React
categories:
- 学习笔记
- React
---



#### 单页面应用

与页面或后续页面的任何交互，都不再需要往返 server 加载资源，即页面不会重新加载

#### 编译器

[Babel](https://babeljs.io/) 是 React 最常用的 compiler

#### 打包工具

常用的打包 React 应用的工具有 [webpack](https://webpack.js.org/) 和 [Browserify](http://browserify.org/)。

#### 管理工具

[npm](https://www.npmjs.com/) 和 [Yarn](https://yarnpkg.com/) 是两个常用的管理 React 应用依赖的 package 管理工具

#### JSX

React DOM 使用 camelCase（驼峰式命名）来定义属性的名称

#### 组件

组件名称应该始终以大写字母开头（`<Wrapper/>` **而不是** `<wrapper/>`）

#### props

`props` 是只读的。不应以任何方式修改它们

#### props.children

每个组件都可以获取到 `props.children`。它包含组件的开始标签和结束标签之间的内容

```
<Welcome>Hello world!</Welcome>
```

#### state

当组件中的一些数据在某些时刻发生变化时，这时就需要使用 `state` 来跟踪状态

`state` 和 `props` 之间最重要的区别是：`props` 由父组件传入，而 `state` 由组件本身管理。组件不能修改 `props`，但它可以修改 `state`。

#### [生命周期方法](https://zh-hans.reactjs.org/docs/state-and-lifecycle.html#adding-lifecycle-methods-to-a-class)

#### [受控组件](https://zh-hans.reactjs.org/docs/forms.html#controlled-components) vs [非受控组件](https://zh-hans.reactjs.org/docs/uncontrolled-components.html)

#### [Ref](https://zh-hans.reactjs.org/docs/refs-and-the-dom.html)

#### [状态提升](https://zh-hans.reactjs.org/docs/lifting-state-up.html)



#### 应该在 React 组件的哪个生命周期函数中发起 AJAX 请求？

在 [`componentDidMount`](https://zh-hans.reactjs.org/docs/react-component.html#mounting) 这个生命周期函数中发起 AJAX 请求

#### [工具链](https://zh-hans.reactjs.org/docs/create-a-new-react-app.html#more-flexible-toolchains)

#### JSX 防止注入攻击

所有的内容在渲染之前都被转换成了字符串。这样可以有效地防止 [XSS（cross-site-scripting, 跨站脚本）](https://en.wikipedia.org/wiki/Cross-site_scripting)攻击

#### JSX 表示对象

Babel 会把 JSX 转译成一个名为 `React.createElement()` 函数调用

`React.createElement()` 会预先执行一些检查，以帮助你编写无错代码，但实际上它创建了一个这样的对象：

```
// 注意：这是简化过的结构
const element = {
  type: 'h1',
  props: {
    className: 'greeting',
    children: 'Hello, world!'
  }
};
```

这些对象被称为 “**React 元素**”。

**仅使用 React 构建的应用通常只有单一的根 DOM 节点**。如果你在将 React 集成进一个已有应用，那么你可以在应用中包含任意多的独立根 DOM 节点。





React 元素是[不可变对象](https://en.wikipedia.org/wiki/Immutable_object)。一旦被创建，你就无法更改它的子元素或者属性。一个元素就像电影的单帧：它代表了某个特定时刻的 UI。

#### 组件

组件，从概念上类似于 JavaScript 函数。它接受任意的入参（即 “props”），并返回用于描述页面展示内容的 React 元素。



建议从组件自身的角度命名 props，而不是依赖于调用组件的上下文命名。

```
<Avatar user={props.author} />

function Avatar(props) {
  return (
    <img className="Avatar"
      src={props.user.avatarUrl}
      alt={props.user.name}
    />
  );
}
```

**所有 React 组件都必须像纯函数一样保护它们的 props 不被更改**

#### 不要直接修改 State

应该使用 `setState()`

构造函数是唯一可以给 `this.state` 赋值的地方

#### [State 的更新可能是异步的](https://zh-hans.reactjs.org/docs/state-and-lifecycle.html)

```
// Wrong
this.setState({
  counter: this.state.counter + this.props.increment,
});
```

```
// Correct
this.setState((state, props) => ({
  counter: state.counter + props.increment
}));
```

### 条件渲染

#### 元素变量

```
{unreadMessages.length > 0 &&
    <h2>
      You have {unreadMessages.length} unread messages.
    </h2>
}
```

#### 与运算符 &&

`true && expression` 总是会返回 `expression`, 而 `false && expression` 总是会返回 `false`。

注意：下面示例中，render 方法的返回值是 `<div>0</div>`

```
 { count && <h1>Messages: {count}</h1>}
```

#### 三目运算符

```
The user is <b>{isLoggedIn ? 'currently' : 'not'}</b> logged in.
```

```
{isLoggedIn
    ? <LogoutButton onClick={this.handleLogoutClick} />
    : <LoginButton onClick={this.handleLoginClick} />
}
```

#### [阻止组件渲染](https://zh-hans.reactjs.org/docs/conditional-rendering.html)

让 `render` 方法直接返回 `null`，而不进行任何渲染

#### 受控组件

表单元素（如`<input>`、 `<textarea>` 和 `<select>`）通常自己维护 state

#### 文件 input 标签

因为它的 value 只读，所以它是 React 中的一个**非受控**组件



#### 提交事件

```
<form onSubmit={this.handleSubmit}>
</form>
```

### 组合 vs 继承

#### 包含关系

有些组件无法提前知晓它们子组件的具体内容。在 `Sidebar`（侧边栏）和 `Dialog`（对话框）等展现通用容器（box）的组件中特别容易遇到这种情况。

我们建议这些组件使用一个特殊的 `children` prop 来将他们的子组件传递到渲染结果中：

```
{props.children}
```

少数情况下，你可能需要在一个组件中预留出几个“洞”。这种情况下，我们可以不使用 `children`，而是自行约定：将所需内容传入 props，并使用相应的 prop

```
<div className="SplitPane">
  <div className="SplitPane-left">
    {props.left}
  </div>
  <div className="SplitPane-right">
    {props.right}
  </div>
</div>
```

#### [将设计好的 UI 划分为组件层级](https://zh-hans.reactjs.org/docs/thinking-in-react.html)



#### 编写组件步骤

1. 第一步：将设计好的 UI 划分为组件层级
2. 第二步：用 React 创建一个静态版本
3. 第三步：确定 UI state 的最小（且完整）表示
4. 第四步：确定 state 放置的位置
5. 第五步：添加反向数据流

> 通过问自己以下三个问题，你可以逐个检查相应数据是否属于 state：
>
> 1. 该数据是否是由父组件通过 props 传递而来的？如果是，那它应该不是 state。
> 2. 该数据是否随时间的推移而保持不变？如果是，那它应该也不是 state。
> 3. 你能否根据其他 state 或 props 计算出该数据的值？如果是，那它也不是 state。
>
> 包含所有产品的原始列表是经由 props 传入的，所以它不是 state；搜索词和复选框的值应该是 state，因为它们随时间会发生改变且无法由其他数据计算而来；经过搜索筛选的产品列表不是 state，因为它的结果可以由产品的原始列表根据搜索词和复选框的选择计算出来。
>
> 综上所述，属于 state 的有：
>
> - 用户输入的搜索词
> - 复选框是否选中的值



哪个组件应该拥有某个 state 

- 找到他们的共同所有者（common owner）组件（在组件层级上高于所有需要该 state 的组件）。



**state 只能由拥有它们的组件进行更改**

state在哪个组件，修改state的方法就在哪个组件