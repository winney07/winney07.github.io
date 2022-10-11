---
title: React-笔记
date: 2021-03-02 12:00:41
tags:
- React
categories:
- 学习笔记
- React
---

[React官网](https://reactjs.org/)

[Create React App](https://create-react-app.dev/)



#### [创建应用](https://zh-hans.reactjs.org/docs/create-a-new-react-app.html#create-react-app)

```
npx create-react-app my-app
cd my-app
npm start
```



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

#### [组合 vs 继承](https://react.docschina.org/docs/composition-vs-inheritance.html)

#### [props.children](https://react.docschina.org/docs/composition-vs-inheritance.html#containment)

每个组件都可以获取到 `props.children`。它包含组件的开始标签和结束标签之间的内容

```
<Welcome>Hello world!</Welcome>
```

少数情况下，你可能需要在一个组件中预留出几个“洞”。这种情况下，我们可以不使用 `children`，而是自行约定：将所需内容传入 props，并使用相应的 prop。

```
function SplitPane(props) {
  return (
    <div className="SplitPane">
      <div className="SplitPane-left">
        {props.left}
      </div>
      <div className="SplitPane-right">
        {props.right}
      </div>
    </div>
  );
}

function App() {
  return (
    <SplitPane
      left={
        <Contacts />
      }
      right={
        <Chat />
      } />
  );
}
```

在 React 中，我们也可以通过组合来实现这一点。“特殊”组件可以通过 props 定制并渲染“一般”组件：

```
function Dialog(props) {
  return (
    <FancyBorder color="blue">
      <h1 className="Dialog-title">
        {props.title}      </h1>
      <p className="Dialog-message">
        {props.message}      </p>
    </FancyBorder>
  );
}

function WelcomeDialog() {
  return (
    <Dialog      title="Welcome"      message="Thank you for visiting our spacecraft!" />  );
}
```

```
function Dialog(props) {
  return (
    <FancyBorder color="blue">
      <h1 className="Dialog-title">
        {props.title}
      </h1>
      <p className="Dialog-message">
        {props.message}
      </p>
      {props.children}
    </FancyBorder>
  );
}

class SignUpDialog extends React.Component {
  constructor(props) {
    super(props);
    this.handleChange = this.handleChange.bind(this);
    this.handleSignUp = this.handleSignUp.bind(this);
    this.state = {login: ''};
  }

  render() {
    return (
      <Dialog title="Mars Exploration Program"
              message="How should we refer to you?">
        <input value={this.state.login}
               onChange={this.handleChange} />
        <button onClick={this.handleSignUp}>
          Sign Me Up!
        </button>
      </Dialog>
    );
  }

  handleChange(e) {
    this.setState({login: e.target.value});
  }

  handleSignUp() {
    alert(`Welcome aboard, ${this.state.login}!`);
  }
}
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

#### 处理多个输入

当需要处理多个 `input` 元素时，我们可以给每个元素添加 `name` 属性，并让处理函数根据 `event.target.name` 的值选择要执行的操作。

```
handleInputChange(event) {
    const target = event.target;
    const value = target.name === 'isGoing' ? target.checked : target.value;
    const name = target.name;

    this.setState({
      [name]: value
    });
}
```

等同 ES5:

```
var partialState = {};
partialState[name] = value;this.setState(partialState);
```

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

[context](https://react.docschina.org/docs/context.html)

> Context 主要应用场景在于*很多*不同层级的组件需要访问同样一些的数据。请谨慎使用，因为这会使得组件的复用性变差。

> **如果你只是想避免层层传递一些属性，[组件组合（component composition）](https://react.docschina.org/docs/composition-vs-inheritance.html)有时候是一个比 context 更好的解决方案。**

```
const ThemeContext = React.createContext('light');

<ThemeContext.Provider value="dark">
    <Toolbar />
</ThemeContext.Provider>

// 中间的组件再也不必指明往下传递 theme 了。
function Toolbar() {
  return (
    <div>
      <ThemedButton />
    </div>
  );
}

class ThemedButton extends React.Component {
  // 指定 contextType 读取当前的 theme context。
  // React 会往上找到最近的 theme Provider，然后使用它的值。
  // 在这个例子中，当前的 theme 值为 “dark”。
  static contextType = ThemeContext;
  render() {
    return <Button theme={this.context} />;
  }
}
```

> 当 Provider 的 `value` 值发生变化时，它内部的所有消费组件都会重新渲染。Provider 及其内部 consumer 组件都不受制于 `shouldComponentUpdate` 函数，因此当 consumer 组件在其祖先组件退出更新的情况下也能更新。

[Context.Consumer](https://react.docschina.org/docs/context.html#contextconsumer)

[消费多个 Context](https://react.docschina.org/docs/context.html#consuming-multiple-contexts)

##### [注意事项](https://react.docschina.org/docs/context.html#caveats)

> 因为 context 会使用参考标识（reference identity）来决定何时进行渲染，这里可能会有一些陷阱，当 provider 的父组件进行重渲染时，可能会在 consumers 组件中触发意外的渲染

为了防止这种情况，将 value 状态提升到父节点的 state 里：

```
class App extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      value: {something: 'something'},
    };
  }

  render() {
    return (
      <Provider value={this.state.value}>
        <Toolbar />
      </Provider>
    );
  }
}
```



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



[懒加载-React.lazy](https://react.docschina.org/docs/code-splitting.html#reactlazy)

```
import React, { Suspense } from 'react';

