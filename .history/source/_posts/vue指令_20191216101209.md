---
title: vue指令
author: shawn
avatar: 'https://cdn.jsdelivr.net/gh/MINTACO/cdn@1.3/img/custom/avatar.jpg'
authorLink: mintaco.cn
authorAbout: 像风一样自由
authorDesc: 像风一样自由
categories: 技术
comments: true
tags: VUE
photos: https://i.loli.net/2019/12/14/j36bxu5srdUBtH7.png
date: 2019-11-12 08:58:37
keywords:
description:
---
1. v-pre 跳过该元素和它的子元素的变异过程，显示原始的{ { } }的标签
2. v-cloak 该指令保持在元素上，直到关联实例结束变异 可与css配合使用隐藏未编译的{ { } }标签
3. v-once 只渲染元素和组件一次。随后的重新渲染，元素/组件及其所有的子节点将被视为静态内容并跳过。这可以用于优化更新性能。vue内部进行了缓存，以后使用的值都是缓存里的结果
4. v-html === innerHTML  XSS  更新元素的innerHTML
5. v-text === innerText 更新元素的innerText，不常用，一般直接使用{ { } }
6. v-if 控制元素是否存在  判断多个相同状态的用<template>标签包裹
7. v-else --  配合v-if，两者必须相邻
8. v-else-if 同理
9. v-show  控制元素的dispaly样式

 ***v-show和v-if的区别？***
    1. v-if是控制该元素是否存在，值为false时，完全移除该元素
      v-show是控制该元素的样式(display)，值为false时，元素的display为none
    2. v-if支持template标签
      v-show不支持template标签

10. v-bind<=>： 绑定属性，当绑定class，style时有两种方式，绑定多个属性可用[],需条件判断可用{}
11. v-on<=>@ 监听事件
    ***this指向***
    1. methods里的函数this指向vue实例
    2. 函数不可写在data里，this指向window
    
***组件无法识别点击事件，可以加修饰符native让组件拥有原生属性,例子：***```<my-cmp ref="cmp" @click.native="func"> </my-cmp>```

```
  <div id="app"> 
    <div v-once>
      {{a}}
    </div>
    <div v-html="dom"></div>
    <template v-if="flag">
      <div>123</div>
      <div>456</div>
    </template>
    <div v-if="count === 1">hello</div>
    <div v-else-if="count === 2">hi</div>
    <div v-else>world</div>
    <div v-show="true">v-show</div>

    <img :src="imgUrl" alt="" class="red" :class="{ red : flag}" />
    <div style="width: 500px; height: 500px;" :style="[divStyle, divStyle1]">i am a  div</div>
    <button @click="fn1(1)">click</button>
  </div>
  
  <script>
    const vm = new Vue({
      el: '#app',
      data:{
        a:1,
        dom:'<div>ls</div>',
        flag:true,
        count: 3，
        imgUrl：'https://i.loli.net/2019/11/12/UmZdgG8HuJ1AMPb.jpg',
        divStyle: {width: '100px', height: '100px', backgroundColor: 'red'},
        divStyle1: { color: '#fff'},
        //属性名和函数名不能重复
      },
      methods: {
        fn1(a){
            console.log(a);
        }
      }
    })
  </script> 
```
12. v-for 循环

```
<div id="app">
        <!-- 遍历数组，需要添加唯一key值，最好不用index -->
        <button @click = "onclick">Click</button>
        <div v-for="item in nameArr" :key="item.id">{{item.name}}</div>
        <br>
        <br>
        <!-- 遍历对象，(value,key) -->
        <div v-for="(value,key) in person" >{{key}} : {{value}}</div>
        <br>
        <!-- 遍历数字 -->
        <!-- <div v-for="item in 10">{{item}}</div> -->
        <br>
        <!-- 遍历字符串 -->
        <!-- <div v-for="item in 'lushuo'">{{item}}</div> -->

        <!-- 渲染多个循环，用<template>包裹，但是<template>不能绑定key值，要绑在内部元素，且每个不能相同 -->
        <template v-for="(item,index) in arr">
            <div :_key="`${index}_1`" :key="`${index}_1`">{{index}}</div>
            <span :_key="`${index}_2`" :key="`${index}_2`">{{item}}</span>
        </template>
        <br>
        <br>

        <!-- key值的另一作用：在dom元素相同时，进行区分。如例子中input为相同dom，vue默认会进行复用，导致填的内容不会随着功能切换而改变，加key值解决 -->
        <div v-if="flag">
            <label for="name">姓名</label>
            <input type="text" id="name" key="name">
        </div>
        <div v-else>
            <label for="age">年龄</label>
            <input type="text" id="age" key="age">
        </div>
        <button @click="change">互换</button>

    </div>
    <script>
        const vm = new Vue({
            el:'#app',
            data:{
                arr:[1,2,3],
                //nameArr:['ls','dh','bb']
                //后台返回的数据，一般都有一个id对应
                nameArr:[
                    {
                        name:'ls',
                        id:201901
                    },
                    {
                        name:'dh',
                        id:201902
                    },
                    {
                        name:'bb',
                        id:201903
                    }
                ],
                person:{
                    name:'ls',
                    desc:'boy',
                    age:23
                },
                flag:true

            },
            methods:{
                onclick(){
                    this.nameArr.reverse();
                },
                change(){
                    this.flag =  !this.flag;
                }
            }

        })
    </script>
```

13.  v-model 数据双向绑定，value+input语法糖
    ***修饰符***
    1. v-model.lazy变成value与change事件得语法糖
    2. v-model.number将输入得数字字符串转成数字
    3. v-model.trim去掉字符串前后空格

```
  <div id="app">
    <input type="text" v-model="content[0]"><br>
    <textarea v-model="content1"></textarea><br>
    {{ content1}}

    <br>
    <!-- <input type="checkbox" v-model="checked1" />
    {{ checked1 }} -->
    <br>
    <label for="cg">1</label>
    <input type="checkbox" v-model="checked" id="cg" value="cgg" />
    <label for="dg">2</label>
    <input type="checkbox" v-model="checked" id="dg" value="dgg" />
    <label for="stg">3</label>
    <input type="checkbox" v-model="checked" id="stg" value="stgg" />
    <br>
    {{ checked }} 
    <!-- 多选存的value值  -->

      <br>
      <br>
      
    <label for="one">one</label>
    <input type="radio" id="one"  value="one" v-model="picked"/>
    <label for="two">two</label>
    <input type="radio" id="two"  value="two" v-model="picked" />
      {{ picked }}

      <br><br>

    <select v-model="selected">
      <option value="" disabled>请选择</option>
      <option value="A">A</option>
      <option value="B">B</option>
      <option value="C">C</option>
    </select>
    {{ selected }}
    <br>
    <br>
    <select v-model="selected" multiple>
      <option value="A">A</option>
      <option value="B">B</option>
      <option value="C">C</option>
    </select>
    {{ selected }}
    
  </div>

  <script>
    const vm = new Vue({
      el: '#app',
      data: {
        content: ['hello','',''],
        content1:[],
        // checked: true
        checked: [],
        checked1: [],
        picked: '',
        //selected: ''
        selected: [],
        show: [false,true],
        
      },
      mathods:{
        
      }
    })
  </script>
```
