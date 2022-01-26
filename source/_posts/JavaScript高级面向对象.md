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

[JavaScript面向对象-原型的内存模型](http://www.htmleaf.com/ziliaoku/qianduanjiaocheng/201512142905.html)

> 通过prototype创建的属性和方法，会存放在函数对象中的`__pro__`属性中，`__pro__`是一个对象
>
> 通过prototype创建的属性和方法，也会存放在该函数对象的`__pro__`属性中的constructor（例如：构造函数是Person)中的prototype中 

创建一个对象是会给它分配内存空间的。

通过构造函数的方法，创建一个对象出来，在新对象的内存空间中会有一个`_proto_`内部属性，这个内部属性是不能被访问的，它也指向构造函数（例如：`Person`）的原型。`_proto_`内部属性是隐藏的

> 需要特别注意的是：原型中的值是不会被替换的，仅仅只是在属性查找时被对象自己空间中的同名属性所覆盖。

[JavaScript面向对象-原型的重写](http://www.htmleaf.com/ziliaoku/qianduanjiaocheng/201512162910.html)

#### 对象的创建方式不一样，存储位置不一样

这里定义了两个对象，即使内容一样，但是存储位置不一样

```
var objectFoo = {same : 'same' };
var objectBar = {same : 'same' };
console.log(objectFoo == objectBar); // false
```

这里也是定义两个对象，但是它们的存储位置一样

```
var objectA = { foo: 'bar' };
var objectB = objectA;
console.log(objectA == objectB);  // true
```

[exports 和 module.exports 的区别](http://cnodejs.org/topic/5231a630101e574521e45ef8)

1. module.exports 初始值为一个空对象 {}

2. exports 是指向的 module.exports 的引用

3. require() 返回的是 module.exports 而不是 exports



[Javascript 面向对象(共有方法，私有方法，特权方法，静态属性和方法，静态类)示例讲解...](https://blog.csdn.net/weixin_30791095/article/details/97718955)

[Javascript 面向对象(共有方法，私有方法，特权方法，静态属性和方法，静态类)示例讲解](https://www.cnblogs.com/xiongzaiqiren/p/6733985.html)

#### 一，私有属性和方法

私有方法：私有方法本身是可以访问类内部的所有属性(即私有属性和公有属性)，但是私有方法是不可以在类的外部被调用。 

```
 1 <script>
 2     /*
 3     * 私有方法：私有方法本身是可以访问类内部的所有属性(即私有属性和公有属性)，但是私有方法是不可以在类的外部被调用。 
 4     */
 5     //JavaScript对象私有属性，私有方法示例
 6     function JSClass() {
 7         //私有变量只有在函数或者对象作用域范围内能访问
 8         var privateAttribute = "私有属性";
 9 
10         function privateMethod_A() {
11             console.log("私有方法A，" + privateAttribute);
12         };
13 
14         var privateMethod_B = function () {
15             console.log("私有方法B，" + privateAttribute);
16         };
17 
18         //私有方法可以在函数作用域范围内使用。
19         privateMethod_A();
20         privateMethod_B();
21         
22         /*
23         私有属性和方法还有个特点：都不能用this访问。
24         下面几种是不行的：
25         this.privateAttribute;
26         this.privateMethod_A();
27         this.privateMethod_B();
28         */
29     };
30 
31     /*new一个实例*/
32     var instance = new JSClass();
33     console.dir(instance); //instance实例访问不到私有属性及私有方法
34 </script>
```

说明：类的构造函数里定义的function，即为私有方法；而在构造函数里用var声明的变量，也相当于是私有变量。(不过类比于c#这类强类型语言中的私有成员概念还是有区别的，比如无法在非构造函数以外的其它方法中调用) 。

私有方法
对象的私有方法和属性,外部是不可以访问的,在方法的内部不是能this调用对象的公有方法、公有属性、特权方法的。

 

 

#### 二，公有属性和方法

公有方法：

1.公有方法是可以在类的外部被调用的，

2.但是它不可以访问类的私有属性。

3.公有方法必须在类的内部或者外部通过类的prototype属性添加。

```
 1 <script>
 2     /*
 3     * 公有方法： 
 4 　　* 1.公有方法是可以在类的外部被调用的； 
 5 　　* 2.但是它不可以访问类的私有属性；
 6 　　* 3.公有方法必须在类的内部或者外部通过类的prototype属性添加。 
 7     */
 8     //JavaScript对象公有属性，公有方法示例
 9     function JSClass() {
10         //公有变量在函数内或者实例都能访问
11         this.publicAttribute = "公有属性";
12 
13         this.publicMethod_A = function () {
14             console.log("公有方法A，" + this.publicAttribute);
15         };
16 
17         //公有方法可以在类的内部添加
18         JSClass.prototype.publicMethod_B = function () {
19             console.log("公有方法B，" + this.publicAttribute);
20         };
21 
22         //公有方法可以在函数作用域范围内使用，也可以在函索作用域范围外使用，可以被实例调用和继承
23         this.publicMethod_A();
24         this.publicMethod_B();
25 
26         /*
27         公有属性和方法有个特点：在内部访问都必须用this访问
28         下面几种是不行的：
29         publicAttribute;
30         publicMethod_A();
31         publicMethod_B();
32         */
33     };
34 
35     //公有方法也可以在类的外部通过类的prototype属性添加
36     JSClass.prototype.publicMethod_C = function () {
37         console.log("公有方法C，" + this.publicAttribute);
38     };
39     
40     /*new一个实例*/
41     var instance = new JSClass();
42     console.log("实例调用公有属性：" + instance.publicAttribute);
43     console.log("实例调用公有方法：" + instance.publicMethod_A());
44     console.log("实例调用公有方法：" + instance.publicMethod_B());
45     console.dir(instance); //instance实例可以访问公有属性及方法
46 
47     //但是,通过实例添加公有属性是不行的
48     //instance.prototype.publicMethod_D = function () {
49     //    console.log("公有方法D，" + this.publicAttribute);
50     //};
51 
52 </script>
```

公有方法的调用规则
调用公有方法，我们必需先实例化对象
公有方法中通过不this调用公有属性和特权方法，不能使用this调用静态方法和属性，必需裁通过对象本身调用，即对象名。公有方法也不能调用私有方法。

 

 

#### 三，特权方法

特权方法：

1.特权方法是可以在类的外部被调用的，

2.但是它可以访问类的私有属性，并且也是可以访问类的公有属性，可以勉强的认为它是一种特殊的公有方法。

3.但是它与上面的公有方法的声明与定义方式不同。特权方法必须在类的内部声明定义。

```
 1 <script>
 2     /*
 3     * 特权方法： 
 4 　　* 1.特权方法是可以在类的外部被调用的；
 5 　　* 2.但是它可以访问类的私有属性，并且也是可以访问类的公有属性，可以勉强的认为它是一种特殊的公有方法；
 6 　　* 3.但是它与上面的公有方法的声明与定义方式不同。特权方法必须在类的内部声明定义。 
 7     */
 8     //JavaScript对象特权方法示例
 9     function JSClass() {
10         //私有变量只有在函数或者对象作用域范围内能访问
11         var privateAttribute = "私有属性";
12         //私有方法
13         function privateMethod() {
14             console.log("私有方法");
15         }
16 
17         //通过使用this关键字定义一个特权方法
18         this.privilegeMethod = function () {
19             //在特权方法中可以访问私有属性和私有方法
20             console.log("特权方法，" + privateAttribute + "," + privateMethod());
21         };
22     };
23     /*new一个实例*/
24     var instance = new JSClass();
25     console.log("实例调用特权方法：" + instance.privilegeMethod());
26     console.dir(instance); //instance实例可以访问公有属性及方法
27 
28     /*
29     * 特权方法浏览器兼容支持性很差，避免使用！
30     */
31 </script>
```

特权方法的调用规则
特权方法通过this调用公有方法、公有属性，通过对象本身调用静态方法和属性，在方法体内直接调用私有属性和私有方法。

 

 

公有方法：就是所有通过该类实例化出来的对象，共同都拥有或者说都可以使用的方法。一般把共用的方法，都放在“原型对象“当中，如果放在构造函数中，会重复创建共同的方法。

私有方法：不能在外部调用。
特权方法：利用的闭包原理，即通过作用域链，让内部函数能够访问外部函数的变量对象(即该类的私有变量、私有方法)。

 

#### 四，静态属性和方法

静态属性和方法：
无需实例化(即无需用new操作符实化对象)就可以调用的方法就叫静态方法。

```
 1 <script>
 2     /*
 3     * 静态属性和方法： 
 4 　　* 无需实例化(即无需用new操作符实化对象)就可以调用的方法就叫静态方法。
 5     */
 6     //JavaScript对象静态属性和方法示例
 7     function JSClass() { };
 8 
 9     JSClass.staticAttribute = "静态属性";
10     JSClass.staticMethod = function () {
11         return "静态方法，" + JSClass.staticAttribute;
12     };
13 
14     //无需实例化(即无需用new操作符实化对象)就可以调用的方法就叫静态方法。
15     console.log(JSClass.staticAttribute);
16     console.log(JSClass.staticMethod());
17 
18     /*new一个实例*/
19     var instance = new JSClass();
20     //instance.staticAttribute; //错误！
21     //instance.staticMethod(); //错误！
22     console.dir(instance); //instance实例不可以访问静态属性及方法
23 </script>
```

 

静态方法的调用规则
使用静态方法时，无需实例化对象，便可以调用，对象实例不能调用对象的静态方法，只能调用实例自身的静态属性和方法。

 

#### 五，静态类

静态类：
无需实例化(即无需用new操作符实化对象)就可以调用的方法就叫静态方法，
只包含静态属性和静态方法的类叫静态类，不能被实例化。

```
 1 <script>
 2     /*
 3     * 静态类： 
 4 　　* 无需实例化(即无需用new操作符实化对象)就可以调用的方法就叫静态方法，
 5     * 只包含静态属性和静态方法的类叫静态类，不能被实例化。
 6     */
 7     //JavaScript对象静态类示例
 8     var jsStaticClass = {
 9         staticAttribute_A: "静态属性A",
10         staticMethod_A: function () {
11             //静态方法内部可以访问静态属性
12             return "静态方法A，" + this.staticAttribute_A + "," + jsStaticClass.staticAttribute_A;
13         }
14     };
15 
16     //静态属性和方法也可以在外部定义和访问
17     jsStaticClass.staticAttribute_B = "静态属性B";
18     jsStaticClass.staticMethod_B = function () {
19         //静态方法内部可以访问静态属性
20         return "静态方法B，" + this.staticAttribute_A + "," + jsStaticClass.staticAttribute_B;
21     };
22 
23 
24     //无需实例化(即无需用new操作符实化对象)就可以调用的方法就叫静态方法。
25     console.log(jsStaticClass.staticAttribute_A);
26     console.log(jsStaticClass.staticAttribute_B);
27     console.log(jsStaticClass.staticMethod_A());
28     console.log(jsStaticClass.staticMethod_B());
29 
30     //var instance = new jsStaticClass(); //静态类不能被实例化！
31 </script>
```

#### [Javascript设计模式详解](https://www.cnblogs.com/tugenhua0707/p/5198407.html)

#### [【原】常用的javascript设计模式](https://www.cnblogs.com/xianyulaodi/p/5827821.html)

#### [深入理解JavaScript系列（31）：设计模式之代理模式](https://www.cnblogs.com/TomXu/archive/2012/02/29/2354979.html)

#### [javascript设计模式——策略模式](https://www.cnblogs.com/xiaohuochai/p/8029651.html)

#### [JavaScript-原型式继承](https://www.cnblogs.com/gehaoyu/p/11804836.html)