---
title: 初识接口Interface
date: 2020-11-10 10:44:44
tags:
-  TypeScript
categories: 
- 工作笔记
- TypeScript
---

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

##### 可选值的定义：

```
age ?: number (age可有可没有)
```

```
interface Girl {
	name: string;
	age : number;
	bust: number;
	waistline ?: number;
}
这样写不会报错：
const getResume = (girl:Girl)=>{
	console.log(girl.name+'年龄是'+girl.age)
	console.log(girl.name+'胸围是'+girl.bust)
	girl.waistline && console.log(girl.name+'腰围是:'+girl.waistline )
}
输出的内容还是跟原来一样

如果将girl改为：
const girl={
	name:'大脚",
	age: 18,
	bust: 94,
	waistline: 21
}

再输出打印，就会将waistline打印出来

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