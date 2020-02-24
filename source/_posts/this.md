---
title: this
author: Darren
avatar: 'https://cdn.jsdelivr.net/gh/MINTACO/cdn@1.3/img/custom/avatar.jpg'
authorLink: mintaco.cn
authorAbout: 像风一样自由
authorDesc: 像风一样自由
categories: 开发
comments: true
tags: Javascript
photos: 'https://i.loli.net/2019/12/14/j36bxu5srdUBtH7.png'
date: 2020-02-17 10:54:02
keywords:
description:
---
# 1.this指向
1. 函数预编译过程 this --> window;
2. 全局作用域里 this --> window;
3. call/apply 可以改变函数运行时this指向；
4. obj.fun(); fun()内部this指向obj

**预编译过程中AO还应包括arguments和this。**

# 2.arguments
# 2.1 arguments.callee
**ES5标准模式不可用**
执行时指代函数自己，比如立即执行函数中要用到递归的场景。
```
var num = (function(n){
    if(n === 1 ){
        return 1;
    }
    return n * arguments.callee(n-1);
})
```