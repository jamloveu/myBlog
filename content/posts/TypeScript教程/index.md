---
title: "TypeScript教程"
subtitle: ""
date: 2022-04-18T21:54:53+08:00
draft: false
author: "Jam"
authorLink: ""
description: ""
keywords: ""
license: ""
comment: false
weight: 0

tags:
- TypeScript
categories:
- TypeScript

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

## 一、基本类型
### 类型声明
- 类型声明是TS非常重要的一个特点
- 通过类型声明可以指定TS变量（参数、形参）的类型
- 指定类型后，当为变量赋值时，TS编辑器会自动检查值是否符合类型声明，符合则赋值，否则报错
- 简而言之，类型声明给变量设置了类型，使得变量只能储存某种类型的值
- 语法：
```
let 变量:类型

let 变量：类型 = 值

function fn(参数:类型, 参数:类型):类型{

}

// 注意：最后面的类型是函数返回值的类型。

```
### 自动类型判断
- TS拥有自动的类型判断机制
- 当对变量的声明和赋值是同时进行的，可以省略掉类型声明
- 类型：


| 类型 | 例子 | 描述 |
| :------------ | :---------- | :------------ |
| number | 1，-2，2.5  | 任意数字|
| string | 'hi' | 任意字符串 |
| boolead | true，false | 布尔值true或者false |
| 字面量 | 其本身 | 限制变量的值就是该字面量的值 |
| any | * | 任意类型 |
| unknown | * | 类型安全的any |
| void | 空值（undefiend） | 没有值（或者undefined） |
| never | 没有值 | 不能是任何值（用的少） |

- 可以使用 | 来连接多个类型
- any 表示的任意类型，一个变量设置类型为any后相当于对该变量关闭了TS的类型检测，使用TS中，不建议使用any类型
- 声明变量如果不指定类型，则TS解析器会自动判断变量的类型为any（隐式的bug）
- 类型是any，它可以赋值给任意变量（可以污染其他的变量的类型），但是unknown不会
- unknown 实际上就是一个类型安全的any，unknown类型的变量，不能直接赋值给其他变量，需要检查：
```
let e:unknown;
e = 10
e = 'hello'
e = true

let s:strinmg

//如果赋值需要这样：
if(typeof e ==='string'){
  s = e
}

// 或者用类型断言
s = e as string
s = <string>e

/*
*
* 语法：
* 1. 变量 as 类型
* 2. <类型>变量
*
*/
```
- void 用来表示为空，以函数为例，就表示没有返回值的函数



