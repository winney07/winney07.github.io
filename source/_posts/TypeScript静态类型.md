---

title: TypeScript静态类型
date: 2020-11-06 11:22:40
tags:
-  TypeScript
categories: 
- 工作笔记
- TypeScript
---
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