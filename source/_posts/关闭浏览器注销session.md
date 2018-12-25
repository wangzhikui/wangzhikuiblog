---
title: 关闭浏览器注销session
categories: web前端
tags: [web前端]
date: 2014-01-05
---
``` js
function   window.onbeforeunload()   
{ 
  if(event.clientX>360&&event.clientY<0||event.altKey)   
  {   
    // window.event.returnValue="确定要退出登录吗？"; 
    var url = "<%=path%>/pages/SessionEnd.jsp"; 
    var callback = processAjaxResponse; 
    executeXhr(callback, url);    
  }   
} 
```