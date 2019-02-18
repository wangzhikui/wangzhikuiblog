---
title: javascript重塑基础系列之-使用void 0 替换undefined
categories: javascript
tags: [javascript,重塑基础]
date: 2019-01-23
---
# 目录
- [概述](#概述)
- [不使用undefined原因](#不使用undefined原因)
- [使用void原因](#使用void原因)
- [其他一些替代写法](#其他一些替代写法)
- [reference](#reference)

# <font color="green" >概述</font>
undefined：表示未定义。

在编码中使用某一个变量或者函数之前有时会判断是否已经定义了，并且不是空然后再做处理。这个时候会使用比如：

``` javascript
if(a !== undefined && a! == null){
  .......
}
```
一般来讲是没有问题的，但如果经常阅读开源源码会发现，如下写法：

``` javascript
if(a !== void 0 && a! == null){
  .......
}
```

两种写法目的是一样的。

# <font color="green" >不使用undefined原因</font>
上面提到两种写法，为什么建议用void 0 ？

主要原因是javascript在设计的时候undefined并不是一个关键字，也就是说如下代码是合理的不会报错:
```javascript
var undefined = 100;
console.log(undefined)
```
不同的浏览器运行的结果不太相同，在chrome中仍然输出undifined，但是在比较老的IE中会输出100；

ES5之后undefined已经是一个只读属性，所以上述输出不同浏览器基本都是undefined。但是在局部作用域中undefined会被修改：
```javascript
(function() {
  var undefined = 100;
  console.log(undefined);
})();
```
结果：输出100

[试一下](https://codepen.io/gaearon/pen/ZpvBNJ?editors=0111)

# <font color="green" >使用void原因</font>
void是javascript中的一个操作符，有两种写法
* void exp
* void(exp)

void：计算一个表达式但无论该表达式原来是否有自己的返回值，其返回值都为undefined
* 作用一：返回undefined，解决上面提到的undefined会被重新定义的问题
* 作用二：防止不必要的行为。比如a标签中我们有一种写法
```javascript
<a href="javascript:void(0)"></a>
```

因为void是关键字所以可以放心的用。为什么是void 0内，其实后面跟什么都会返回undefined，只是最简单的就是0这个字符，其实void 1，void 2，void("hello") 都可以。void 0可以做到占用字节数最少。


# <font color="green" >其他一些替代写法</font>
```javascript
//取整
parseInt(a,10); //Before
Math.floor(a); //Before
a>>0; //Before
~~a; //After
a|0; //After
 
//四舍五入
Math.round(a); //Before
a+.5|0; //After
 
//内置值
undefined; //Before
void 0; //After, 快
0[0]; //After, 略慢
 
//内置值
Infinity;
1/0;
 
//布尔值短写法
true; //Before
!0; //After
 
//布尔值短写法
false; //Before
!1; //After

```

# <font color="green" >reference</font>
https://blog.csdn.net/qq_33834489/article/details/81540018