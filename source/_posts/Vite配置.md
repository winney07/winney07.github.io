---
title: Vite配置
date: 2022-08-04 10:36:44
tags:
- Vite
- Vue3
---

配置文件：`vite.config.ts`

### 1.配置打包公共路径-base

```
base:'./'
```

### 2.配置地址别名-[alias](https://vitejs.cn/config/#resolve-alias)

使用简短的别名去替代一个较长的路径

`__dirname`：项目的绝对路径

1. 安装

   ```
   npm install --save path
   ```

2. 引入

   ```
   import { resolve } from 'path'
   ```

3. 配置

   ```
   export default defineConfig({
     resolve:{
       alias: {
         test: resolve(__dirname, 'src/components/test/'),
         icon: resolve(__dirname, './src/assets/images/')
       }
     }
   })
   ```

4. 使用

   ```
   // 修改前：
   import ViteSet from '../../components/test/ViteSet.vue';
   <img src="../../assets/images/zhangyu.svg" alt="章鱼小丸子">
           
   // 修改后：
   import ViteSet2 from 'test/ViteSet.vue';
   <img src="icon/zhangyu.svg" alt="章鱼小丸子">
   
   
   <ViteSet></ViteSet>
   <ViteSet2></ViteSet2>
   ```



#### 2.1图片的地址的别名-特殊处理

> 图片使用`icon: resolve(__dirname, './src/assets/images/')`这种配置，打包上线后，页面可以正常显示图片，但本地测试是加载不出图片的。
>
> 所以不能直接写 `名称：resolve(...)`，要使用引号加`斜杠开头的别名`

##### 2.1.1配置

```
resolve:{
    alias: {
      '/icon':'./src/assets/images/'
    }
}
```

##### 2.1.2使用

```
// 修改前：
<img src="../../assets/images/zhangyu.svg" alt="章鱼小丸子">
// 修改后：
<img src="/icon/zhangyu.svg" alt="章鱼小丸子">
```

> **这样本地环境和正式环境都能正常显示**

