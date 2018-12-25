---
title: ajax实现用户注册
categories: web前端
tags: [ajax]
date: 2013-01-05
---

# regist.jsp 文件：一个简单的注册页面
``` jsp
<%@ page contentType="text/html; charset=gb2312"%>
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN">
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=gb2312">
<title>注册页面</title> 
<script type="text/javascript" src="http://www.knowsky.com/js/ajax.js"> </script>
<script type=text/javascript>
<!--            
  function myAlert(strTitle) {
    var message=document.getElementById("myDiv").innerHTML;
    var win1 = new Zapatec.AlertWindow(message, {title:strTitle, modal:true, width : 580,height:330});
  }
  function doCheck() {
  var f = document.forms[0];
  if(f.username.value!="") {
    document.getElementById("feedback_info").innerHTML = "系统正在处理您的请求，请稍后。";
    send_request("GET","checkUsername.jsp?username="+f.username.value,null,"text",showFeedbackInfo);
  }
  else {
    document.getElementById("feedback_info").innerHTML = "请输入用户名称。";
  }
}
function showFeedbackInfo() {
  if (http_request.readyState == 4) { // 判断对象状态
    if (http_request.status == 200) { // 信息已经成功返回，开始处理信息
        document.getElementById("feedback_info").innerHTML = http_request.responseText;
    } else { //页面不正常
        alert("您所请求的页面有异常。");
    }
  }
}
//-->            
</script>
</head>
<body>
<form name="form1" method="post" action="">
<table style="font-size:12px;">
  <tr>
      <td width="80">用户名：</td>
      <td><input type="text" name="username" onblur="doCheck()"></td>
  </tr>
  <tr>
    <td colspan="2"><span id="feedback_info" style="color:#FF0000"></span></td>
  </tr>
  <tr>
      <td>一级密码：</td>
      <td><input type="password" name="pwd"></td>
  </tr>
</table>
</form>
</body>
</html>
```

# js文件源代码如下：（ajax.js）
``` js
//定义XMLHttpRequest对象实例
var http_request = false;
//定义可复用的http请求发送函数
function send_request(method,url,content,responseType,callback) {//初始化、指定处理函数、发送请求的函数
     http_request = false;
     //开始初始化XMLHttpRequest对象
     if(window.XMLHttpRequest) { //Mozilla 浏览器
         http_request = new XMLHttpRequest();
         if (http_request.overrideMimeType) {//设置MiME类别
             http_request.overrideMimeType("text/xml");
         }
     }
     else if (window.ActiveXObject) { // IE浏览器
         try {
             http_request = new ActiveXObject("Msxml2.XMLHTTP");
         } catch (e) {
             try {
                 http_request = new ActiveXObject("Microsoft.XMLHTTP");
             } catch (e) {}
         }
     }
     if (!http_request) { // 异常，创建对象实例失败
         window.alert("不能创建XMLHttpRequest对象实例.");
         return false;
     }
     if(responseType.toLowerCase()=="text") {
         //http_request.onreadystatechange = processTextResponse;
         http_request.onreadystatechange = callback;
     }
     else if(responseType.toLowerCase()=="xml") {
         //http_request.onreadystatechange = processXMLResponse;
         http_request.onreadystatechange = callback;
     }
     else {
         window.alert("响应类别参数错误。");
         return false;
     }
     // 确定发送请求的方式和URL以及是否异步执行下段代码
     if(method.toLowerCase()=="get") {
         http_request.open(method, url, true);
     }
     else if(method.toLowerCase()=="post") {
         http_request.open(method, url, true);
         http_request.setRequestHeader("Content-Type","application/x-www-form-urlencoded");
     }
     else {
         window.alert("http请求类别参数错误。");
         return false;
     }
     http_request.send(content);
}
// 处理返回文本格式信息的函数
function processTextResponse() {
     if (http_request.readyState == 4) { // 判断对象状态
         if (http_request.status == 200) { // 信息已经成功返回，开始处理信息
             //alert(http_request.responseText);
             alert("Text文档响应。");
         } else { //页面不正常
             alert("您所请求的页面有异常。");
         }
     }
}
//处理返回的XML格式文档的函数
function processXMLResponse() {
     if (http_request.readyState == 4) { // 判断对象状态
         if (http_request.status == 200) { // 信息已经成功返回，开始处理信息
             //alert(http_request.responseXML);
             alert("XML文档响应。");
         } else { //页面不正常
             alert("您所请求的页面有异常。");
         }
     }
} 
```

# checkUsername.jsp源代码如下：
``` jsp
<%@ page contentType="text/html; charset=gb2312"%>
<%@ page import="com.kemei.user.util.MemberManager" %>
<%
  String name=request.getParameter("username");
  MemberManager manager=new MemberManager();
  if(manager.searchByUsername(username))
    out.println("用户名称["+username+"]已经被注册，请更换其他用户名称再注册。");
  else 
    out.println("用户名称["+username+"]尚未被注册，您可以继续。");
  manager.closeDAO();
%>
```
到此，一个简单的异步验证用户名的程序已经完成，当你输入完用户名后，切换光标，将会异步验证数据的正确性，但是，在使用时还遇到点不问题，最初输入英文或数字验证用户名时，没问题，但我输入中文难时却出现乱码，于是对checkUsername.jsp进行了修改，修改后源程序如下：

``` jsp
<%@ page contentType="text/html; charset=gb2312"%>
<%@ page import="com.kemei.user.util.MemberManager" %>
<%
  String name=request.getParameter("username");
  String username=new String(name.getBytes("ISO8859-1"),"gb2312");
  MemberManager manager=new MemberManager();
  if(manager.searchByUsername(username))
    out.println("用户名称["+username+"]已经被注册，请更换其他用户名称再注册。");
  else 
    out.println("用户名称["+username+"]尚未被注册，您可以继续。");
  manager.closeDAO();
%>

```