const OtherComponent = React.lazy(() => import('./OtherComponent'));

function MyComponent() {
  return (
    <div>
      <Suspense fallback={<div>Loading...</div>}>
        <OtherComponent />
      </Suspense>
    </div>
  );
}
```

[异常捕获边界](https://react.docschina.org/docs/code-splitting.html#error-boundaries)

[基于路由的代码分割](https://react.docschina.org/docs/code-splitting.html#route-based-code-splitting)

[错误边界（Error Boundaries）](https://react.docschina.org/docs/error-boundaries.html#introducing-error-boundaries)

#### [Refs 转发](https://react.docschina.org/docs/forwarding-refs.html#forwarding-refs-to-dom-components)

```
const FancyButton = React.forwardRef((props, ref) => (
  <button ref={ref} className="FancyButton">
    {props.children}
  </button>
));

// 你可以直接获取 DOM button 的 ref：
const ref = React.createRef();
<FancyButton ref={ref}>Click me!</FancyButton>;
```

> 出于同样的原因，当 `React.forwardRef` 存在时有条件地使用它也是不推荐的：它改变了你的库的行为，并在升级 React 自身时破坏用户的应用。

#### [高阶组件](https://react.docschina.org/docs/higher-order-components.html)

高阶组件是参数为组件，返回值为新组件的函数。

组件是将 props 转换为 UI，而高阶组件是将组件转换为另一个组件。

#### [深入 JSX](https://react.docschina.org/docs/jsx-in-depth.html)

> `if` 语句以及 `for` 循环不是 JavaScript 表达式，所以不能在 JSX 中直接使用。但是，你可以用在 JSX 以外的代码中

##### [字符串字面量](https://react.docschina.org/docs/jsx-in-depth.html#string-literals)

如下两个 JSX 表达式是等价的：

```
<MyComponent message="hello world" />

<MyComponent message={'hello world'} />
```

当你将字符串字面量赋值给 prop 时，它的值是未转义的。所以，以下两个 JSX 表达式是等价的：

```
<MyComponent message="&lt;3" />

<MyComponent message={'<3'} />
```

##### [Props 默认值为 “True”](https://react.docschina.org/docs/jsx-in-depth.html#props-default-to-true)

以下两个 JSX 表达式是等价的

```
<MyTextBox autocomplete />

<MyTextBox autocomplete={true} />
```

##### [属性展开](https://react.docschina.org/docs/jsx-in-depth.html#spread-attributes)

以下两个组件是等价的：

```
function App1() {
  return <Greeting firstName="Ben" lastName="Hector" />;
}

function App2() {
  const props = {firstName: 'Ben', lastName: 'Hector'};
  return <Greeting {...props} />;
}
```

你还可以选择只保留当前组件需要接收的 props，并使用展开运算符将其他 props 传递下去。

```
const Button = props => {
  const { kind, ...other } = props;
  const className = kind === "primary" ? "PrimaryButton" : "SecondaryButton";
  return <button className={className} {...other} />;
};

const App = () => {
  return (
    <div>
      <Button kind="primary" onClick={() => console.log("clicked!")}>
        Hello World!
      </Button>
    </div>
  );
};
```

##### [字符串字面量](https://react.docschina.org/docs/jsx-in-depth.html#string-literals-1)

你可以将字符串放在开始和结束标签之间，此时 `props.children` 就只是该字符串。这对于很多内置的 HTML 元素很有用。例如：

```
<MyComponent>Hello world!</MyComponent>
```

React 组件也能够返回存储在数组中的一组元素：

```
render() {
  // 不需要用额外的元素包裹列表元素！
  return [
    // 不要忘记设置 key :)
    <li key="A">First item</li>,
    <li key="B">Second item</li>,
    <li key="C">Third item</li>,
  ];
}
```

JavaScript 表达式可以被包裹在 `{}` 中作为子元素。例如，以下表达式是等价的：

```
<MyComponent>foo</MyComponent>

<MyComponent>{'foo'}</MyComponent>
```

##### [布尔类型、Null 以及 Undefined 将会忽略](https://react.docschina.org/docs/jsx-in-depth.html#booleans-null-and-undefined-are-ignored)

```
<div>
  {props.messages.length > 0 &&
    <MessageList messages={props.messages} />
  }
</div>
```

如果你想渲染 `false`、`true`、`null`、`undefined` 等值，你需要先将它们[转换为字符串](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String#String_conversion)：

```
<div>
  My JavaScript variable is {String(myVariable)}.