参考：[vite vue3.0 配置拦截，路由跳转](https://blog.csdn.net/liujucai/article/details/112280937)

### 3.生产环境去除console.log的配置

[build.terserOptions](https://vitejs.cn/config/#build-terseroptions)

```
export default defineConfig({
  build:{
    minify: 'terser', // 必须配置'terser'，不然terserOptions不生效，因为minify默认不是'terser'
    terserOptions: {
        compress: {
            //生产环境时移除console
            drop_console: true,
            drop_debugger: true,
        },
    },
  }
})
```

#### 3.1报错处理

打包上线会出现报错：

`[vite:terser] terser not found. Since Vite v3, terser has become an optional dependency. You need to install it.`

解决：Vite V3需要安装[terser依赖包](https://www.npmjs.com/package/terser)

```
cnpm i terser
```

### 4.mock数据的配置

```
npm i vite-plugin-mock mockjs  -D
```

**[vite-plugin-mock](https://github.com/vbenjs/vite-plugin-mock)**

[使用](https://github.com/vbenjs/vite-plugin-mock#usage)

#### 4.1引入

```
import { viteMockServe } from 'vite-plugin-mock'

plugins: [
  vue(),
  viteMockServe({
    // default
    mockPath: 'mock',
  }),
],
```

#### 4.2使用

在根目录新建mock目录

[示例](https://github.com/vbenjs/vite-plugin-mock#mock-file-example)

##### 4.2.1mock/index.ts：

```
// test.ts
import { MockMethod } from 'vite-plugin-mock'
export default [
  {
    url: '/api/get',
    method: 'get',
    response: ({ query }) => {
      return {
        code: 0,
        data: {
          name: 'vben',
        },
      }
    },
  },
  {
    url: '/api/post',
    method: 'post',
    timeout: 2000,
    response: {
      code: 0,
      data: {
        name: 'vben',
      },
    },
  },
  {
    url: '/api/text',
    method: 'post',
    rawResponse: async (req, res) => {
      let reqbody = ''
      await new Promise((resolve) => {
        req.on('data', (chunk) => {
          reqbody += chunk
        })
        req.on('end', () => resolve(undefined))
      })
      res.setHeader('Content-Type', 'text/plain')
      res.statusCode = 200
      res.end(`hello, ${reqbody}`)
    },
  },
] as MockMethod[]
```

##### 4.2.2引入axios

```
cnpm i axios
```

```
import axios from 'axios'

async function fn() {
  const { data } = await axios.get('/api/get')
  console.log(data);
}
fn()
```

##### 使用mock来模拟更多数据

```
npm install mockjs --save-dev
```

使用示例：

```
import Mock from 'mockjs'

// 定义数据类型
var data = Mock.mock({
  // 20条数据
  "data|20": [{
    // 商品种类
    "goodsClass": "女装",
    // 商品Id
    "goodsId|+1": 1,
    //商品名称
    "goodsName": "@ctitle(10)",
    //商品地址
    "goodsAddress": "@county(true)",
    //商品等级评价★
    "goodsStar|1-5": "★",
    //商品图片
    "goodsImg": "@Image('100x100','@color','小甜甜')",
    //商品售价
    "goodsSale|30-500": 30
  }]
})
// 输出结果随机生成的数据（node index.js）
 console.log(data);
```

##### 将mock模拟的数据放到接口返回中

mock/index.ts：

```
// test.ts
import { MockMethod } from 'vite-plugin-mock'
import Mock from 'mockjs'
var list = Mock.mock({
  // 20条数据
  "data|20": [{
    // 商品种类
    "goodsClass": "女装",
    // 商品Id
    "goodsId|+1": 1,
    //商品名称
    "goodsName": "@ctitle(10)",
    //商品地址
    "goodsAddress": "@county(true)",
    //商品等级评价★
    "goodsStar|1-5": "★",
    //商品图片
    "goodsImg": "@Image('100x100','@color','小甜甜')",
    //商品售价
    "goodsSale|30-500": 30

  }]
})
export default [
  {
    url: '/api/get',
    method: 'get',
    response: ({ query }) => {
      return {
        code: 0,
        data: list
      }
    },
  },
  },
] as MockMethod[]
```

### 5.配置前端跨域代理

`proxy`

```
server: {
    proxy: {
        '/ss': {
            target: 'https://saucenao.com/search.php?db=999&output_type=2&url=https://pica.zhimg.com/v2-178387c7e8e907910d715e890bfd7519_1440w.jpg?source=172ae18b&api_key=33d4bee5c19583cd3756ee47f2ebef8edd5bef7e',
            changeOrigin: true,
            rewrite: (path) => path.replace(/^\/ss/, ''),
        },
    },
},
```

```
axios.get('/ss').then(res => {
    console.log(res);
})
```

```
export default defineConfig({
	plugins:[vue()],
	server:{	//中转服务器
        proxy:{		//通过代理实现跨域
        // https://i.maoyan.com
            '/path':{
                target:'https://i.maoyan.com',		//替换的服务端地址
                changeOrigin:true,		//开启代理，允许跨域
                rewrite: path=>path.replace(/^\/path/,'')		//设置重写的路径
             }
        }
    }
})
```

### 6.env环境变量的配置

#### 6.1环境变量配置

`.env.development`：

可配置多个

```
VITE_BASE_API = /api
VITE_BASE_API = /api2
VITE_BASE_API = /api3
```

`.env.production`：

```
VITE_BASE_API = https://www.manga2020.com/api/v3/comic/hydxjxrwgb/chapter/cb321fca-c608-11e8-879b-024352452ce0?timeout=10000
```

#### 6.2修改请求链接

```
async function fn() {
  const { data } = await axios.get(import.env.VITE_BASE_API as string)
  console.log(data);
}
fn()
```

> 本地环境使用mock数据： /api    正式环境使用正式的api链接
>
> 这样本地可以使用mock数据，正式使用正式的api数据。互不影响。  

### 7.CDN的配置

`备注：暂时配置不成功`

**[vite-plugin-cdn-import](https://github.com/MMF-FE/vite-plugin-cdn-import)**

[vue使用示例](https://github.com/MMF-FE/vite-plugin-cdn-import#vueuse-demo)

```
npm install vite-plugin-cdn-import --save-dev
```

```
import importToCDN, { autoComplete } from 'vite-plugin-cdn-import'

export default {
    plugins: [
        vue(),
        importToCDN({
            modules: [
                autoComplete('vue'), // vue2 use autoComplete('vue2')
                autoComplete('@vueuse/shared'),
                autoComplete('@vueuse/core')
            ],
        }),
    ],
}
```



### 8.代码压缩的配置-gzip

**[vite-plugin-compression](https://github.com/vbenjs/vite-plugin-compression)**

```
npm i vite-plugin-compression -D
```

```\
import viteCompression from 'vite-plugin-compression';

export default () => {
  return {
    plugins: [viteCompression()],
  };
};
```

### 9.打包图片

**[vite-plugin-imagemin](https://github.com/vbenjs/vite-plugin-imagemin)**

```
cnpm i vite-plugin-imagemin@0.4.6 -D
```

```
import viteImagemin from 'vite-plugin-imagemin'
export default () => {
  return {
    plugins: [
      viteImagemin({
        gifsicle: {
          optimizationLevel: 7,
          interlaced: false,
        },
        optipng: {
          optimizationLevel: 7,
        },
        mozjpeg: {
          quality: 20,
        },
        pngquant: {
          quality: [0.8, 0.9],
          speed: 4,
        },
        svgo: {
          plugins: [
            {
              name: 'removeViewBox',
            },
            {
              name: 'removeEmptyAttrs',
              active: false,
            },
          ],
        },
      }),
    ],
  }
}
```

以上代码，本地会报错，需重启一下

参考：[搭建vite2.0+vue3.0+ts+多页面打包+多环境+gzip+图片压缩框架](https://www.icode9.com/content-4-1151614.html)

[Vite图片压缩(vite-plugin-imagemin) imagemin error: XXXX解决办法](https://www.pudn.com/news/627cb910ebb030486dd6b752.html)



### 10.[element plus按需引入](https://element-plus.gitee.io/zh-CN/guide/quickstart.html#%E6%8C%89%E9%9C%80%E5%AF%BC%E5%85%A5)





[做个开源博客学习Vite2 + Vue3 （二）设置别名、代理和ESLint](https://www.jianshu.com/p/5f70056a03b6)

