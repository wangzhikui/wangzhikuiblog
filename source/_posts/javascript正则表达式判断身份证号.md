---
title: javascript正则表达式判断身份证号
categories: web前端
tags: [javascript,正则表达式]
date: 2012-01-12
---
```js
//判断身份证
function isIdCardNo(num) 
{ 
     if (isNaN(num)) {alert("输入身份证的不是数字！"); return false;} 
     var len = num.length; 
     var re;
     if (len == 15) 
         re = new RegExp(/^(\d{6})()?(\d{2})(\d{2})(\d{2})(\d{3})$/); 
     else if (len == 18) 
         re = new RegExp(/^(\d{6})()?(\d{4})(\d{2})(\d{2})(\d{3})(\d)$/); 
     else {alert("身份证输入的数字位数不对！"); return false;} 
         var a = num.match(re); 
     if (a != null) 
     { 
         if (len==15) 
         { 
             var D = new Date("19"+a[3]+"/"+a[4]+"/"+a[5]); 
             var B = D.getYear()==a[3]&&(D.getMonth()+1)==a[4]&&D.getDate()==a[5]; 
         } 
         else 
         { 
             var D = new Date(a[3]+"/"+a[4]+"/"+a[5]); 
             var B = D.getFullYear()==a[3]&&(D.getMonth()+1)==a[4]&&D.getDate()==a[5]; 
         } 
         if (!B) {alert("输入的身份证号 "+ a[0] +" 里出生日期不对！"); return false;} 
      } 
     return true; 
} 
```