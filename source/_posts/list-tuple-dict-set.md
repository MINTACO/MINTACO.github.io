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
## list操作
1. 取值
通过索引访问元素,索引越界时，会抛出IndexError错误，最后一个元素的索引是len(classmates) - 1。  
例：`name[0] > 'Michael'`    
从后往前取还可用负数索引：  
例：`name[-1] > 'Tracy'` ，以此类推-2，-3 

2. 插入元素
`list.append(obj)` 追加元素到末尾
`list.insert(index,obj)` 插入到指定位置

3. 删除元素
`list.pop(i)` 删除索引为i的元素，省略i删除最后一个元素

4. 替换元素
`list[i] = obj` 直接赋值覆盖

# tuple
有序列表，和list很相似，区别是tuple一旦初始化就**不能修改**，没有append()，insert()这样的方法。   
例：`name = ('Michael', 'Bob', 'Tracy')`   
**因为tuple不可变，所以代码更安全。如果可能，能用tuple代替list就尽量用tuple。**
**
*当tuple的元素中有list时，list的元素是可变的，变得是list，不是tuple，tuple元素的指向永远不变***
## tuple操作
1. 定义
tuple时，在定义的时候，tuple的元素就必须被确定下来。
定义空tuple：`t = ()`  
定义只有一个元素的tuple：`t = (1,)`  **必须加逗号，否则会解析成数字1**
2. 取值
和list相同

# dict
Python内置了字典：dict的支持，dict全称dictionary，在其他语言中也称为map，使用键-值（key-value）存储，具有**极快的查找速度**。
例：`d = {'Michael': 95, 'Bob': 75, 'Tracy': 85}`

## dict操作
1. 取值,赋值
通过key取值赋值，例：`d['Bob'] > 75`
2. 判断key是否在dict中的方法
    1. key in dict   返回布尔值
    2. dict.get(key,自定义value(可省略))   存在返回对应的value，不存在返回None或者自定义的value
3. 删除key和对应的value
dict.pop(key)

**dict内部存放的顺序和key放入的顺序是没有关系的,dict的key必须是不可变对象**

# set
set和dict类似，也是一组key的集合，但不存储value。由于key不能重复，所以，在set中，**没有重复的key**。  
## set操作
1. 创建set
需要传入一个list  
`s = set([1, 2, 3])`=>`s > {1, 2, 3}`  
set也是无序的
2. 添加元素
`s.add(key)`  
可以重复提添加，但会被过滤掉
3. 删除元素
`s.remove(key)`
4. 交集，并集
set可以看成数学意义上的无序和无重复元素的集合，因此，两个set可以做数学意义上的交集、并集等操作：  
```
>>> s1 = set([1, 2, 3])
>>> s2 = set([2, 3, 4])
>>> s1 & s2
{2, 3}
>>> s1 | s2
{1, 2, 3, 4}
```

**set内部不能放可变对象，因为无法判断两个可变对象是否相等，即无法保证无重复元素**