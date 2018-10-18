---
title: 设置Tomcat不用输入端口号和目录名就可以访问
categories: tomcat
tags: tomcat
date: 2012-01-01
---

# 情况一
如果你的TOMCAT所在的机器纯粹就是只装TOMCAT作为JSP的服务器，那么将server.xml文件里的默认端口号由8080改为80即可。
此时不用输入端口号也能正确访问，而且地址栏也不会出现端口号。   
  
# 情况二  
如果你的TOMCAT所在机器除了装TOMCAT运行JSP外，还有IIS同时也运行ASP的话，那么这个8080端口屏蔽不了。
有文章介绍可以将TOMCAT和IIS结合，可以去掉端口号，但是在这种情况下JSP里的SESSION不能用，跳到下页SESSION值就丢失了。
故一个比较不得以的办法就是使用页面跳转。具体做法是:在IIS下建一站点，该站点对应你的网站的域名。该站点下就一个文件index.htm：   
``` javascript
  <script   language=vbscript>   
  window.location.href="http://xxx.xxx.xxx.xxx:8080"   
  </script> 
```  

则别人在访问你的域名时就不用输入端口号。而由系统自己跳转到TOMCAT。但此刻在地址栏会出现8080，但也只好如此了。






