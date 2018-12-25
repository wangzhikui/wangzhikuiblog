---
title: jsp-关于request和reponse退出时的位置定向问题
categories: web前端
tags: [jsp,servlet]
date: 2014-01-02
---
```jsp
<%@page contentType="text/html;charset=gb2312" import="java.util.*"%>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
  <meta  content="text/html; charset=gb2312">
<body>
  <% 
  request.getSession().invalidate();
  //request.getRequestDispatcher("/index.jsp").forward(request, response);用这个logout后不能刷新
  response.sendRedirect("/research/index.jsp");
  %> 
</body>
</html>
```
如果是这样的话

request.getRequestDispatcher("/index.jsp").forward(request, response);

这条语句跳到index.jsp页面后 如果刷新则会出现一下异常
``` java
HTTP Status 500 - 
--------------------------------------------------------------------------------
type Exception report
message 
description The server encountered an internal error () that prevented it from fulfilling this request.
exception 
org.apache.jasper.JasperException: An exception occurred processing JSP page /admin/logout.jsp at line 9
6: <body>
7:   <% 
8:   request.getSession().invalidate();
9:   request.getRequestDispatcher("/index.jsp").forward(request, response);
10:   //response.sendRedirect("/research/index.jsp");
11:   %> 
12: </body>
Stacktrace:
	org.apache.jasper.servlet.JspServletWrapper.handleJspException(JspServletWrapper.java:505)
	org.apache.jasper.servlet.JspServletWrapper.service(JspServletWrapper.java:410)
	org.apache.jasper.servlet.JspServlet.serviceJspFile(JspServlet.java:342)
	org.apache.jasper.servlet.JspServlet.service(JspServlet.java:267)
	javax.servlet.http.HttpServlet.service(HttpServlet.java:717)
	com.fitler.bean.Filter_Login.doFilter(Filter_Login.java:42)
	com.fitler.bean.Filter_chinese.doFilter(Filter_chinese.java:21)
root cause 
java.lang.IllegalStateException: Cannot forward after response has been committed
	org.apache.jsp.admin.logout_jsp._jspService(logout_jsp.java:63)
	org.apache.jasper.runtime.HttpJspBase.service(HttpJspBase.java:70)
	javax.servlet.http.HttpServlet.service(HttpServlet.java:717)
	org.apache.jasper.servlet.JspServletWrapper.service(JspServletWrapper.java:374)
	org.apache.jasper.servlet.JspServlet.serviceJspFile(JspServlet.java:342)
	org.apache.jasper.servlet.JspServlet.service(JspServlet.java:267)
	javax.servlet.http.HttpServlet.service(HttpServlet.java:717)
	com.fitler.bean.Filter_Login.doFilter(Filter_Login.java:42)
	com.fitler.bean.Filter_chinese.doFilter(Filter_chinese.java:21)
note The full stack trace of the root cause is available in the Apache Tomcat/6.0.18 logs.
```

使用response.sendRedirect("/research/index.jsp");重定向过去就没有这个问题， 
问题解决，但是还未具体研究为什么
