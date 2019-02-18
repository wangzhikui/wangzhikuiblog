---
title: javascript重塑基础系列之-拆箱&装箱
categories: javascript
tags: [javascript,重塑基础]
date: 2019-01-24
---
# 目录
- [概述](#概述)
- [装箱](#装箱)
- [拆箱](#拆箱)
- [总结](#总结)

# <font color="green" >概述</font>
**装箱：**把基本数据类型转换为对应的引用类型的操作

**拆箱：**把引用类型转换为基本的数据类型

# <font color="green" >装箱</font>

> 每当读取一个基本类型的时候，后台就会创建一个对应的基本包装类型对象，从而让我们能够调用一些方法来操作这些数据

```javascript
var str1 = "hello world";
var str2 = str1.substring(7);
````

如上示例，str1是一个基本类型，js内部为我们做了装箱处理，使得它能使用方法.类似如下方式:

```javascript
var str1 = new String("hello world");
var str2 = str1.substring(7);
str1 = null;
```
* 创建 String 类型的实例
* 调用实例方法
* 销毁实例

# <font color="green" >拆箱</font>
> 将引用类型对象转换为对应的值类型对象，它是通过引用类型的valueOf()或者toString()方法来实现的。如果是自定义的对象，你也可以自定义它的valueOf()/tostring()方法，实现对这个对象的拆箱

```javascript
//定义两个对象
var num = new Number(1314);  
var str =new String("1314");  

console.log(num) //1314
console.log(str) //"1314"

```
如上会自动调用valueOf()和toString实现拆箱

[试一下](https://codepen.io/anon/pen/RvEvxe?editors=0111)

# <font color="green" >总结</font>
装箱&拆箱逻辑并不复杂，但是要知道其中的原理，一旦涉及到底层api的时候才不会懵