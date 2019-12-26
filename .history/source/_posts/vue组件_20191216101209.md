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
photos: https://i.loli.net/2019/12/14/j36bxu5srdUBtH7.png
date: 2019-11-15 16:07:00
keywords:
description:
---
# 1.组件好处
方便复用，易于维护

# 2.组件定义
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
# 3.组件间数据传递
## 3.1 父传子
### 3.1.1 通过prop向子组件传递数据
Prop 是在组件上注册的一些自定义特性。当一个值传递给一个 prop 特性的时候，它就变成了那个组件实例的一个属性。
```
Vue.component('blog-post', {
  props: ['title'],
  template: '<h3>{{ title }}</h3>'
})
```
一个组件默认可以拥有任意数量的 prop，任何值都可以传递给任何 prop。在上述模板中，你会发现我们能够在组件实例中访问这个值，就像访问 data 中的值一样。  

**prop类型**
1. 字符串数组，如:```props: ['title', 'likes', 'isPublished', 'commentIds', 'author']```
2. 对象，在每个prop的值都需要特定类型时，对象的名称和值分别是 prop 各自的名称和类型匹配要求，如:  
```
props: {
   // 基础的类型检查 (`null` 和 `undefined` 会通过任何类型验证)
    propA: Number,
    // 多个可能的类型
    propB: [String, Number],
    // 必填的字符串
    propC: {
      type: String,
      required: true
    },
    // 带有默认值的数字
    propD: {
      type: Number,
      default: 100
    },
    // 带有默认值的对象
    propE: {
      type: Object,
      // 对象或数组默认值必须从一个工厂函数获取
      default: function () {
        return { message: 'hello' }
      }
    },
    // 自定义验证函数
    propF: {
      validator: function (value) {
        // 这个值必须匹配下列字符串中的一个
        return ['success', 'warning', 'danger'].indexOf(value) !== -1
      }
    }
    // prop 会在一个组件实例创建之前进行验证，所以实例的属性 (如 data、computed 等) 在 default 或 validator 函数中是不可用的。
}
```
当 prop 验证失败的时候，(开发环境构建版本的) Vue 将会产生一个控制台的警告。

**单向数据流**
所有的 prop 都使得其父子 prop 之间形成了一个单向下行绑定：父级 prop 的更新会向下流动到子组件中，但是反过来则不行。这样会防止从子组件意外改变父级组件的状态，从而导致应用的数据流向难以理解。  

两种常见的试图改变一个 prop 的情形：
1. 这个 prop 用来传递一个初始值；最好定义一个本地的 data 属性并将这个 prop 用作其初始值：
```
props: ['initialCounter'],
data: function () {
  return {
    counter: this.initialCounter
  }
}
```
2. 这个 prop 以一种原始的值传入且需要进行转换。在这种情况下，最好使用这个 prop 的值来定义一个计算属性：
```
props: ['size'],
computed: {
  normalizedSize: function () {
    return this.size.trim().toLowerCase()
  }
}
```
***注意在 JavaScript 中对象和数组是通过引用传入的，所以对于一个数组或对象类型的 prop 来说，在子组件中改变这个对象或数组本身将会影响到父组件的状态。***

