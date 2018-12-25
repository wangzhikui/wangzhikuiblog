---
title: j2ee_5中mail包与使用的mail包冲突解决
categories: java
tags: [java,eclipse]
date: 2013-01-07
---
``` java
Exception in thread "main" java.lang.NoClassDefFoundError: com/sun/mail/util/LineInputStream 
```
当出现以上错误时，恭喜您已经离接收邮件不远了，否则请您解决好所有的异常后再来看这个帖子。
javax.mail和javax.activation这两个包已经在javaEE5当中属于基础包了，就是JDK中自带了已经，但是里面的方法与现在外面的mail.jar和activation.jar有一些出入，所以初学者在直接copy别人代码的时候往往会出现上面的错误。 
废话不多说下面是解决方法 
进到
```
X:\Program Files\MyEclipse 6.5\myeclipse\eclipse\plugins\com.genuitec.eclipse.j2eedt.core_6.5.0.zmyeclipse650200806\data\libraryset\EE_5
```
这个路径里,可以看到javaee.jar,用rar把这个文件打开,然后进到javax文件夹里,删除mail.jar和activation.jar(我的javaee.jar里，这两个东西是文件夹，总之删掉就OK，不过要注意备份一下

