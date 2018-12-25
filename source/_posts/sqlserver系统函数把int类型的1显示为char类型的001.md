---
title: sqlserver系统函数把int类型的1显示为char类型的001
categories: 数据库
tags: [SQLServer,数据库]
date: 2014-01-06
---

to_char(1, '000 ')函数
```sql
select to_char(1, '000 ') from demo
```

``` sql
select   right( '00 '+cast(CustomerID   as   varchar(3)),3)   from   ... 
```
right((10000+字段名),3)就是3位的.

支持可以处理得简单些： 
```sql
select   right( '00 '+cast(CustomerID   as   varchar(3)),3)   from   ... 
```

