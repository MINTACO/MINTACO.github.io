---
title: filter
author: shawn
avatar: 'https://cdn.jsdelivr.net/gh/MINTACO/cdn@1.3/img/custom/avatar.jpg'
authorLink: mintaco.cn
authorAbout: 像风一样自由
authorDesc: 像风一样自由
categories: 技术
comments: true
tags: VUE
photos: https://i.loli.net/2019/12/14/j36bxu5srdUBtH7.png
date: 2019-11-15 15:15:22
keywords:
description:
---
# vue过滤器
在不改变原有数据的情况下改变要显示内容。

```
<div id="app">
    {{ money | toMoney(a) | test }}
    
</div>

<script>
//filter全局，第一个参数value一定是管道符之前的值，这里就是money
  Vue.filter('toMoney', (value, times) => {
      return (value * times).toLocaleString();
    });

    //这里的value是10000
  Vue.filter('test', value => {
      console.log(value);
      return value;
    })

  var vm = new Vue({
    el: '#app',
    data: {
      a: 10,
      money: 1000
    },
   
   
  })
</script> 
```