---
title: SQLServer-企业管理器无法打开
categories: 数据库
tags: [SQLServer,数据库]
date: 2012-01-20
---

# 方法一:
* 在运行里面输入—c
* 依次点击控制台--忝加/删除管理单元--忝加--找到Microsoft SQL企业管理器--忝加--关闭--确定

（注：此处点击忝加完后可以关闭了，不要等待响应，如果你多次点击了添加，后来可以看到n多个sql企业管理器）
再回到控制台一选项一控制台楼 式选择“用户模式完全访问“—将下面的选择全部取消•最后，从控制台--另存为-存储为c:\Program Files\Micr〇S〇ft SQL S erver\80\Tools\BIHH\SQL Server Enterprise Manager.MSC (即SqlServer的安装目录下的bin文件夹）•
# 方法二:
```
regsvr32 C:\Windows\system32\insxinl3.dll
```