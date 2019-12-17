---
title: javascript重塑基础系列之-模块化
categories: javascript
tags: [javascript,重塑基础]
date: 2019-01-27
---

JavaScript 并非模块化编程语言，至少 ES6 落地之前都不是。然而对于一个复杂的 Web 应用，模块化编程是一个最基本的要求。这时，可以使用**立即执行函数** 来实现模块化。

正如很多 JS 库比如 jQuery 以及我们 Fundebug 都是这样实现的

```javascript
var module = (function(){
  var name = "allen";
  function work(){
    console.log("working")
  }
  function say(){
    console.log("hello world Im allen")
  }
  return {
    age: 100,
    say: say
  }
})()
console.log(module.age)//100
console.log(module.say())//hello world Im allen
```
所谓模块化，就是根据需要控制模块内属性与方法的可访问性，即私有或者公开。

在代码中，

module 为一个独立的模块

name 为其私有属性

work 为其私有方法

age 为其公有属性

say 为共有方法