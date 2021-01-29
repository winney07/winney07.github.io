---
title: JavaScript高级面向对象
date: 2021-01-21 17:46:22
tags:
- 听课笔记
categories:
- 工作笔记
- 听课笔记
---

### 1.面向对象编程介绍

#### 1.2面向过程编程POP(Process-oriented programming)

**面向过程**就是分析出解决问题所需要的步骤，然后用函数把这些步骤一步一步实现，使用的时候再一个一个的依次调用就可以了。

举个粟子∶将大象装进冰箱，面向过程做法。

1. 打开冰箱门
2. 大象装进去
3. 关上冰箱门

> 面向过程，就是按照我们分析好了的步骤，按照步骤解决问题。



#### 1.3面向对象编程OOP(Object Oriented Programming)

**面向对象**是把事务分解成为一个个对象，然后由对象之间分工与合作。

举个粟子：将大象装进冰箱，面向对象做法。
先找出对象，并写出这些对象的功能:

1. 大象对象

   -进去

2. 冰箱对象

   -打开

   -关闭

3. 使用大象和冰箱的功能

> 面向对象是以对象功能来划分问题，而不是步骤。



在面向对象程序开发思想中，每一个对象都是功能中心，具有明确分工。

面向对象编程具有灵活、代码可复用、容易维护和开发的优点，更适合多人合作的大型软件项目。

##### 面向对象的特性:

- 封装性
- 继承性
- 多态性



#### 1.4面向过程和面向对象的对比

##### 面向过程

- 优点︰性能比面向对象高，适合跟硬件联系很紧密的东西，例如单片机就采用的面向过程编程

- 缺点：没有面向对象易维护、易复用、易扩展



##### 面向对象

- 优点：易维护、易复用、易扩展，由于面向对象有封装、继承、多态性的特性，可以设计出低耦合的系统，使系统更加灵活、更加易于维护心

- 缺点：性能比面向过程低

  

用面向过程的方法写出来的程序是一份蛋炒饭，而用面向对象写出来的程序是一份盖浇饭。



### 2.ES6中的类和对象

#### 面向对象

面向对象更贴近我们的实际生活,可以使用面向对象描述现实世界事物。但是事物分为具体的事物和抽象的事物

手机   抽象的(泛指的)
           具体的(特指的)

面向对象的思维特点:
1．抽取(抽象)对象共用的属性和行为组织(封装)成一个类（模板）

2．对类进行实例化,获取类的对象

面向对象编程我们考虑的是有哪些对象，按照面向对象的思维特点不断的创建对象,使用对象,指挥对象做事情.

#### 2.1对象

现实生活中∶万物皆对象，对象是`一个具体的事物`，看得见摸得着的实物。例如，一本书、一辆汽车、一个人可以是“对象”，一个数据库、一张网页、一个与远程服务器的连接也可以是“对象”。
`在JavaScript中，对象是一组无序的相关属性和方法的集合，所有的事物都是对象`，例如字符串、数值、数组、函数等。

对象是由`属性`和`方法`组成的:

- 属性：事物的`特征`，在对象中用`属性`来表示(常用名词)
- 方法：事物的`行为`，在对象中用`方法`来表示(常用动词)

#### 2.2类class

在ES6中新增加了类的概念，可以使用`class`关键字声明一个类，之后以这个类来实例化对象。

`类`抽象了对象的公共部分，它`泛指`某一大类( class )

`对`象`特指`某一个，通过类实例化一个具体的对象

面向对象的思维特点:

1. 抽取（抽象）对象共用的属性和行为组织(封装)成一个`类`(模板)

2. 对类进行实例化,获取类的`对象`

#### 2.3创建类

语法︰

```
class name {
  class body
}
```

创建实例:

```
var XX = new name();
```

`注意：类必须使用new实例化对象`

1．创建类class创建一个明星类

```
class Star {
    constructor(uname, age) {
    	this.uname = uname;
    	this.age = age;
    }
}
```

2．利用类创建对象 new

```
var ldh = new Star('刘德华', 18);
var zxy = new star(张学友"，20);
console.log(ldh);
console.log(zxy);
```

- (1）通过class关键字创建类，类名我们还是习惯性定义首字母大写
- (2)   类里面有个constructor函数,可以接受传递过来的参数,同时返回实例对象
- (3)   constructor函数只要new生成实例时,就会自动调用这个函数，如果我们不写这个函数,类也会自动生成这个函数
- (4)   生成实例new不能省略
- (5）最后注意语法规范，创建类类名后面不要加小括号,生成实例类名后面加小括号，构造函数不需要加function

#### 2.5类添加方法

语法：

```
class Person {
	constructor (name, age){     // constructor构造器或者构造函数
		this.name = name;
		this.age = age;
	}
	say(){
		console.log (this.name + "你好");
	}
	sing(song){
		console.log ("我唱歌");
		console.log (this.name + song);
	}
}
var ldh = new Star('刘德华', 18);
var zxy = new star(张学友"，20);
// 1)我们类里面所有的函数不需要写function
// 2)多个函数方法之间不需要添加逗号分隔
ldh.sing("冰雨");
zxy.sing("李香兰");
```

### 3.类的继承

#### 3.1继承

现实中的继承：子承父业，比如我们都继承了父亲的姓。

程序中的继承：子类可以继承父类的一些属性和方法。

语法︰

```
// 父类
class Father{
	money() {
		console.log(100);
	}
}
// 子类继承父类
class Son extends Father{ 
}
var son = new Son();
son.money();
```

这样写，会报错：

```
// 父类
class Father{
	constructor(x, y){
		this.x = x;
		this.y = y;
	}
	sum() {
		console.log(this.x + this.y);
	}
}
// 子类继承父类
class Son extends Father{ 
	constructor(x, y){
		this.x = x;
		this.y = y;
	}
}
var son2 = new Son(1, 2);
son2.sum();
```

```
Uncaught ReferenceError:Must call super constructor in derived class before accessing 'this ' or returningfrom derived constructor
```

解决方法：

```
// 子类继承父类
class Son extends Father{ 
	constructor(x, y){
		super(x, y);   // 调用了父类中的构造函数
	}
}
```

#### 3.2 super关键字

`super关键字`用于访问和调用对象父类上的函数。`可以调用父类的构造函数`，也可以调用父类的普通函数



------

#### prototype-深入浅出原型

```
function Dogs() {

}
Dogs.prototype.name = 'collie';
Dogs.prototype.age = 24;
Dogs.prototype.DogsName = function() {
    alert(this.name);
}

//JS在创建对象（不论是普通对象还是函数对象）的时候，都有一个叫做__proto__的内置属性，用于指向创建它的函数对象的原型对象prototype
var DogsA = new Dogs();
// console.log(DogsA.DogsName());

// DogsA 的construtor（构造函数）是Dogs()
console.log(Dogs.prototype);
console.log(DogsA.constructor);
console.log(DogsA);

// DogsA的__proto__属性等于Dogs的prototype属性
console.log(Dogs.prototype === DogsA.__proto__);   //true

//Dogs.prototype对象也有 _proto _ 属性，它指向创建它的函数对象（Object）的 prototype。
//Dogs.prototype的__proto__属性等于Object的prototype属性
console.log(Dogs.prototype.__proto__ === Object.prototype);  //true

//判断是不是某实例化对象的原型
console.log(Dogs.prototype.isPrototypeOf(DogsA));
```

