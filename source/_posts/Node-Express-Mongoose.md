---
title: Node-Express-Mongoose
date: 2024-03-19 16:45:21
tags:
- express
- mongodb
categories:
- node.js
---

`app.js`

```
//uselNewUrlParser这个属性会在url里识别验证用户所需的db,未升级前是不需要指定的,升级到一定要指定。
mongoose.connect('mongodb://127.0.0.1:27017/egecms',{ useNewUrlParser: true },function(err){
    if(err){
        console.log(err);
        return;
    }
    console.log( '数据库连接成功")
);
```

```
// 定义数据表（集合的）映射︰注意。字段名称必须和数据库保持一致
var UserSchema=mongoose.Schema({
    name:String,
    age:Number,
    status:{
        type:Number,
        default:1
    }
})
// 定义model操作数据库
```

`user.js`

```
var mongoose = require('./db.js');
var UserSchema=mongoose.Schema({
    name:String,
    age:Number,
    status:{
        type:Number,
        default:1
    }
})
module.exports=mongoose.model( "User", UserSchema, "user');
```

`app.js`

```
var UserModel=require("./model/user.js");

UserModel.find({},function(err,docs){
    if(err){
        console.log(err);
        return;
    }
    console.log(docs);
})
```

`news.js`

```
var mongoose=require('./db.js');

var NewsSchema=mongoose.Schema({
    title:{
        type:String,
        trim:true	//定义 mongoose模式修饰符去掉空格
    },
    author: String,
    pic:String,
    content:String,
    status:{
        type:Number,
        default:1
    }
})

module.exports=mongoose.model('News',NewsSchema, 'news');
```

`app.js`

```
console.time('user');
var UserModel=require("./model/user.js");
console.timeEnd('user');
console.time('news');
var NewsModel=require('./model/news.js');
console.timeEnd('news');
```

### Mongoose预定义模式修饰符Getters与Setters自定义修饰符

#### 一、mongoose预定义模式修饰符

lowercase、uppercase 、 trim

mongoose提供的预定义模式修饰符，可以对我们增加的数据进行一些格式化。

#### 二、Mongoose Getters 与Setters自定义修饰符

除了mongoose内置的修饰符以外，我们还可以通过set(建议使用）修饰符在增加数据的时候对数据进行格式化。也可以通过get(不建议使用）在实例获取数据的时候对数据进行

### Mongoose索引、Mongoose内置CURD方法、扩展Mongoose Model的静态方法和实例方法

#### 一、Mongoose索引

#### 二、Mongoose内置CURD

### Mongoose数据校验

#### 一、Mongoose校验参数

- required :表示这个数据必须传入
- max用于Number类型数据,最大值
- min:用于Number类型数据,最小值
- enum:枚举类型，要求数据必须满足枚举值`enum: ['0','1','2']`
- match:增加的数据必须符合match(正则)的规则
- maxlength:最大值
- minlength:最小值

### Mongoose中使用aggregate聚合管道
