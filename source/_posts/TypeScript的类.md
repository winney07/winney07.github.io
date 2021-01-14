---
title: TypeScript的类
date: 2020-11-10 16:30:26
tags:
-  TypeScript
categories: 
- 工作笔记
- TypeScript
---

#### TypeScript中类的概念和使用

> #### 类的基本使用

```
class Lady {
  content = "Hi，帅哥";
  sayHello() {
    return this.content;
  }
}

const goddess = new Lady();
console.log(goddess.sayHello());
```

> #### 类的继承
>

```
class Lady {
  content = "Hi，帅哥";
  sayHello() {
    return this.content;
  }
}
class XiaoJieJie extends Lady {
  sayLove() {
    return "I love you";
  }
}

const goddess = new XiaoJieJie();
console.log(goddess.sayHello());
console.log(goddess.sayLove());
```

> #### 类的重写
>

```
class XiaoJieJie extends Lady {
  sayLove() {
    return "I love you!";
  }
  sayHello() {
    return "Hi , honey!";
  }
}
```

> #### super关键字的使用
>

```
class XiaoJieJie extends Lady {
  sayLove() {
    return "I love you!";
  }
  sayHello() {
    return super.sayHello() + "。你好！";
  }
}
```

#### TypeScript中类的访问类型

> 其实类的访问类型就是基于三个关键词`private`、`protected`和`public`

```
class Person {
    public name:string;
}
```

> #### public访问属性讲解
>

> `public`从英文字面的解释就是`公共的`或者说是`公众的`，在程序里的意思就是允许在类的内部和外部被调用.

```
class Person {
    public name:string;
    public sayHello(){
        console.log(this.name + ' say Hello')
    }
}
```

```
class Person {
    public name:string;
    public sayHello(){
        console.log(this.name + 'say Hello')
    }
}
//-------以下属于类的外部--------
const person = new Person()
person.name = 'jspang.com'
person.sayHello()
console.log(person.name)
```

> #### private访问属性讲解
>

> private 访问属性的意思是，只允许再类的内部被调用，外部不允许调用

比如现在我们把 name 属性改成`private`,这时候在类的内部使用不会提示错误，而外部使用`VSCode`直接会报错。

```
class Person {
    private name:string;
    public sayHello(){
        console.log(this.name + 'say Hello')  //此处不报错
    }
}
//-------以下属于类的外部--------
const person = new Person()
person.name = 'jspang.com'    //此处报错
person.sayHello()
console.log(person.name)  //此处报错
```

> #### protected访问属性讲解
>

> protected 允许在类内及继承的子类中使用

#### TypeScript类的构造函数

> #### 类的构造函数

```
class Person{
    public name :string ;
    constructor(name:string){
        this.name=name
    }

}

const person= new Person('jspang')
console.log(person.name)
```

###### 简单写法：

```
class Person{
    constructor(public name:string){
    }
}

const person= new Person('jspang')
console.log(person.name)
```

> #### 类继承中的构造器写法

```
class Person{
    constructor(public name:string){}
}

class Teacher extends Person{
    constructor(public age:number){
        super('jspang')
    }
}

const teacher = new Teacher(18)
console.log(teacher.age)
console.log(teacher.name)
```

这就是子类继承父类并有构造函数的原则，就是在子类里写构造函数时，必须用`super()`调用父类的构造函数，如果需要传值，也必须进行传值操作。就算是父类没有构造函数，子类也要使用`super()`进行调用，否则就会报错。

```
class Person{}

class Teacher extends Person{
    constructor(public age:number){
        super()
    }
}

const teacher = new Teacher(18)
console.log(teacher.age)
```

#### TypeScript类的Getter、Setter和static使用

类的访问类型`private`，它的最大用处是封装一个属性，然后通过 Getter 和 Setter 的形式来访问和修改这个属性。

> #### 类的Getter和Setter

```
class Xiaojiejie {
  constructor(private _age:number){}
}
```

```
class Xiaojiejie {
  constructor(private _age:number){}
  get age(){
      return this._age
  }
}

const dajiao = new Xiaojiejie(28)

console.log(dajiao.getAge)
```

玄妙就在于`getter`里，我们可以对`_age`进行处理

```
class Xiaojiejie {
  constructor(private _age:number){}
  get age(){
      return this._age-10
  }
}
```

