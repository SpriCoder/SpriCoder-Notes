01-浏览器原理
---

<!-- TOC -->

- [1. 浏览器的渲染原理](#1-浏览器的渲染原理)
  - [1.1. 浏览器架构](#11-浏览器架构)
  - [1.2. 渲染流程](#12-渲染流程)
    - [1.2.1. 基本概念](#121-基本概念)
    - [1.2.2. 过程](#122-过程)
  - [1.3. DOM解析](#13-dom解析)
  - [1.4. CSS解析](#14-css解析)
  - [1.5. Reflow/Layout过程](#15-reflowlayout过程)
    - [1.5.1. 布局的过程](#151-布局的过程)
    - [1.5.2. Dirty bit系统](#152-dirty-bit系统)
  - [1.6. Repaint 和 Reflow](#16-repaint-和-reflow)
  - [1.7. ⽤JS完成交互](#17-js完成交互)
    - [1.7.1. script in html](#171-script-in-html)
    - [1.7.2. script in js file](#172-script-in-js-file)
    - [1.7.3. async](#173-async)
  - [1.8. 参考文献](#18-参考文献)

<!-- /TOC -->

# 1. 浏览器的渲染原理

## 1.1. 浏览器架构
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Software-Engineering-and-Computing-II/img/web/1.png)

1. Broswer Engineer:浏览操作，选择等等

## 1.2. 渲染流程
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Software-Engineering-and-Computing-II/img/web/2.png)

### 1.2.1. 基本概念
1. DOM(Document Object Model) Tree: 由HTML文件parse生成代表内容的树状结构。
2. CSSOM(CSS Object Model) Tree: 由CSS代码parse生成的样式负责的树种结构。
3. Render Tree:包含显示属性(颜色和大小的长方形组成的树状结构)

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Software-Engineering-and-Computing-II/img/web/3.png)

### 1.2.2. 过程
1. parse：parse HTML/SVG/XHTML文件，生成DOM Tree:Parse CSS文件生成CSS Rule Tree
2. construct:DOM树和CSS规则树连接在一起construct形成Render Tree(渲染树)
3. reflow/layout：计算出Render Tree每个节点的具体位置。
4. paint:调用系统图形API，通过显卡，将Layout后的节点内容分别呈现在屏幕上。

## 1.3. DOM解析
```html
<html>
<head>
    <title>Web page parsing</title>
</head>
<body>
    <div>
        <h1>Web page parsing</h1>
        <p>This is an example Web page.</p>
    </div>
</body>
</html>
```
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Software-Engineering-and-Computing-II/img/web/4.png)

## 1.4. CSS解析
```html
<doc> 
<title>A few quotes</title>
<para>
    Franklin said that <quote>"A penny saved is a penny earned."</quote>
</para>
<para>
    FDR said <quote>"We have nothing to fear but <span>fear itself.</span>"
</quote>
</para>
</doc>
```
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Software-Engineering-and-Computing-II/img/web/5.png)

```css
/* rule 1 */ doc { display: block; text-indent: 1em; }
/* rule 2 */ title { display: block; font-size: 3em; }
/* rule 3 */ para { display: block; }
/* rule 4 */ [class="emph"] { font-style: italic; }
```
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Software-Engineering-and-Computing-II/img/web/6.png)

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Software-Engineering-and-Computing-II/img/web/7.png)

## 1.5. Reflow/Layout过程

### 1.5.1. 布局的过程
1. parent渲染对象决定它的宽度
2. parent渲染对象读取chilidren，并：
   1. a. 放置child渲染对象(设置它的x和y)
   2. b. 在需要时(它们当前为dirty或是处于全局layout或者其他原因)调⽤child渲染对象的layout，这将计算child的⾼度
3. parent渲染对象使⽤child渲染对象的累积⾼度，以及margin和padding的⾼度来设置⾃⼰的高度
－这将被parent渲染对象的parent使⽤
4. 将dirty标识设置为false

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Software-Engineering-and-Computing-II/img/web/8.png)

1. The output of the layout process is a "box model," which precisely captures the exact position and size of each element within the viewport: all of the relative measurements are converted to absolute pixels on the screen. 布局过程的输出是一个"盒子模型"，它精确地捕获了视口中每个元素的确切位置和大小：所有相对测量值都转换为屏幕上的绝对像素。
    1. The "Layout" event captures the render tree construction, position, and size calculation in the Timeline. "布局"事件捕获时间轴中的渲染树构造，位置和大小计算。
    2. When layout is complete, the browser issues "Paint Setup" and "Paint" events, which convert the render tree to pixels on the screen. 布局完成后，浏览器将发出" Paint Setup"和" Paint"事件，这些事件会将渲染树转换为屏幕上的像素。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Software-Engineering-and-Computing-II/img/web/9.png)

### 1.5.2. Dirty bit系统
1. 为了不因为每个⼩变化都全部重新布局，浏览器使⽤⼀个dirty bit系统，⼀个渲染对象发⽣了变化
或是被添加了，就标记它及它的children为dirty——需要layout。存在两个标识——dirty及children are
dirty，children are dirty说明即使这个渲染对象可能没问题，但它⾄少有⼀个child需要layout。

## 1.6. Repaint 和 Reflow
1. Repaint——屏幕的⼀部分要重画，⽐如某个CSS的背景⾊变了。但是元素的**几何尺⼨没有变**。
2. Reflow——意味着元件的**几何尺⼨变了**，我们需要重新验证并计算Render Tree。是Render Tree 的⼀部分或全部发⽣了变化。这就是Reflow，或是Layout。(**HTML使⽤的是flow based layout，也就是流式布局，所以，如果某元件的⼏何尺⼨发⽣了变化，需要重新布局，也就叫 reflow**)reflow 会从这个root frame开始递归往下，依次计算所有的结点⼏何尺⼨和位置，在reflow过程中，可能会增加⼀些frame，⽐如⼀个⽂本字符串必需被包装起来。

## 1.7. ⽤JS完成交互

### 1.7.1. script in html
```html
<!DOCTYPE html>
<html>
 <head>
    <meta name="viewport" content="width=device-width,initial-scale=1">
    <link href="style.css" rel="stylesheet">
    <title>Critical Path: Script</title>
 </head>
 <body>
    <p>Hello <span>web performance</span> students!</p>
    <div><img src="awesome-photo.jpg"></div>
    <script>
        var span = document.getElementsByTagName('span')[0];
        span.textContent = 'interactive'; // change DOM text content
        span.style.display = 'inline'; // change CSSOM property
         // create a new element, style it, and append it to the DOM
        var loadTime = document.createElement('div');
        loadTime.textContent = 'You loaded this page on: ' + new Date();
        loadTime.style.color = 'blue';
        document.body.appendChild(loadTime);
    </script>
 </body>
</html>
```
1. This can cause the browser significant delays in processing and rendering the page on the screen: 这可能会导致浏览器在处理和呈现屏幕上的页面时出现严重的延迟：
   1. The location of the script in the document is significant. 脚本在文档中的位置很重要。
   2. When the browser encounters a script tag, DOM construction pauses until the script finishes 当浏览器遇到脚本标记时，DOM构建将暂停，直到脚本完成
   3. executing.
   4. JavaScript can query and modify the DOM and the CSSOM.javaScript可以查询和修改DOM和CSSOM。
   5. JavaScript execution pauses until the CSSOM is ready JavaScript执行暂停，直到CSSOM准备就绪
2. JS可以修改DOM树和GUI
3. 直接修改DOM树是一个比较重的操作

### 1.7.2. script in js file
```html
<!DOCTYPE html>
<html>
 <head>
    <meta name="viewport" content="width=device-width,initial-scale=1">
    <link href="style.css" rel="stylesheet">
    <title>Critical Path: Script External</title>
 </head>
 <body>
    <p>Hello <span>web performance</span> students!</p>
    <div><img src="awesome-photo.jpg"></div>
    <script src="app.js"></script>
 </body>
</html>
```
```js
//app.js
var span = document.getElementsByTagName('span')[0];
span.textContent = 'interactive'; // change DOM text content
span.style.display = 'inline'; // change CSSOM property
// create a new element, style it, and append it to the DOM
var loadTime = document.createElement('div');
loadTime.textContent = 'You loaded this page on: ' + new Date();
loadTime.style.color = 'blue';
document.body.appendChild(loadTime);
```

### 1.7.3. async
1. JS是一个异步的调用
2. Adding the async keyword to the script tag tells the browser not to block DOM construction while it waits for the script to become available, which can significantly improve performance. 在脚本标签中添加async关键字可以告诉浏览器在等待脚本可用之前不要阻止DOM的构建，这可以显着提高性能。
```html
<!DOCTYPE html>
<html>
 <head>
    <meta name="viewport" content="width=device-width,initial-scale=1">
    <link href="style.css" rel="stylesheet">
    <title>Critical Path: Script External</title>
 </head>
 <body>
    <p>Hello <span>web performance</span> students!</p>
    <div><img src="awesome-photo.jpg"></div>
    <script src="app.js" async></script>
 </body>
</html>
```

## 1.8. 参考文献
1. <a href = "https://developers.google.com/web/fundamentals/performance/critical-rendering-path/render-tr ee-construction?hl=en">参考一</a>
2. <a href = "https://kb.cnblogs.com/page/129756/">参考二</a>