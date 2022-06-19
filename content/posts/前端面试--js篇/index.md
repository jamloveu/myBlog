---
title: "前端面试--js篇"
subtitle: ""
date: 2022-04-15T22:12:48+08:00
draft: false
author: "jam"
authorLink: ""
description: ""
keywords: ""
license: ""
comment: false
weight: 0

tags:
- draft
categories:
- draft

hiddenFromHomePage: false
hiddenFromSearch: false

summary: ""
resources:
- name: featured-image
  src: featured-image.jpg
- name: featured-image-preview
  src: featured-image-preview.jpg

toc:
  enable: true
math:
  enable: false
lightgallery: false
seo:
  images: []

# See details front matter: /theme-documentation-content/#front-matter
---

<!--more-->
## 1、JS数据类型有哪些？
### 基本概念
一共八种：数字、字符串、布尔、null、undefined、对象、symbol、bigint
```
number、string、Boolean、null、undefined、object、symbol、bigint
```

### 推展
- 表示一个对象为空用null，表示一个非对象为空，用undefiend
- symbol、bigint的新加的。
- 用bigint？js的number默认是一个双精度浮点数，位数是有限的。使用方法是数字后面加一个n，比如：12345678912345677n

```
输入-> 12345678912345677
输出<- 12345678912345676

输入-> 12345678912345677n
输出<- 12345678912345677n
```

- bigint只支持整数，不支持小数
- symbol日常开发几乎没有用，一般做库需要用到

- 提了就0分的答案：数组、函数、日期。这些是类，不是类型。


## 2、原型链是什么？
大概念题，答题思路为大概念化成小概念（分割），抽象化成具体（举例）。
我的答题思路如下：
哦，原型链涉及到的概念挺多的，我举例说明一下吧。
假设我们有一个普通对象 `x={}`，这个x会有一个隐藏属性，叫做`__?????__`，这个属性会指向`Object.prototype`，即
```
x.__?????__=== Object.prototype  //原型
```

此时，我们说 x 的原型 是 Object.prototype，或者说 Object.prototype 是 x 的原型。

而这个 __?????__ 属性的唯一作用就是用来指向 x 的原型的。

如果没有 __?????__ 属性，x 就不知道自己的原型是谁了。

为什么我用问号来表示？因为这样你不容易晕。

接下来我来说说原型链，我还是举例说明吧。

假设我们有一个数组对象 `a=[]` ，这个 a 也会有一个隐藏属性，叫做 `__?????__` ，这个属性会指向 `Array.prototype` ，即

```
a.__?????__ === Array.prototype
```

此时，我们说 a 的原型是 `Array.prototype`，跟上面的 x 一样。但又有一点不一样，那就是 `Array.prototype` 也有一个隐藏属性 `__?????__ `，指向 `Object.prototype` ，即

```
// 用 x 表示 Array.prototype
x.__?????__ === Object.prototype
```

这样一来，a 就有两层原型：

1. a 的原型是 Array.prototype 
2. a 的原型的原型是 Object.prototype 
于是就通过隐藏属性 __?????__ 形成了一个链条：
```
a ===> Array.prototype ===> Object.prototype 
```
这就是原型链。

### 如何去修改原型链的？

看起来只要改写 x 的隐藏属性 __?????__ 就可以改变 x 的原型（链）
```
x.__?????__ = 原型
```
但是这不是标准推荐的写法，为了设置 `x.__?????___`，推荐的写法是

```
const x = Object.create(原型)
// 或
const x = new 构造函数() // 会导致 x.__?????__ === 构造函数.prototype
```

### 解决了什么问题?
在没有 Class 的情况下实现「继承」。以 `a ===> Array.prototype ===> Object.prototype`  为例，我们说：
1. a 是 Array 的实例，a 拥有 Array.prototype 里的属性
2. Array 继承了 Object（注意专业术语的使用）
3. a 是 Object 的间接实例，a 拥有 Object.prototype 里的属性

这样一来，a 就既拥有 Array.prototype 里的属性，又拥有 Object.prototype 里的属性。

优点：

简单、优雅。

缺点：

跟 class 相比，不支持私有属性。

怎么解决缺点：

使用 class 呗。但 class 是 ES6 引入的，不被旧 IE 浏览器支持。

推荐阅读：https://www.zhihu.com/question/56770432/answer/315342130