</div>
```

#### [性能优化](https://react.docschina.org/docs/optimizing-performance.html)

##### [Brunch](https://react.docschina.org/docs/optimizing-performance.html#brunch)

通过安装 [`terser-brunch`](https://github.com/brunch/terser-brunch) 插件，来获得最高效的 Brunch 生产构建：

##### [避免调停](https://react.docschina.org/docs/optimizing-performance.html)

```
shouldComponentUpdate(nextProps, nextState) {
  return true;
}
```

如果你知道在什么情况下你的组件不需要更新，你可以在 `shouldComponentUpdate` 中返回 `false` 来跳过整个渲染过程。其包括该组件的 `render` 调用以及之后的操作。



如果你的组件只有当 `props.color` 或者 `state.count` 的值改变才需要更新时，你可以使用 `shouldComponentUpdate` 来进行检查：

```
shouldComponentUpdate(nextProps, nextState) {
    if (this.props.color !== nextProps.color) {
      return true;
    }
    if (this.state.count !== nextState.count) {
      return true;
    }
    return false;
}
```

大部分情况下，你可以使用 `React.PureComponent` 来代替手写 `shouldComponentUpdate`



#### [不可变数据的力量](https://react.docschina.org/docs/optimizing-performance.html)

```
handleClick() {
  this.setState(state => ({
    words: state.words.concat(['marklar'])
  }));
}
```

```
handleClick() {
  this.setState(state => ({
    words: [...state.words, 'marklar'],
  }));
};
```

为了不改变原本的对象，我们可以使用 [Object.assign](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/assign) 方法：

```
function updateColorMap(colormap) {
  return Object.assign({}, colormap, {right: 'blue'});
}
```

添加[对象扩展属性](https://github.com/sebmarkbage/ecmascript-rest-spread)以使得更新不可变对象变得更方便：

```
function updateColorMap(colormap) {
  return {...colormap, right: 'blue'};
}
```

[Polyfill](https://developer.mozilla.org/zh-CN/docs/Glossary/polyfill)

[HTML5 Cross Browser Polyfills](https://github.com/Modernizr/Modernizr/wiki/HTML5-Cross-Browser-Polyfills)

#### [Portals](https://react.docschina.org/docs/portals.html)

Portal 提供了一种将子节点渲染到存在于父组件以外的 DOM 节点的优秀的方案。

```
ReactDOM.createPortal(child, container)
```

第一个参数（`child`）是任何[可渲染的 React 子元素](https://react.docschina.org/docs/react-component.html#render)，例如一个元素，字符串或 fragment。第二个参数（`container`）是一个 DOM 元素。

```
render() {
  // React 并*没有*创建一个新的 div。它只是把子元素渲染到 `domNode` 中。
  // `domNode` 是一个可以在任何位置的有效 DOM 节点。
  return ReactDOM.createPortal(
    this.props.children,
    domNode  );
}
```

一个 portal 的典型用例是当父组件有 `overflow: hidden` 或 `z-index` 样式时，但你需要子组件能够在视觉上“跳出”其容器。例如，对话框、悬浮卡以及提示框：

#### [Profiler](https://react.docschina.org/docs/profiler.html)

`Profiler` 测量渲染一个 React 应用多久渲染一次以及渲染一次的“代价”。 它的目的是识别出应用中渲染较慢的部分，或是可以使用[类似 memoization 优化](https://react.docschina.org/docs/hooks-faq.html#how-to-memoize-calculations)的部分，并从相关优化中获益。

#### [不使用 ES6](https://react.docschina.org/docs/react-without-es6.html)的使用方法

无论是函数组件还是 class 组件，都拥有 `defaultProps` 属性：

```
Greeting.defaultProps = {
  name: 'Mary'
};
```

如果使用 `createReactClass()` 方法创建组件，那就需要在组件中定义 `getDefaultProps()` 函数：

```
getDefaultProps: function() {
    return {
      name: 'Mary'
    };
},
```

[初始化 State](https://react.docschina.org/docs/react-without-es6.html#setting-the-initial-state)

[自动绑定](https://react.docschina.org/docs/react-without-es6.html#autobinding)

为了保险起见，以下三种做法都是可以的：

- 在 constructor 中绑定方法。
- 使用箭头函数，比如：`onClick={(e) => this.handleClick(e)}`。
- 继续使用 `createReactClass`。

#### [Render Props](https://react.docschina.org/docs/render-props.html) 

```
class Cat extends React.Component {
  render() {
    const mouse = this.props.mouse;
    return (
      <img src="/cat.jpg" style={{ position: 'absolute', left: mouse.x, top: mouse.y }} />
    );
  }
}

class Mouse extends React.Component {
  constructor(props) {
    super(props);
    this.handleMouseMove = this.handleMouseMove.bind(this);
    this.state = { x: 0, y: 0 };
  }

  handleMouseMove(event) {
    this.setState({
      x: event.clientX,
      y: event.clientY
    });
  }

  render() {
    return (
      <div style={{ height: '100vh' }} onMouseMove={this.handleMouseMove}>

        {/*
          Instead of providing a static representation of what <Mouse> renders,
          use the `render` prop to dynamically determine what to render.
        */}
        {this.props.render(this.state)}
      </div>
    );
  }
}

