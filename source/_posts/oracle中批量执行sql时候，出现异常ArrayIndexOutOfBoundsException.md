---
title: oracle中批量执行sql时候，出现异常ArrayIndexOutOfBoundsException
categories: 数据库
tags: [oracle,数据库]
date: 2015-03-17
---

## 问题说明
使用jdbc接口PreparedStatement.executeBatch()向oracle中批量执行sql时候，出现异常ArrayIndexOutOfBoundsException，
具体信息如下：
``` java
  [java] view plaincopyprint?
1.      java.lang.ArrayIndexOutOfBoundsException: -32413  
2.	    at oracle.jdbc.driver.OraclePreparedStatement.setupBindBuffers(OraclePreparedStatement.java:2672)  
3.	    atoracle.jdbc.driver.OraclePreparedStatement.executeBatch(OraclePreparedStatement.java:10688)  
4.	    atcom.keyi.xxx.dal.xx.importFile(PublicCustomerImportDao.java:107)  
```

## 问题分析

The 10g driver apparently keeps a global serialnumber for all parameters in the entire batch, 
with a "short"variable. So you can have at most 32768 parameters in the batch. 
I was havingthe same exception because I have a INSERT statement with 42 parameters and mybatches 
can be as big as 1000 records, so 42000 > 32768 and this overflowsto a negative index. 
I reduced the batch factor to 100 to be safe, and all iswell. 
I guess your update DML should have a larger number of parameters perrecord, 
right? (My diagnostic of the bug is just deduction from the symptoms)


网上查找原始帖子地址为：https://community.oracle.com/thread/599441?start=15&tstart=0

大体的意思是，oracle的preparedStatement批量执行sql时，对参数个数是有上限的（针对不同版本的oracle驱动，这个上限对不同的可能是不同的）
这个参数个数的含义指addBatch的次数*每条sql中的参数个数。对于Oracle 10g的驱动来说，
这个值可能是32768，所以编程时，addBatch的次数*每条sql中的参数个数应该小于这个值，否则报错。

按照这个思路，将addBatch的数量减少，使每次executeBatch的参数值小于32768，发现异常解决。




