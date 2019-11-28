---
title: DOM
author: shawn
avatar: 'https://cdn.jsdelivr.net/gh/MINTACO/cdn@1.3/img/custom/avatar.jpg'
authorLink: mintaco.cn
authorAbout: 像风一样自由
authorDesc: 像风一样自由
categories: 技术
comments: true
tags: Javascript
photos: 'https://cdn.jsdelivr.net/gh/MINTACO/cdn@1.4/img/category/lab.png'
date: 2019-11-27 14:43:33
keywords:
description:
---
# 1.DOM:Document  Object  Model(文档对象模型) 
DOM（文档对象模型）是针对 HTML 和 XML 文档的一个 API（应用程序编程接口）。DOM 描
绘了一个层次化的节点树，允许开发人员添加、移除和修改页面的某一部分。DOM 脱胎于
Netscape 及微软公司创始的 DHTML（动态 HTML），但现在它已经成为表现和操作页面标记的真正的跨
平台、语言中立的方式。

***IE 中的所有 DOM 对象都是以 COM 对象的形式实现的。这意味着 IE 中的
DOM 对象与原生 JavaScript 对象的行为或活动特点并不一致。***

# 2.节点层次
## 2.1 Node类型
### 2.1.1 确定节点类型
DOM1 级定义了一个 Node 接口，该接口将由 DOM 中的所有节点类型实现。这个 Node 接口
JavaScript 中是作为 Node 类型实现的；除了 IE 之外，在其他所有浏览器中都可以访问到这个类型。
JavaScript 中的所有节点类型都继承自 Node 类型，因此所有节点类型都共享着相同的基本属性和方法。

每个节点都有一个 nodeType 属性，用于表明节点的类型。节点类型由在 Node 类型中定义的下列
12 个数值常量来表示，任何节点类型必居其一：

 Node.ELEMENT_NODE(1)；   
 Node.ATTRIBUTE_NODE(2)；   
 Node.TEXT_NODE(3)；   
 Node.CDATA_SECTION_NODE(4)；   
 Node.ENTITY_REFERENCE_NODE(5)；   
 Node.ENTITY_NODE(6)；   
 Node.PROCESSING_INSTRUCTION_NODE(7)；   
 Node.COMMENT_NODE(8)；    
 Node.DOCUMENT_NODE(9)；   
 Node.DOCUMENT_TYPE_NODE(10) 
 Node.DOCUMENT_FRAGMENT_NODE(11)
 Node.NOTATION_NODE(12)。

**nodeType确定节点类型**  
```someNode.nodeType```  
返回值：节点类型的数字值  
nodeName 节点名  
nodeValue 内容，对于元素节点，始终为null  

### 2.1.2 节点关系
1. 父子节点 ：上下两层节点之间的关系。   
   每个节点都有childNodes属性,其中保存着一个 NodeList 对象(类数组)，DOM 结构动态变动会直接反映在NodeList对象中，对应的其中的所有节点都有对应的唯一父节点parentNode。  
   1. 访问：
   ```
   var firstChild = someNode.childNodes[0]/firstChild;
   var lastChild = someNode.childNodes[someNode.childNodes.length-1]/lastChild;  
   var secondChild = someNode.childNodes.item(1); 
   var count = someNode.childNodes.length;
   ```
   2. 将NodeList转化为数组：
   ```
    function convertToArray(nodes){ 
       var array = null; 
       try { 
          array = Array.prototype.slice.call(nodes, 0); //针对非 IE 浏览器
        } catch (ex) { 
          array = new Array(); 
          for (var i=0, len=nodes.length; i < len; i++){ 
            array.push(nodes[i]); 
          } 
       } 
       return array; 
    }
   ```
   ***由于IE8 及更早版本将 NodeList
实现为一个 COM 对象，不能直接截取***  

   3. 判断是否有子节点
   ```hasChildNodes()```在节点包含一或多个子节点的情况下返回 true,比判断length更方便。




1. 同胞节点 ：包含在childNodes 列表中的每个节点相互之间都是同胞节点。  
   previousSibling和 nextSibling 属性


### 2.1.3 操作节点
父节点基础上的操作
1. ```appendChild( newNode )``` 
2. ```insertBefore( newNode,参照节点 )```
3. ```replaceChild( newNode,要替换的节点 )```  
   *以上对节点的操作均为剪切，而非复制*
4. ```removeChild( 要删除的节点 )```
   
所有节点公有方法
1. ```cloneNode( true/false )```   
   创建调用这个方法的节点的一个完全相同的副本,参数为 true的情况下，执行深复制，也就是复制节点及其整个子节点树；在参数为 false 的情况下，执行浅复制，即只复制节点本身。复制后返回的节点副本属于文档所有，但并没有为它指定父节点。因此，这个节点副本就成为了一个“孤儿”，除非通过 appendChild()、insertBefore()或 replaceChild()将它添加到文档中。  
例子：  
```
<ul> 
 <li>item 1</li> 
 <li>item 2</li> 
 <li>item 3</li> 
</ul>

var deepList = myList.cloneNode(true); 
alert(deepList.childNodes.length); //3（IE < 9）或 7（其他浏览器）
var shallowList = myList.cloneNode(false); 
alert(shallowList.childNodes.length); //0
```
***cloneNode()方法不会复制添加到 DOM 节点中的 JavaScript 属性，例如事件处
理程序等。这个方法只复制特性、（在明确指定的情况下也复制）子节点，其他一切
都不会复制。IE 在此存在一个 bug，即它会复制事件处理程序，所以我们建议在复制
之前最好先移除事件处理程序。***

2. ```normalize()```