class MouseTracker extends React.Component {
  render() {
    return (
      <div>
        <h1>移动鼠标!</h1>
        <Mouse render={mouse => (
          <Cat mouse={mouse} />
        )}/>
      </div>
    );
  }
}
```

```
// 如果你出于某种原因真的想要 HOC，那么你可以轻松实现
// 使用具有 render prop 的普通组件创建一个！
function withMouse(Component) {
  return class extends React.Component {
    render() {
      return (
        <Mouse render={mouse => (
          <Component {...this.props} mouse={mouse} />
        )}/>
      );
    }
  }
}
```

**render prop 是一个用于告知组件需要渲染什么内容的函数 prop。**

#### [静态类型检查](https://react.docschina.org/docs/static-type-checking.html)

建议在大型代码库中使用 Flow 或 TypeScript 来代替 `PropTypes`。

##### flow

- [Flow 文档：类型注解](https://flow.org/en/docs/types/)
- [Flow 文档：编辑器](https://flow.org/en/docs/editors/)
- [Flow 文档：React](https://flow.org/en/docs/react/)
- [在 Flow 中进行 lint](https://medium.com/flow-type/linting-in-flow-7709d7a7e969)

##### TypeScript

- [TypeScript](https://www.typescriptlang.org/)

- [在 React 中使用 TypeScript](https://github.com/Microsoft/TypeScript-React-Starter#typescript-react-starter)
- [TypeScript 文档：基本类型](https://www.typescriptlang.org/docs/handbook/basic-types.html)
- [TypeScript 文档：JavaScript 迁移](https://www.typescriptlang.org/docs/handbook/migrating-from-javascript.html)
- [TypeScript 文档：React 与 Webpack](https://www.typescriptlang.org/docs/handbook/react-&-webpack.html)

- [在 Create React App 中使用 TypeScript](https://react.docschina.org/docs/static-type-checking.html#using-typescript-with-create-react-app)

```
npx create-react-app my-app --template typescript
```

将 TypeScript 添加到**现有的 Create React App 项目**中，[请参考此文档](https://facebook.github.io/create-react-app/docs/adding-typescript).

[配置 TypeScript 编译器](https://react.docschina.org/docs/static-type-checking.html#configuring-the-typescript-compiler)

```
yarn run tsc --init
```

如果你使用 [npm](https://www.npmjs.com/)，执行：

```
npx tsc --init
```

`tsconfig.json` 文件中，有许多配置项用于配置编译器。查看所有配置项的的详细说明，[请参考此文档](https://www.typescriptlang.org/docs/handbook/tsconfig-json.html)。

```
// tsconfig.json

{
  "compilerOptions": {
    // ...
    "rootDir": "src",
    "outDir": "build"
    // ...
  },
}
```

[TypeScript React Starter](https://github.com/Microsoft/TypeScript-React-Starter/blob/master/tsconfig.json) 提供了一套默认的 `tsconfig.json` 帮助你快速上手。

在 React 中，你的组件文件大多数使用 `.js` 作为扩展名。在 TypeScript 中，提供两种文件扩展名：`.ts` 是默认的文件扩展名，而 `.tsx` 是一个用于包含 `JSX` 代码的特殊扩展名。

##### [运行 TypeScript](https://react.docschina.org/docs/static-type-checking.html#running-typescript)

如果你按照上面的说明操作，现在应该能运行 TypeScript 了。

```
yarn build
```

如果你使用 npm，执行：

```
npm run build
```

如果你没有看到输出信息，这意味着它编译成功了

#### [严格模式](https://react.docschina.org/docs/strict-mode.html)

你可以为应用程序的任何部分启用严格模式。例如：

```
import React from 'react';

function ExampleApplication() {
  return (
    <div>
      <Header />
      <React.StrictMode>        
      	<div>
          <ComponentOne />
          <ComponentTwo />
        </div>
      </React.StrictMode>      
      <Footer />
    </div>
  );
}
```

`StrictMode` 目前有助于：

- [识别不安全的生命周期](https://react.docschina.org/docs/strict-mode.html#identifying-unsafe-lifecycles)
- [关于使用过时字符串 ref API 的警告](https://react.docschina.org/docs/strict-mode.html#warning-about-legacy-string-ref-api-usage)
- [关于使用废弃的 findDOMNode 方法的警告](https://react.docschina.org/docs/strict-mode.html#warning-about-deprecated-finddomnode-usage)
- [检测意外的副作用](https://react.docschina.org/docs/strict-mode.html#detecting-unexpected-side-effects)
- [检测过时的 context API](https://react.docschina.org/docs/strict-mode.html#detecting-legacy-context-api)

渲染阶段的生命周期包括以下 class 组件方法：

- `constructor`
- `componentWillMount` (or `UNSAFE_componentWillMount`)
- `componentWillReceiveProps` (or `UNSAFE_componentWillReceiveProps`)
- `componentWillUpdate` (or `UNSAFE_componentWillUpdate`)
- `getDerivedStateFromProps`
- `shouldComponentUpdate`
- `render`
- `setState` 更新函数（第一个参数）

#### [使用 PropTypes 进行类型检查](https://react.docschina.org/docs/typechecking-with-proptypes.html)

```
import PropTypes from 'prop-types';

class Greeting extends React.Component {
  render() {
    return (
      <h1>Hello, {this.props.name}</h1>
    );
  }
}

