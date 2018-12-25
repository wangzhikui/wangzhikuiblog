---
title: jsp退出页面处理
categories: web前端
tags: [jsp,servlet]
date: 2012-01-14
---
由于HTTP协议以请求/响应的方式工作，所以客户端退出系统时需要主动往Web服务器发送一个请求，通知Web服务器及时销毁会话，否则Web服务器只会等到会话过期时才会销毁它。

我们用一个quit.jsp来处理用户退出系统的操作，quit.jsp负责注销session，及时释放资源。

　　·注销session。

　　·关闭浏览器窗口。

其代码如下所示：
``` js
＜%@ page contentType="text/html; charset=GBK" %＞
＜%
  session.invalidate();
%＞
＜script language="javaScript" ＞
  window.opener = null;
  window.close();
＜/script＞ 
```
其中第3行负责注销session，原先放入session的对象将解绑定，等待垃圾回收以释放资源。对于本例而言，session中有一个名为ses_userBean的userBean对象（它是在switch.jsp中放入session的），调用session.invalidate()后，userBean从session中解绑定，它的valueUnbound()方法会被触发调用，然后再等待垃圾回收。

第5~8行是一段JavaScript脚本程序，负责关闭窗口，如果网页不是通过脚本程序打开的（window.open()），调用window.close()脚本关闭窗口前，必须先将window.opener对象置为null，如第6行所示，否则浏览器会弹出一个确定关闭的对话框，笔者发现这个问题困扰了不少的Web程序员，故特别指出。
