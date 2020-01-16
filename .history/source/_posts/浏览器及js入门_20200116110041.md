---
title: 浏览器及js入门
author: Darren
avatar: 'https://cdn.jsdelivr.net/gh/MINTACO/cdn@1.3/img/custom/avatar.jpg'
authorLink: mintaco.cn
authorAbout: 像风一样自由
authorDesc: 像风一样自由
categories: 开发
comments: true
tags: Javascript
photos: 'https://i.loli.net/2019/12/14/9FaBYsRX1DJcCTH.png'
date: 2020-01-15 10:42:57
keywords:
description:
---
# 1.浏览器发展
Mosaic,1993年问世，是互联网第一个**普遍使用**的能显示图片的**网页浏览器**。1994年4月，马克安德森和吉姆克拉克在加州创立Mosaic Communication Corporation。由于Mosaic商标权被伊利诺伊大学持有，且伊利诺伊大学将技术转让给了Spy Glass公司，开发团队只能重写浏览器代码，并将浏览器名称更名为Netscape Navigator,公司也于1994年11月更名为Netscape Communication Corporation,译为“网景”。IE即微软买下Spy Glass的技术发展而来，Mozilla Firefox则是网景开放源代码后的衍生版本。   

Javascript作为Netscape Navigator的一部分首次出现在1996年，起初叫livescript，为了推广与Sun公司合作改名Javascript，Sun公司后来被Oracle收购，Javascript版权归Oracle所有。

# 2.浏览器组成
1. shell
   用户操作的部分
2. 内核
   内部代码，用户看不见的地方   
   内核又分为：1.渲染引擎（语法规则和渲染，绘制页面） 2.js引擎 3.其他模块    
   各大主流浏览器内核：1.IE-->trident; 2.Chrome-->blink; 3.firefox-->Gecko; 4.Opera-->presto; 5.Safari-->webkit


   * js引擎发展：2001年IE6首次实现js引擎分离；2008年chrome问世，搭载V8引擎，可以直接将js转化成机械码，速度极快；后Firefox也推出自己的渲染引擎

# 3.js特点
1. 解释型语言
2. 单线程
3. 轮转时间片：js会把多个任务中的每个任务切成无数个片段，塞到任务队列中，顺序完全随机，将队列往js引擎中送