Greeting.propTypes = {
  name: PropTypes.string
};
```

出于性能方面的考虑，`propTypes` 仅在开发模式下进行检查。

#### [默认 Prop 值](https://react.docschina.org/docs/typechecking-with-proptypes.html)

```
class Greeting extends React.Component {
  render() {
    return (
      <h1>Hello, {this.props.name}</h1>
    );
  }
}

// 指定 props 的默认值：
Greeting.defaultProps = {
  name: 'Stranger'
};

// 渲染出 "Hello, Stranger"：
ReactDOM.render(
  <Greeting />,
  document.getElementById('example')
);
```

`defaultProps` 用于确保 `this.props.name` 在父组件没有指定其值时，有一个默认值。

#### [非受控组件](https://react.docschina.org/docs/uncontrolled-components.html)

```
class NameForm extends React.Component {
  constructor(props) {
    super(props);
    this.handleSubmit = this.handleSubmit.bind(this);
    this.input = React.createRef();
  }

  handleSubmit(event) {
    alert('A name was submitted: ' + this.input.current.value);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Name:
          <input type="text" ref={this.input} />
        </label>
        <input type="submit" value="Submit" />
      </form>
    );
  }
}
```

如果你还是不清楚在某个特殊场景中应该使用哪种组件，那么 [这篇关于受控和非受控输入组件的文章](https://goshakkk.name/controlled-vs-uncontrolled-inputs-react/) 会很有帮助。

##### [默认值](https://react.docschina.org/docs/uncontrolled-components.html#default-values)

```
<input
defaultValue="Bob"
type="text"
ref={this.input} />
```

希望 React 能赋予组件一个初始值，但是不去控制后续的更新。 在这种情况下, 你可以指定一个 `defaultValue` 属性，而不是 `value`。

同样，`<input type="checkbox">` 和 `<input type="radio">` 支持 `defaultChecked`，`<select>` 和 `<textarea>` 支持 `defaultValue`。

##### [文件输入](https://react.docschina.org/docs/uncontrolled-components.html#the-file-input-tag)

在 HTML 中，`<input type="file">` 可以让用户选择一个或多个文件上传到服务器，或者通过使用 [File API](https://developer.mozilla.org/en-US/docs/Web/API/File/Using_files_from_web_applications) 进行操作。

```
<input type="file" />
```

在 React 中，`<input type="file" />` 始终是一个非受控组件，因为它的值只能由用户设置，而不能通过代码控制。

```
class FileInput extends React.Component {
  constructor(props) {
    super(props);
    this.handleSubmit = this.handleSubmit.bind(this);
    this.fileInput = React.createRef();
  }
  handleSubmit(event) {
    event.preventDefault();
    alert(
      `Selected file - ${this.fileInput.current.files[0].name}`
    );
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Upload file:
          <input type="file" ref={this.fileInput} />
        </label>
        <br />
        <button type="submit">Submit</button>
      </form>
    );
  }
}
```

#### [Web Components](https://react.docschina.org/docs/web-components.html)

#### [React 顶层 API](https://react.docschina.org/docs/react-api.html#cloneelement)

##### 转换元素

`React` 提供了几个用于操作元素的 API：

- [`cloneElement()`](https://react.docschina.org/docs/react-api.html#cloneelement)
- [`isValidElement()`](https://react.docschina.org/docs/react-api.html#isvalidelement)
- [`React.Children`](https://react.docschina.org/docs/react-api.html#reactchildren)

##### Fragments

`React` 还提供了用于减少不必要嵌套的组件。

- [`React.Fragment`](https://react.docschina.org/docs/react-api.html#reactfragment)

##### Refs

- [`React.createRef`](https://react.docschina.org/docs/react-api.html#reactcreateref)
- [`React.forwardRef`](https://react.docschina.org/docs/react-api.html#reactforwardref)

##### Suspense

Suspense 使得组件可以“等待”某些操作结束后，再进行渲染。目前，Suspense 仅支持的使用场景是：[通过 `React.lazy` 动态加载组件](https://react.docschina.org/docs/code-splitting.html#reactlazy)。它将在未来支持其它使用场景，如数据获取等。

- [`React.lazy`](https://react.docschina.org/docs/react-api.html#reactlazy)
- [`React.Suspense`](https://react.docschina.org/docs/react-api.html#reactsuspense)

##### [Hook](https://react.docschina.org/docs/react-api.html#hooks)

*Hook* 是 React 16.8 的新增特性。它可以让你在不编写 class 的情况下使用 state 以及其他的 React 特性。Hook 拥有[专属文档章节](https://react.docschina.org/docs/hooks-intro.html)和单独的 API 参考文档：

- [基础 Hook](https://react.docschina.org/docs/hooks-reference.html#basic-hooks)
  - [`useState`](https://react.docschina.org/docs/hooks-reference.html#usestate)
  - [`useEffect`](https://react.docschina.org/docs/hooks-reference.html#useeffect)
  - [`useContext`](https://react.docschina.org/docs/hooks-reference.html#usecontext)
- [额外的 Hook](https://react.docschina.org/docs/hooks-reference.html#additional-hooks)
  - [`useReducer`](https://react.docschina.org/docs/hooks-reference.html#usereducer)
  - [`useCallback`](https://react.docschina.org/docs/hooks-reference.html#usecallback)
  - [`useMemo`](https://react.docschina.org/docs/hooks-reference.html#usememo)
  - [`useRef`](https://react.docschina.org/docs/hooks-reference.html#useref)
  - [`useImperativeHandle`](https://react.docschina.org/docs/hooks-reference.html#useimperativehandle)
  - [`useLayoutEffect`](https://react.docschina.org/docs/hooks-reference.html#uselayouteffect)
  - [`useDebugValue`](https://react.docschina.org/docs/hooks-reference.html#usedebugvalue)

##### [React.PureComponent](https://react.docschina.org/docs/react-api.html#reactpurecomponent)

`React.PureComponent` 与 [`React.Component`](https://react.docschina.org/docs/react-api.html#reactcomponent) 很相似。两者的区别在于 [`React.Component`](https://react.docschina.org/docs/react-api.html#reactcomponent) 并未实现 [`shouldComponentUpdate()`](https://react.docschina.org/docs/react-component.html#shouldcomponentupdate)，而 `React.PureComponent` 中以浅层对比 prop 和 state 的方式来实现了该函数。

如果赋予 React 组件相同的 props 和 state，`render()` 函数会渲染相同的内容，那么在某些情况下使用 `React.PureComponent` 可提高性能。

[注意](https://react.docschina.org/docs/react-api.html#reactpurecomponent)

> `React.PureComponent` 中的 `shouldComponentUpdate()` 仅作对象的浅层比较。如果对象中包含复杂的数据结构，则有可能因为无法检查深层的差别，产生错误的比对结果。仅在你的 props 和 state 较为简单时，才使用 `React.PureComponent`，或者在深层数据结构发生变化时调用 [`forceUpdate()`](https://react.docschina.org/docs/react-component.html#forceupdate) 来确保组件被正确地更新。你也可以考虑使用 [immutable 对象](https://facebook.github.io/immutable-js/)加速嵌套数据的比较。

##### [React.memo](https://react.docschina.org/docs/react-api.html#reactmemo)

```
const MyComponent = React.memo(function MyComponent(props) {
  /* 使用 props 渲染 */
});
```

`React.memo` 为[高阶组件](https://react.docschina.org/docs/higher-order-components.html)。它与 [`React.PureComponent`](https://react.docschina.org/docs/react-api.html#reactpurecomponent) 非常相似，但只适用于函数组件，而不适用 class 组件。

```
function MyComponent(props) {
  /* 使用 props 渲染 */
}
function areEqual(prevProps, nextProps) {
  /*
  如果把 nextProps 传入 render 方法的返回结果与
  将 prevProps 传入 render 方法的返回结果一致则返回 true，
  否则返回 false
  */
}
export default React.memo(MyComponent, areEqual);
```

此方法仅作为**[性能优化](https://react.docschina.org/docs/optimizing-performance.html)**的方式而存在。但请不要依赖它来“阻止”渲染，因为这会产生 bug。

##### [createElement()](https://react.docschina.org/docs/react-api.html#createelement)

```
React.createElement(
  type,
  [props],
  [...children]
)
```

##### [cloneElement()](https://react.docschina.org/docs/react-api.html#cloneelement)

```
React.cloneElement(
  element,
  [props],
  [...children]
)
```

##### [isValidElement()](https://react.docschina.org/docs/react-api.html#isvalidelement)

```
React.isValidElement(object)
```

验证对象是否为 React 元素，返回值为 `true` 或 `false`。

##### [React.Children](https://react.docschina.org/docs/react-api.html#reactchildren)

`React.Children` 提供了用于处理 `this.props.children` 不透明数据结构的实用方法。

##### [React.createRef](https://react.docschina.org/docs/react-api.html#reactcreateref)

##### [React.forwardRef](https://react.docschina.org/docs/react-api.html#reactforwardref)

##### [React.lazy](https://react.docschina.org/docs/react-api.html#reactlazy)

```
// 这个组件是动态加载的
const SomeComponent = React.lazy(() => import('./SomeComponent'));
```

##### [React.Suspense](https://react.docschina.org/docs/react-api.html#reactsuspense)

`React.Suspense` 可以指定加载指示器（loading indicator），以防其组件树中的某些子组件尚未具备渲染条件。目前，懒加载组件是 `<React.Suspense>` 支持的**唯一**用例：

```
// 该组件是动态加载的
const OtherComponent = React.lazy(() => import('./OtherComponent'));

