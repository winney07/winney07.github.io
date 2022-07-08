---
title: Vue3.0-笔记
date: 2022-06-08 16:35:13
tags:
 Vue3
---

#### [Vue3.x--系列学习](https://www.kancloud.cn/cyyspring/vue3/2696499)

#### [vue3+ts(2)：TypeScript 语法汇总](https://zhuanlan.zhihu.com/p/360553463)

- vue3+ts项目系列第1篇**[《vue3项目从0到1搭建》](https://link.zhihu.com/?target=https%3A//mp.weixin.qq.com/s/MpmoEbJPTWKCSHdtpd1jCw)**
- vue3+ts项目系列第2篇**[《TypeScript 语法汇总》](https://link.zhihu.com/?target=https%3A//lianpf.github.io/posts/%E5%89%8D%E7%AB%AF%E5%9F%BA%E7%A1%80/03.ts%E5%9F%BA%E7%A1%80%E8%AF%AD%E6%B3%95/)**
- vue3+ts项目系列第3篇**[《vue3组合式api及重要属性变更》](https://link.zhihu.com/?target=https%3A//lianpf.github.io/posts/%E5%89%8D%E7%AB%AF%E6%A1%86%E6%9E%B6/07.vue3%E7%BB%84%E5%90%88%E5%BC%8Fapi%E5%8F%8A%E9%87%8D%E8%A6%81%E5%B1%9E%E6%80%A7%E5%8F%98%E6%9B%B4/)**

#### 仅限 TypeScript 的功能

#### [#](https://v3.cn.vuejs.org/api/sfc-script-setup.html#仅限类型的-props-emit-声明)仅限类型的 props/emit 声明

[关于vue3.x中的emits的用法](https://blog.csdn.net/qq_43612538/article/details/117753657)

[【vue3 之 emits & $emit() 讲解 】监听子组件事件、emit事件验证、options写法、composition setup写法](https://blog.csdn.net/lijiahui_/article/details/123944591)

[vue：匿名slot、具名slot、作用域slot（技术栈Vue3 + TS）](https://blog.csdn.net/snowball_li/article/details/123298575)

[博客参考](https://www.cnblogs.com/jing-zhe/p/14171863.html)

**diff方法优化：http://vue-next-template-explorer.netlify.app/**

[组合式API](https://v3.cn.vuejs.org/api/composition-api.html#setup)

[vscode自定义代码片段](https://blog.csdn.net/weixin_51754955/article/details/119062659)

[vscode 中，vue导入组件路径提示](https://blog.csdn.net/weixin_46357198/article/details/121308557)

[带你熟练vue3的setup语法糖＜script setup＞](https://blog.csdn.net/qq_61233877/article/details/125092310)

[vue3的script setup语法糖中使用toRefs](https://blog.csdn.net/weixin_42776027/article/details/121007438)

[vue3的script setup语法糖中使用toRefs](https://wenku.baidu.com/view/dd64aaffa68da0116c175f0e7cd184254b351b21.html)

[Vue3 学习笔记—Script Setup 语法糖用了才知道有多爽](http://www.zzvips.com/article/212964.html)

[Vue3新的script setup语法糖](https://www.cnblogs.com/MrSlow/p/15777696.html)

#### 安装Vue Language Features (Volar)插件



### [防抖和节流](https://v3.cn.vuejs.org/guide/data-methods.html#%E9%98%B2%E6%8A%96%E5%92%8C%E8%8A%82%E6%B5%81)

Vue 没有内置支持防抖和节流，但可以使用 [Lodash](https://lodash.com/) 等库来实现



#### vee-validate

Vue项目中使用[vee-validate进行表单验证](https://wenku.baidu.com/view/7aba411740323968011ca300a6c30c225901f022.html)



#### 自动添加前缀

Vue 是通过运行时检测来确定哪些样式的 property 是被当前浏览器支持的。如果浏览器不支持某个 property，Vue 会进行多次测试以找到支持它的前缀。



####  在 `<template>` 元素上使用 `v-if` 条件渲染分组



#### Vue3-VSCode代码片段

```
"vue-template": {
		"prefix": "vue3",
		"body": [
		"<template>",
		"",
		"</template>",
		"",
		"<script setup lang='ts'>",
		"",
		"</script>",
		"",
		"<style lang='less'>",
		"",
		"</style>",
		],
		"description": "my vue3 template"
	}
```

#### [props -- defineProps Ts 版本](https://www.kancloud.cn/cyyspring/vue3/2748147)

#### [vue3 setup单文件组件中配置inheritAttrs](https://blog.csdn.net/xuefeng11111/article/details/121584181)

```
<script>
    export default {
        inheritAttrs: false
    }
</script>
```

##### ts写法

```
<script lang='ts'>
    export default {
        inheritAttrs: false
    }
</script>
```



#### [mande-插件](https://www.npmjs.com/package/mande)

fetch-插件

*mande* has better defaults to communicate with APIs using `fetch`

```
npm install mande
yarn add mande
```

```
import { mande } from 'mande'

const users = mande('/api/users')

users
  .post({
    name: 'Dio',
    password: 'irejectmyhumanityjojo',
  })
  .then((user) => {
    // ...
  })
```

#### [defineProps Ts 版本](https://www.kancloud.cn/cyyspring/vue3/2748147)

- `defineProps` 在ts 版本支持 **泛型参数来定义 prop**
- 传递给`defineProps`的泛型参数本身**不能**是一个导入的类型
- 基于类型的声明或者运行时声明都可以使用，但是你不能同时使用两者
- 接口或对象字面类型可以包含从其他文件导入的类型引用
- ts 类型编译时候 require 默认不是false 是true

1. **泛型参数来定义 prop**

```
<template> {{ props.name }} </template>

<script setup lang="ts">
  // js 版本使用支持的
  // const props = defineProps({
  //   name: String,
  // });

 // 类型字面量定义
  // type Props = {
  //   name: string;
  //   age: number | string;
  // };

  // ts 泛型形式定义
  interface Props {
    name: string;
    age?: number | string;
  }
  const props = defineProps<Props>();
</script>

<style></style>
```

1. 传递给`defineProps`的泛型参数本身**不能**是一个导入的类型

```
import { Props } from './other-file'

// 不支持！
defineProps<Props>()
```

1. 基于类型的声明或者运行时声明都可以使用，但是你不能同时使用两者

```
<template> <div></div>{{ props.name }} </template>

<script setup lang="ts">
  // 不可以两种写法混用
  type Props = {
    name: string;
    age: number | string;
  };
  const props = defineProps<Props>({
    name: String,
  });
</script>

<style></style>
```

1. 接口或对象字面类型可以包含从其他文件导入的类型引用

```
type a = string;
export default a;
<template> <div></div>{{ props.name }} </template>

<script setup lang="ts">
  import a from '../Props/props';
  // 接口中调用的类型可以从 其他文件导入
  type Props = {
    name: a; // 我使用其他文件类型
    age: number | string;
  };
  const props = defineProps<Props>();
</script>

<style></style>
```

1. ts 类型编译时候 require 默认不是false 是true `defineProps<{ msg: string }>`会被编译为`{ msg: { type: String, required: true }}`。
   ![img](https://img.kancloud.cn/b4/3d/b43d7135b2cf177ffff9704b2cd01fad_518x138.png)

> ##### ts 泛型参数来定义 -- 定义默认值

```
interface Props {
  msg?: string // ? 相当于 require 是否必填默认必填
  labels?: string[],
  age:12 | 13, //  相当于 validator，但复杂的不行

}

// 定义默认值比较复杂 需要withDefaults 函数 
const props = withDefaults(defineProps<Props>(), {
  msg: 'hello',
  labels: () => ['one', 'two']
})
```

> ##### ts 泛型参数来定义 -- 开启响应式语法糖

这种形式必须是**开启响应式语法糖**，默认是关闭的目前在实验属性，需要版本 [可以参考](https://staging-cn.vuejs.org/guide/extras/reactivity-transform.html#explicit-opt-in)
`vue@^3.2.25`。

### Vite[#](https://staging-cn.vuejs.org/guide/extras/reactivity-transform.html#vite)

- 需要`@vitejs/plugin-vue@^2.0.0`
- 应用于 SFC 和 js(x)/ts(x) 文件。在执行转换之前，会对文件进行快速的使用检查，因此不使用宏的文件应该不会有性能损失。
- 注意`refTransform`现在是一个插件的顶层选项，而不再是位于`script.refSugar`之中了，因为它不仅仅只对 SFC 起效。

```
// vite.config.js
export default {
  plugins: [
    vue({
      reactivityTransform: true
    })
  ]
}
```

### `vue-cli`[#](https://staging-cn.vuejs.org/guide/extras/reactivity-transform.html#vue-cli)

- 目前仅对 SFC 起效
- 需要`vue-loader@^17.0.0`

```
// vue.config.js
module.exports = {
  chainWebpack: (config) => {
    config.module
      .rule('vue')
      .use('vue-loader')
      .tap((options) => {
        return {
          ...options,
          reactivityTransform: true
        }
      })
  }
}
```

### 仅用`webpack`+`vue-loader`[#](https://staging-cn.vuejs.org/guide/extras/reactivity-transform.html#plain-webpack-vue-loader)

- 目前仅对 SFC 起效
- 需要`vue-loader@^17.0.0`

```
// webpack.config.js
module.exports = {
  module: {
    rules: [
      {
        test: /\.vue$/,
        loader: 'vue-loader',
        options: {
          reactivityTransform: true
        }
      }
    ]
  }
}
```

- 开启后使用

```
<script setup lang="ts">
  interface Props {
    msg: string
    count?: number
    foo?: string
  }

  const {
    msg,
    // 默认值正常可用
    count = 1,
    // 解构时命别名也可用
    // 这里我们就将 `props.foo` 命别名为 `bar`
    foo: bar
  } = defineProps<Props>()

  watchEffect(() => {
    // 会在 props 变化时打印
    console.log(msg, count, bar)
  })
</script>
```

> ##### 最佳实践

`Volar`可以赋予上文中的 template 很友好的 TS 提示与校验，解决了 template 的 TS 提示问题。**注意**，使用它时，要先**移除`Vetur`**，以避免造成冲突，如下图如果使用ts 并且使用 Vetur 并不会有props 提示并且使用setup 组件会显示没有使用，图使用`Volar` 解决了这些问题

![img](https://img.kancloud.cn/aa/83/aa83cc72e95290db156be8dd7c4e4825_627x376.png)

####  [SFC -Single-File Components](https://vuejs.org/guide/scaling-up/sfc.html)



[Vite-config](https://vitejs.dev/config/)

#### [vite热更新（vue3）](https://blog.csdn.net/weixin_45369499/article/details/125158995)

`vite.config.ts`文件中添加代码：

```javascript
hmr: true,  // 开启热更新
```

```
export default defineConfig({
  plugins: [vue()],
  server:{
    hmr: true,  // 开启热更新
  }
})
```

#### [Ant Design Vue3.x中动态渲染icon图标](https://blog.csdn.net/m0_53056203/article/details/124568024)

#### [Vue 3 Ant Design Vue 动态渲染icons](https://blog.csdn.net/DevilAngelia/article/details/124959849)

```
import * as antIcons from '@ant-design/icons-vue' // 引入ant icons

const antIconsList: any = antIcons; // 重新赋值定义类型 避免后续遍历注册组件的时候ts报错

<component :is="antIconsList[item.meta.icon]" />
```

