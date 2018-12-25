---
title: mysql专杀使mysql无法启动
categories: 数据库
tags: [mysql,数据库]
date: 2013-01-02
---

今天发现电脑上有恶意插件.

就下了个360强力木马专杀工具.

最后这玩意居然把我的mysql给咔嚓了..没有启动.

解决方法:

看看服务里面有没有mysql的服务.启动即可.

没有就

启动cmd，切换至mysql安装目录/bin下，执行 
``` batch
mysqld-nt.exe -install 
net start mysql 
```

解决......