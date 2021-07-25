JQuery
---

<!-- TOC -->

- [1. 简介](#1-简介)
- [2. JQuery安装](#2-jquery安装)
- [3. JQuery语法](#3-jquery语法)
- [4. JQuery事件](#4-jquery事件)
  - [4.1. $(document).ready()](#41-documentready)
  - [4.2. click()](#42-click)
  - [4.3. mousedown()](#43-mousedown)
  - [4.4. mouseup()](#44-mouseup)
  - [4.5. hover()](#45-hover)
  - [4.6. focus()](#46-focus)
  - [4.7. blur()](#47-blur)
  - [4.8. 事件绑定](#48-事件绑定)
  - [4.9. 解除事件绑定](#49-解除事件绑定)

<!-- /TOC -->

# 1. 简介
1. 简化DOM操作，AJAX调用和Event处理
2. 特点
   1. 处理DOM是容易的
   2. 多浏览器适配

# 2. JQuery安装
1. 网页中添加 jQuery 可以通过多种方法在网页中添加 jQuery。
   1. jquery.com 下载 jQuery 库。
   2. 从 CDN 中载入 jQuery, 如从 Google 中加载 jQuery。
2. 有两个版本的 jQuery 可供下载。 
   1. Production version - 用于实际的网站中，已被精简和压缩。
   2. Development version - 用于测试和开发(未压缩，是可读的代码)
3. 下载 jQuery
   1. jQuery 库是一个 JavaScript 文件，可以使用 HTML 的 `<script>` 标签引用它：
```js
<head>
<script src = "jquery-1.10.2.min.js"></script>
</head>
```

# 3. JQuery语法
1. 选择HTML元素，并对选取的元素执行某些操作
   1. 选择器`.`:class
   2. 选择器`#`:id

```js
$(selector).action()
$(this).hide() - 隐藏当前元素
$("p").hide() - 隐藏所有 <p> 元素
$("p.test").hide() - 隐藏所有 class="test" 的 <p> 元素
$("#test").hide() - 隐藏所有 id="test" 的元素
```

2. 所有 jQuery 函数位于一个 document ready 函数中，这是为了防止文档在完全加载 (就绪)之前运行 jQuery 代码，即在 DOM 加载完成后才可以对 DOM 进行操作。 如果在文档没有完全加载之前就运行函数，操作可能失败。下面是两个具体的例子：
   1. 试图隐藏一个不存在的元素。
   2. 获得未完全加载的图像的大小。

```js
$(document).ready(function(){

})
```

# 4. JQuery事件
1. 页面对不同访问者的响应叫做事件。
2. 事件处理程序指的是当 HTML 中发生某些事件时所调用的方法。
   1. 在元素上移动鼠标。
   2. 选取单选按钮。
   3. 点击元素。 

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/tec01/1.png)

## 4.1. $(document).ready()
1. $(document).ready() 方法允许我们在文档完全加载完后执行函数。之前已经介绍过了。

## 4.2. click()
1. click() 方法是当按钮点击事件被触发时会调用一个函数。 在下面的实例中，当点击事件在某个 `<p>` 元素上触发时，隐藏当前的 `<p>` 元素。 

```js
$("p").click(function(){
   $(this).hide();
})
```

## 4.3. mousedown()
1. 当鼠标指针移动到元素上方，并按下鼠标按键时，会发生 mousedown 事件。

```js
$("#p1").mousedown(function(){
   alert("鼠标在该段落上按下");
})
```

## 4.4. mouseup()
1. 当在元素上松开鼠标按钮时，会发生 mouseup 事件。

```js
$("#p1").mouseup(function(){
   alert("鼠标在该段落上松开");
})
```

## 4.5. hover()
1. hover()方法用于模拟光标悬停事件。

```js
$("#p1").hover{
   function(){
      alert("你进入了p1");
   },
   function(){
      alert("你离开了p1");
   }
}
```

## 4.6. focus()
1. 当元素获得焦点时，发生 focus 事件。
2. 当通过鼠标点击选中元素或通过 tab 键定位到元素时，该元素就会获得焦点。

```js
$("input").focus(function(){
   $(this).css("background-color","#cccccc");//修改css
})
```

## 4.7. blur()
1. 当元素失去焦点时，发生 blur 事件。
2. 点击了另一个元素

```js
$("input").blur(function(){
   $(this).css("background-color","#ffffff");//修改css
})
```

## 4.8. 事件绑定
1. 以绑定click为例
```js
$().事件名(事件处理函数) 如： $("#d").click(function(){})
$().on("事件名",事件处理函数) 如：$("#d").on("click",function(){})
$().bind("事件名",事件处理函数) 如：$("#d").bind("click",function(){})
```

## 4.9. 解除事件绑定
1. 函数写在外面，才能通过名字绑定

```js
$().unbind("事件名") 
```