function MyComponent() {
  return (
    // 显示 <Spinner> 组件直至 OtherComponent 加载完成
    <React.Suspense fallback={<Spinner />}>
      <div>
        <OtherComponent />
      </div>
    </React.Suspense>
  );
}
```

#### [React.Component](https://react.docschina.org/docs/react-component.html#the-component-lifecycle)

##### [组件的生命周期](https://react.docschina.org/docs/react-component.html#the-component-lifecycle)

[生命周期图谱](http://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/)

[shouldComponentUpdate()](https://react.docschina.org/docs/react-component.html#shouldcomponentupdate)

此方法仅作为**[性能优化的方式](https://react.docschina.org/docs/optimizing-performance.html)**而存在。不要企图依靠此方法来“阻止”渲染，因为这可能会产生 bug。

##### [constructor()](https://react.docschina.org/docs/react-component.html#constructor)

```
constructor(props)
```

**如果不初始化 state 或不进行方法绑定，则不需要为 React 组件实现构造函数。**

##### [setState()](https://react.docschina.org/docs/react-component.html#setstate)

```
this.setState((state, props) => {
  return {counter: state.counter + props.step};
});
```

##### [forceUpdate()](https://react.docschina.org/docs/react-component.html#forceupdate)

##### [defaultProps](https://react.docschina.org/docs/react-component.html#defaultprops)

##### [state](https://react.docschina.org/docs/react-component.html#state)

 [State & 生命周期](https://react.docschina.org/docs/state-and-lifecycle.html)

#### [DOM 元素](https://react.docschina.org/docs/dom-elements.html)

#### [合成事件](https://react.docschina.org/docs/events.html)

#### [React 术语词汇表](https://react.docschina.org/docs/glossary.html)

#### [Hook 简介](https://react.docschina.org/docs/hooks-intro.html)

##### [自定义 Hook](https://react.docschina.org/docs/hooks-overview.html#building-your-own-hooks)

[`useContext`](https://react.docschina.org/docs/hooks-reference.html#usecontext)

 [`useReducer`](https://react.docschina.org/docs/hooks-reference.html#usereducer)

#### [useState](https://react.docschina.org/docs/hooks-state.html) 

```
function Counter({initialCount}) {
  const [count, setCount] = useState(initialCount);
  return (
    <>
      Count: {count}
      <button onClick={() => setCount(initialCount)}>Reset</button>
      <button onClick={() => setCount(prevCount => prevCount - 1)}>-</button>
      <button onClick={() => setCount(prevCount => prevCount + 1)}>+</button>
    </>
  );
}
```

与 class 组件中的 `setState` 方法不同，`useState` 不会自动合并更新对象

```
setState(prevState => {
  // 也可以使用 Object.assign
  return {...prevState, ...updatedValues};
});
```



#### [useEffect](https://react.docschina.org/docs/hooks-effect.html) 

[需要清除的 effect](https://react.docschina.org/docs/hooks-effect.html#%E9%9C%80%E8%A6%81%E6%B8%85%E9%99%A4%E7%9A%84-effect)

##### [清除 effect](https://react.docschina.org/docs/hooks-reference.html#cleaning-up-an-effect)

```
useEffect(() => {
  const subscription = props.source.subscribe();
  return () => {
    // 清除订阅
    subscription.unsubscribe();
  };
});
```

[effect 的执行时机](https://react.docschina.org/docs/hooks-reference.html#timing-of-effects)

[`useLayoutEffect`](https://react.docschina.org/docs/hooks-reference.html#uselayouteffect) Hook 来处理这类 effect。它和 `useEffect` 的结构相同，区别只是调用时机不同。

#### [Hook 规则](https://react.docschina.org/docs/hooks-rules.html)

只在最顶层使用 Hook

不要在循环，条件或嵌套函数中调用 Hook

#### [自定义 Hook](https://react.docschina.org/docs/hooks-custom.html)

#### [Hook API 索引](https://react.docschina.org/docs/hooks-reference.html)

##### [useContext](https://react.docschina.org/docs/hooks-reference.html#usecontext)

即使祖先使用 [`React.memo`](https://react.docschina.org/docs/react-api.html#reactmemo) 或 [`shouldComponentUpdate`](https://react.docschina.org/docs/react-component.html#shouldcomponentupdate)，也会在组件本身使用 `useContext` 时重新渲染。

[把如下代码与 Context.Provider 放在一起](https://react.docschina.org/docs/hooks-reference.html#usecontext)

##### [useReducer](https://react.docschina.org/docs/hooks-reference.html#usereducer)

```
const [state, dispatch] = useReducer(reducer, initialArg, init);
```

```
用 reducer 重写 useState 一节的计数器示例：

