---
title: 'typeof,类型转换'
author: Darren
avatar: 'https://cdn.jsdelivr.net/gh/MINTACO/cdn@1.3/img/custom/avatar.jpg'
authorLink: mintaco.cn
authorAbout: 像风一样自由
authorDesc: 像风一样自由
categories: 开发
comments: true
tags: Javascript
photos: 'https://i.loli.net/2019/12/14/j36bxu5srdUBtH7.png'
date: 2020-01-22 15:24:52
keywords:
description:
---
# 1.typeof()
输出当前参数类型; 
可输出值：**number,string,boolean,object,undefined,function**;   
object泛指引用值，对象，数组，null都返回object;s   
也可写作`typeof param`;

# 2.类型转换
## 2.1 显示类型转换
1. Number(mix)
   将参数转化为数字，不能转化为数字的变为NaN,也是数字类型
   ![微信截图_20200122153854.png](https://i.loli.net/2020/01/26/ByCzAdXE6J5tfnR.png)
2. parseInt(string, radix)
    解析一个字符串，并返回一个整数,从数字位开始看，到非数字为止。radix可选。表示要解析成十进制的数字的基数。该值介于 2 ~ 36 之间。
如果省略该参数或其值为 0，则数字将以 10 为基础来解析。如果它以 “0x” 或 “0X” 开头，将以 16 为基数。
如果该参数小于 2 或者大于 36，则 parseInt() 将返回 NaN。
![2020-01-26_094946.png](https://i.loli.net/2020/01/26/Hr6OqKi9bWUvZQC.png)       
**妙用**
例如从获取的像素字符串中取出像素的值`parseInt("200px")`
3. parseFloat(string)
   解析一个字符串，并返回一个浮点数,从数字位开始看，到出了点以外的非数字位为止。没有基底参数。

4. String(mix)
   将参数转化为字符串
5. toString(radix)
   作用与String()基本相同，使用方法不同，且null和undefined不可用，原型上无此属性。radix参数规定转化的目标进制。
   ```
   //parseInt              toString
   //2     ----    10   ---    16
   var num = 10101010
   num1 = parseInt(num,2).toString(16) 
   ```
6. Boolean()
   将参数转化为布尔值

## 2.2 隐式类型转换
1. isNaN()
   用于检查其参数是否是非数字值。如果参数值为 NaN 或字符串、对象、undefined等非数字值则返回 true, 否则返回 false。   
   **内部过程：**`Number(参数)  <-->  NaN`
2. ++/--    +/-
   先调用Number(),变成数字类型。
3. +
   加号两侧有一侧为字符串类型，则调用String()将两侧都变成字符串类型。
4. -*/%
   对两侧数据调用Number(),再运算。
5. && || ！
   调用Boolean()。
6. < > <= >=
   一侧位数字类型，则都转换为数字类型
7. ==  !=
   ```
   1 == "1" //true
   1 == true  //true
   //判断时要用“===/!==”
   ```
8. 特殊
   ```
   null == undefined  //true
   NaN == NaN         //false
   ```

<br/>

   ![2020-01-26_124907.png](https://i.loli.net/2020/01/26/iJdRoNYQGnDP1SV.png)

