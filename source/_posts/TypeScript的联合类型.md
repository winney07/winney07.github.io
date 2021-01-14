---
title: TypeScript的联合类型
date: 2020-11-11 15:43:27
tags:
-  TypeScript
categories: 
- 工作笔记
- TypeScript
---

#### 联合类型和类型保护

> #### 联合类型展示

所谓联合类型，可以认为一个变量可能有两种或两种以上的类型。所以我们使用了联合类型，关键符号是`|`(竖线)。

```
interface Waiter {
  anjiao: boolean;
  say: () => {};
}

interface Teacher {
  anjiao: boolean;
  skill: () => {};
}

function judgeWho(animal: Waiter | Teacher) {}
```

```
function judgeWho(animal: Waiter | Teacher) {
  animal.say();
}
```

但这时候问题来了，如果我直接写一个这样的方法，就会报错，因为`judgeWho`不能准确的判断联合类型具体的实例是什么。

这时候就需要再引出一个概念叫做`类型保护`

> #### 类型保护-类型断言

类型断言就是通过断言的方式确定传递过来的准确值

```
interface Waiter {
  anjiao: boolean;
  say: () => {};
}

interface Teacher {
  anjiao: boolean;
  skill: () => {};
}

function judgeWho(animal: Waiter | Teacher) {
  if (animal.anjiao) {
    (animal as Teacher).skill();
  }else{
    (animal as Waiter).say();
  }
}
```

> #### 类型保护-in语法

经常使用`in`语法来作类型保护，比如用`if`来判断`animal`里有没有`skill()`方法。

```
function judgeWhoTwo(animal: Waiter | Teacher) {
  if ("skill" in animal) {
    animal.skill();
  } else {
    animal.say();
  }
}
```

这里的`else`部分能够自动判断，得益于`TypeScript`的自动判断。

> #### 类型保护-typeof 语法

```
function add(first: string | number, second: string | number) {
  return first + second;
}
```

这时候会报错，解决这个问题，就可以直接用type of来进行解决

```
function add(first: string | number, second: string | number) {
  if (typeof first === "string" || typeof second === "string") {
    return `${first}${second}`;
  }
  return first + second;
}
```

> #### 类型保护-instanceof 语法

比如现在要作类型保护的是一个对象，这时候就可以使用`instanceof`语法来作

```
class NumberObj {
  count: number;
}
```

```
function addObj(first: object | NumberObj, second: object | NumberObj) {
  return first.count + second.count;
}
```

报错不要紧，直接使用`instanceof`语法进行判断一下，就可以解决问题。

```
function addObj(first: object | NumberObj, second: object | NumberObj) {
  if (first instanceof NumberObj && second instanceof NumberObj) {
    return first.count + second.count;
  }
  return 0;
}
```

#### Enum 枚举类型讲解

初级程序员写法：

```js
function getServe(status: number) {
  if (status === 0) {
    return "massage";
  } else if (status === 1) {
    return "SPA";
  } else if (status === 2) {
    return "dabaojian";
  }
}
const result = getServe(0);
console.log(`我要去${result}`);
```

中级程序员写法：

```js
const Status = {
  MASSAGE: 0,
  SPA: 1,
  DABAOJIAN: 2,
};

function getServe(status: any) {
  if (status === Status.MASSAGE) {
    return "massage";
  } else if (status === Status.SPA) {
    return "spa";
  } else if (status === Status.DABAOJIAN) {
    return "dabaojian";
  }
}

const result = getServe(Status.SPA);

console.log(`我要去${result}`);
```

高级程序员写法：

```js
enum Status {
  MASSAGE,
  SPA,
  DABAOJIAN,
}

function getServe(status: any) {
  if (status === Status.MASSAGE) {
    return "massage";
  } else if (status === Status.SPA) {
    return "spa";
  } else if (status === Status.DABAOJIAN) {
    return "dabaojian";
  }
}

const result = getServe(Status.SPA);

console.log(`我要去${result}`);
```

> #### 枚举类型的对应值

你调用时传一个`1`,也会输出`我要去spa`。

```js
const result = getServe(1);
```

因为枚举类型是有对应的数字值的，默认是从 0 开始的

```js
console.log(Status.MASSAGE);
console.log(Status.SPA);
console.log(Status.DABAOJIAN);
```

可以看出结果就是`0,1,2`。那这时候不想默认从 0 开始，而是想从 1 开始。可以这样写。

```js
enum Status {
  MASSAGE = 1,
  SPA,
  DABAOJIAN,
}
```

> #### 枚举通过下标反查

```js
console.log(Status.MASSAGE, Status[1]);
```