---
title: Redux笔记
date: 2021-04-12 14:24:57
tags: 
- Redux
categories:
- 学习笔记
- Redux
---

[Redux](https://redux.js.org/)

[Redux 中文官网](http://cn.redux.js.org/)

[React Redux](https://react-redux.js.org/)

[Redux 中文文档](https://www.redux.org.cn/)

[七步搞定React Redux](https://zhuanlan.zhihu.com/p/103420294)

[React-Redux](https://blog.csdn.net/weixin_57218747/article/details/118070930)

[「HearLing」React学习之路-redux、react-redux](https://baijiahao.baidu.com/s?id=1707122824099613498&wfr=spider&for=pc)

[学习资源](http://cn.redux.js.org/introduction/learning-resources)

[示例](https://github.com/reduxjs/redux.git)

[Redux（基本用法）](https://www.jianshu.com/p/9dcfa43d4e5a)

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

#### Action 

Action 是把数据传入 store 的惟一途径，所以任何数据，无论来自 UI 事件，网络回调或者是其它资源如 WebSockets，最终都应该以 action 的形式被 dispatch

#### [applyMiddleware(...middleware)](http://cn.redux.js.org/api/applymiddleware/)

[redux-thunk](https://github.com/reduxjs/redux-thunk)

[Writing Logic with Thunks](https://redux.js.org/usage/writing-logic-thunks)

Middleware 是一个组合 [dispatch 函数](http://cn.redux.js.org/understanding/thinking-in-redux/glossary/#dispatching-function) 的高阶函数，返回一个新的 dispatch 函数，通常将[异步 action](http://cn.redux.js.org/understanding/thinking-in-redux/glossary/#异步-action) 转换成 action

### [subscribe(listener)](http://cn.redux.js.org/api/store#subscribelistener)

[Redux学习篇:关于store.subscribe()监听方法与取消监听的认识](https://blog.csdn.net/weixin_40119412/article/details/120811920)

> Store 允许使用store.subscribe方法设置[监听](https://so.csdn.net/so/search?q=监听&spm=1001.2101.3001.7020)函数，一旦 State 发生变化，就自动执行这个函数。
>
> store.subscribe方法返回一个函数，调用这个函数就可以解除监听