`_age`是私有的，那类的外部就没办法改变，所以这时候可以用`setter`属性进行改变：

```
class Xiaojiejie {
  constructor(private _age:number){}
  get age(){
      return this._age-10
  }
  set age(age:number){
    this._age=age
  }
}

const dajiao = new Xiaojiejie(28)
dajiao.age=25
console.log(dajiao.age)
```

其实`setter`也是可以保护私有变量的，现在大脚的年龄输出是 15 岁，在`setter`里给他加上个 3 岁，就18

```
set age(age:number){
   this._age=age+3
}
```

> #### 类中的static

```
class Girl {
  sayLove() {
    return "I Love you";
  }
}

const girl = new Girl();
console.log(girl.sayLove());
```

不想`new`出对象，而直接使用这个方法，那`TypeScript`为你提供了快捷的方式，用`static`声明的属性和方法，不需要进行声明对象，就可以直接使用

```
class Girl {
  static sayLove() {
    return "I Love you";
  }
}
console.log(Girl.sayLove());
```

#### 类的只读属性和抽象类

抽象类跟父类很像，都需要继承，但是抽象类里一般都有抽象方法。继承抽象类的类必须实现抽象方法才可以

> #### 类里的只读属性 readonly

```js
class Person {
    constructor(public name:string ){ }
}

const person = new Person('jspang')
console.log(person.name)
```

比如我现在有一个需求，就是在实例化对象时赋予的名字，以后不能再更改了，也就是我们常说的只读属性。我们先来看现在这种情况是可以随意更改的：

```
class Person {
    constructor(public name:string ){ }
}

const person = new Person('jspang')
person.name= '谢广坤'
console.log(person.name)
```

这时候就可以用一个关键词`readonly`,也就是只读的意思，来修改`Person`类代码。

```
class Person {
    public readonly _name :string;
    constructor(name:string ){
        this._name = name;
    }
}

const person = new Person('jspang')
person._name= '谢广坤'
console.log(person._name)
```

这样写完后，`VSCode`就回直接给我们报错，告诉我们`_name`属性是只读属性，不能修改。

> #### 抽象类的使用

比如我开了一个红浪漫洗浴中心，里边有服务员，有初级技师，高级技师，每一个岗位我都写成一个类，那代码就是这样的

```
class Waiter {}

class BaseTeacher {}

class seniorTeacher {}
```

我要求无论是什么职位，都要有独特的技能，比如服务员就是给顾客倒水，初级技师要求会泰式按摩，高级技师要求会 SPA 全身按摩。这是一个硬性要求，但是每个职位的技能有不同，这时候就可以用抽象类来解决问题。

抽象类的关键词是`abstract`,里边的抽象方法也是`abstract`开头的，现在我们就写一个`Girl`的抽象类。

```
abstract class Girl{
    abstract skill()  //因为没有具体的方法，所以我们这里不写括号
}
```

有了这个抽象类，三个类就可以继承这个类，然后会要求必须实现`skill()`方法，代码如下：

```
abstract class Girl{
    abstract skill()  //因为没有具体的方法，所以我们这里不写括号

}

class Waiter extends Girl{
    skill(){
        console.log('大爷，请喝水！')
    }
}

class BaseTeacher extends Girl{
    skill(){
        console.log('大爷，来个泰式按摩吧！')
    }
}

class seniorTeacher extends Girl{
    skill(){
        console.log('大爷，来个SPA全身按摩吧！')
    }
}
```

#### 配置文件-初识 tsconfig.json

> #### 生成 tsconfig.json 文件

```
tsc --init
```

如果此时你的`tsc`执行不了，很有可能是你没有全局安装 TypeScript,可以全局安装一下。

找到`complilerOptions`属性下的`removeComments:true`选项，把注释去掉。

如果要想编译配置文件起作用，我们可以直接运行`tsc`命令，这时候`tsconfig.json`才起作用，可以看到生成的`js`文件已经不带注释了。

> #### include 、exclude 和 files

1. 第一种：使用 include 配置

   `include`属性是用来指定要编译的文件的，比如现在我们只编译`demo.ts`文件，而不编译其他

   ```
   {
     "include":["demo.ts"],
     "compilerOptions": {
         //any something
         //........
     }
   }
   ```

   

