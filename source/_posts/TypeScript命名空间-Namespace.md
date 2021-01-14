---
title: TypeScript命名空间-Namespace
date: 2020-11-12 10:37:53
tags:
-  TypeScript
categories: 
- 工作笔记
- TypeScript
---

#### 初识命名空间-Namespace

以前的课程都是通过`Node`来运行代码的，这节课为了有更好的演示效果，我们要在浏览器中运行代码。这就要求我们重新创建一个项目，直接在桌面上建立一个文件夹`TSWeb`。

> #### 搭建浏览器开发环境步骤

1. 建立好文件夹后，打开 VSCode，把文件夹拉到编辑器当中，然后打开终端，运行`npm init -y`,创建`package.json`文件。
2. 生成文件后，我们接着在终端中运行`tsc -init`,生成`tsconfig.json`文件。
3. 新建`src`和`build`文件夹，再建一个`index.html`文件。
4. 在`src`目录下，新建一个`page.ts`文件，这就是我们要编写的`ts`文件了。
5. 配置`tsconfig.json`文件，设置`outDir`和`rootDir`(在 15 行左右)，也就是设置需要编译的文件目录，和编译好的文件目录。
6. 然后编写`index.html`，引入`<script src="./build/page.js"></script>`,当让我们现在还没有`page.js`文件。
7. 编写`page.ts`文件，加入一句输出`console.log('jspang.com')`,再在控制台输入`tsc`,就会生成`page.js`文件
8. 再到浏览器中查看`index.html`文件，如果按`F12`可以看到`jspang.com`，说明我们的搭建正常了。

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <script src="./build/page.js"></script>
    <title>Document</title>
  </head>
  <body></body>
</html>
```

> #### 没有命名空间时的问题

为了你更好的理解，先写一下这样代码，用类的形式在`index.html`中实现`header`,`content`和`Footer`部分，类似我们常说的模板。

在`page.ts`文件里，写出下面的代码：

```js
class Header {
  constructor() {
    const elem = document.createElement("div");
    elem.innerText = "This is Header";
    document.body.appendChild(elem);
  }
}

class Content {
  constructor() {
    const elem = document.createElement("div");
    elem.innerText = "This is Content";
    document.body.appendChild(elem);
  }
}

class Footer {
  constructor() {
    const elem = document.createElement("div");
    elem.innerText = "This is Footer";
    document.body.appendChild(elem);
  }
}

class Page {
  constructor() {
    new Header();
    new Content();
    new Footer();
  }
}
```

写完后我们用`tsc`进行编译一次，然后修改`index.html`文件，在`<body>`标签里引入`<script>`标签，并实例化`Page`，代码如下:

```js
<body>
  <script>new Page();</script>
</body>
```

这时候再到浏览器进行预览，就可以看到对应的页面被展现出来了。看起来没有什么问题，但是有经验的程序员就会发现，这样写全部都是全局变量（通过查看`./build/page.js`文件可以看出全部都是`var`声明的变量）。**过多的全局变量会让我们代码变的不可维护。**

这时候你在浏览器的控制台(`Console`)中，分别输入`Header`、`Content`、`Footer`和`Page`都时可以拿到对应的变量的,说明他们全都是全局变量。

其实你理想的是，只要有`Page`这个全局变量就足够了，剩下的可以模块化封装起来，不暴露到全局。

> #### 命名空间的使用

`命名空间`这个语法，很类似编程中常说的模块化思想，比如`webpack`打包时，每个模块有自己的环境，不会污染其他模块,不会有全局变量产生。命名空间就跟这个很类似，注意这里是类似，而不是相同。

命名空间声明的关键词是`namespace` 比如声明一个`namespace Home`,需要暴露出去的类，可以使用`export`关键词，这样只有暴漏出去的类是全局的，其他的不会再生成全局污染了。修改后的代码如下：

```js
namespace Home {
  class Header {
    constructor() {
      const elem = document.createElement("div");
      elem.innerText = "This is Header";
      document.body.appendChild(elem);
    }
  }

  class Content {
    constructor() {
      const elem = document.createElement("div");
      elem.innerText = "This is Content";
      document.body.appendChild(elem);
    }
  }

  class Footer {
    constructor() {
      const elem = document.createElement("div");
      elem.innerText = "This is Footer";
      document.body.appendChild(elem);
    }
  }

