---
id: JavaScriptDom笔记
title: JavaScript Dom 编程艺术（第二版）笔记
sidebar_label: JavaScript Dom 编程艺术（第二版）笔记
---
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200711031720913.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDA4OTU0NA==,size_16,color_FFFFFF,t_70)


### 综合案例1（第四章）照片墙（HTML绑定事件）

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <style>
      body {
        font-family:Verdana, Geneva, Tahoma, sans-serif;
        color: #333333;
        background-color:#ccc;
        margin:1em 10%
      }

      h1{
        color: #333;
        background-color:transparent;
      }

      a{
        color: #c60;
        background-color:transparent;
        font-weight:bold;
        text-decoration:none;
      }

      ul{
        padding:0;
      }

      li{
        float: left;
        padding:1em;
        list-style:none;
      }

      img{
        display:block;
        clear:both;
        max-width: 600px;
        max-height: 300px;
      }

      p{
        margin-left:150px;
      }

    </style>
    
    <title>照片墙</title>
  </head>
  
    <h1>Snapshots</h1>
    <ul>
      <li><a href="./img/Fireworks.jpg" onclick="showPic(this);return false;" title="A fireworks display">Fireworks</a></li>
      <li><a href="./img/Coffee.jpg" onclick="showPic(this);return false;" title="A cup of black coffee">Coffee</a></li>
      <li><a href="./img/Rose.jpg" onclick="showPic(this);return false;" title="A red ,red rose"> Rose</a></li>
      <li><a href="./img/bigben.jpg" onclick="showPic(this);return false;" title="The famous clock">Big Ben</a></li>
    </ul>
    <img id = "placeholder" src="./img/Rose.jpg" alt="my favorite">
      <p id="description">Choose a image.</p>
    <script>

      // 展示选择的图片
    function showPic(whichpic) {
      // dom中读取地址
      var source = whichpic.getAttribute("href");
      // 找到dom中元素
      var placeholder = document.getElementById("placeholder");
      // 元素设置属性
      placeholder.setAttribute("src", source);
      //获取元素title
      var text = whichpic.getAttribute("title");
      //获取p元素
      var description = document.getElementById("description");
      //设置内容
      description.firstChild.nodeValue = text;

      return true;
    }
      
    </script>
  </d>
</html>
```

### 综合案例2（第六章）照片墙（结构分离绑定事件）
```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <style>
    body {
      font-family: Verdana, Geneva, Tahoma, sans-serif;
      color: #333333;
      background-color: #ccc;
      margin: 1em 10%
    }

    h1 {
      color: #333;
      background-color: transparent;
    }

    a {
      color: #c60;
      background-color: transparent;
      font-weight: bold;
      text-decoration: none;
    }

    ul {
      padding: 0;
    }

    li {
      float: left;
      padding: 1em;
      list-style: none;
    }

    img {
      display: block;
      clear: both;
      max-width: 600px;
      max-height: 300px;
    }

    p {
      margin-left: 150px;
    }
  </style>

  <title>照片墙</title>
</head>

<h1>Snapshots</h1>
<ul id="imagegallery">
  <li><a href="./img/Fireworks.jpg" title="A fireworks display">Fireworks</a></li>
  <li><a href="./img/Coffee.jpg" title="A cup of black coffee">Coffee</a></li>
  <li><a href="./img/Rose.jpg" title="A red ,red rose"> Rose</a></li>
  <li><a href="./img/bigben.jpg" title="The famous clock">Big Ben</a></li>
</ul>
<img id="placeholder" src="./img/Rose.jpg" alt="my favorite">
<p id="description">Choose a image.</p>
<script>
  // 页面加载执行函数
  window.load = prepareGallery();

    // 绑定点击事件
    function prepareGallery() {
      // 找到ID（imagegallery）
      var gallery = document.getElementById("imagegallery");
      // 找到ID（imagegallery）中a 标签
      var links = gallery.getElementsByTagName("a");
      //  循环遍历监听事件
      for (var i = 0; i < links.length; i++) {
        // 绑定点击事件
        links[i].onclick = function() {
          // 调用显示函数
          return showPic(this) ? false : true;
        };
      }
    }

    // 展示选择的图片
    function showPic(whichpic) {
      // dom中读取地址
      var source = whichpic.getAttribute("href");
      // 找到dom中元素
      var placeholder = document.getElementById("placeholder");
      // 元素设置属性
      placeholder.setAttribute("src", source);
      //获取元素title
      var text = whichpic.getAttribute("title");
      //获取p元素
      var description = document.getElementById("description");
      //设置内容
      description.firstChild.nodeValue = text;

      return true;
    }
    
</script>


