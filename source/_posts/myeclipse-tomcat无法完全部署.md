---
title: myeclipse-tomcat无法完全部署
categories: 研发工具
tags: [eclipse,MyEclipse]
date: 2012-01-15
---

问题：
```
item could not be redeployed because it could not be completely removed in the undeployment pitem could not be redeployed because it could not be completely removed in the undeployment phase the most common cause of this problem is attempting to redeploy while the server is running which has locked one or more files           
to correct the deployment you will need to shop the server and then redeploy the project before restarting the server 
```
我的tomcat也配好了服务也启动的 就是家在项目时候出错
 

解决的办法就是在Eclipse中把项目中引用的jar文件重新加一遍就行了，基本原因就是以前的jar文件不存在了，但是项目信息中还有，即项目的.classpath文件中还有不存在的jar文件引用。 

可以右键点项目名称，选择Properties,选择Java Build Path,选择Libraries,把所有项目中的jar都remove，然后再点"add jars"，把项目中的jar文件都加进来，再次部署就正常了。
 
