---
title: Vue3.0-笔记
date: 2022-06-08 16:35:13
tags:
- Vue3
categories:
- 前端开发框架
- Vue.js
---



#### 《Vue.js 3.x高效前端开发（视频教学版)》

[资源下载链接](https://www.wqyunpan.com/preview-wx.html?id=206715&code=051Zs3ll2zWxAa41Qall2hmqw74Zs3lY&state=wx
)

> 本书配套源码、PPT课件、教学视频、教学教案、上机习题及答案、Vue.js 3.x常见错误及解决方法、30个企业级实战项目源码、就业面试题及解答、Vue.js 3.x开发经验及技巧汇总等丰富的学习和教学资源，需要`使用微信扫描下面二维码下载`，可按扫描后的页面提示，把链接转发到自己的邮箱中下载。如果有疑问，请联系booksaga@163.com，邮件主题写“Vue.js 3.x高效前端开发”。

![课程链接](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/Vue3-0-%E7%AC%94%E8%AE%B0/wx-code.png)

#### [Vue3.x--系列学习](https://www.kancloud.cn/cyyspring/vue3/2696499)

#### [vue3+ts(2)：TypeScript 语法汇总](https://zhuanlan.zhihu.com/p/360553463)

- vue3+ts项目系列第1篇**[《vue3项目从0到1搭建》](https://link.zhihu.com/?target=https%3A//mp.weixin.qq.com/s/MpmoEbJPTWKCSHdtpd1jCw)**
- vue3+ts项目系列第2篇**[《TypeScript 语法汇总》](https://link.zhihu.com/?target=https%3A//lianpf.github.io/posts/%E5%89%8D%E7%AB%AF%E5%9F%BA%E7%A1%80/03.ts%E5%9F%BA%E7%A1%80%E8%AF%AD%E6%B3%95/)**
- vue3+ts项目系列第3篇**[《vue3组合式api及重要属性变更》](https://link.zhihu.com/?target=https%3A//lianpf.github.io/posts/%E5%89%8D%E7%AB%AF%E6%A1%86%E6%9E%B6/07.vue3%E7%BB%84%E5%90%88%E5%BC%8Fapi%E5%8F%8A%E9%87%8D%E8%A6%81%E5%B1%9E%E6%80%A7%E5%8F%98%E6%9B%B4/)**



#### vite + vue3 + ts 富文本编辑器

[vite + vue3 + ts 安装 tinymce 富文本编辑器](https://www.lanmper.cn/vue/t9834.html)

[tinymce](https://github.com/tinymce/tinymce)

[tiny官网](https://www.tiny.cloud/)

**[tinymce-vue](https://github.com/tinymce/tinymce-vue)**

[文档](https://www.tiny.cloud/docs/quick-start/)

[tiny中文文档](http://tinymce.ax-z.cn/)



[在vue中的使用](http://tinymce.ax-z.cn/integrations/integrate-index.php)

[Vue中的使用-官网](https://www.tiny.cloud/docs/integrations/vue/)

#### 1.安装

[Vue3项目的安装](https://www.tiny.cloud/docs/tinymce/6/vue-pm/)

```
npm install --save tinymce "@tinymce/tinymce-vue@^4"
```

`注：此应用包共有两个目录文件：*tinymce*和*@tinymce*。以后若需要卸载的话，可以直接删除这两个目录文件`

#### 2.安装汉化语言包

[语言包下载列表](https://www.tiny.cloud/get-tiny/language-packages/)，选择*Chinese Simplified*，解压得到*zh-Hans.js*文件。

然后，在`/node_modules/tinymce`下，新建设目录*langs*，把*zh-Hans.js*复制过去。注意：langs 目录必须与 themes，处于同等目录下，否则不起作用。



[vue富文本编辑器](https://blog.csdn.net/m0_46850900/article/details/112500444?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522165969109816782395347116%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=165969109816782395347116&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-1-112500444-null-null.142^v39^pc_rank_v37,185^v2^control&utm_term=vue%E5%AF%8C%E6%96%87%E6%9C%AC%E7%BC%96%E8%BE%91%E5%99%A8&spm=1018.2226.3001.4187)

[最好用的 7 款 Vue 3 富文本编辑器](https://blog.csdn.net/weixin_48201324/article/details/122632208?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522165969109816782395347116%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=165969109816782395347116&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_click~default-4-122632208-null-null.142^v39^pc_rank_v37,185^v2^control&utm_term=vue%E5%AF%8C%E6%96%87%E6%9C%AC%E7%BC%96%E8%BE%91%E5%99%A8&spm=1018.2226.3001.4187)

[vue实现富文本编辑器(附图)-vue-quill-editor](https://blog.csdn.net/w1418899532/article/details/100867223?ops_request_misc=&request_id=&biz_id=102&utm_term=vue%E5%AF%8C%E6%96%87%E6%9C%AC%E7%BC%96%E8%BE%91%E5%99%A8&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-3-100867223.142^v39^pc_rank_v37,185^v2^control&spm=1018.2226.3001.4187)

[在vuecli3.0+中使用tinymce及实现多图上传，文件上传，公式编辑等功能](https://www.cnblogs.com/huihuihero/p/13877589.html)



#### [vue3+vite的项目如何将打包后的绝对路径改为相对路径](https://blog.csdn.net/zy21131437/article/details/125861170)

在vue3+vite的项目中，配置文件名为 **`vite.config.js`**，如果没有就在[根目录](https://so.csdn.net/so/search?q=根目录&spm=1001.2101.3001.7020)下新建一个，文件名固定为：**`vite.config.js`**，然后在里面加上base属性，设置值为 `"./"`，如下：

```
import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [vue()],
  base: './'
})
```

如果不是用Vite的，[vue cli3.x打包后如何修改生成的静态资源的目录和路径](

#### 仅限 TypeScript 的功能

[Ant Design Pro](https://preview.pro.ant.design/dashboard/analysis)

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

[vue3 学习笔记 (五)——vue3 的 setup 如何实现响应式功能？](https://blog.csdn.net/weixin_43880397/article/details/121464597)

### [防抖和节流](https://v3.cn.vuejs.org/guide/data-methods.html#%E9%98%B2%E6%8A%96%E5%92%8C%E8%8A%82%E6%B5%81)

Vue 没有内置支持防抖和节流，但可以使用 [Lodash](https://lodash.com/) 等库来实现

#### setup语法糖处理异步-响应式数组数据

```
let data = reactive([]);

api.get('/apps/getapps').then(res => {
    if(res.code === 1) {
        console.log(res.data)
        data.push(...res.data)
    }
})
```

#### [Vue3 数据响应式](https://blog.csdn.net/hx_1551/article/details/124623872)

在vue3中一般返回的数据是不响应的，如果需要响应式需要在定义时声明
方法1：reactive（）：
    定义：reactive（）是一个函数，可以用来定义复杂数据类型完成响应式
    案例：

```
<div>{{userInfo.name}}</div>
//4，结果打印Cat
<button @click="userNameUpdate"><button>
<script lang='setup'>
//1，引用reactive
import {reactive} from 'vue'
//2，定义响应式对象
const userInfo = reactive({
    name:''
})
//3，点击改变响应式对象中name的值
const userNameUpdate = ()=>{
    userInfo.name = "Cat"
}
</script>
```

方法2：toRef（）：
    定义：当我们在渲染数据时，不希望用到前缀时，可以使用组合toRef（）
       toRef（）是函数，**转换响应式对象**中的某个属性为单独响应式数据，他们之间依然相互绑定
    案例：

```
<div>{{name}}</div>
//先打印Vue2
<button @click='nameUpdata'>修改</button>
//点击后打印Vue3
<script lang='setup'>
//1，引用reactive，toRef
import {reactive,toRef} from 'vue'
//2，定义响应式对象
const userInfo = reactive({
    name:'Vue2'
})
//3，定义单独响应式变量
const name = toRef(userInfo,'name')
//4，点击修改name值
const nameUpdata = ()=>{
    name.value = 'Vue3'
}
</script>
```

方法3：toRefs（）：
    定义：可以定义转换响应式对象中所有属性为响应式数据，通常用于结构reactive定义的对象，转换响应式对象中所有属性（也可以是一部分）为单独响应式数据，对象成为普通对象，且数据关联
    案例：

```

<div>姓名：{{name}}</div>
<div>年龄：{{age}}</div>
<button @click = 'upData'>修改信息</button>
<script lang='setup'>
//1，引用reactive、toRefs
import {reactive,toRefs} from 'vue'
//2，定义响应式对象
const userInfo = reactive({
    name:'张三',
    age:'23'
})
//3，定义转换单独响应式数据
const {name,age} =toRefs(userInfo)
//4，修改数据事件
const upData = () =>{
    name.value = '李四'
    age.value = '24'
} 
</script>

```

方法4：ref（）：
        定义：ref（）是一个函数，用来定义简单类型数据响应式
        注意：
                1）在修改值和获取值时需要用.value
                2）在渲染数据时可以省略.value
        案例：

```

<div>{{name}}</div>
<button @click="upData">修改</button>
<script lang='setup'>
//1，引用ref
import {ref} from 'vue'
//2，定义响应式变量
const name = ref('vue2')
//3，修改数据事件
const upData = ()=>{
    name.value = 'vue3'
    conslot.log(name.value)
}
</script>
```

#### [vue中数组的七个响应式方法](https://www.csdn.net/tags/OtDaEg4sMjUxMTUtYmxvZwO0O0OO0O0O.html)

#### [antd Select组件placeholder不显示解决办法和原因](https://blog.csdn.net/GMLGDJ/article/details/122754487)

 <Select
        placeholder="placeholder"
        // value={undefined} //显示
        value=''  // 不显示
      // value={null}  // 不显示
      >
        <Option value="lucy">Lucy</Option>
      </Select>
解决办法：placeholder不显示是因为设置了value值为"或者null，把value值设为undefined就可以了

原因：placeholder是当前组件值为空时显示的替换文本，只有值为空的时候才会显示。当组件绑定了value后，值不再是空，即时初始化值为""或null也视为有值，所以placeholder自然就不会显示。



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

#### [vue 3 的复制功能 vue-clipboard3](https://www.jianshu.com/p/c3fb60e8eccb)

#### 组件-国际化-中文

[Vue+antd 国际化--默认英文改成中文](https://blog.51cto.com/u_15316082/3209711)

[Vue 解决 Warning: [antdv: LocaleProvider\] `LocaleProvider` is deprecated. Please use `locale` .....](https://blog.csdn.net/zz00008888/article/details/112895429)

```plain
import zh_CN from "ant-design-vue/lib/locale-provider/zh_CN";

<a-config-provider :locale="zh_CN">
  <div id="app">
    <router-view></router-view>
  </div>
</a-config-provider>
```

- 原因：在使用 ant-design-for-vue 国际化的时候，LocaleProvider 已弃用，需要换成 ConfigProvider。
- 解决：把` <a-locale-provider>` 标签换成 `<a-config-provider>` 标签即可



[antd-vue实现导出excel](http://www.manongjc.com/detail/24-fqjxxougfxbdcin.html)

[antd-vue实现导出excel](http://t.zoukankan.com/llive-p-14880959.html)

[Vue3将数据导出为Excel—公司偷学技术的第1天](https://cloud.tencent.com/developer/article/2047844)、

### [导出表格-js-table2excel](https://www.npmjs.com/package/js-table2excel)

```plain
npm install js-table2excel
```

#### 可以设置表格的单元格的宽高和类型

```plain
const column = [
    {
        title: 'Name',
        key: 'name',
        type: 'text'
    },
    {
        title: 'Pic',
        key: 'pic',
        type: 'image',
        width: 80,
        height: 50
    }
]
const data = [
    {
        name: 'xiao',
        age: '18',
        pic: ''
    },
    {
        name: 'jie',
        age: '18',
        pic: ''
    }
]
const excelName = 'boy'
 
table2excel(column, data, excelName)
```

#### 报错处理

引入`import table2excel from 'js-table2excel'`，在`js-table2excel`上会有以下警告：

```plain
无法找到模块“js-table2excel”的声明文件。“H:/Gitee/Vue3_demo/vue3-app-manage/node_modules/_js-table2excel@1.0.3@js-table2excel/index.js”隐式拥有 "any" 类型。
  尝试使用 `npm i --save-dev @types/js-table2excel` (如果存在)，或者添加一个包含 `declare module 'js-table2excel';` 的新声明(.d.ts)文件
```

#### [已安装对应模块，但报无法找到模块“XXX”的声明文件的解决方案](https://www.cnblogs.com/feibiubiu/p/12603807.html)

#### 解决方法：

在src目录下，新建`shime-vue.d.ts`文件，在里面进行声明：

```plain
declare module 'js-table2excel';
```

#### [vue3网络请求到的数据为proxy对象时，如何获取值](https://www.bilibili.com/read/cv12282506)



#### [将proxy对象转为普通数组-toRaw](https://v3.cn.vuejs.org/api/basic-reactivity.html#toraw)

注意：`toRaw`的时候，要加上`.value`

```plain
const selectedRowsArr = ref<DataType[]>([]);

const list = toRaw(selectedRowsArr.value);  // 这个就是普通数组
```

#### [13个开发常用的Vue UI组件库](https://www.jianshu.com/p/f98a14effc81)



#### [vue跳转页面的几种方法(推荐)](https://www.jb51.net/article/183611.htm)

1. router-link跳转

   ```
   <!-- 直接跳转 -->
   <router-link to='/testDemo'>
    <button>点击跳转2</button>
   </router-link>
     
   <!-- 带参数跳转 -->
   <router-link :to="{path:'testDemo',query:{setid:123456}}">
    <button>点击跳转1</button>
   </router-link>
     
   <router-link :to="{name:'testDemo',params:{setid:1111222}}">
    <button>点击跳转3</button>
   </router-link>
   ```

2. this.$router.push()

   ```
   this.$router.push('/testDemo');
   ```

   element-ui下拉菜单的事件监听@command做页面跳转

   ```
   <el-dropdown class="ml15" @command="handleCommand">
       <span class="el-dropdown-link">
           <!-- <i class="el-icon-user-solid"></i> -->
           <el-button icon="el-icon-user-solid" circle size="mini"></el-button>
       </span>
       <el-dropdown-menu slot="dropdown">
           <el-dropdown-item command="/user/updatepass">修改密码</el-dropdown-item>
           <el-dropdown-item command="/login">退出登录</el-dropdown-item>
       </el-dropdown-menu>
   </el-dropdown>
   
   handleCommand(command) {
     console.log(command)
     this.$router.push(command)
   }
   ```

   获取当前路由—this.$route.path

   ```
   this.$route.path
   
   if(this.$route.path!='/Home'){
         this.$router.push({
             path:'/Home',
         })
     }
   ```

   

#### vue项目中引入本地json文件

```
const appsId = require('@/utils/appsId.json');
```

appsId.json文件：

```
{
    "1": "未分类", 
    "2": "哈哈哈项目", 
    "3": "测试模块", 
    "4": "呵呵呵项目", 
    "5": "好啊好啊项目", 
    "6": "哈哈哈哈哈项目", 
}
```

在服务器上跑node服务，配置mongodb啊，你本地怎么运行的，服务器就怎么运行，只不过服务器上的node服务也好nginx也好，读取的是打包压缩后的静态项目资源，`服务器也就是可以通过外网ip访问的的一台电脑`

#### [路由懒加载](https://router.vuejs.org/zh/guide/advanced/lazy-loading.html)

```
// 将
// import UserDetails from './views/UserDetails.vue'
// 替换成
const UserDetails = () => import('./views/UserDetails.vue')

const router = createRouter({
  // ...
  routes: [{ path: '/users/:id', component: UserDetails }],
})
```

#### 状态管理

[provide](https://cn.vuejs.org/api/options-composition.html#provide)/[inject](https://cn.vuejs.org/api/options-composition.html#inject)跨级通信

```
// App.vue

<script>
import Home from "./views/Home.vue";
import store from "./store";
// vue3中如何设置状态管理
// provide/inject跨级通信
export default{
    provide: {
    	store,
    },
    components: {
    	Home,
    },
};
</script>

<template>
    <Home />
</template>
```

```
// Home.vue
<template>
    <div>{{store.state.msg}}</div>
</template
<script>
export default {
    inject:['store']
</script>
```

