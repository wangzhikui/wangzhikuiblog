---
title: javascript捕获窗口关闭事件有两种方法
categories: web前端
tags: [javascript]
date: 2013-01-10
---
# 用javascript重新定义 window.onbeforeunload()  事件
在javascript里定义一个函数即可
```js
function  window.onbeforeunload()  
{  
  alert("关闭窗口")
}
//alert()事件将会在关闭窗口前执行，你也可以用户决定是否关闭窗口

function  window.onbeforeunload()  {  
 if  (event.clientX>document.body.clientWidth  &&  event.clientY<0 ||event.altKey)  
     window.event.returnValue="确定要退出本页吗？";  
 }
```
# 用onUnload方法
在body 标签里加入onUnload事件
``` html
body onUnload="myClose()"
```
然后在javascript里定义myClose()方法
但是onUnload方法是在关闭窗口之后执行，不是在关闭窗口之前执行，如果你想在关闭窗口之前做判断，请用第一种方法