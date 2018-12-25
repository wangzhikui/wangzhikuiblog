---
title: SQLServer-自增标量值更改语句
categories: 数据库
tags: [SQLServer,数据库]
date: 2012-01-17
---
```sql
dbcc checkident('risk_item',reseed,0)
```