---
title: Redux笔记
date: 2021-04-12 14:24:57
tags: 
- Redux
categories:
- 学习笔记
- Redux
---

[Redux-Github](https://github.com/reduxjs)

[Redux-官网](https://redux.js.org/)

[Redux 中文官网](http://cn.redux.js.org/)

[React Redux](https://react-redux.js.org/)

[Redux 中文文档](https://www.redux.org.cn/)

[Redux工具包-中文文档](https://redux-toolkit-cn.netlify.app/)

[Redux Toolkit](https://redux-toolkit.js.org/)

[七步搞定React Redux](https://zhuanlan.zhihu.com/p/103420294)

[React-Redux](https://blog.csdn.net/weixin_57218747/article/details/118070930)

[「HearLing」React学习之路-redux、react-redux](https://baijiahao.baidu.com/s?id=1707122824099613498&wfr=spider&for=pc)

[学习资源](http://cn.redux.js.org/introduction/learning-resources)

[示例](https://github.com/reduxjs/redux.git)

[Redux（基本用法）](https://www.jianshu.com/p/9dcfa43d4e5a)

**[使用Redux工具包的示例----rtk-convert-todos-example](https://github.com/reduxjs/rtk-convert-todos-example)**

Redux 有很好的[文档](https://link.jianshu.com/?t=http://redux.js.org/)，还有配套的小视频（[前30集](https://link.jianshu.com/?t=https://egghead.io/courses/getting-started-with-redux)，[后30集](https://link.jianshu.com/?t=https://egghead.io/courses/building-react-applications-with-idiomatic-redux)）

#### [createStore(reducer, [preloadedState], [enhancer])](http://cn.redux.js.org/api/createstore)

`reducer` *(Function)*: 接收两个参数，分别是当前的 state 树和要处理的 [action](http://cn.redux.js.org/understanding/thinking-in-redux/glossary#action)，返回新的 [state 树](http://cn.redux.js.org/understanding/thinking-in-redux/glossary#state)

 Reducer 必须是**纯函数**

**不要在 reducer 中调用 API 接口请求**

```
import { createStore } from 'redux'

function todos(state = [], action) {
  switch (action.type) {
    case 'ADD_TODO':
      return state.concat([action.text])
    default:
      return state
  }
}

let store = createStore(todos, ['Use Redux'])

store.dispatch({
  type: 'ADD_TODO',
  text: 'Read the docs'
})

console.log(store.getState())
// [ 'Use Redux', 'Read the docs' ]
```

#### 小贴士[#](http://cn.redux.js.org/api/createstore#小贴士)

- 应用中不要创建多个 store！相反，使用 [`combineReducers`](http://cn.redux.js.org/api/combinereducers) 来把多个 reducer 创建成一个根 reducer。
- Redux state 通常是普通 JS 对象或者数组。
- 如果 state 是普通对象，永远不要修改它！比如，reducer 里不要使用 `Object.assign(state, newData)`，应该使用 `Object.assign({}, state, newData)`。这样才不会覆盖旧的 `state`。如果可以的话，也可以使用 [对象拓展操作符（object spread spread operator](http://cn.redux.js.org/recipes/using-object-spread-operator) 特性中的 `return { ...state, ...newData }`。
- 对于服务端运行的同构应用，为每一个请求创建一个 store 实例，以此让 store 相隔离。dispatch 一系列请求数据的 action 到 store 实例上，等待请求完成后再在服务端渲染应用。
- 当 store 创建后，Redux 会 dispatch 一个 action 到 reducer 上，来用初始的 state 来填充 store。你不需要处理这个 action。但要记住，如果第一个参数也就是传入的 state 是 `undefined` 的话，reducer 应该返回初始的 state 值。
- 要使用多个 store 增强器的时候，你可能需要使用 [compose](http://cn.redux.js.org/api/compose)



#### [combineReducers(reducers)](http://cn.redux.js.org/api/combinereducers/)

`combineReducers` 辅助函数的作用是，把一个由多个不同 reducer 函数作为 value 的 object，合并成一个最终的 reducer 函数，然后就可以对这个 reducer 调用 [`createStore`](http://cn.redux.js.org/api/createstore) 方

##### 示例

`reducers/todos.js`

```
export default function todos(state = [], action) {
  switch (action.type) {
    case 'ADD_TODO':
      return state.concat([action.text])
    default:
      return state
  }
}
```

`reducers/counter.js`

```
export default function counter(state = 0, action) {
  switch (action.type) {
    case 'INCREMENT':
      return state + 1
    case 'DECREMENT':
      return state - 1
    default:
      return state
  }
}
```

`reducers/index.js`

```
import { combineReducers } from 'redux'
import todos from './todos'
import counter from './counter'

export default combineReducers({
  todos,
  counter
})
```

`App.js`

```
import { createStore } from 'redux'
import reducer from './reducers/index'

let store = createStore(reducer)
console.log(store.getState())
// {
//   counter: 0,
//   todos: []
// }

store.dispatch({
  type: 'ADD_TODO',
  text: 'Use Redux'
})
console.log(store.getState())
// {
//   counter: 0,
//   todos: [ 'Use Redux' ]
// }
```

#### [Store](http://cn.redux.js.org/api/store/#store-%E6%96%B9%E6%B3%95)

#### [Store](http://cn.redux.js.org/tutorials/essentials/part-1-overview-concepts#store)

```
import { configureStore } from '@reduxjs/toolkit'

const store = configureStore({ reducer: counterReducer })

console.log(store.getState())
// {value: 0}
```





#### Action 

Action 是把数据传入 store 的惟一途径，所以任何数据，无论来自 UI 事件，网络回调或者是其它资源如 WebSockets，最终都应该以 action 的形式被 dispatch

[**action**](http://cn.redux.js.org/tutorials/essentials/part-1-overview-concepts#action) 是一个具有 `type` 字段的普通 JavaScript 对象。**你可以将 action 视为描述应用程序中发生了什么的事件**.

`type` 字段是一个字符串，给这个 action 一个描述性的名字，比如`"todos/todoAdded"`。我们通常把那个类型的字符串写成“域/事件名称”，其中第一部分是这个 action 所属的特征或类别，第二部分是发生的具体事情。

action 对象可以有其他字段，其中包含有关发生的事情的附加信息。按照惯例，我们将该信息放在名为 `payload` 的字段中。

```
const addTodoAction = {
  type: 'todos/todoAdded',
  payload: 'Buy milk'
}
```

[**action creator**](http://cn.redux.js.org/tutorials/essentials/part-1-overview-concepts#action-creator) 是一个创建并返回一个 action 对象的函数。它的作用是让你不必每次都手动编写 action 对象：

```
const addTodo = text => {
  return {
    type: 'todos/todoAdded',
    payload: text
  }
}
```

#### [Reducer](http://cn.redux.js.org/tutorials/essentials/part-1-overview-concepts#reducer)

**reducer** 是一个函数，接收当前的 `state` 和一个 `action` 对象，必要时决定如何更新状态，并返回新状态。函数签名是：`(state, action) => newState`。 **你可以将 reducer 视为一个事件监听器，它根据接收到的 action（事件）类型处理事件。**



- 禁止任何异步逻辑、依赖随机值或导致其他“副作用”的代码

```
const initialState = { value: 0 }

function counterReducer(state = initialState, action) {
  // 检查 reducer 是否关心这个 action
  if (action.type === 'counter/increment') {
    // 如果是，复制 `state`
    return {
      ...state,
      // 使用新值更新 state 副本
      value: state.value + 1
    }
  }
  // 返回原来的 state 不变
  return state
}
```

#### [Dispatch](http://cn.redux.js.org/tutorials/essentials/part-1-overview-concepts#dispatch)

```
store.dispatch({ type: 'counter/increment' })

console.log(store.getState())
```

我们通常调用 action creator 来调用 action：

```
const increment = () => {
  return {
    type: 'counter/increment'
  }
}

store.dispatch(increment())

console.log(store.getState())
// {value: 2}
```

### [Redux 数据流](http://cn.redux.js.org/tutorials/essentials/part-1-overview-concepts#redux-%E6%95%B0%E6%8D%AE%E6%B5%81)

初始启动：

- 使用最顶层的 root reducer 函数创建 Redux store



![动画的方式来表达数据流更新](http://cn.redux.js.org/assets/images/ReduxDataFlowDiagram-49fa8c3968371d9ef6f2a1486bd40a26.gif)



#### 总结

- Redux 是一个管理全局应用状态的库
  - Redux 通常与 React-Redux 库一起使用，把 Redux 和 React 集成在一起
  - Redux Toolkit 是编写 Redux 逻辑的推荐方式
- Redux 使用 "单向数据流"
  - State 描述了应用程序在某个时间点的状态，UI 基于该状态渲染
  - 当应用程序中发生某些事情时：
    - UI dispatch 一个 action
    - store 调用 reducer，随后根据发生的事情来更新 state
    - store 通知 UI state 发生了变化
  - UI 基于新 state 重新渲染
- Redux 有这几种类型的代码
  - *Action* 是有 `type` 字段的纯对象，描述发生了什么
  - *Reducer* 是纯函数，基于先前的 state 和 action 来计算新的 state
  - 每当 dispatch 一个 action 后，*store* 就会调用 root reducer

#### [applyMiddleware(...middleware)](http://cn.redux.js.org/api/applymiddleware/)

[redux-thunk](https://github.com/reduxjs/redux-thunk)

[Writing Logic with Thunks](https://redux.js.org/usage/writing-logic-thunks)

Middleware 是一个组合 [dispatch 函数](http://cn.redux.js.org/understanding/thinking-in-redux/glossary/#dispatching-function) 的高阶函数，返回一个新的 dispatch 函数，通常将[异步 action](http://cn.redux.js.org/understanding/thinking-in-redux/glossary/#异步-action) 转换成 action

### [subscribe(listener)](http://cn.redux.js.org/api/store#subscribelistener)

[Redux学习篇:关于store.subscribe()监听方法与取消监听的认识](https://blog.csdn.net/weixin_40119412/article/details/120811920)

> Store 允许使用store.subscribe方法设置[监听](https://so.csdn.net/so/search?q=监听&spm=1001.2101.3001.7020)函数，一旦 State 发生变化，就自动执行这个函数。
>
> store.subscribe方法返回一个函数，调用这个函数就可以解除监听



## 计数器示例应用程序

本项目使用 [Create-React-App 的官方 Redux 模板](https://github.com/reduxjs/cra-template-redux) 创建。开箱即用，它已经配置了标准的 Redux 应用程序结构，使用 [Redux Toolkit](https://redux-toolkit.js.org/) 创建 Redux 存储和逻辑，以及 [React-Redux](https://react-redux.js.org/) 将 Redux 存储和 React 组件连接在一起。

```
npx create-react-app redux-essentials-example --template redux
```

#### react-redux

**[react-redux](https://baijiahao.baidu.com/s?id=1707122824099613498&wfr=spider&for=pc)发布了新的版本，与之前的contextAPI分离，提供对hooks的支持，那这不就更香了新的redux带来的改变**

1. **「不再需要使用」**mapStateToProps，mapDispatchToProps和connect来维护单独的container组件和UI组件，而是在组件中直接使用redux提供的hooks,读取redux中的state。
2. 可以将任何现有的自定义**「hooks与redux集成」**，而不是将通过hooks创建的state，作为参数传递给其他hooks



- **「useSelector：」** 用于从Redux存储的state中提取值并订阅该state。

- **「useDispatch：」** 除了读取store中的state，还能dispatch actions更新store中的state。

- **「useStore：」** 用于获取创建的store实例

#### [useSelector](http://cn.redux.js.org/tutorials/fundamentals/part-5-ui-react/#reading-state-from-the-store-with-useselector) 

<span style="color:red">使用useSelector、useDispatch等HooksApi替代connect，减少模板代码。</span>

`useSelector` accepts a single function, which we call a **selector** function. **A selector is a function that takes the entire Redux store state as its argument, reads some value from the state, and returns that result**.

```
const selectTodos = state => state.todos
```

```
const selectTotalCompletedTodos = state => {
  const completedTodos = state.todos.filter(todo => todo.completed)
  return completedTodos.length
}
```

```
import React from 'react'
import { useSelector } from 'react-redux'
import TodoListItem from './TodoListItem'

const selectTodos = state => state.todos

const TodoList = () => {
  const todos = useSelector(selectTodos)

  // since `todos` is an array, we can loop over it
  const renderedListItems = todos.map(todo => {
    return <TodoListItem key={todo.id} todo={todo} />
  })

  return <ul className="todo-list">{renderedListItems}</ul>
}

export default TodoList
```

> useSelector 自动为我们订阅了 Redux 存储！ 这样，任何时候分派一个动作，它都会立即再次调用它的选择器函数。 如果选择器返回的值与上次运行时相比发生了变化，useSelector 将强制我们的组件使用新数据重新渲染。 我们所要做的就是在我们的组件中调用 useSelector() 一次，它会为我们完成剩下的工作

还值得注意的是，我们不必将选择器函数编写为单独的变量。您可以直接在 useSelector 调用中编写选择器函数

```
const todos = useSelector(state => state.todos)
```

#### [useDispatch](http://cn.redux.js.org/tutorials/fundamentals/part-5-ui-react/#dispatching-actions-with-usedispatch)

```
import React, { useState } from 'react'
import { useDispatch } from 'react-redux'

const Header = () => {
  const [text, setText] = useState('')
  const dispatch = useDispatch()

  const handleChange = e => setText(e.target.value)

  const handleKeyDown = e => {
    const trimmedText = e.target.value.trim()
    // If the user pressed the Enter key:
    if (e.key === 'Enter' && trimmedText) {
      // Dispatch the "todo added" action with this text
      dispatch({ type: 'todos/todoAdded', payload: trimmedText })
      // And clear out the text input
      setText('')
    }
  }

  return (
    <input
      type="text"
      placeholder="What needs to be done?"
      autoFocus={true}
      value={text}
      onChange={handleChange}
      onKeyDown={handleKeyDown}
    />
  )
}

export default Header
```

hook 是一个 JS 函数，所以它不能自动从 store.js 中自动导入 store

We do this by **rendering a `<Provider>` component around our entire `<App>`, and passing the Redux store as a prop to `<Provider>`**

```
import React from 'react'
import ReactDOM from 'react-dom'
import { Provider } from 'react-redux'

import App from './App'
import store from './store'

ReactDOM.render(
  // Render a `<Provider>` around the entire `<App>`,
  // and pass the Redux store to as a prop
  <React.StrictMode>
    <Provider store={store}>
      <App />
    </Provider>
  </React.StrictMode>,
  document.getElementById('root')
)
```

React-Redux 与 React 结合使用的关键部分：

- Call the `useSelector` hook to read data in React components
- Call the `useDispatch` hook to dispatch actions in React components
- Put `<Provider store={store}>` around your entire `<App>` component so that other components can talk to the store

### Global State, Component State, and Forms

[在 React + Redux 应用程序中，你的全局状态应该放在 Redux 存储中，而你的本地状态应该留在 React 组件中](http://cn.redux.js.org/tutorials/fundamentals/part-5-ui-react/#react-redux-patterns)：

- Do other parts of the application care about this data?
- Do you need to be able to create further derived data based on this original data?
- Is the same data being used to drive multiple components?
- Is there value to you in being able to restore this state to a given point in time (ie, time travel debugging)?
- Do you want to cache the data (ie, use what's in state if it's already there instead of re-requesting it)?
- Do you want to keep this data consistent while hot-reloading UI components (which may lose their internal state when swapped)?

**Most form state probably shouldn't be kept in Redux**



### [Using Multiple Selectors in a Component](http://cn.redux.js.org/tutorials/fundamentals/part-5-ui-react/#using-multiple-selectors-in-a-component)

**We can call `useSelector` multiple times within one component**. In fact, this is actually a good idea - **each call to `useSelector` should always return the smallest amount of state possible**





### [**Redux Toolkit**](https://redux-toolkit.js.org/)

#### [Redux Toolkit 是什么？](http://cn.redux.js.org/redux-toolkit/overview/#redux-toolkit-%E6%98%AF%E4%BB%80%E4%B9%88%EF%BC%9F)

> 简化最常见场景下的 Redux 开发，包括配置 store、定义 reducer，不可变的更新逻辑、甚至可以立即创建整个状态的 “切片 slice”，而无需手动编写任何 action creator 或者 action type。它还包括使用最广泛的 Redux 插件，例如 Redux Thunk 用于异步逻辑，而 Reselect 用于编写选择器 selector 函数，因此你可以立即使用它们。

#### [createSlice](https://redux-toolkit.js.org/api/createSlice)

接受一组化 reducer 函数，一个 slice 切片名和初始状态 initial state，并自动生成具有相应 action creator 和 action type 的 slice reducer

##### nanoid 

```
import { nanoid } from '@reduxjs/toolkit'

const id = nanoid()
```

`createSlice` will return an object that looks like：

```
{
    name : string,
    reducer : ReducerFunction,
    actions : Record<string, ActionCreator>,
    caseReducers: Record<string, CaseReducer>.
    getInitialState: () => State
}
```

```
{
  name: "todos",
  reducer: (state, action) => newState,
  actions: {
    addTodo: (payload) => ({type: "todos/addTodo", payload}),
    toggleTodo: (payload) => ({type: "todos/toggleTodo", payload})
  },
  caseReducers: {
    addTodo: (state, action) => newState,
    toggleTodo: (state, action) => newState,
  }
}
```



##### Examples

```
import { createSlice, createAction } from '@reduxjs/toolkit'
import { createStore, combineReducers } from 'redux'

const incrementBy = createAction('incrementBy')
const decrementBy = createAction('decrementBy')

const counter = createSlice({
  name: 'counter',
  initialState: 0,
  reducers: {
    increment: (state) => state + 1,
    decrement: (state) => state - 1,
    multiply: {
      reducer: (state, action) => state * action.payload,
      prepare: (value) => ({ payload: value || 2 }), // fallback if the payload is a falsy value
    },
  },
  // "builder callback API", recommended for TypeScript users
  extraReducers: (builder) => {
    builder.addCase(incrementBy, (state, action) => {
      return state + action.payload
    })
    builder.addCase(decrementBy, (state, action) => {
      return state - action.payload
    })
  },
})

const user = createSlice({
  name: 'user',
  initialState: { name: '', age: 20 },
  reducers: {
    setUserName: (state, action) => {
      state.name = action.payload // mutate the state all you want with immer
    },
  },
  // "map object API"
  extraReducers: {
    [counter.actions.increment]: (
      state,
      action /* action will be inferred as "any", as the map notation does not contain type information */
    ) => {
      state.age += 1
    },
  },
})

const reducer = combineReducers({
  counter: counter.reducer,
  user: user.reducer,
})

const store = createStore(reducer)

store.dispatch(counter.actions.increment())
// -> { counter: 1, user: {name : '', age: 21} }
store.dispatch(counter.actions.increment())
// -> { counter: 2, user: {name: '', age: 22} }
store.dispatch(counter.actions.multiply(3))
// -> { counter: 6, user: {name: '', age: 22} }
store.dispatch(counter.actions.multiply())
// -> { counter: 12, user: {name: '', age: 22} }
console.log(`${counter.actions.decrement}`)
// -> "counter/decrement"
store.dispatch(user.actions.setUserName('eric'))
// -> { counter: 12, user: { name: 'eric', age: 22} }
```

#### [createAction](https://redux-toolkit.js.org/api/createAction)

创建actions的原先做法：

```
const INCREMENT = 'counter/increment'

function increment(amount) {
  return {
    type: INCREMENT,
    payload: amount,
  }
}

const action = increment(3)
// { type: 'counter/increment', payload: 3 }
```

The `createAction` helper combines these two declarations into one. It takes an action type and returns an action creator for that type. The action creator can be called either without arguments or with a `payload` to be attached to the action. Also, the action creator overrides [toString()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/toString) so that the action type becomes its string representation.

```
import { createAction } from '@reduxjs/toolkit'

const increment = createAction('counter/increment')

let action = increment()
// { type: 'counter/increment' }

action = increment(3)
// returns { type: 'counter/increment', payload: 3 }

console.log(increment.toString())
// 'counter/increment'

console.log(`The action type is: ${increment}`)
// 'The action type is: counter/increment'
```



`createAction` accepts an optional second argument: a "prepare callback" that will be used to construct the payload value.

```
import { createAction, nanoid } from '@reduxjs/toolkit'

const addTodo = createAction('todos/add', function prepare(text) {
  return {
    payload: {
      text,
      id: nanoid(),
      createdAt: new Date().toISOString(),
    },
  }
})

console.log(addTodo('Write more docs'))
/**
 * {
 *   type: 'todos/add',
 *   payload: {
 *     text: 'Write more docs',
 *     id: '4AJvwMSWEHCchcWYga3dj',
 *     createdAt: '2019-10-03T07:53:36.581Z'
 *   }
 * }
 **/
```

#### [Usage with createReducer()](https://redux-toolkit.js.org/api/createAction)

```
import { createAction, createReducer } from '@reduxjs/toolkit'

const increment = createAction('counter/increment')
const decrement = createAction('counter/decrement')

const counterReducer = createReducer(0, (builder) => {
  builder.addCase(increment, (state, action) => state + action.payload)
  builder.addCase(decrement, (state, action) => state - action.payload)
})
```

#### [builder.addCase](https://redux-toolkit.js.org/api/createReducer#builderaddcase)

#### Parameters

- **actionCreator** Either a plain action type string, or an action creator generated by [`createAction`](https://redux-toolkit.js.org/api/createAction) that can be used to determine the action type.
- **reducer** The actual case reducer function.

#### [createReducer()](https://redux-toolkit.js.org/api/createReducer)

Redux [reducers](https://redux.js.org/basics/reducers) are often implemented using a `switch` statement, with one `case` for every handled action type

```
const initialState = { value: 0 }

function counterReducer(state = initialState, action) {
  switch (action.type) {
    case 'increment':
      return { ...state, value: state.value + 1 }
    case 'decrement':
      return { ...state, value: state.value - 1 }
    case 'incrementByAmount':
      return { ...state, value: state.value + action.payload }
    default:
      return state
  }
}
```

With `createReducer`, your reducers instead look like:

```
import { createAction, createReducer } from '@reduxjs/toolkit'

const increment = createAction('counter/increment')
const decrement = createAction('counter/decrement')
const incrementByAmount = createAction('counter/incrementByAmount')

const initialState = { value: 0 }

const counterReducer = createReducer(initialState, (builder) => {
  builder
    .addCase(increment, (state, action) => {
      state.value++
    })
    .addCase(decrement, (state, action) => {
      state.value--
    })
    .addCase(incrementByAmount, (state, action) => {
      state.value += action.payload
    })
})
```

##### Parameters

- **initialState** `State | (() => State)`:

- **builderCallback** `(builder: Builder) => void`      ` builder.addCase(actionCreatorOrType, reducer)`

#### [configureStore](https://redux-toolkit.js.org/api/configureStore)

#### [getDefaultMiddleware](https://redux-toolkit.js.org/api/getDefaultMiddleware)



[Redux工具包-使用教程](https://redux-toolkit-cn.netlify.app/tutorials/intermediate-tutorial)



#### Store数据-持久化

[如何在React中实现全局数据的状态持久化？一篇文章让你看懂状态持久化](https://blog.csdn.net/weixin_47077674/article/details/122617851?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522165025080216782246469362%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fall.%2522%257D&request_id=165025080216782246469362&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~first_rank_ecpm_v1~rank_v31_ecpm-1-122617851.142^v9^control,157^v4^control&utm_term=%E5%A6%82%E4%BD%95%E5%9C%A8React%E4%B8%AD%E5%AE%9E%E7%8E%B0%E5%85%A8%E5%B1%80%E6%95%B0%E6%8D%AE%E7%9A%84%E7%8A%B6%E6%80%81%E6%8C%81%E4%B9%85%E5%8C%96&spm=1018.2226.3001.4187)

[react-几步搞定redux-persist-持久化存储](https://www.jianshu.com/p/59a85632d781)

##### src/app/RootReducers.js

```
import { combineReducers } from "@reduxjs/toolkit";
import userReducer from "../reducers/userSlice";

export default combineReducers({
    user: userReducer
})
```

##### src/app/store.js

```
import { configureStore } from '@reduxjs/toolkit';
import { persistStore, persistReducer } from 'redux-persist';
import storage from 'redux-persist/lib/storage';
import rootReducer from './RootReducers';

const persistConfig = {
  key: 'root',
  storage
}

const persistedReducer = persistReducer(
  persistConfig,
  rootReducer
)

export const store = configureStore({
  reducer: persistedReducer,
  middleware: (getDefaultMiddleware) =>
    getDefaultMiddleware({
      serializableCheck: false,
    }),
})
export const persistor = persistStore(store)

```

##### src/index.js

```
import React from 'react';
import { Provider } from 'react-redux';
import { BrowserRouter } from 'react-router-dom'
import './index.css';
import App from './App';
import * as serviceWorker from './serviceWorker';
import { store, persistor } from './app/store';
import { PersistGate } from "redux-persist/integration/react"

import { createRoot } from 'react-dom/client';
const container = document.getElementById('root');
const root = createRoot(container);
root.render(
    <React.StrictMode>
        <Provider store={store}>
            <PersistGate loading={null} persistor={persistor}>
                <BrowserRouter>
                    <App/>
                </BrowserRouter>
            </PersistGate>
    </Provider>
    </React.StrictMode>
);

// If you want your app to work offline and load faster, you can change
// unregister() to register() below. Note this comes with some pitfalls.
// Learn more about service workers: https://bit.ly/CRA-PWA
serviceWorker.unregister();
```



```
{/* <Routes>
        <Route path="/" element={<Container/>} />
        <Route path="/login" element={<Login />} />
        <Route path="/home" element={<Home />}>
          <Route path="/home/:id" element={<Home />} />
        </Route> */}
        {/* <Route path="/product" element={<Container />}>
          <Route path="/product/add" element={<AddProduct />} />
          <Route path="/product/edit/:id" element={<EditProduct />} />
        </Route> */}

      {/* </Routes> */}
```

