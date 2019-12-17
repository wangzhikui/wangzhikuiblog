---
title: javascript重塑基础系列之-prototype属性
categories: javascript
tags: [javascript,重塑基础]
date: 2019-01-26
---

每个 JavaScript 构造函数都有一个 prototype 属性，用于设置所有实例对象需要共享的属性和方法。prototype 属性不能列举。JavaScript 仅支持通过 prototype 属性进行继承属性和方法。到了ES6以后引入了class，使其和其他后端面向对象语言一样如java，c++等。但是运行时机制还是通过模拟状类来实现，即:基于函数

```javascript
function Square(w,h){
  this.width = w
  this.height = h
}
Square.prototype.getArea =  function(){
  return this.width * this.height
}

var s1 = new Square(10,20)
var s2 = new Square(30,40)

console.log(s1.getArea())//200
console.log(s2.getArea())//1200
```

代码中，w 和 h 都是构造函数 Square 创建的对象实例，它们通过 prototype 继承了 getArea 方法。