</html>
```

### 综合案例3（第七章）照片墙（添加节点绑定事件）
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <style>
      body {
        font-family: Verdana, Geneva, Tahoma, sans-serif;
        color: #333333;
        background-color: #ccc;
        margin: 1em 10%;
      }

      h1 {
        color: #333;
        background-color: transparent;
      }

      a {
        color: #c60;
        background-color: transparent;
        font-weight: bold;
        text-decoration: none;
      }

      ul {
        padding: 0;
      }

      li {
        float: left;
        padding: 1em;
        list-style: none;
      }

      img {
        display: block;
        clear: both;
        max-width: 600px;
        max-height: 300px;
      }

      p {
        margin-left: 150px;
      }
    </style>

    <title>照片墙</title>
  </head>

  <h1>Snapshots</h1>
  <ul id="imagegallery">
    <li>
      <a href="./img/Fireworks.jpg" title="A fireworks display">Fireworks</a>
    </li>
    <li><a href="./img/Coffee.jpg" title="A cup of black coffee">Coffee</a></li>
    <li><a href="./img/Rose.jpg" title="A red ,red rose"> Rose</a></li>
    <li><a href="./img/bigben.jpg" title="The famous clock">Big Ben</a></li>
  </ul>
  <!-- <img id="placeholder" src="./img/Rose.jpg" alt="my favorite" />
  <p id="description">Choose a image.</p> -->
  <script>
    // 页面加载执行函数
    function addLoadEvent(func) {
      // 记录初始执行
      var oldonload = window.onload;
      // 如果为空添加执行函数
      if (typeof window.onload != "function") {
        window.onload = func;
        // 不为空在后面追加一个执行函数
      } else {
        window.onload = function() {
          oldonload();
          func();
        };
      }
    }

    // 在目标节点后添加节点
    function insertAfter(newElement, targetElement) {
      // 取出目标节点的父节点
      var parent = targetElement.parentNode;
      // 如果父节点的最后一个字节的是目标节点
      if (parent.lastChild == targetElement) {
        // 给父节点添加新节点
        parent.appendChild(newElement);
      } else {
        // 否则在目标节点紧跟着的节点添加新节点
        parent.insertBefore(newElement, targetElement.nextSibling);
      }
    }

    // 准备图片控制节点（添加节点）
    function preparePlaceholder() {
      //   创建图片元素
      var placeholder = document.createElement("img");
      //   设置id
      placeholder.setAttribute("id", "placeholder");
      //   设置路径
      placeholder.setAttribute("src", "img/Rose.jpg");
      //   设置alt
      placeholder.setAttribute("alt", "my image gallery");
      //   创建段落元素
      var description = document.createElement("p");
      //  设置图片id
      description.setAttribute("id", "description");
      //   设置文本元素
      var desctext = document.createTextNode("Choose an image");
      //   将destest设置为description的子元素
      description.appendChild(desctext);
      //   获取imagegallery元素
      var gallery = document.getElementById("imagegallery");
      //   在gallery后加入placeholder
      insertAfter(placeholder, gallery);
      //   在description后加入placeholder
      insertAfter(description, placeholder);
    }

    // 绑定点击事件
    function prepareGallery() {
      // 找到ID（imagegallery）
      var gallery = document.getElementById("imagegallery");
      // 找到ID（imagegallery）中a 标签
      var links = gallery.getElementsByTagName("a");
      //  循环遍历监听事件
      for (var i = 0; i < links.length; i++) {
        // 绑定点击事件
        links[i].onclick = function() {
          // 调用显示函数
          return showPic(this) ? false : true;
        };
      }
    }

    // 展示选择的图片
    function showPic(whichpic) {
      // dom中读取地址
      var source = whichpic.getAttribute("href");
      // 找到dom中元素
      var placeholder = document.getElementById("placeholder");
      // 元素设置属性
      placeholder.setAttribute("src", source);
      //获取元素title
      var text = whichpic.getAttribute("title");
      //获取p元素
      var description = document.getElementById("description");
      //设置内容
      description.firstChild.nodeValue = text;

      return true;
    }

    // 添加执行函数
    addLoadEvent(preparePlaceholder);
    addLoadEvent(prepareGallery);
  </script>
</html>
```