const initialState = {count: 0};

function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return {count: state.count + 1};
    case 'decrement':
      return {count: state.count - 1};
    default:
      throw new Error();
  }
}

function Counter() {
  const [state, dispatch] = useReducer(reducer, initialState);
  return (
    <>
      Count: {state.count}
      <button onClick={() => dispatch({type: 'decrement'})}>-</button>
      <button onClick={() => dispatch({type: 'increment'})}>+</button>
    </>
  );
}
```

##### [惰性初始化](https://react.docschina.org/docs/hooks-reference.html#lazy-initialization)

```
function init(initialCount) {
  return {count: initialCount};
}

function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return {count: state.count + 1};
    case 'decrement':
      return {count: state.count - 1};
    case 'reset':
      return init(action.payload);
    default:
      throw new Error();
  }
}

function Counter({initialCount}) {
  const [state, dispatch] = useReducer(reducer, initialCount, init);
  return (
    <>
      Count: {state.count}
      <button
        onClick={() => dispatch({type: 'reset', payload: initialCount})}>
        Reset
      </button>
      <button onClick={() => dispatch({type: 'decrement'})}>-</button>
      <button onClick={() => dispatch({type: 'increment'})}>+</button>
    </>
  );
}
```

##### [useCallback](https://react.docschina.org/docs/hooks-reference.html#usecallback)

```
const memoizedCallback = useCallback(
  () => {
    doSomething(a, b);
  },
  [a, b],
);
```

##### [useMemo](https://react.docschina.org/docs/hooks-reference.html#usecallback)

##### [useRef](https://react.docschina.org/docs/hooks-reference.html#useref)

##### [useImperativeHandle](https://react.docschina.org/docs/hooks-reference.html#useimperativehandle)

##### [useLayoutEffect](https://react.docschina.org/docs/hooks-reference.html#uselayouteffect)

##### [useDebugValue](https://react.docschina.org/docs/hooks-reference.html#usedebugvalue)

#### [Hooks FAQ](https://react.docschina.org/docs/hooks-faq.html)



#### [测试概览](https://react.docschina.org/docs/testing.html)

**[Jest](https://facebook.github.io/jest/)** 

#### [AJAX and APIs](https://react.docschina.org/docs/faq-ajax.html)

比如社区比较流行的 [Axios](https://github.com/axios/axios)，[jQuery AJAX](https://api.jquery.com/jQuery.ajax/)，或者是浏览器内置的 [window.fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)。

在 [`componentDidMount`](https://react.docschina.org/docs/react-component.html#mounting) 这个生命周期函数中发起 AJAX 请求

#### [在组件中使用事件处理函数](https://react.docschina.org/docs/faq-functions.html)

[Yehuda Katz 的文章](https://yehudakatz.com/2011/08/11/understanding-javascript-function-invocation-and-this/)详细解释了什么是绑定，以及函数在 JavaScript 中怎么起作用。

传递参数

```
<button onClick={() => this.handleClick(id)} />
```

```
<button onClick={this.handleClick.bind(this, id)} />
```

##### [通过箭头函数传递参数](https://react.docschina.org/docs/faq-functions.html#example-passing-params-using-arrow-functions)

```
<ul>
  {this.state.letters.map(letter =>
    <li key={letter} onClick={() => this.handleClick(letter)}>
      {letter}
    </li>
  )}
