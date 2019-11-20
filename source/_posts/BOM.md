---
title: BOM(Browser Object Model 浏览器对象模型)
author: shawn
avatar: 'https://cdn.jsdelivr.net/gh/MINTACO/cdn@1.3/img/custom/avatar.jpg'
authorLink: mintaco.cn
authorAbout: 像风一样自由
authorDesc: 像风一样自由
categories: 技术
comments: true
tags: Javascript
photos: 'https://cdn.jsdelivr.net/gh/MINTACO/cdn@1.4/img/cover/code2.jpg'
date: 2019-11-17 16:34:06
keywords:
description:
---
&emsp;&emsp;ECMAScript 是 JavaScript 的核心，但如果要在 Web 中使用 JavaScript，那么 BOM（浏览器对象模
型）则无疑才是真正的核心。BOM 提供了很多对象，用于访问浏览器的功能，这些功能与任
何网页内容无关。多年来，缺少事实上的规范导致 BOM 既有意思又有问题，因为浏览器提供商会按照各
自的想法随意去扩展它。于是，浏览器之间共有的对象就成为了事实上的标准。这些对象在浏览器中得以
存在，很大程度上是由于它们提供了与浏览器的互操作性。W3C 为了把浏览器中 JavaScript 最基本的部分
标准化，已经将 BOM 的主要方面纳入了 HTML5 的规范中。

# 1.window对象
&emsp;&emsp;BOM 的核心对象是 window，它表示浏览器的一个实例。在浏览器中，window 对象有双重角色，
它既是通过 JavaScript 访问浏览器窗口的一个接口，又是 ECMAScript 规定的 Global 对象。这意味着
在网页中定义的任何一个对象、变量和函数，都以 window 作为其 Global 对象，因此有权访问
parseInt()等方法。
## 1.1 全局作用域
有在全局作用域中声明的变量、函数都会变成 window 对象的属性和方法。但定义全局变量与在 window 对象上直接定义属性还是有一点差别：
1. 全局变量不能通过 delete 操作符删除，而直接在 window 对象上的定义的属性可以。
```
var age = 29;
window.color = "red";
//在 IE < 9 时抛出错误，在其他所有浏览器中都返回 false
delete window.age;
//在 IE < 9 时抛出错误，在其他所有浏览器中都返回 true
delete window.color; //returns true
alert(window.age); //29
alert(window.color); //undefined
```
2. 直接访问未定义的变量会抛出错误，但是访问未定义的window属性则不会，会返回undefined。可以知道某个可能未声明的变量是否存在。
## 1.2 导航和打开窗口
**函数**：window.open(URL,窗口目标，特性字符串，是否打开新页面标志)；  
四个参数中，一般只需要传URL，最后一个参数传_self时新窗口覆盖当前窗口，默认为打开新窗口。  
特性表：  
![](https://i.loli.net/2019/11/19/xvFCBrUjIfqQHDL.png)
表中所列的部分或全部设置选项，都可以通过逗号分隔的名值对列表来指定。其中，名值对以等号
表示（注意，整个特性字符串中不允许出现空格），如下面的例子所示。
```
window.open("http://www.baidu.com","wroxWindow",
"height=400,width=400,top=10,left=10,resizable=yes");
```
**返回值**：新打开窗口的window对象
**opener属性**：新打开的窗口都有一个opener属性，保存着打开它的原始窗口的window对象。但原始窗口中并没有这样的指针指向弹出窗口。可指定opener为null；
**opener.close()**：可以关闭本窗口中通过js打开的窗口；
不同浏览器使用close()方法的策略不同：
 1. ff : 无法关闭
 2. chrome : 直接关闭
 3. ie : 询问用户
```
<button>open</button>
<button>close</button>

<script>
  var oBtn = document.getElementsByTagName('button')[0];
  var oBtn1 = document.getElementsByTagName('button')[1];
  var wroxWin; 
  oBtn.onclick = function(){
    wroxWin = window.open("http://www.baidu.com/","wroxWindow",
        "height=400,width=400,top=10,left=10,resizable=yes");
    // wroxWin.opener = null;
    console.log(wroxWin);
  };
  oBtn1.onclick = function(){
    wroxWin.close();
  }
</script> 
```

