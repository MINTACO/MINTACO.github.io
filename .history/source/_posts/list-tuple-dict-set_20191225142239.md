---
title: 'list,tuple,dict,set'
author: Darren
avatar: 'https://cdn.jsdelivr.net/gh/MINTACO/cdn@1.3/img/custom/avatar.jpg'
authorLink: mintaco.cn
authorAbout: 像风一样自由
authorDesc: 像风一样自由
categories: 开发
comments: true
tags: Python
photos: 'https://i.loli.net/2019/11/12/UmZdgG8HuJ1AMPb.jpg'
date: 2019-12-25 10:34:57
keywords:
description:
---
# list
有序集合，可随时添加和删除其中的元素，例：`name = ['Michael', 'Bob', 'Tracy']`
## 操作
1. 取值
通过索引访问元素,索引越界时，会抛出IndexError错误，最后一个元素的索引是len(classmates) - 1。  
例：`name[0] > 'Michael'`    
从后往前取还可用负数索引：  
例：`name[-1] > 'Tracy'` ，以此类推-2，-3 

