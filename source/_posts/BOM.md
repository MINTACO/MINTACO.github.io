---
title: BOM
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
## 1.1全局作用域