---
title: tomcat多项目配置
categories: tomcat
tags: [tomcat]
date: 2014-01-01
---

```xml
<host>
...
<Context path="/NCRE" docBase="d:/NCRE"
        debug="5" reloadable="true" crossContext="true">
</Context>
..
</host>
```
tomcat配置文件servlet.xml

path=""为url上输入的地址 如 http:localhost:8080/NCRE

docBase=""为项目的绝对路径，

若想配置多个项目 只需增加 <Context></Context>即可


