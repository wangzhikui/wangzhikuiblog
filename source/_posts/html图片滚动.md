---
title: html图片滚动
categories: web前端
tags: [jsp,servlet]
date: 2014-01-03
---
```html
<html>
<body>
<DIV id=demo  style="OVERFLOW: hidden; WIDTH: 600px; HEIGHT: 190px;">
   <table border="0" cellspacing="0" cellpadding="0">
      <tr>
         <td valign="top"  id=demo1>
            <!-- 要循环滚动的图片 -->
            <table width="600" border="0" align="center" cellpadding="0" cellspacing="0" >
               <tr>
                  <td width="200" height="150" align="center">
                     <img src="images/pic1.jpg" width="194" height="147" border="0" />
                  </td>
                  <td width="200" align="center">
                     <img src="images/pic2.jpg" width="194" height="147" border="0" />
                  </td>
                  <td align="center">
                     <img src="images/pic3.jpg" width="194" height="147" border="0" />
                  </td>
               </tr>
            </table>

         </td>
         <TD id=demo2 width=1></TD>
      </tr>
   </table>
</DIV> 
<SCRIPT>
   var speed=30//速度数值越大速度越慢
   var demo2 = document.getElementById("demo2");
   var demo = document.getElementById("demo");
   var demo1 = document.getElementById("demo1");
   demo2.innerHTML=demo1.innerHTML
   function Marquee(){
      if(demo2.offsetWidth-demo.scrollLeft<=0)
         demo.scrollLeft-=demo1.offsetWidth
      else{
         demo.scrollLeft++
      }
   }
   var MyMar=setInterval(Marquee,speed)
   demo.onmouseover=function() {clearInterval(MyMar)}
   demo.onmouseout=function() {MyMar=setInterval(Marquee,speed)}
</SCRIPT>
</body>
</html>
```