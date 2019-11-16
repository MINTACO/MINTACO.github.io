---
title: vue组件
author: shawn
avatar: 'https://cdn.jsdelivr.net/gh/MINTACO/cdn@1.3/img/custom/avatar.jpg'
authorLink: mintaco.cn
authorAbout: 像风一样自由
authorDesc: 像风一样自由
categories: 技术
comments: true
tags: VUE
photos: 'https://i.loli.net/2019/11/12/UmZdgG8HuJ1AMPb.jpg'
date: 2019-11-15 16:07:00
keywords:
description:
---
# 1.组件好处
方便复用，易于维护

## 2.组件定义
分为全局组件和局部组件，组件里的data必须写成函数形式，使每个组件的data有独立的作用域，否则复用时会出现干扰。  
命名采用大驼峰/小驼峰，用时可以为连字符。
**注意项**
 1. 组件在html中不能写成自闭合标签；
 2. 在html中不能使用大驼峰式，会被解析成小驼峰，以至于找不到组件，最好写成连字符形式。

```

  <div id="app">
    <hello-world></hello-world>

  </div>
  
  <script> 
  //全局组件
    // Vue.component('hello-world', {
      //组件里的数据要求写成函数
    //   data () {
    //     return {
    //       msg: 'hello world'
    //     }
    //   },
    //   template: `<div>{{ msg }}</div>`
    // })

    //局部组件
    const vm = new Vue({
      el: '#app',
      components: {
        helloWorld: {
          data () {
            return {
              msg: 'hello world'
            }
          },
          template: `<div>{{ msg }}</div>`
        }
      }
    }) 
  </script>
```