---
title: mac中连接mysql常见错误
categories: mysql
tags: [mac,mysql]
date: 2019-01-16
---
# <font color=green>问题描述</font>

## <font color=green>Navicat连接本地数据库报错</font>
```
navicat for mysql[Mac]解决Can't connect to MySQL server on '127.0.0.1'(61 "Connection refused")
```
![](/images/mysql1.png)
# <font color=green>处理过程</font>
网上找了很多方法都没有解决，应该是场景不一样。

## 步骤一：查看mysql服务是否启动（发现没有启动）

## 步骤二：启动mysql服务（启动报错）
执行命令
```
sudo /usr/local/mysql/support-files/mysql.server start
```
启动过程报错
```
ERROR! The server quit without updating PID file (/usr/local/mysql/data/bogon.pid).
```
## 步骤三：处理启动mysql服务报错问题
同样的网上找了很多问题也没发现原因，无意间点开mac上的mysql控制面板
![](/images/mysql2.png)
看到一条很有用的信息
```
“Warning:The /usr/local/mysql/data directory is not owned by the 'mysql' or '_mysql' ”
```
修改权限
```
sudo chown -R mysql /usr/local/mysql/data
sudo /usr/local/mysql/support-files/mysql.server start
```
启动正常
## 步骤四：再次使用Navicat连接（成功）

# <font color=green>补充</font>
停止MySQL服务
```
sudo /usr/local/mysql/support-files/mysql.server stop
```
 
重启MySQL服务
```
sudo /usr/local/mysql/support-files/mysql.server restart
```