2. 第二种：使用exclude配置

   `exclude`是不包含，除了demo2.ts不编译，其他都编译。

   ```
   {
      "exclude":["demo2.ts"],
     "compilerOptions": {
         //any something
         //........
     }
   }
   ```

3. 第三种：使用 files 配置

   `files`的配置效果和`include`几乎一样

   ```
   {
     "files":["demo.ts"],
     "compilerOptions": {
         //any something
         //........
     }
   }
   ```

#### 配置文件-初识 compilerOptions 配置项

它是告诉`TypeScript`具体如何编译成`js`文件的

> #### removeComments 属性

它的用处是告诉`TypeScript`对编译出来的`js`文件是否显示注释（注解）。比如我们现在把`removeComments`的值设置为`true`，就是在`js`中不显示注释。

```
// I'm JSPang
const person: string = "jspang";
```

把`removeComments`的值，设置为`true`，编译后：

```
"use strict";
var person = "jspang";
```

把`removeComments`的值，设置为`false`,编译后：

```
"use strict";
// I‘m JSPang
var person = "jspang";
```

> #### strict 属性

`strict`属性如果设置为`true`,就代表我们的编译和书写规范，要按照`TypeScript`最严格的规范来写，如果我们把这个设置为`false`或者注释掉，意思是我们可以对设置一些不严格的写法。

> #### noImplicitAny 属性

`noImplicitAny`属性的作用是，允许你的注解类型 any 不用特意表明

```
function jspang(name) {
  return name;
}
```

这时候我们的`TypeScript`是进行报错的，我们用`tsc`编译也是报错的。这就是因为我们开启了`strict:true`,我们先注释掉，然后把`noImplicitAny`的值设置为`false`,就不再报错了。

如果设置为`noImplicitAny:true`,意思就是值就算是 any（任意值），你也要进行类型注释。

```
function jspang(name: any) {
  return name;
}
```

你可以简单的理解为，设置为 true，就是必须明确置顶 any 类型的值。

> #### strictNullChecks 属性

我们先把`strictNullChecks`设置为`false`,它的意思就是，**不强制检查 NULL 类型。**我们举个例子，让你能一下子就明白，还是删除`demo.ts`里的代码，然后编写代码.

```
const jspang: string = null;
```

代码写完后，你会发现这段代码是不报错的，如果是以前，一定是报错的，这就是我们配置了“不强制检验 null 类型”。如果你设成`strictNullChecks:true`，这时候就报错了。

> #### ts-node 遵循 tsconfig.js 文件

#### 配置文件- compilerOptions 配置内容详解

> #### rootDir 和 outDir

```
{
    "outDir": "./build" ,
    "rootDir": "./src" ,
}
```

> #### 编译 ES6 语法到 ES5 语法-allowJs

```
export const name = "jspang";
```

如果不做任何配置，这时候试用`tsc`是没有效果的。需要到`tsconfig.js`文件里进行修改，修改的地方有两个。

```
"target":'es5' ,  // 这一项默认是开启的，你必须要保证它的开启，才能转换成功
"allowJs":true,   // 这个配置项的意思是联通
```

这两项都开启后，在使用`tsc`编译时，就会编译`js`文件了。

> #### sourceMap 属性

> sourceMap 简单说，Source map 就是一个信息文件，里面储存着位置信息。也就是说，转换后的代码的每一个位置，所对应的转换前的位置。有了它，出错的时候，除错工具将直接显示原始代码，而不是转换后的代码。这无疑给开发者带来了很大方便。

> #### noUnusedLocals 和 noUnusedParameters

```
const jspang: string = null;
export const name = "jspang";
```

这时候你会发现`jspang`这个变量没有任何地方使用，但是我们编译的话，它依然会被编译出来，这就是一种资源的浪费。

```
//编译后的文件
"use strict";
exports.__esModule = true;
exports.name = void 0;
var jspang = null;
exports.name = "jspang";
```

这时候我们可以开启`noUnusedLocals：true`，开启后我们的程序会直接给我们提示不能这样编写代码，有没有使用的变量。

`noUnusedParameters`是针对于名优使用的函数的，方法和`noUnusedLocals：true`一样，小伙伴们自己尝试吧。

###### 编译选项详解

[编译选项](https://www.tslang.cn/docs/handbook/compiler-options.html)