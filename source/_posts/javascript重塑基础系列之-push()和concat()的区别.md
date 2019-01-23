---
title: javascript重塑基础系列之-push()和concat()的区别
categories: javascript
tags: [javascript,重塑基础]
date: 2019-01-22
---
# 目录
- [区别](#区别)
- [示例1-往数组添加元素](#示例1-往数组添加元素)
- [示例2-往数组中添加数组](#示例2-往数组中添加数组)
- [效率](#效率)

# <font color="green" >区别</font>
功能：往数组末尾追加数据

push
   * 会改变原有数组
   * 如果添加一个数组，会把数组作为对象追加到末尾
   * 如果添加一个数组并要解析，需要使用arr.push.apply()orArray.prototype.push.apply()

concat
   * 不会改变原有数组，而是返回追加数据后的数组的副本，原有数组不变
   * 如果添加一个数组，会把数组解析成元素逐个追加到末尾

# <font color="green" >示例1-往数组添加元素</font>

## push
```javascript
var arr_src = new Array()
arr_src[0] = 1
arr_src[1] = 2
arr_src[2] = 3
arr_src[3] = 4
console.log(arr_src) //输出 [1,2,3,4]
var result = arr_src.push(5)
console.log(arr_src)  //输出[1,2,3,4,5]
console.log(result)   //输出5   即返回数组长度
```
[运行结果](https://codepen.io/anon/pen/MLWGZP?editors=0011)

## concat

```javascript
var arr_src = new Array()
arr_src[0] = 1
arr_src[1] = 2
arr_src[2] = 3
arr_src[3] = 4
console.log(arr_src) //输出 [1,2,3,4]
var result = arr_src.concat(5)
console.log(arr_src)  //输出[1,2,3,4]
console.log(result)   //返回合并后的数组 输出[1,2,3,4,5]
```
[运行结果](https://codepen.io/anon/pen/zeYjEy?editors=0011)

# <font color="green" >示例2-往数组中添加数组</font>
## push
```javascript
var arr_src = new Array()
arr_src[0] = 1
arr_src[1] = 2
arr_src[2] = 3
arr_src[3] = 4
var arr_add = new Array()
arr_add[0] = 5
arr_add[1] = 6
console.log(arr_src) //输出 [1,2,3,4]
console.log(arr_add) //输出 [5,6]
arr_src.push(arr_add)
console.log(arr_src)  //输出[1,2,3,4,[5,6}]
console.log(arr_add)  //输出[5,6]
```
[运行结果](https://codepen.io/anon/pen/jdOzRy?editors=0012)

如果要解析数组逐个追加可以使用apply,如下两种方法均可,arr_src数组会被改变，arr_add不变
```javascript
arr_src.push.apply(arr_src,arr_add)        //[1, 2, 3, 4, 5,6]
//或者
Array.prototype.push.apply(arr_scr,arr_add)
```
[尝试一下](https://codepen.io/anon/pen/jdOzRy?editors=0012)

## concat

```javascript
var arr_src = new Array()
arr_src[0] = 1
arr_src[1] = 2
arr_src[2] = 3
arr_src[3] = 4
console.log(arr_src) //输出 [1,2,3,4]
var result = arr_src.concat([5,6])
console.log(arr_src)  //输出[1,2,3,4]
console.log(result)   //输出[1,2,3,4,5,6]
```
[运行结果](https://codepen.io/anon/pen/pGoVGZ?editors=0011)

# <font color="green" >效率</font>

## 测试环境
* 两个10万的数组合并
* chrome浏览器 Version 71.0.3578.98 (Official Build) (64-bit)

## 测试结果
* concat优与apply
* concat没有长度限制，apply在chrome浏览器下20万-30万之间就内存溢出，实际边界没有测试，不同浏览器不同

## 测试代码如下：保存为html用浏览器打开即可
```html
<!DOCTYPE html>
<head>
<script>
var testArray1=[]
var testArray2=[]
function reset(){
  var count = document.getElementById("count").value
  for(var i=0; i<count;i++){
    testArray1.push(i)
    testArray2.push(i+count)
  }
}
function setValue(id,value){
  document.getElementById(id).innerHTML = value
}
function testApply(){
  //初始化数组
  reset()
  var startTime=0
  var endTime=0
  console.log('开始：'+ (startTime=new Date().getTime()))
  setValue("startTime",startTime)
  var result=Array.prototype.push.apply(testArray1,testArray2) // result为合并后的数组长度
  console.log(result)
  console.log('结束：'+ (endTime=new Date().getTime()))
  setValue("endTime",endTime)
  console.log('耗时：'+(endTime-startTime))
  setValue("totalTime",endTime-startTime)
}
function testConcat(){
  //初始化数组
  reset()
  var startTime=0
  var endTime=0
  console.log('开始：'+ (startTime=new Date().getTime()))
  setValue("startTime",startTime)
  var result=testArray1.concat(testArray2) //result为合并后的数组
  console.log(result.length)
  console.log('结束：'+ (endTime=new Date().getTime()))
  setValue("endTime",endTime)
  console.log('耗时：'+(endTime-startTime))
  setValue("totalTime",endTime-startTime)
}
</script>
</head>
<body>
  <input type="text" id="count" />
  <button onclick="testApply()">testApply</button>
  <button onclick="testConcat()">testConcat</button>
  <br>
  <ul>
    <li>开始:<div id="startTime"></div></li>
    <li>结束:<div id="endTime"></div></li>
    <li>耗时:<div id="totalTime"></div>毫秒</li>
  </ul>
</body>
</html>
```
效果图：

![](/images/javascript重塑/1.png)