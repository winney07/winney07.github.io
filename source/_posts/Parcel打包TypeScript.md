---
title: Parcel打包TypeScript
date: 2020-11-12 10:46:45
tags:
- TypeScript
categories: 
- 工作笔记
- TypeScript
---

#### 用 Parcel 打包 TypeScript 代码

> #### 建立一个新项目

1. 教学需要，这里我们重新建立一个项目`TSTest`,在桌面新建立一个文件夹，然后在`VSCode`中打开。
2. 打开终端，输入`npm init -y`,创建`package.json`文件
3. 在终端中输入`tsc --init`,创建`tsconfig.json`文件
4. 修改`tsconfig.json`配置`rootDir`和`outDir`.
5. 新建`src`文件夹，在里边建立`index.html`,`page.ts`文件
6. 编写`index.html`文件，并引入`page.ts`文件
7. 编写`page.ts`文件

index.html

```js
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <script src="./page.ts"></script>
    <title>Document</title>
  </head>
  <body></body>
</html>
```

page.ts

```js
const teacher: string = "jspang";
console.log(teacher);
```

> #### Parcel 的安装和使用

`npm`或者`yarn`来进行安装

```js
yarn add --dev parcel@next
```

修改package.json

```js
{
  "scripts": {
    "test": "parcel ./src/index.html"
  },
}
```

然后打开终端输入`yarn test`,这时候终端会给出一个地址`http://localhost:1234`,把地址放到浏览器上，可以看到浏览器的控制台会输出`jspang`。

这说明`Parcel`会自动对`index.html`中引入的`TypeScript`文件进行编译，然后打包好后，就可以直接使用了。

#### 在 TypeScript 中使用 JQuery

> #### 引入 JQuery 框架库

直接在`index.html`加入`<script>`标签

```js
<script src="https://cdn.bootcdn.net/ajax/libs/jquery/3.5.1/jquery.js"></script>
```

有了 jquery 框架，就可以在`TypeScript`文件中进行使用`JQuery`的语法

然后在`page.ts`文件中编写如下代码

```js
const teacher: string = "jspang";
console.log(teacher);

$(function () {
  alert("jspang");
});
```

写完后到终端中输入`yarn test`进行编译和启动服务。然后在地址栏输入了`http://localhost:1234`,可以看到程序可以正常输出，也没有任何的报错。

> #### 安装 types/jquery(解决方法)

第一种：就是安装别人写好的文件

但是在`vscode`中是会报错的，这时候就需要我们安装类型文件`type file`,直接可以用 npm 进行安装。

```js
npm i @types/jquery
```

第二种:简单粗暴

还有一种简单粗暴的方法的方式就是直接在`page.ts`文件的头部加入这句代码：

```js
declare var $: any;
```

第三种：自己写一个`.d.ts`声明文件的类库，如果你用的类库很少见，就需要自己写了。这个写起来还是很麻烦的。 比如 JQuery 就有几十个接口，如果你要写，这个文件会写很长，所以原则就是有别人写好的就直接用，实在没有就用粗暴的方法，如果实在不行，再考虑写`.d.ts`声明文件。

