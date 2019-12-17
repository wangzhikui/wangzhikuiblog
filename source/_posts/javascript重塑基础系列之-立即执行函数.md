---
title: javascript重塑基础系列之-立即执行函数
categories: javascript
tags: [javascript,重塑基础]
date: 2019-01-25
---

**立即执行函数**：Immediately Invoked Function Expression (IIFE)，创建函数的同时立即执行。
```javascript
(function(){
  console.log("hello world")
})();
```
function(){…}  是一个匿名函数，包围它的一对括号将其转换为一个表达式，紧跟其后的一对括号调用了这个函数。立即执行函数也可以理解为立即调用一个匿名函数。

立即执行函数最常见的应用场景就是：将 var 变量的作用域限制于函数内，这样可以避免命名冲突。