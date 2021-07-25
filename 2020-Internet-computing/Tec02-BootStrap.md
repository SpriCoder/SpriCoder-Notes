BootStrap
---

<!-- TOC -->

- [1. BootStrap简介](#1-bootstrap简介)
- [2. BootStrap特点](#2-bootstrap特点)
- [3. Bootstrap结构](#3-bootstrap结构)
- [4. BootStrap使用](#4-bootstrap使用)
- [5. CSS 简介－盒子模型](#5-css-简介盒子模型)
  - [5.1. Bootstrap网格系统](#51-bootstrap网格系统)
    - [5.1.1. 基本结构](#511-基本结构)
    - [5.1.2. 网格列偏移](#512-网格列偏移)
  - [5.2. 排版](#52-排版)
    - [5.2.1. 排版类](#521-排版类)
  - [5.3. 文本(代码)](#53-文本代码)
  - [5.4. 表格](#54-表格)
    - [5.4.1. 表格<tr>, <th> 和 <td> 类](#541-表格tr-th-和-td-类)
  - [5.5. BootStrap表单](#55-bootstrap表单)
    - [5.5.1. BootStrap表单控件](#551-bootstrap表单控件)
    - [5.5.2. Bootstrap按钮](#552-bootstrap按钮)
  - [5.6. BootStrap图片](#56-bootstrap图片)
  - [5.7. 布局组件](#57-布局组件)
  - [5.8. BootStrap插件](#58-bootstrap插件)

<!-- /TOC -->

# 1. BootStrap简介
1. Bootstrap 是由 Twitter 的 Mark Otto 和 Jacob 
2. Thornton 开发的，用于快速开发 Web 应用程序和网站的前端框架。
3. Bootstrap是基于 HTML、CSS、JAVASCRIPT 的前端框架，实际上是CSS样式的合集。

# 2. BootStrap特点
1. 移动设备优先：自 Bootstrap 3 起，框架包含了贯穿于整个库的移动设备优先的样式。(移动设备 > 桌面程序)
2. 浏览器支持：所有的主流浏览器都支持 Bootstrap。
3. 响应式设计：Bootstrap 的响应式 CSS 能够自适应于台式机、平板电脑和手机。
4. 容易上手：只要具备 HTML 和 CSS 的基础知识，就可以开始学习 Bootstrap。
5. 官方文档提供了Demo和样式

# 3. Bootstrap结构
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/tec02/1.png)

1. bootStrap.js包含的js操作
2. 部署网站可以使用bootstrap.min.js:可以快速加载
3. bootstrap.map：存储对应位置

# 4. BootStrap使用
1. 下载bootstrap:http://getbootstrap.com/

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/tec02/2.png)

1. 在html文档中加载bootstrap相关的文件(jquery.js、bootstrap.min.js 和 bootstrap.min.css 文件)
    + Bootstrap 所有 JavaScript 插件都依赖 jQuery，因此 jQuery 必须在 Bootstrap 之前引入， jQuery 也必须使用最新版。
2. 为了Bootstrap开发的网站对移动设备友好，确保适当的显示和触屏缩放，需要在网页的head中增加viewport meta 标签

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/tec02/3.png)

- 最上面要使用html5
- meta标签提供用户看不到的标签
  - 标签属性:
    - http-equiv:HTTP标识信息
    - name:页面描述信息
    - inital-scale：避免缩放
  - user-scalable-no：禁用缩放，常常和maxiumn-scale = 1.0 配合使用

# 5. CSS 简介－盒子模型
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/tec02/4.png)

1. 总元素的宽度=宽度+左填充+右填充+左边框+右边框+左边距+右边距
2. 总元素的高度=高度+顶部填充+底部填充+上边框+下边框+上边距+下边距
3. Margin:外边距:边框外面，透明
4. Border:内外边距之间的
5. Padding:内边距:内容周围，透明
6. content:框子内容

## 5.1. Bootstrap网格系统
1. Bootstrap包含了一个响应式的、移动设备优先的、不固定的网格系统，可以随着设备和视口大小的增加而适当的增加到最多12列
   1. 优先设计手机这种小的设备
   2. 之后适配更大的设备
2. 移动设备优先策略
   1. 内容：决定什么是最重要的
   2. 布局：优先设计更小的宽度
   3. 渐进增强：随着屏幕大小的增加而添加元素
3. 行必须放置在 .container class 内：保证内容和边距
4. 使用行来创建列的水平组
5. 内容应该放置在列内，且唯有列可以是行的直接子元素。
6. 预定义的网格类，比如 .row 和 .col-xs-4，可用于快速创建网格布局。
7. 列通过padding来创建列内容之间的间隙。该内边距是通过.rows 上的margin取负，表示第一列和最后一列的行偏移
8. 网格系统是通过指定想要横跨的12个可用的列来创建的

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/tec02/5.png)

- 第二行:3个相等的列
- 最多分为12列

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/tec02/6.png)

- 不同的前缀描述对应

### 5.1.1. 基本结构
```js
<div class="container">
    <div class="row">
        <div class="col-sm-3 col-md-6 col-lg-8" style="…">适用于手机、平板、台式电脑</div>
        <div class="col-sm-9 col-md-6 col-lg-4"></div>      
    </div>
    <div class="row"></div>
</div>
```

- 出现在更小的设备会默认使用12列

### 5.1.2. 网格列偏移
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/tec02/7.png)

- 内容左边增加*列

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/tec02/8.png)

- 两行:两列(12/6 = 2)

## 5.2. 排版
1. 内联子标题`<h3>我是标题<small>我是副标题</small></h3>`:字号更小颜色更浅
2. 列表
   1. 有序列表`<ol></ol>`
   2. 无序列表`<ul></ul>`
   3. 未定义样式列表`<ul class="list-unstyled"></ul>`
   4. 内联列表`<ul class="list-inline"></ul>`
   5. 定义列表 `<dl></dl>`
   6. 内联列表 `<dl class="dl-horizontal"></dl>`
3. 强调` <small>  <strong>  <em>`
```js
<small>本行内容是在标签内</small><br> <strong>本行内容是在标签内</strong><br>
<em>本行内容是在标签内，并呈现为斜体</em>
<br> <p class="text-left">向左对齐文本</p> 
<p class="text-center">居中对齐文本</p>
<p class="text-right">向右对齐文本</p>
<p class="text-muted">本行内容是减弱的</p>
<p class="text-primary">primary class</p>
<p class="text-success">success class</p>
<p class="text-info">info class</p>
<p class="text-warning">warning class</p>
<p class="text-danger">danger class</p>
```

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/tec02/12.png)

### 5.2.1. 排版类
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/tec02/9.png)

## 5.3. 文本(代码)
1. Bootstrap允许以两种形式显示代码：
   1. `<code>标签`
   2. `<pre>标签`：多行
2. `<p><code>&lt;header&gt;</code> 作为内联元素被包围。</p>`
3. `<header>`:作为内联元素被包围
```js
<pre> &lt;article&gt;
    &lt;h1&gt;Article Heading&lt;
/h1&gt;
&lt;/article&gt;
</pre>
```

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/tec02/10.png)

- 不常用

## 5.4. 表格
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/tec02/11.png)

1. class="table"设置内边距以及水平分割线
2. class="table-striped"在`<tbody>`内容主体上添加斑马线形式的条纹
3. class="table-bordered"表格周围增加边框
4. class="table-hover"在`<tbody>`内某一行启用鼠标悬停高亮换色
5. class="table-condensed"紧凑表格
6. 以上为特有样式

### 5.4.1. 表格<tr>, <th> 和 <td> 类
1. 上下文类，用来改变表格行或单个单元格背景颜色
2. class="active"  在行或单元格上应用悬停颜色
3. class="success" 成功
4. class="info" 信息变化
5. class="warning" 提醒
6. class="danger" 紧急/错误
7. `<div class="table-responsive"><table></div>`响应式表格，让表格水平滚动以适应小型设备(小于 768px)

## 5.5. BootStrap表单
1. 垂直表单 `<form role="form">`
2. 内联表单 `<form class="form-inline" role="form">`
3. 水平表单 `<form class="form-horizontal" role="form">`
4. `<div class="form-group">  …</div>`
5. 向所有的文本元素 `<input>`、`<textarea>` 和`<select>` 添加class ="form-control" 

### 5.5.1. BootStrap表单控件
1. 输入框:Type： text、password、datetime、datetime-local、date、month、time、week、number、email、url、search、tel、color

```js
<form role="form">
    <div class="form-group">
        <label for="name">标签</label>
        <input type="text" class="form-control" 
        placeholder="文本输入">
    </div>
</form>
```

2. 文本框textarea `<textarea class="form-control" rows="3"></textarea>`
3. 复选框Checkbox和单选框Radio
```js
<label class="checkbox">
    <input type="checkbox" id="…" value="option1"> 选项 1
</label>
```
4. 对一系列复选框和单选框使用 .checkbox-inline 或.radio-inline，控制它们显示在同一行上
5. 选择框Select
```js
<select class="form-control">
    <option>…</option>
</select>
```
6. 表单控件大小:在class中添加.input-* 和 .col-lg-*来分别控制高度和宽度: *是用来
```js
<div class="row">
    <div class="col-lg-2">
        <input class="form-control input-lg" type="text" >
    </div>
</div>
```
1. -2表示占有12个格子中的2个

### 5.5.2. Bootstrap按钮
1. 任何带有 class .btn 的元素都会继承圆角灰色按钮的默认外观
2. 提供一些选项来定义按钮样式，可用于`<a>`, `<button>`, 或`<input>` 元素上
3. 建议您在 `<button>` 元素上使用按钮 class，避免跨浏览器的不一致性问题
4. 控制按钮大小 .btn-lg/sm/xs/block
```js
<button type="button" class="btn btn-default">默认按钮</button>
<button type="button" class="btn btn-primary">原始按钮</button>
<button type="button" class="btn btn-success">成功按钮</button>
<button type="button" class="btn btn-info">信息按钮</button>
<button type="button" class="btn btn-warning">警告按钮</button>
<button type="button" class="btn btn-danger">危险按钮</button>
<button type="button" class="btn btn-link">链接按钮</button>
```

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/tec02/13.png)

## 5.6. BootStrap图片
1. .img-rounded：添加 border-radius:6px 来获得图片圆角
2. .img-circle：添加 border-radius:50% 来让整个图片变成圆形
3. .img-thumbnail：添加一些内边距(padding)和一个灰色的边框
4. `<img src="…" class="img-circle">`

## 5.7. 布局组件
1. 字体图标
2. 下拉菜单
3. 按钮组
4. 按钮下拉菜单
5. 输入框组
6. 导航元素
7. 导航栏
8. 面包屑导航
9. 分页
10. 标签
11. 徽章
12. 超大屏幕
13. 页面标题
14. 缩略图
15. 警告
16. 进度条
17. 多媒体对象
18. 列表组
19. 面板

## 5.8. BootStrap插件
1. Bootstrap 自带 12 种 jQuery 插件，扩展了功能，可以给站点添加更多的互动
2. 单独引用插件。使用 Bootstrap 的个别的 *.js 文件。一些插件和 CSS 组件依赖于其他插件。
3. 编译(同时)引用插件。使用 bootstrap.js 或压缩版的bootstrap.min.js。(不必同时引入)
4. 明确之间的关系