### 3.1.2 vm.$attrs配合inheritAttrs:false
$attrs包含未注册的属性,inheritAttrs:false 使没有被注册的属性也不会显示在行间
```
 <div id="app">
        <my-content :title="title" :content="content" :index="index"> </my-content>
    </div>

    <script>
        const vm = new Vue({
            el:'#app',
            data:{
                title:"标题",
                content:'我是内容',
                index:20
            },
            components:{
                myContent:{
                    props:['title'],
                    inheritAttrs:false,
                    created(){
                        console.log(this.$attrs)
                    },
                    template:`<div>
                            <h2>{{title}}</h2>
                            <my-p v-bind="$attrs"></my-p>
                        </div>`,
                    components:{
                        myP:{
                            created(){
                                console.log(this.$attrs)
                            },
                            props:['content'],
                            template:`<p>{{content}}</p>`

                        }
                    }

                }    
            }
        })
    </script>
```
输出：
![](https://i.loli.net/2019/11/18/a4vZofGnrjhkRJN.png)
![](https://i.loli.net/2019/11/18/LMBoq8gRmO3VCi5.png)

### 3.1.3 vm.$parent/vm.$children
```
<div id="app">
        <my-content> </my-content>
    </div>

    <script>
        const vm = new Vue({
            el:'#app',
            data:{
                title:"标题",
                content:'我是内容',
                index:20
            },
            components:{
                myContent:{
                    created(){
                        console.log(this.$parent);
                        //父级vue实例
                        this.title = this.$parent.title;
                        // this.content = this.$parent.content;
                    },
                    mounted(){
                        console.log(this.$children);
                        // 数组，包含子组件实例
                    },
                    template:`<div>
                            <h2>{{title}}</h2>
                            <my-p ></my-p>
                        </div>`,
                    components:{
                        myP:{
                            created(){
                                console.log(this.$parent);
                                this.content = this.$parent.$parent.content;
                            },
                            template:`<p>{{content}}</p>`
                        }
                    }
                }   
            }
        })
    </script>
```
输出：
![](https://i.loli.net/2019/11/18/S8IDGJ7UdTsKbVP.png)
![](https://i.loli.net/2019/11/18/4ZlAVbN8oXswK7P.png)

### 3.1.4 provide-inject
```
    <div id="app">
            <my-content> </my-content>
    </div>

    <script>
        const vm = new Vue({
            el:'#app',
            provide:{
                title:"标题",
                content:'我是内容',
                index:20
            },
            components:{
                myContent:{
                    inject:['title'],
                    template:`<div>
                            <h2>{{title}}</h2>
                            <my-p ></my-p>
                        </div>`,
                    components:{
                        myP:{
                            inject:['content'],
                            template:`<p>{{content}}</p>`

                        }
                    }
                }
            }
        })
    </script>
```
## 3.2 子传父
### 3.2.1 通过引用 ref
引用 ref 可以用在Dom上/组件上 ，通过this.$refs可以获取dom或者组件实例。  
不能赋值名字相同的ref，后面的会覆盖前者，除非是v-for生成的循环，例子：```<div ref="dom" v-for="item in 5">hi</div>```,此时this.$refs.dom会输出数组[div,div,div,div,div]。  
在父组件中通过this.$refs.子组件可以获取子组件的实例，进而获取子组件的数据和方法。
### 3.2.2 通过函数传值，$emit/$listeners
$emit主动触发绑定的事件,第一个参数为事件名，第二个参数为要传递的参数
```
	<div id="app">
        <my-cmp @click="func"></my-cmp>
    </div>
    <script>
        const vm = new Vue({
            el:"#app",
            methods:{
                func(data){
                    console.log(data);
                }
            },
            components:{
                myCmp:{
                    template:`<div>
                                <button @click="handleClick">点击</button>                         
                            </div>`,
                    methods:{
                        handleClick(){
                            this.$emit('click',this.msg);
                        }
                    },
                    data(){
                        return {
                            msg:"hello world"
                        }
                    }
                }
            }
        })
    </script>
```
$listeners,通过v-on=“$listeners”获得组件上所有通过@绑定的事件，但是不能传参
```
	<div id="app">
        <my-cmp @click="func" @mousedown="func1"></my-cmp>
    </div>
    <script>
        const vm = new Vue({
            el:"#app",
            methods:{
                func(data){
                    console.log(data);
                },
                func1(){
                    console.log('func1');
                }
            },
            components:{
                myCmp:{
                    template:`<div>
                                <button v-on="$listeners">click</button>
                            </div>`,
                }
            }
        })
    </script>
```
## 3.3 兄弟组件传值
### 3.3.1 事件总线event bus
```
<div id="app">
    <my-input></my-input>
    <hr />
    <my-content></my-content>
  </div>
  
  <script> 
    // event bus 事件总线
    // vue 实例 一个兄弟组件触发的同时另一个监听
    Vue.prototype.bus = new Vue();

    const vm = new Vue({
      el: '#app',
      components: {
        myContent: {
          data () {
            return {
              content: ''
            }
          },
          created () {
            this.bus.$on('click', content => {
              this.content = content;
            })
          },
          template: `<div>{{ content }}</div>`
        },

        myInput: {
          data () {
            return {
              inputVal: ''
            }
          },
          methods: {
            handleClick () {
              console.log(this.inputVal);
              this.bus.$emit('click', this.inputVal);
            }
          },
          template: `<div>
                      <input type="text" v-model="inputVal"/>
                      <button @click="handleClick">提交</button>
                    </div>`
        }
      }
    })
  </script> 
```