</ul>
```

##### [通过 data-attributes 传递参数](https://react.docschina.org/docs/faq-functions.html#example-passing-params-using-data-attributes)

```
handleClick(e) {
    this.setState({
      justClicked: e.target.dataset.letter
    });
}

<ul>
  {this.state.letters.map(letter =>
    <li key={letter} data-letter={letter} onClick={this.handleClick}>
      {letter}
    </li>
  )}
</ul>
```

##### [怎样阻止函数被调用太快或者太多次？](https://react.docschina.org/docs/faq-functions.html#how-can-i-prevent-a-function-from-being-called-too-quickly-or-too-many-times-in-a-row)

如果你有一个 `onClick` 或者 `onScroll` 这样的事件处理器，想要阻止回调被触发的太快，那么可以限制执行回调的速度，可以通过以下几种方式做到这点：

- **节流**：基于时间的频率来进行抽样更改 (例如 [`_.throttle`](https://lodash.com/docs#throttle))
- **防抖**：一段时间的不活动之后发布更改 (例如 [`_.debounce`](https://lodash.com/docs#debounce))
- **`requestAnimationFrame` 节流**：基于 requestAnimationFrame 的抽样更改 (例如 [raf-schd](https://react.docschina.org/docs/[`raf-schd`](https://github.com/alexreardon/raf-schd)))

可以看这个比较 throttle 和 debounce 的[可视化页面](http://demo.nimius.net/debounce_throttle/)

#### [节流](https://react.docschina.org/docs/faq-functions.html#throttle)

```
import throttle from 'lodash.throttle';

class LoadMoreButton extends React.Component {
  constructor(props) {
    super(props);
    this.handleClick = this.handleClick.bind(this);
    this.handleClickThrottled = throttle(this.handleClick, 1000);
  }

  componentWillUnmount() {
    this.handleClickThrottled.cancel();
  }

  render() {
    return <button onClick={this.handleClickThrottled}>Load More</button>;
  }

  handleClick() {
    this.props.loadMore();
  }
}

```

#### [防抖](https://react.docschina.org/docs/faq-functions.html#debounce)

防抖确保函数不会在上一次被调用之后一定量的时间内被执行。当必须进行一些费时的计算来响应快速派发的事件时（比如`鼠标滚动或键盘事件时`），防抖是非常有用的。下面这个例子以 250ms 的延迟来改变文本输入。

```
import debounce from 'lodash.debounce';

class Searchbox extends React.Component {
  constructor(props) {
    super(props);
    this.handleChange = this.handleChange.bind(this);
    this.emitChangeDebounced = debounce(this.emitChange, 250);
  }

  componentWillUnmount() {
    this.emitChangeDebounced.cancel();
  }

  render() {
    return (
      <input
        type="text"
        onChange={this.handleChange}
        placeholder="Search..."
        defaultValue={this.props.value}
      />
    );
  }

  handleChange(e) {
    this.emitChangeDebounced(e.target.value);
  }

  emitChange(value) {
    this.props.onChange(value);
  }
}

```



#### [组件状态](https://react.docschina.org/docs/faq-state.html)