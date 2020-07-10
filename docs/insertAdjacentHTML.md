---
id: insertAdjacentHTML方法详解
title: insertAdjacentHTML方法详解
sidebar_label: insertAdjacentHTML
---
添加HTML内容与文本内容以前用的是innerHTML与innerText方法，

最近发现还有insertAdjacentHTML和 insertAdjacentText方法，

这两个方法更灵活，可以在指定的地方插入html内容和文本内容。

 

insertAdjacentText方法与 insertAdjacentHTML方法类似，只不过只能插入纯文本，参数相同

方法名称：insertHtml(where,el,html)

参数介绍：
where：插入位置。包括beforeBegin,beforeEnd,afterBegin,afterEnd。
el：用于参照插入位置的html元素对象
html：要插入的html代码




insertAdjacentHTML 方法：在指定的地方插入html标签语句

原型：insertAdajcentHTML(swhere,stext)



参数：

swhere: 指定插入html标签语句的地方，

stext:要插入的内容



有四种值可用：

1.beforeBegin: 插入到标签开始前

2.afterBegin:插入到标签开始标记之后

3.beforeEnd:插入到标签结束标记前

4.afterEnd:插入到标签结束标记后

实例:
```javascript
<html>
     <head>
     <mce:script language="javascript"><!--
     function myfun(){
         var obj = document.getElementById("btn1");
         obj.insertAdjacentHTML("afterEnd","<br><input name="txt1">");
     }
     
// --></mce:script>
     </head>
     <body>
         <input name="txt">
         <input id="btn1" name="btn1" type="button" value="更多" οnclick="myfun()">
     </body>
 </html>
```

```javascript
<html>
 <head>
 <title>24.htm insertAdjacentHTML插入新内容</title>
 <mce:script language="jscript"><!--
 function addsome()
 {
     document.all.paral.insertAdjacentHTML("afterBegin","<h1> 在文本前容器内插入内容1</h1>");
     document.all.paral.insertAdjacentHTML("beforeEnd","<h2> 在文本后容器内插入内容2</h2>");
     document.all.paral.insertAdjacentHTML("beforeBegin","<h4> 在文本前容器外插入内容4</h1>");
     document.all.paral.insertAdjacentHTML("afterEnd","<h5> 在文本后容器外插入内容5</h2>");
 }
 
// --></mce:script>
 </head>
 <body οnlοad="addsome()">
 <div id="paral" style="fontsize:6;color='#ff00ff'" mce_style="fontsize:6;color='#ff00ff'">原来的内容</div><hr>
 </body>
 </html> 
```
