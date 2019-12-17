---
title: JSON.stringify/JSON.parse技巧
author: Darren
avatar: 'https://cdn.jsdelivr.net/gh/MINTACO/cdn@1.3/img/custom/avatar.jpg'
authorLink: mintaco.cn
authorAbout: 像风一样自由
authorDesc: 像风一样自由
categories: 技术
comments: true
tags: Javascript
photos: https://i.loli.net/2019/12/14/j36bxu5srdUBtH7.png
date: 2019-11-19 10:40:57
keywords:
description:
---
JSON.stringify()的作用是将js对象转换为 JSON 字符串，而JSON.parse()可以将JSON字符串转为一个对象。
# 1.深度拷贝
在实际开发中，为了不影响原对象，可利用```JSON.parse( JSON.stringify(obj) )```深度拷贝原obj的副本。
# 2.判断数组中是否包含某对象
```
//判断数组是否包含某对象
let data = [
    {name:'hi'},
    {age:'13'},
    {job:'coder'},
    ],
    val = {name:'hi'};
JSON.stringify(data).indexOf(JSON.stringify(val)) !== -1;//true

```
# 3.判断对象（数组）是否相等
```
  let a = [1,2,3],
    b = [1,2,3];
console.log(JSON.stringify(a) === JSON.stringify(b));
```
