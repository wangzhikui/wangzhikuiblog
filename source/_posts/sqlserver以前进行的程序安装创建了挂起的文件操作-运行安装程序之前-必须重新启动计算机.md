---
title: sql Server 以前进行的程序安装创建了挂起的文件操作,运行安装程序之前,必须重新启动计算机
categories: 数据库
tags: [SQLServer,数据库]
date: 2012-01-16
---
打开注册表找到
```
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session   Manager
```
中找到PendingFileRenameOperations删除