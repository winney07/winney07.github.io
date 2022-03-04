---
title: React-使用笔记
date: 2021-03-02 14:15:34
tags:
- React
categories:
- 工作笔记
- React
---

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