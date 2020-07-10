---
id: H5中的本地存储
title: H5中的本地存储
sidebar_label: H5中的本地存储
---

概念：如今网页应用越来越普遍，同时也变的越来越复杂，为了满足各种各样的需求，会经常性在本地存储大量的数据，HTML5规范提出了相关解决方案。
本地存储分为sessionStorage、localStorage 其中他们有一些共同特性：

 - 读写方便，页面刷新不丢失数据
 - 存储容量较大，sessionStorage约5M、localStorage约20M
 - 只能存储字符串，可以将对象通过JSON.stringify() 编码后存储

不同的是：

***sessionStorage生命周期为关闭浏览器窗口，在同一个窗口(页面)下数据可以共享。
 localStorage永久生效，除非手动删除（关闭页面也会存在），可以多窗口（页面）共享，同一浏览器可以共享本地存储的数据。***


**常用方法：**

 - setItem(key, value) 设置存储内容
 - getItem(key) 读取存储内容
 - removeItem(key) 删除键值为key的存储内容
 - clear() 清空所有存储内容
 
代码如下：

```
<input type="text">
<button>存</button>
<button>读</button>
<button>删</button>
<script>
    let input = document.querySelectorAll('input')[0];
    console.log(input);
    let save = document.querySelectorAll('button')[0];
    let get = document.querySelectorAll('button')[1];
    let del = document.querySelectorAll('button')[2];
    let val = input.value;
    //存
    save.addEventListener('click',()=>{
        val = input.value;
        window.sessionStorage.setItem('user',val);
        console.log(val);
    });
    //读
    get.addEventListener('click',()=>{
        console.log(window.sessionStorage.getItem('user'));
    });
    //删
    del.addEventListener('click',()=>{
        window.sessionStorage.removeItem('user',val)
    });
    //删除所有缓存
    window.sessionStorage.clear()
</script>
```
具体查看位置如图：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190330191637204.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDA4OTU0NA==,size_16,color_FFFFFF,t_70)
就这么简单。。正好项目中会用到，很开心 但是具体应用场景还不知道 暂时能想到的只有登录。。

上面是sessionStorage，localStorage用法一模一样就不啰嗦了。


**接下来是全屏：**
HTML5规范允许用户自定义网页上任一元素全屏显示，只需要两个api：

 - Node.requestFullScreen() 开启全屏显示
 - Node.cancelFullScreen() 关闭全屏显示

值得注意的是由于其兼容性原因，不同浏览器需要添加前缀
	webkit内核浏览器：webkitRequestFullScreen、webkitCancelFullScreen
	Gecko内核浏览器：mozRequestFullScreen、mozCancelFullScreen
	ms内核浏览器：msRequestFullScreen、msCancelFullScreen

其他操作：
document.fullScreen检测当前是否处于全屏（不同浏览器需要添加不同前缀，如：document.webkitIsFullScreen）
全屏伪类选择器：:full-screen、:-webkit-full-screen {}、:-moz-full-screen {}


代码如下：
```
<body>
    <div id="box" style="text-align: center">
        <img src="img/mac.png" alt="">
        <br>
        <br>
        <div style="text-align: center">
            <button id="full">全屏</button>
            <button id="cancel_full">取消全屏</button>
            <button id="is_full">当前的状态</button>
        </div>
    </div>
<script type="text/javascript" src="js/jquery-3.3.1.js"></script>
<script type="text/javascript">
    $(function () {
         let box = $('#box').get(0);
         // 1. 全屏显示
         $('#full').on('click', ()=>{
             if(box.requestFullscreen){ // 正常浏览器
                 box.requestFullscreen();
             }else if(box.webkitRequestFullScreen){ // webkit内核
                 box.webkitRequestFullScreen()
             }else if(box.mozRequestFullScreen){ // moz内核
                 box.mozRequestFullScreen()
             }else if(box.msRequestFullScreen){ // ie内核
                 box.msRequestFullScreen();
             }else {
                 box.oRequestFullScreen();
             }
         });

         // 2. 取消
        $('#cancel_full').on('click', ()=>{
            document.webkitCancelFullScreen();
        });

        // 3. 判断当前是否是全屏的状态
        $('#is_full').on('click', ()=>{
            alert(document.webkitIsFullScreen === false ? '非全屏':'全屏');
        })
    });
</script>
```
[另一位老哥的帖子写的很好...学习到了](https://blog.csdn.net/a727911438/article/details/54290931/)