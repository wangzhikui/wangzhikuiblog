---
title: javascript重塑基础系列之-柯里化
categories: javascript
tags: [javascript,重塑基础]
date: 2019-01-29
---
柯里化，即 Currying ，可以是函数变得更加灵活。我们可以一次性传入多个参数调用它；也可以只传入一部分参数来调用它，让它返回一个函数去处理剩下的参数。

```javascript
var add = function(x){
  return function(y){
    return x + y
  }
}

console.log(add(1)(2))//3

var add1 = add(1)
console.log(add1(1))//2
```
代码中，我们可以一次性传入 1 个 2 作为参数 add(1)(2) ，也可以传入 1 个参数之后获取 add1 函数，这样使用起来非常灵活。