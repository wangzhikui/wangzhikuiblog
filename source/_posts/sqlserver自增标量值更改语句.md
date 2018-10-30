---
title: SQLServer-自增标量值更改语句
categories: SQLServer
tags: [SQLServer]
date: 2012-01-17
---
```sql
dbcc checkident('risk_item',reseed,0)
```