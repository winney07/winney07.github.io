---
title: TypeScript函数泛型-难点
date: 2020-11-11 17:37:35
tags:
-  TypeScript
categories: 
- 工作笔记
- TypeScript
---

#### TypeScript 函数泛型-难点

> #### 编写一个联合类型 Demo

```js
function join(first: string | number, second: string | number) {
  return `${first}${second}`;
}
join("jspang", ".com");
```

那现在所学的知识就完成不了啦，所以需要学习`泛型`来解决这个问题。

> #### 初始泛型概念-generic

> 泛型：[generic - 通用、泛指的意思],那最简单的理解，泛型就是泛指的类型。

泛型的定义使用`<>`（尖角号）进行定义的

```js
function join<JSPang>(first: JSPang, second: JSPang) {
  return `${first}${second}`;
}
join < string > ("jspang", ".com");
```

如果要是`number`类型，就直接在调用方法的时候进行更改就可以了。

```js
join < number > (1, 2);
```

> #### 泛型中数组的使用

如果传递过来的值要求是数字，如何用泛型进行定义那?两种方法，第一种是直接使用`[]`，第二种是使用`Array<泛型>`。形式不一样，其他的都一样。

第一种写法：

```js
function myFun<ANY>(params: ANY[]) {
  return params;
}
myFun < string > ["123", "456"];
```

第二种写法：

```js
function myFun<ANY>(params: Array<ANY>) {
  return params;
}
myFun < string > ["123", "456"];
```

在工作中，我们经常使用`<T>`来作泛型的表示

> #### 多个泛型的定义

```js
function join<T, P>(first: T, second: P) {
  return `${first}${second}`;
}
join < number, string > (1, "2");
```

> #### 泛型的类型推断

```js
function join<T, P>(first: T, second: P) {
  return `${first}${second}`;
}
join(1, "2");
```

不建议大量使用类型推断，这会让你的代码易读和健壮性都会下降

#### TypeScript 类中泛型-难点

> #### 编写一个基本类

```js
class SelectGirl {
  constructor(private girls: string[]) {}
  getGirl(index: number): string {
    return this.girls[index];
  }
}

const selectGirl = new SelectGirl(["大脚", "刘英", "晓红"]);
console.log(selectGirl.getGirl(1));
```

在 TypeScript 中，编写复杂代码的时候，会经常使用泛型。

```js
class SelectGirl {
  constructor(private girls: string[] | number[]) {}
  getGirl(index: number): string | number {
    return this.girls[index];
  }
}
```

> #### 初始类的泛型

用`<>`编写

```js
class SelectGirl<T> {
  constructor(private girls: T[]) {}
  getGirl(index: number): T {
    return this.girls[index];
  }
}

const selectGirl = new SelectGirl(["大脚", "刘英", "晓红"]);
console.log(selectGirl.getGirl(1));
```

这时候代码并不报错，也使用了泛型，但是在实例化对象的时候，TypeScript 是通过类型推断出来的。这种方法并不好，所以还是需要在实例化对象的时候，对泛型的值进行确定，比如是`string`类型，就这样写。

```js
const selectGirl = new SelectGirl() < string > ["大脚", "刘英", "晓红"];
```

> #### 泛型中的继承

现在需求又变了，要求返回是一个对象中的`name`,也就是下面的代码要改成这个样子。

```js
return this.girls[index].name;
```

现在的代码一定时报错的，但是这时候还要求我们这么做，意思就是说传递过来的值必须是一个对象类型的，里边还要有`name`属性。这时候就要用到继承了，我用接口的方式来实现。写一个`Girl`的接口，每个接口里都要有 name 属性。代码如下：

```js
interface Girl {
  name: string;
}
```

有了接口后用`extends`关键字实现泛型继承，代码如下：

```js
class SelectGirl<T extends Girl> {
 ...
}
```

这句代码的意思是泛型里必须有一个`name`属性，因为它继承了`Girl`接口。

现在程序还是报错的，因为我们`getGirl`方法的返回类型还不对，这时候应该是一个`string`类型才对，所以代码应该改为下面的样子：

```js
interface Girl {
  name: string;
}

class SelectGirl<T extends Girl> {
  constructor(private girls: T[]) {}
  getGirl(index: number): string {
    return this.girls[index].name;
  }
}

const selectGirl = new SelectGirl([
  { name: "大脚" },
  { name: "刘英" },
  { name: "晓红" },
]);
console.log(selectGirl.getGirl(1));
```

> #### 泛型约束

现在的泛型可以是任意类型，可以是对象、字符串、布尔、数字都是可以的。但你现在要求这个泛型必须是`string`或者`number`类型。我们还是拿上面的例子，不过把代码改为最初的样子。

```js
class SelectGirl<T> {
  constructor(private girls: T[]) {}
  getGirl(index: number): T {
    return this.girls[index];
  }
}

const selectGirl = new SelectGirl<string>(["大脚", "刘英", "晓红"]);
console.log(selectGirl.getGirl(1));
```

然后进行约束，这时候还是可以使用关键字`extends`来进行约束，把代码改成下面的样子。

```js
class SelectGirl<T extends number | string> {
  //.....
}
```
