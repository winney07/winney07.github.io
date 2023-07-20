---
title: TypeScript--笔记
date: 2022-05-16 15:48:09
tags:
-  TypeScript
categories: 
- JavaScript
- TypeScript
---

[Typescript-官网](https://www.typescriptlang.org/)

[TypeScript中文网](https://www.tslang.cn/docs/home.html)

[TypeScript 中文手册](https://typescript.bootcss.com/)

[TypeScript React Starter](https://github.com/Microsoft/TypeScript-React-Starter/blob/master/tsconfig.json) 

- [在 React 中使用 TypeScript](https://github.com/Microsoft/TypeScript-React-Starter#typescript-react-starter)
- [TypeScript 文档：基本类型](https://www.typescriptlang.org/docs/handbook/basic-types.html)
- [TypeScript 文档：JavaScript 迁移](https://www.typescriptlang.org/docs/handbook/migrating-from-javascript.html)
- [TypeScript 文档：React 与 Webpack](https://www.typescriptlang.org/docs/handbook/react-&-webpack.html)

- [在 Create React App 中使用 TypeScript](https://react.docschina.org/docs/static-type-checking.html#using-typescript-with-create-react-app)

如需将 TypeScript 添加到**现有的 Create React App 项目**中，[请参考此文档](https://facebook.github.io/create-react-app/docs/adding-typescript).

通过[此文档](https://github.com/Microsoft/TypeScript-React-Starter#typescript-react-starter) 了解更多有关在 React 中使用 TypeScript 的知识。

安装

```
cnpm insatll -g typescript 
```

查看版本

```
tsc -v
```



JavaScript，只是一个脚本语言，并非设计用于开发大型 web应用，JavaScript。没有提供类和模块的概念，而TypeScript，扩展了JavaScript，实现了这些特性。

#### Typescript，主要特点包括：

Typescript，是微软推出的开源语言，使用Apache授权协议

TypeScript，是Javascript的超集.

Typescript，增加了可选类型、类和模块

Typescript，可编译成可读的、标准的Javascript

Typescript，支持开发大规模Javascript应用

Typescript，设计用于开发大型应用，并保证编译后的JavaScript代码兼容性

Typescript，扩展了Javascript的语法，因此已有的avascript代码可直接与

TypeScript，一起运行无需更改

TypeScript，文件扩展名是ts，而Typescript编译器会编译成js文件

Typescript，语法与Jscript. .NET相同

#### typescript中定义函数

> 在现在编程领域，强调开发人员能够开发高可靠性，高复用，可测试，易于维护
> 的代码，对编程人员来说一个基本的要求。而原生的javascript做到以上的几点非常不容易，那么，typescript是以原生javascript为基础，提供了一个满足以上几点的js扩展框架，极大的增强了javascript的设计和开发能力。

在javascript编程中最为重要的一个对象就是function
我们都知道function,他是一个特除的对象，我们可以用function来帮助我们实现抽象层，function在原生的定义上面其代码的可读性并不强，
在typescript里面，对function做了进一步讲法上的扩展，这些扩展大大的增加了我们代码的可读性和可维护性

1. 函数类型(有名函数,匿名函数)
2. 可选/默认参数
3. 可变参数
4. 函数重载
5. Lambads和this关键字

##### 有名函数

```
function test(){}
```

##### 匿名函数

```
var test2 = function(){}
```

##### 可选参数，在参数后加？

```
function test2(n:string, age?:number):string{
	return "ok";
}
```

##### 默认值

```
function test3(n:string, age=19):number{
	return age;
}
```

#### typescript的类

```
// ts的写法
class Person {
	// 类的成员属性
	name:string;
	age:number;
	instrestes:string[];
	
	// 类的实例方法
	say():void{
		alert(this.name + ": say hello class!")
	}
}

// 原生js的写法
function Person(){
	this.name = "";
	this.age = "";
}
Person.prototype.say = function() {
	alert(this.name + ": say hello class!")
}
```

#### 定义接口

```
interface Girl {
	name: string;
	age : number;
	bust: number;
}
```

```
const girl={
	name:'大脚",
	age: 18,
	bust: 94
}
const screenResume= (girl : Girl)=>{
	girl.age < 24 && girl.bust >=90 && console.log( girl.name+'进入面试')
	girl.age >= 24 || girl.bust <90 && console.log( girl.name+'你被淘汰")
}
const getResume = (girl:Girl)=>{
	console.log(girl.name+'年龄是'+girl.age)
	console.log(girl.name+ '胸围是'+girl.bust)
}
screenResume(girl)
getResume(girl)
```

```
const screenResume= (name: string,age: number,bust:number)=>{
	age < 24 && bust >=90 && console.log(name+'进入面试')
	age >= 24 || bust <90 && console.log(name+'你被淘汰')
}
const getResume = (name : string, age : number, bust: number)=>{
	console.log(name+'年龄是'+age)
	console.log(name+'胸围是'+bust)
}
screenResume('大脚',18,94)
getResume('大脚",18,94)
```

##### 可选值的定义：

```
age ? : number (age可有可没有)
```

```
interface Girl {
	name: string;
	age : number;
	bust: number;
	waistline ?: number;
}
// 这样写不会报错：
const getResume = (girl:Girl)=>{
	console.log(girl.name+'年龄是'+girl.age)
	console.log(girl.name+'胸围是'+girl.bust)
	girl.waistline && console.log(girl.name+'腰围是:'+girl.waistline )
}
// 输出的内容还是跟原来一样

// 如果将girl改为：
const girl={
	name:'大脚",
	age: 18,
	bust: 94,
	waistline: 21
}

// 再输出打印，就会将waistline打印出来
```

##### 定义一个可以加任何属性

```
[propname:string]: any;
```

```
interface Girl {
	name: string;
	age : number;
	bust: number;
	waistline ?: number;
	[propname:string]: any;
}
const girl={
	name: "大脚",
	age: 18,
	bust:94,
	waistline: 21,
	sex:'女’
}
```

##### 添加方法：

```
interface Girl {
	name: string;
	age : number;
	bust: number;
	waistline ?: number;
	[propname:string]: any;
	say(): string;
}
const girl={
	name:'大脚"，
	age: 18,
	bust:94,
	waistline: 21,
	sex: '女'，
	say(){
		return "欢迎光临，红浪漫洗浴!!”
	}
}
```

##### 接口和类的约束

```
class xiaojieJie implements Girl{
	name="刘英"
	age=18
	bust=90
	say(){
		return "欢迎光临,红浪漫洗浴!!"
	}
}
```

##### 接口间的继承

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

```
console.log(Status.MASSAGE, Status[1]);
```

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

```
class SelectGirl<T extends number | string> {
  //.....
}
```

#### TypeScript 静态类型

##### TypeScript 最主要的特点就是可以定义静态类型

Static Typing  (一旦定义了就不可以再改变了)

```
let count : number = 1;   (一旦定义了是number，就是number，不能改变类型。)
count.后面可以跟number的所有方法
```

```
interface XiaojieJie {
    uname: string, 
    age: number
}

const xiaohong : XiaojieJie = {
    uname: '小红', 
    age: 18
}
console.log(xiaohong.age) 
```

#### 基础静态类型和对象静态类型

##### 基础静态类型

```
const count0 : number = 918;
const myName : string = 'jspang';
// null , undefinde , booLean, void, symboL
```

##### 对象静态类型

```
const xiaojieJie: {
    name : string,
    age : number 
} = {
    name : '大脚',
    age:18
}
```

```
const xiaojiejie : string [] = ["小红", "小林", "小星星"]

class Person{}
const dajiao : Person = new Person();
```

定义一个函数，返回值必须是字符串：

```
const jianXiaoJieJie :()=>string =()=>{return '大脚'}
//对象类型，数组类型，类类型，函数类型
```

#### 类型注解和类型推断

##### 类型注解 - type annotation

```
let count : number ;

function getTotal(one : number , two : number){
	return one + two
}
const total = getTotal(1,2);
```



##### 类型推断 - type inference



#### 函数参数和返回类型的注解

```
function getTotal(one : number , two : number){
	return one + two +''
}
const total = getTotal(1,2);  (会有错误提示) （定义的是number类型，返回的是string类型）

解决方法：对返回做注解
function getTotal(one : number , two : number): number{
	return one + two +''  (这样写，编辑器就会有错误的提示)
}

改正：
function getTotal(one : number , two : number): number{
	return one + two 
}
```

###### void：

```
function sayHe1lo(): void{
	console.log('Hello worid')
	return "";(如果在函数中，任何地方有return就会报错，就会很直观的知道);
}
```

###### never：

```
抛出异常：
function errorFuntion() : never{
	throw new Error()
	console.log("Hello world")
}
或者死循环：
function forNever() : never{
	while(true){}
	console.log( 'Hello world ')
}
```

```
function add({one ,two} : {one : number ,two : number} ){
	return one + two
}
const total = add(fone: 1,two:2}); 

function getNumber({one} : {one : number}){
	return one
}
const one = getNumber({one: 1})
```

#### 数组类型注解的方法

##### 类型推断

```
const numberArr = [1,2,3]
(鼠标放上去，能够看到推断出是number类型)
```

##### 类型注释

```
const numberArr : number[] = [1,2,3];
const stringArr : string[] = ['a', 'b', 'c'];
const undefinedArr : undefined[] = [undefined, undefined];
const arr : (number | string)[] = [1, 'string', 2];
```

##### 对象数组

```
const xiaojiejies :{name : string, age:number}[] =[
	{name: '刘英', age: 18},
	{name : '谢大脚", age: 28},
]
```

###### 其他形式写法：

1. ###### type alias 类型别名

   ```
   type Lady = {name: string,age: number}
   const xiaojiejies : Lady[] [
   	{name:'刘英', age: 18},
   	{name : '谢大脚" , age:28},
   ]
   ```

2. ###### 类

   ```
   class Madam {
   	name: string ;
   	age : number;
   }
   const xiaojiejies : Madam[] = [
   	{name: '刘英', age: 18},
   	{name: '谢大脚", age: 28},
   ]
   ```

   

#### 元组的使用和类型约束

##### 类型约束

```
// const xiaojiejie : (string | number)[] = [ 'dajiao ' , 'teacher ', 28]
```

##### 元组的写法

```
const xiaojiejie : [string,string,number] = [ 'dajiao' , 'teacher',28]
```

##### CSV（现在很少用）

```
const xiaojiejies : [string, string, number][] =[
	[ 'dajiao ' , 'teacher" ,28],
	[ 'liuying" , 'teacher' ,18],
	[ " cuihua ' , 'teacher" ,22]
]
```

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



[【技术胖博客】](https://jspang.com/detailed?id=63)

###### Demo1.ts

```
function jspang() 
{ 
    let web: string = "Hello world" 
    console.log (web)
}
jspang()
```



##### 初步运行

```
node Demo.ts

会出现报错：
SyntaxError: Unexpected token ':'
表示异常，不支持这个东西。
```

输入以下语句来转ts为js：

```
tsc Demo1.ts
```

如果出现：
 无法将“tsc”项识别为 cmdlet、函数、脚本文件或可运行程序的名称。请检查名称的拼写，如果包括路径，请确保路径正确，然后再试一次。

[参考](https://www.cnblogs.com/vickylinj/p/12228773.html)  则：

```
npm install typescript -g
cnpm install typescript -g

再次运行即可：
tsc Demo1.ts
node Demo1.js
```

每次都这样的操作比较麻烦，可以全局安装ts-node

```
cnpm install -g ts-node 
```

即可直接输入以下语句执行：

```
ts-node Demo1.ts
```

#### typescript安装与配置

查看版本：

```
tsc --version
```

创建tsconfig.json文件：

```
tsc --init
```

使用tsc命令的时候，会在执行tsc命令的当前目录下找，有没有tsconfig.json文件，如果有，就会读取里面的配置项，对当前目录文件进行编辑工作

[tsconfig.json](https://www.tslang.cn/docs/handbook/tsconfig-json.html)

[编译选项](https://www.tslang.cn/docs/handbook/compiler-options.html)

`"module": "commonjs",`是不允许输出的，即设置`"module": "commonjs",`的时候，再设置`out:"build/out.js"`， 是会报错的，需要将module改为`"module": "system"`



在编程的过程中发现错误