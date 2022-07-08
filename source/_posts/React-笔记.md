---
title: React-笔记
date: 2021-03-02 12:00:41
tags:
- React
categories:
- 学习笔记
- React
---



react使用Apifox的项目案例，可参考`Gitee/ad_manage_react`项目

json-server的使用，可参考`全球新闻发布系统项目`

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



#### **[生命周期图谱](https://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/)**

#### [组件的生命周期](https://zh-hans.reactjs.org/docs/react-component.html)



#### React权限菜单设计

[React项目配置6(前后端分离如何控制用户权限)](https://blog.csdn.net/oKeYue/article/details/79092903)

[(源码开放) React + webpack3 多页面应用 及 常见问题解答](https://blog.csdn.net/oKeYue/article/details/81130922?spm=1001.2014.3001.5502)

##### [10分钟快速搭建React权限菜单设计](https://www.csdn.net/tags/NtDaIg3sMDg5MTktYmxvZwO0O0OO0O0O.html)

##### [React 组件权限控制的实现](https://www.jb51.net/article/237335.htm)



[React的React.FC与React.Component的初步认识](https://blog.csdn.net/qq_18913129/article/details/105491090)

[useMemo和useEffect有什么区别？怎么使用useMemo](https://www.jianshu.com/p/94ace269414d)

[useMemo 使用指南](https://zhuanlan.zhihu.com/p/411190859)

[react-hooks中的一些懵逼点](https://blog.csdn.net/weixin_33782386/article/details/88610257)

> `useEffect`只能在`DOM`更新后再触发再去控制
>
> `memo`是在`DOM`更新前触发的，就像官方所说的，类比生命周期就是[shouldComponentUpdate](https://links.jianshu.com/go?to=https%3A%2F%2Fzh-hans.reactjs.org%2Fdocs%2Fhooks-faq.html%23how-do-lifecycle-methods-correspond-to-hooks)

> 在前端开发的过程中，我们需要缓存一些内容，以避免在需渲染过程中因大量不必要的耗时计算而导致的性能问题。为此 React 提供了一些方法可以帮助我们去实现数据的缓存，useMemo 就是其中之一



#### React Hooks

[React Hooks 解析（上）：基础](https://segmentfault.com/a/1190000018928587)

[React Hooks 解析（下）：进阶](https://segmentfault.com/a/1190000018950566)

[useCallback](https://www.jianshu.com/p/be8fb469d507)



> 解释这个 Hook 之前先理解下什么是副作用。网络请求、订阅某个模块或者 DOM 操作都是副作用的例子，Effect Hook 是专门用来处理副作用的。正常情况下，在`Function Component`的函数体中，是不建议写副作用代码的，否则容易出 bug。

> 在绝大多数情况下，`useEffect`Hook 是更好的选择。唯一例外的就是需要根据新的 UI 来进行 DOM 操作的场景。`useLayoutEffect`会保证在页面渲染前执行，也就是说页面渲染出来的是最终的效果。如果使用`useEffect`，页面很可能因为渲染了 2 次而出现抖动。

##### useContext

```
function HeaderBar() {
  const user = useContext(CurrentUser);
  const notifications = useContext(Notifications);

  return (
    <header>
      Welcome back, {user.name}!
      You have {notifications.length} notifications.
    </header>
  );
}
```

##### useReducer

`useReducer`的用法跟 Redux 非常相似，当 state 的计算逻辑比较复杂又或者需要根据以前的值来计算时，使用这个 Hook 比`useState`会更好。

##### useCallback

```javascript
function Foo() {
  const [count, setCount] = useState(0);

  const memoizedHandleClick = useCallback(
    () => console.log(`Click happened with dependency: ${count}`), [count],
  ); 
  return <Button onClick={memoizedHandleClick}>Click Me</Button>;
}
```

> `useCallback`缓存的是方法的引用，而`useMemo`缓存的则是方法的返回值。使用场景是减少不必要的子组件渲染：

##### useRef

```
function() {
  const myRef = useRef(null);

  useEffect(() => {
    myRef.current.focus();
  }, [])
  
  return <input ref={myRef} type="text" />;
}
```

> `useRef`返回一个普通 JS 对象，可以将任意数据存到`current`属性里面，就像使用实例化对象的`this`一样。另外一个使用场景是获取 previous props 或 previous state

##### 自定义 Hook

> 自定义 Hook 的命名有讲究，必须以`use`开头，在里面可以调用其它的 Hook。入参和返回值都可以根据需要自定义，没有特殊的约定。使用也像普通的函数调用一样，Hook 里面其它的 Hook（如`useEffect`）会自动在合适的时候调用



#### [Effect Hook](https://zh-hans.reactjs.org/docs/hooks-overview.html#effect-hook)

> 在 React 组件中执行过**数据获取、订阅或者手动修改过 DOM**。我们统一把这些操作称为“**副作用**”，或者简称为“作用”。
>
> `useEffect` 就是一个 Effect Hook，给函数组件增加了操作副作用的能力。它跟 class 组件中的 `componentDidMount`、`componentDidUpdate` 和 `componentWillUnmount` 具有相同的用途，只不过被合并成了一个 API。（我们会在[使用 Effect Hook](https://zh-hans.reactjs.org/docs/hooks-effect.html) 里展示对比 `useEffect` 和这些方法的例子。）



#### [Hook概览](https://zh-hans.reactjs.org/docs/hooks-overview.html#effect-hook)