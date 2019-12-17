---
title: javascript重塑基础系列之-变量提升
categories: javascript
tags: [javascript,重塑基础]
date: 2019-01-28
---

JavaScript 会将所有变量和函数声明移动到它的作用域的最前面，这就是所谓的变量提升 (Hoisting)  

。也就是说，无论你在什么地方声明变量和函数，解释器都会将它们移动到作用域的最前面。因此我们可以先使用变量和函数，而后声明它们。
但是，仅仅是变量声明被提升了，而变量赋值不会被提升。如果你不明白这一点，有时则会出错：

```javascript
console.log(x)//undefined
x = 2//初始化x
```
所谓模块化，就是根据需要控制模块内属性与方法的可访问性，即私有或者公开。

在代码中，

module 为一个独立的模块

name 为其私有属性

work 为其私有方法

age 为其公有属性

say 为共有方法