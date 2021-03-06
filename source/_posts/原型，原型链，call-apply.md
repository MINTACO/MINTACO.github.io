---
title: 原型，原型链，call/apply
author: Darren
avatar: 'https://cdn.jsdelivr.net/gh/MINTACO/cdn@1.3/img/custom/avatar.jpg'
authorLink: mintaco.cn
authorAbout: 像风一样自由
authorDesc: 像风一样自由
categories: 开发
comments: true
tags: Javascript
photos: 'https://i.loli.net/2019/12/14/j36bxu5srdUBtH7.png'
date: 2020-02-10 15:17:26
keywords:
description:
---
# 1.原型
# 1.1 原型概念
原型是**function对象**的一个属性，它定义了构造函数制造出的对象的公共祖先。这个属性是系统自带的，在函数出生的时候即被定义。通过该构造函数产生的对象，可以继承该原型的属性和方法。**原型也是对象**。    

可以形象化的理解为：构造函数.prototype是通过构造函数构造出的对象的父级。

***只有function对象有原型***
```
//利用原型特点，可以提取公有属性
// Car.prototype.carName = "BMW";
// Car.prototype.length = 5000;
Car.prototype = {
    carName : 'BMW',
    length : 5000
}
function Car(owner, color){
    this.owner = owner;
    this.color = color;
    this.length = 1000;   
}

var car = new Car('Darren', 'black')
console.log(car.length);  //1000   自身有属性则优先级高于原型上的属性
car.carName = 'Benz';  //不会修改原型上的属性，修改的只是自身的属性
delete car.carName;    //true  删除的只是自身的属性，不可能通过构造出的对象修改原型上的属性。
// 除非直接操作原型。

```
## 1.2 constructor属性
constructor属性：构造器，返回实例的构造函数，是**原型自带**的属性，可以手动更改，例如：
![constructor.png](https://i.loli.net/2020/02/12/1x4QwiuLtnUk6lX.png)
```
function Person(){

}

var person = new Person();

console.log(person.constructor);  //function Person(){}  从原型继承而来

function Student(){}

Person.prototype.constructor = Student;

console.log(person.constructor);  //function Student(){}
```


# 2.原型链
## 2.1 定义
定义:像作用域链一样访问的原型链，通过__proto__来串联。
```
function Person(){
    // var this = {
    //     __proto__ : Person.prototype   
    //}
    //链接到原型，可以被修改
}

var person = new Person();
console.log(person.__proto__)   //对象查看原型，通过__proto__
```
原型链示意:
```
//绝大多数对象原型链的尽头都是Object.prototype,即Grand.prototype.__proto__ = Object.prototype

Grand.prototype.age = 90;
function Grand(){

}
var grand = new Grand();

Father.prototype = grand;

function Father(){
    this.name = 'father';
}
var father = new Father();

Son.prototype = father;

function Son(){

}
var son = new Son();

console.log(son.age);//90
```

## 2.1 特殊情况
```
var obj = {} 
//对象字面量也有原型，等同于 var obj = new Object();开发时必须用字面量形式定义
//obj.__proto__ = Object.prototype

```

**Object.create( null/object )**
```
//用法
Person.prototype.name = 'Darren';
function Person(){

}

var person = Object.create(Person.prototype);

//特殊情况：在以null作为原型构造出的对象没有原型
var obj = Object.create( null );
console.log(obj.__proto__);   //undefined
//因为有这个特例，所以才说绝大多数对象继承自Object.prototype,而不是全部
```
## 2.3 引申

```
//平时我们用的num.toString(),boolean.toString()就是由于包装类的存在而调用了原型链上的toString()方法
//像undefined这种原始值或者null则没有原型，即不能用toString()方法

123.toString();  //报错，因为js会首先识别成浮点型
var num = 123;
num.toString();  //正确用法

var obj = {};
obj.toString()    //[object Object]
//对象调用toString即调用Object.prototype上的toString()方法
//num,boolean值调用的则是自身包装类上重写的toString()方法
//num.toString() --> new Number(num).toString()
Number.prototype.toString = function(){
    //重写的方法
}
Number.prototype.__proto__ = Object.prototype   //优先使用自身的方法

//Number,Array,String,Boolean都重写了toString()方法

//本身的方法输出的结果平时没啥用，但可用作区分数组与对象，例如
Object.prototype.toString.call([]);  //"[object Array]"
var obj = {};
Object.prototype.toString.call(obj);  //"[object Object]"
```
**区分数组与对象的三种方法：**  
1. constructor
2. instanceof
3. Object.prototype.toString()

# 3.call/apply
## 3.1 作用
1. 改变this指向

```
function test(){

}

test()  <==>  test.call()  函数执行的原本形态

//用法
function Person(name, age){
    this.name = name;
    this.age = age;
}

var obj = {};

Person.call(obj, 'Darren', 23)
//此时Person中的this指向变为obj，call得后续参数为实参列表

```
2. 可以借助改变this指向实现共享方法
   
```
function Person(name, age){
   this.name = name;
   this.age = age;
}

function Student(name, age, sex, score){
   Person.call(this, name, age);
   this.sex = sex;
   this.score = score;

}
var st = new Student( 'Darren', 23, 'male', 100 )
```
## 3.2 call/apply区别
传参形式不同，call可以一个个传实参进去，apply只能传实参列表，如下所示：
```
function Person(name, age){
   this.name = name;
   this.age = age;
}

function Student(name, age, sex, score){
   Person.apply(this, [name, age]);
   this.sex = sex;
   this.score = score;

}
var st = new Student( 'Darren', 23, 'male', 100 )

```