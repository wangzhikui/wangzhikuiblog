---
title: javascript重塑基础系列之-闭包
categories: javascript
tags: [javascript,重塑基础]
date: 2019-01-25
---

# <font color="green" >闭包</font>
**闭包(closure)**：当外部函数返回之后，内部函数依然可以访问外部函数的变量。
```javascript
function f1(){
  var a = 1; //a是f1的局部变量
  function f2(){//f2是函数f1的内部函数，是闭包
    a = a+1;//内部函数使用了f1中的变量a
    console.log(a);
  }
  return f2;
}
var test = f1();
test();//2
test();//3
```
代码中，外部函数 f1 只执行了一次，变量 a 设为 1 ，并将内部函数 f2 赋值给了变量 test 。由于外部函数 f1 已经执行完毕，其内部变量 a 应该在内存中被清除，然而事实并不是这样：我们每次调用 test 的时候，发现变量 a 一直在内存中，并且在累加。这就是闭包的神奇之处了！

# <font color="green" >使用闭包定义私有变量</font>

```javascript
function people(){
  var name;
  function getName(){
    return name;
  }
  function setName(value){
    name = value;
  }
}
var person = new people();
person.setName("张三");

console.log(person.name);//undefined
console.log(person.getName());//张三
```

代码中，对象 person 的的 name 属性为私有属性，使用 person.name 不能直接访问。