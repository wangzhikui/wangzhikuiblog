---
title: java连接各种数据库驱动名写法和语句
categories: java
tags: [java]
date: 2012-01-10
---
# java数据库连接:

## access 数据库连接:
```java
Class.forName("sun.jdbc.odbc.JdbcOdbcDriver");
DriverManager.getConnection("jdbc:odbc:[dsn]"); 注:dsn为数据源
```

## MySQL 数据库连接:
```java
Class.forName("com.mysql.jdbc.Driver");
DriverManager.getConnection("jdbc:mysql://localhost/[DataBase name]?user=root&passWord=yuyang")
```

## Oracle(thin)数据库连接:
```java
Class.forName("oracle.jdbc.driver.OracleDriver");
DriverManager.getConnection("jdbc:oracle:thin:@localhost:1521:[DataBase Name]","scott","tiger");
```

本机专用:
```java
con=DriverManager.getConnection("jdbc:oracle:thin:@localhost:1521:orcl","scott","tiger");
```

## Oracle(OCI driver)数据库连接:
```java
Class.forName("oracle.jdbc.driver.OracleDriver");
DriverManager.getConnection("jdbc:oracle:oci8:@localhost:1521:[DataBase Name]","scott","tiger");
```
## Microsoft SQL Server 2005数据库连接:
```java
1.Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");
2.DriverManager.getConnection("jdbc:sqlserver://localhost:1433;database=MySchool;user=sa;password=yuyang");
```
注:如果电脑中安装Dr.COM 宽带登录客户端软件，且处于运行状态，则连接数据库读取数据库时将会出现如下异常
```
Unrecognized Windows Sockets error: 997: recv failed
```
如果想运行，必须先把Dr.COM这个软件停掉方可

## Microsoft SQL Server 2000

### 一.Microsoft SQL Server:
```java
Class.forName("com.microsoft.jdbc.sqlserver.SQLServerDriver");
DriverManager.getConnection
("jdbc:microsoft:sqlserver://localhost:1433;databasename=MySchool","sa","yuyang");
```
### 二.Microsoft SQL Server(jTDS driver):
```java
Class.forName("net.sourceforge.jtds.jdbc.Driver")
DriverManager.getConnection
("jdbc:jtds:sqlserver://localhost:1433/MySchool","sa","yuyang");
```