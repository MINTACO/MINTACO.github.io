---
title: vue挂载流程，render函数
author: shawn
avatar: 'https://cdn.jsdelivr.net/gh/MINTACO/cdn@1.3/img/custom/avatar.jpg'
authorLink: mintaco.cn
authorAbout: 像风一样自由
authorDesc: 像风一样自由
categories: 技术
comments: true
tags: VUE
photos: https://i.loli.net/2019/12/14/j36bxu5srdUBtH7.png
date: 2019-11-13 20:21:34
keywords:
description:
---
# 1.Vue挂载流程图

![Vue挂载流程图](https://i.loli.net/2019/11/13/gWoyD9XxVtpZOza.png)

# 2.render函数
```
const vm = new Vue({
      el: '#app',
      // template: '<h2>{{ msg }}</h2>',
      //render的第一个参数一定是creatElement函数，写成其他名称也是
      render ( h ) {
        return h('h1', {
          //属性
          class: 'haha',
          style: {
            color: 'red',
            fontSize: '12px'
          }
        },[
          //子元素
          '我是一个h1标题',
          h('p', '我是一个p标签')
        ])

        // const tag = "div";
        // return (
        //   <tag 
        //     class="haha" 
        //     style={{color: 'red', fontSize: '12px'}}
        //     on-click={()=>{console.log('haha')}}
        //   >
        //     <p>哈哈</p>
        //   </tag>
        // )
       
        // return h(
        //   'h1',
        //   {
        //     class:'haha',
        //     style:{
        //       color:'blue',
        //       fontSize:'20px'
        //     }
        //   },'hello'
        // )
      },
})
```