  export class Page {
    constructor() {
      new Header();
      new Content();
      new Footer();
    }
  }
}
```

TS 代码写完后，再到`index.html`文件中进行修改，用命名空间的形式进行调用，就可以正常了。 写完后，记得用`tsc`编译一下，当然你也可以使用`tsc -w`进行监视了，只要有改变就会进行重新编译。

```js
new Home.Page();
```

现在再到浏览器中进行查看，可以看到现在就只有`Home.Page`是在控制台可以得到的，其他的`Home.Header`...这些都是得不到的，说明只有`Home.Page`是全局的，其他的都是模块化私有的。

这就是 TypeScript 给我们提供的类似模块化开发的语法，它的好处就是让全局变量减少了很多，实现了基本的封装，减少了全局变量的污染。

#### 深入命名空间-Namespace

> #### 用命名空间实现组件化

在`src`目录下新建一个文件`components.ts`，编写代码如下：

```js
namespace Components {
  export class Header {
    constructor() {
      const elem = document.createElement("div");
      elem.innerText = "This is Header";
      document.body.appendChild(elem);
    }
  }

  export class Content {
    constructor() {
      const elem = document.createElement("div");
      elem.innerText = "This is Content";
      document.body.appendChild(elem);
    }
  }

  export class Footer {
    constructor() {
      const elem = document.createElement("div");
      elem.innerText = "This is Footer";
      document.body.appendChild(elem);
    }
  }
}
```

这里需要注意的是，我每个类(`class`)都使用了`export`导出，导出后就可以在`page.ts`中使用这些组件了。比如这样使用-代码如下。

```js
namespace Home {
  export class Page {
    constructor() {
      new Components.Header();
      new Components.Content();
      new Components.Footer();
    }
  }
}
```

这时候你可以使用`tsc`进行重新编译，但在预览时，你会发现还是会报错，找不到`Components`,想解决这个问题，我们必须要在`index.html`里进行引入`components.js`文件。

```js
<script src="./build/page.js"></script>
<script src="./build/components.js"></script>
```

> #### 多文件编译成一个文件

直接打开`tsconfig.json`文件，然后找到`outFile`配置项，这个就是用来生成一个文件的设置，但是如果设置了它，就不再支持`"module":"commonjs"`设置了，我们需要把它改成`"module":"amd"`,然后在去掉对应的`outFile`注释，设置成下面的样子。

```js
{
  "outFile": "./build/page.js"
}
```

配置好后，删除掉`build`下的`js`文件，然后用`tsc`进行再次编译。

然后删掉`index.html`文件中的`component.js`,在浏览器里还是可以正常运行的。

> #### 子命名空间

```js
namespace Components {
  export namespace SubComponents {
    export class Test {}
  }

  //someting ...
}
```

写完后在控制台再次编辑`tsc`，然后你在浏览器中也是可以查到这个命名空间的`Components.SubComponents.Test`(需要刷新页面后才会显示)。

#### TypeScript 如何使用 import 语法

> #### 修改 components.ts 文件

现在去掉`components.ts`里的`namespace`命名空间代码，写成 `ES6` 的 `export` 导出模式。代码如下：

```js
export class Header {
  constructor() {
    const elem = document.createElement("div");
    elem.innerText = "This is Header";
    document.body.appendChild(elem);
  }
}

export class Content {
  constructor() {
    const elem = document.createElement("div");
    elem.innerText = "This is Content";
    document.body.appendChild(elem);
  }
}

export class Footer {
  constructor() {
    const elem = document.createElement("div");
    elem.innerText = "This is Footer";
    document.body.appendChild(elem);
  }
}
```

现在三个类就都已经用`export`导出了，也就是说可以实现用`import`进行引入了。

> #### 修改 page.ts 文件

来到`page.ts`文件，去掉`namespace`命名空间对应的代码，然后使用 `import` 语法进行导入`Header`、`Content`和`Footer`,代码如下：

```js
import { Header, Content, Footer } from "./components";
export class Page {
  constructor() {
    new Header();
    new Content();
    new Footer();
  }
}
```

现在看起来确实和工作中写的代码非常类似了。这时候可以使用`tsc`进行编译。然后可以看到编译好的代码都是`define`开头的(这是 amd 规范的代码，不能直接在浏览器中运行，可以在 Node 中直接运行)，这种代码在浏览器中是没办法被直接运行的，需要其他库(`require.js`)的支持。

> #### 引入 require.js

```js
<script src="https://cdnjs.cloudflare.com/ajax/libs/require.js/2.3.6/require.js"></script>
```

这时候就可以解析`define`这样的语法了。然后把`page.ts`中加入`default`关键字，如果不加是没办法直接引用到的。

```js
import { Header, Content, Footer } from "./components";

export default class Page {
  constructor() {
    new Header();
    new Content();
    new Footer();
  }
}
```

这时候再用`tsc`进行编译一下，你会发现还是又问题。因为使用`export default`这种形式的语法，需要在`html`里用`require`来进行引入。

> #### require 方式引入

因为你已经加入了`require.js`这个库，所以现在可以直接在代码中使用`require`了。具体代码如下

```js
<body>
  <script>
    require(["page"], function (page) {
      new page.default();
    });
  </script>
</body>
```

当我们有了`webpack`和`Parcel`的时候就不会这么麻烦，这些都交给打包工具来处理就好了。