### 综合练习4（第七章）Ajax 练习

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Ajax</title>
  </head>
  <body>
    <button id="button">请求纯文本</button>
    <script>
      document.getElementById("button").addEventListener("click", loadText);
      function loadText() {
        var xhr = new XMLHttpRequest();
        console.log(xhr);
        // open(type(请求类型),url/file（请求路径）,async（是否异步）)
        xhr.open("GET", "example.txt", true);
        // 两种请求 onload onreadystattechange

        xhr.onprogress = function(){
            console.log(this.readyState);
        }

        xhr.onload = function() {
            console.log(this.readyState);
          console.log(this.responseText);
        };

        xhr.onreadystatechange = function() {
          if(this.readyState==4&&this.status==200){
              console.log(this.responseText);
          }else if(this.status==404){
              console.log("请求的网页不存在");
          }
        };

        // readyState
        // 0:请求未初始化
        // 1：服务器已建立
        // 2：请求已接受
        // 3：请求处理中
        // 4：请求已完成，且响应已就绪

        // HTTP 状态码
        // 200 - 服务器成功返回网站
        // 404 - 请求的网页不存在
        // 503 - 服务器暂不可用

        xhr.send();
      }
    </script>
  </body>
</html>
```

### 综合练习5（第八章）缩写列表、文献来源、快捷键

html

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta http-equiv="content-type" content="text/html; charset=utf-8" />
    <title>Explaining the Document Object Model</title>
    <link rel="stylesheet" type="text/css" media="screen" href="styles/typography.css" />
    <script type="text/javascript" src="scripts/addLoadEvent.js"></script>
    <script type="text/javascript" src="scripts/displayAbbreviations.js"></script>
    <script type="text/javascript" src="scripts/displayCitations.js"></script>
    <script type="text/javascript" src="scripts/displayAccesskeys.js"></script>
  </head>
  <body>
    <ul id="navigation">
      <li><a href="index.html" accesskey="1">Home</a></li>
      <li><a href="search.html" accesskey="4">Search</a></li>
      <li><a href="contact.html" accesskey="0">Contact</a></li>
    </ul>
    <h1>What is the Document Object Model?</h1>
    <p>
The <abbr title="World Wide Web Consortium">W3C</abbr> defines
 the <abbr title="Document Object Model">DOM</abbr> as:
    </p>
    <blockquote cite="http://www.w3.org/DOM/">
      <p>
A platform- and language-neutral interface that will allow programs
 and scripts to dynamically access and update the
 content, structure and style of documents.
      </p>
    </blockquote>
    <p>
It is an <abbr title="Application Programming Interface">API</abbr>
 that can be used to navigate <abbr title="HyperText Markup Language">
HTML</abbr> and <abbr title="eXtensible Markup Language">XML
</abbr> documents.
    </p>
  </body>
</html>
```

css

```css
body {
  font-family: "Helvetica","Arial",sans-serif;
  font-size: 10pt;
}
abbr {
  text-decoration: none;
  border: 0;
  font-style: normal;
}
```

javascript（缩写列表） displayAbbreviations

```javascript
function displayAbbreviations() {
  if (
    !document.getElementsByTagName ||
    !document.createElement ||
    !document.createTextNode
  )
    return false;
  //获取所有缩写
  var abbreviations = document.getElementsByTagName("abbr");
  // 监测全文是否有缩写
  if (abbreviations.length < 1) return false;
  // 保存每个缩写
  var defs = new Array();
  // loop through the abbreviations
  for (var i = 0; i < abbreviations.length; i++) {
    var current_abbr = abbreviations[i];
    // 监测全文是否有缩写
    if (current_abbr.childNodes.length < 1) continue;
    //获取缩写标签的title
    var definition = current_abbr.getAttribute("title");
    // 获取key（获取缩写节点的最后一个节点信息）
    var key = current_abbr.lastChild.nodeValue;
    // 绑定键值
    defs[key] = definition;
  }
  // 创建dl节点
  var dlist = document.createElement("dl");
  // 遍历生成键值列表
  for (key in defs) {
    var definition = defs[key];
    // 创建dt节点
    var dtitle = document.createElement("dt");
    // 设置dt节点文本内容为key（缩写）
    var dtitle_text = document.createTextNode(key);
    // 给dtitle绑定文本节点
    dtitle.appendChild(dtitle_text);
    // 创建dd节点
    var ddesc = document.createElement("dd");
    // 设置dd节点文本内容为definition（全写）
    var ddesc_text = document.createTextNode(definition);
    // 绑定节点
    ddesc.appendChild(ddesc_text);
    dlist.appendChild(dtitle);
    dlist.appendChild(ddesc);
  }
  // 监测全文是否有缩写
  if (dlist.childNodes.length < 1) return false;
  // 创建h2标签节点
  var header = document.createElement("h2");
  // 为header添加文本节点
  var header_text = document.createTextNode("Abbreviations");
  // 添加header_text文本节点添加到header
  header.appendChild(header_text);
  // 添加header到body
  document.body.appendChild(header);
  // 添加dlist到body
  document.body.appendChild(dlist);
}
// 添加执行函数
addLoadEvent(displayAbbreviations);
```

javascript（文献来源）

