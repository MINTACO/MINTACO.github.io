---
title: vue插值表达式
author: shawn
avatar: 'https://cdn.jsdelivr.net/gh/MINTACO/cdn@1.3/img/custom/avatar.jpg'
authorLink: mintaco.cn
authorAbout: 像风一样自由
authorDesc: 像风一样自由
categories: 技术
comments: true
tags: VUE
photos: 'https://i.loli.net/2019/11/12/UmZdgG8HuJ1AMPb.jpg'
date: 2019-11-12 09:01:59
keywords:
description:
---

## 简介
Vue.js 使用了基于 HTML 的模板语法，允许开发者声明式地将 DOM 绑定至底层 Vue 实例的数据。  
在底层的实现上，Vue 将模板编译成虚拟 DOM 渲染函数。结合响应系统，Vue 能够智能地计算出最少需要重新渲染多少组件，并把 DOM 操作次数减到最少。  
数据绑定最常见的形式就是使用“Mustache”语法 (双大括号) 的文本插值，即插值表达式。

## 用法
1.插值表达式中使用的数据必须先在data中存在，才能实现数据绑定；  
2.支持js**表达式**,但不支持~~语句~~及~~流控制~~，可用**三目表达式**；    
2.要更改的数据必须先存在，视图才会刷新；  
3.通过索引或者长度的方式改变数组，视图不会刷新，必须使用数组的变异方法，如push、pop、shift、unshift、sort、reverse、splice；  
4.$set可用来更改对象的值，例：```vm.$set(vm.obj, 'xxx', 90);```;也可以更改其他元素，大多用来更改对象。

```
 <div id="app">
    {{ 'a' }}<br/>
    {{ 1 }}<br/>
    {{ true }}<br/>
    {{ [1, 2, 3] }}<br/>
    {{ {a: 1, b: 10} }}<br/>
    {{ 1+1 }}<br/>
    {{ 1-1 }}<br/>
    {{ 'a' + 'b' }}<br/>

    <!-- {{ var a = 10; return a; }} 语句不支持<br/>
    {{ if(true) { return 'a'} }} 流控制不支持，可用三元表达式<br/> -->

    {{ !true ? 'a' : 'b' }}<br/>
    {{ name }}<br/>
    {{ desc }}<br/>
    {{ arr[0] }}<br/>
    {{ obj["b"] }}<br/>
  </div>
  <script>
    const vm = new Vue({
      el:"#app",
      data:{
        name: 'ls',
        desc: 'coder',
        arr: [1, 2, 3],
        obj: {
          a: 1, b: 10
        }
      }
    })
    // vm.$mount('#app');另一种挂载方法
    // $el 返回vue作用的DOM元素
</script>
```