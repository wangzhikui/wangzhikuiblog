---
title: jsp获取各种路径
categories: web前端
tags: [jsp,servlet]
date: 2012-01-13
---

我的upload.jsp在D:\tomcat\webapps\hr下，在upload.jsp中有如下代码

```java
System.out.println("The Path1 is "+request.getContextPath());
System.out.println("The Path2 is "+request.getRealPath(request.getRequestURI()));
System.out.println("The Path3 is "+new java.io.File(application.getRealPath(request.getRequestURI())).getParent());
System.out.println("The Path4 is "+request.getServletPath());
System.out.println("The Path5 is "+new java.io.File(request.getRealPath(request.getServletPath())).getParent());
```

```
The Path1 is /hr
The Path2 is D:\tomcat\webapps\hr\hr\upload.jsp
The Path3 is D:\tomcat\webapps\hr\hr
The Path4 is /upload.jsp
The Path5 is D:\tomcat\webapps\hr
```