```javascript
function displayCitations() {
  // 检测是否支持dom
  if (!document.getElementsByTagName || !document.createElement || !document.createTextNode) return false;
// 获取文献节点
  var quotes = document.getElementsByTagName("blockquote");
// 获取文献链接并绑定节点
  for (var i=0; i<quotes.length; i++) {
// 检测是否有cite属性
    if (!quotes[i].hasAttribute("cite")) continue;
// 获取cite的属性
    var url = quotes[i].getAttribute("cite");
// 找到文献节点的所有节点
    var quoteChildren = quotes[i].getElementsByTagName('*');
// 检测是否存在文献的子节点
    if (quoteChildren.length < 1) continue;
// 得到文献的最后一个节点
    var elem = quoteChildren[quoteChildren.length - 1];
// 创建文件列表并绑定信息
    var link = document.createElement("a");
    var link_text = document.createTextNode("source");
    link.appendChild(link_text);
    link.setAttribute("href",url);
    var superscript = document.createElement("sup");
    superscript.appendChild(link);
    elem.appendChild(superscript);
  }
}
// 设置执行函数
addLoadEvent(displayCitations);
```

javascript（快捷键）

```javascript
function displayAccesskeys() {
  if (!document.getElementsByTagName || !document.createElement || !document.createTextNode) return false;
// 获取超链接
  var links = document.getElementsByTagName("a");
// 创建数组存储快捷键
  var akeys = new Array();
  for (var i=0; i<links.length; i++) {
    var current_link = links[i];
// 检测是否存在快捷键
    if (current_link.getAttribute("accesskey") == null) continue;
// 获取accesskey的属性
    var key = current_link.getAttribute("accesskey");
// 获取快捷键节点的文本节点
    var text = current_link.lastChild.nodeValue;
// 键值绑定
    akeys[key] = text;
  }
// 创建列表
  var list = document.createElement("ul");
// 创建快捷键列表
  for (key in akeys) {
    var text = akeys[key];
//  创建列表文本
    var str = key + " : "+text;
// 创建列表项
    var item = document.createElement("li");
    var item_text = document.createTextNode(str);
    item.appendChild(item_text);
// 列表项绑定到列表
    list.appendChild(item);
  }
// 创建快捷键标题
  var header = document.createElement("h3");
  var header_text = document.createTextNode("Accesskeys");
  header.appendChild(header_text);
//添加快捷键标题到网页
  document.body.appendChild(header);
//添加快捷键列表到网页中
  document.body.appendChild(list);
}
addLoadEvent(displayAccesskeys);
```


    基本快捷键约定俗成
    accesskey = "1" 返回本网页主页
    accesskey = "2"	退回前一个页面
    accesskey = "4"	大开本站搜索表单/页面
    accesskey = "9"	本站联系方法
    accesskey = "0"	查看本站的快捷键列表


### 综合练习6（第九章）Dom控制css样式

getNextElement（获取下一个标签节点）

```javascript
// 获取下一个标签节点
function getNextElement(node) {
  // 检测是否为标签节点
  if (node.nodeType == 1) {
    return node;
  }
  // 检测下一个紧挨着的节点
  if (node.nextSibling) {
    //递归调用
    return getNextElement(node.nextSibling);
  }
  return null;
}
```

addClass (定义添加类属性)

```javascript
// 定义添加类属性
function addClass(element, value) {
  // 如果为空给添加类
  if (!element.className) {
    element.className = value;
    // 否则追加类
  } else {
    element.className += " ";
    element.className += value;
  }
}
```

styleHeaderSiblings (为h1标签后面紧跟着的元素添加类）

```javascript
function styleHeaderSiblings() {
  // 检测是否能获取标签
  if (!document.getElementsByTagName) return false;
  // 获取标题
  var headers = document.getElementsByTagName("h1");
  // 获取h1后面紧跟着的元素
  for (var i = 0; i < headers.length; i++) {
    // 获取h1的元素节点
    var elem = getNextElement(headers[i].nextSibling);
    // 添加类属性
    addClass(elem, "intro");
  }
}
addLoadEvent(styleHeaderSiblings);
```

highlightRows(鼠标悬浮加粗)

```javascript
function highlightRows() {
  // 检测能否获取标签
  if (!document.getElementsByTagName) return false;
  // 获取表格
  var rows = document.getElementsByTagName("tr");
  // 循环绑定事件
  for (var i = 0; i < rows.length; i++) {
    // 鼠标悬浮设置加粗
    rows[i].onmouseover = function () {
      this.style.fontWeight = "bold";
    }
    // 鼠标移开设置普通
    rows[i].onmouseout = function() {
      this.style.fontWeight = "normal";
    }
  }
}
addLoadEvent(highlightRows);
```

