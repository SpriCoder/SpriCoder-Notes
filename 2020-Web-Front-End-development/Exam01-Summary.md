Exam01-Summary
---

# 1. 基础知识

## 1.1. Internet
Internet是在一个通信网络中连接的计算机的大规模集合，通过装置连接起来，相互之间可以通信。

### 1.1.1. IP
根据端到端的设计原则，IP只为主机提供一种无连接、不可靠的、尽力而为的数据包传输服务。

### 1.1.2. URI、URL、URN
1. 统一资源定位符(Uniform/Universal' Resource Locator, URL)用于标识Internet 中的文档(资源)。Internet 中有许多不同类型的资源，可以通过不同格式的URL标识它们。
2. URI(统一资源标识符，Uniform Resource Identifier)允许资源驻留在Internet上的任何位置
3. URL(统一资源定位符，Uniform Resource Locator)显示资源副本的位置
4. URN(统一资源名称，Uniform Resource Name)是资源的唯一名称
5. URL、URN是URI的子集，其中URL和URN有交集。

### 1.1.3. DNS
1. DNS之前，转换是通过FTP到中央服务器上下载hosts.txt文件
2. DNS(Domain Name System)是一个分布式数据库，本地负责控制整个数据库的部分段，客户向DNS服务器请求，得到从域名到IP地址的转化。
3. 组成
   1. 解析器：保存该网络中所有域名和IP地址映射关系的服务器，并将域名转换为IP地址。
   2. 域名解析：将域名解析成IP地址的过程。
4. 工作过程：
   1. 客户向域名服务器发起查询请求
   2. 域名服务器本地查询结果
      1. 如果找到，则返回
      2. 如果未找到则发送到根域名服务器，根域名服务器查询根域名解析，将包含下一级域名信息的DNS地址返回给客户的域名服务器。
   3. 客户的域名服务器根据根域名服务器解析的地址访问下一级DNS，如此递归逐级查询，直到找到位置。
   4. 客户的域名DNS服务器将查询结果返回客户机。
   5. 客户根据IP地址访问目标机。

### 1.1.4. Http1.1、/2、/3协议
| 阶段    | 描述                                                                         |
| ------- | ---------------------------------------------------------------------------- |
| HTTP1.0 | 非持续连接，2个RTT时间，使用TCP链接                                          |
| HTTP1.1 | 支持持久连接，在相同TCP上通讯；支持流水线，可以不等反馈发送很多信息          |
| HTTP2.0 | 支持HTTP1.1，在数据如何封装成帧上有区别，降低了request传输次数，对其多路传输 |
| HTTP3.0 | 和HTTP2完全不同，使用UDP协议，通过重传保证效率                               |


## 1.2. 网络机器人
1. 网络爬虫是以自动方式爬取万维网上信息的计算机程序；主要是用来从网页搜集信息/支持搜索引擎/开展数据分析等等；特点
   1. 分布式
   2. 可扩展
   3. 效率高
   4. 性能强
   5. 实时性
2. 网站会给出URL/robots.txt，说明哪些 URL 是可以被抓取的，连接限制
   1. 传统爬虫：传统爬虫从一个或若干初始网页的 URL 开始，获得初始网页上的 URL ，在抓取网页的过程中不断从当前页面上抽取新的 URL 放入队列 直到满足系统的一定停止条件
   2. 聚焦爬虫：聚焦爬虫是一个自动下载网页的程序，它根据既定的抓取目标，有选择的访问万维网上的网页与相关的链接，获取所需要的信息。与通用爬虫
3. 必要性：传统的搜索引擎的局限性
   1. 不同领域、不同背景的用户往往具有不同的检索目的和需求，通用搜索引擎所返回的结果包含大量用户不关心的网页大量用户不关心的网页
   2. 通用搜索引擎的目标是尽可能大的网络覆盖率，有限的搜索引擎服务器资源与无限的通用搜索引擎的目标是尽可能大的网络覆盖率，有限的搜索引擎服务器资源与无限的网络数据网络数据资源之间的矛盾将进一步加深资源之间的矛盾将进一步加深
   3. 万维网数据形式的丰富和网络技术的不断发展，图片、数据库、音频万维网数据形式的丰富和网络技术的不断发展，图片、数据库、音频//视频多媒体等不同数据大视频多媒体等不同数据大量出现，通用搜索引擎往往对这些信息含量密集且具有一定结构的数据无能为力，不能很好量出现，通用搜索引擎往往对这些信息含量密集且具有一定结构的数据无能为力，不能很好地地发现和获取发现和获取
   4. 通用搜索引擎大多提供基于关键字的检索，难以支持根据语义信息提出的查询通用搜索引擎大多提供基于关键字的检索，难以支持根据语义信息提出的查询

## 1.3. web

### 1.3.1. Web的发展
1. Web x.0表示 的是一个阶段，是促成这个阶段的各种技术和相关产品服务的一个称呼
2. Web1.0是以**编辑**为特征，网站提供给用户的内容是**网站**编辑进行编辑处理后提供的，用户阅读网站提供的内容。这个过程是**网站到用户的单向行为**，比如搜狐等，静态网页为主。
3. Web2.0则是以加强了**网站与用户**之间的互动，网站内容基于**用户**提供，网站的诸多功能也由**用户参与建设**，实现了网站与用户**双向的交流与参与**，比如博客中国等。
4. web3.0是以**主动性、数字最大化、多维化**等为特征的，以**服务**为内容的第三代互联网系统。

### 1.3.2. Web前端的发展趋势
1. 静态页面 到 动态页面
2. Ajax 到 JIT，REST，SPA等改善
3. 交互、UI、逻辑 到 Nodejs大前端、同构（同一份代码在浏览器端和服务器端都可以运行）趋势

### 1.3.3. MEAN
1. Mean：Mongo Express Angular Node，是一个Javascript平台的现代Web开发框架总称
   1. MongoDB是一个使⽤JSON风格存储的数据库，⾮常适合javascript。(JSON是JS数据格式)
   2. ExpressJS是一个Web应用框架，提供有帮助的组件和模块帮助建立一个网站应用。
   3. AngularJS是一个前端MVC框架。
   4. Node.js是一个**并发异步**事件驱动的Javascript服务器后端开发平台。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Web-Front-End-development/img/exam1/3.png)

# 2. 浏览器端

## 2.1. HTML/XHTML
1. HTML：标记语言(物理标记：与显示相关，逻辑标记)，结构化特征。
2. <a href = "https://www.cnblogs.com/web-wjg/p/7240985.html">优雅降级与渐进增强</a>
   1. 优雅降级(Graceful Degradation)：一开始就构建站点的完整功能，然后针对浏览器测试和修复。比如一开始使用 CSS3 的特性构建了一个应用，然后逐步针对各大浏览器进行 hack 使其可以在低版本浏览器上正常浏览。
   2. 渐进增强(Progressive Enhancement)：一开始就针对低版本浏览器进行构建页面，完成基本的功能，然后再针对高级浏览器进行效果、交互、追加功能达到更好的体验。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Web-Front-End-development/img/exam1/11.png)

### 2.1.1. 结构、表现、行为
1. 结构：DOCTYPE、Head、Body
2. // PPT
3. 去掉或样式丢失的时候能让页面呈现清晰的结构 
4. 屏幕阅读器(如果访客有视障)会完全根据你的标记来"读"你的网页.
5. PDA、手机等设备可能无法像普通电脑的浏览器一样来渲染网页(通常是因为这些设备对CSS的支持较弱).
6. 搜索引擎的爬虫也依赖于标记来确定上下文和各个关键字的权重.
7. 你的页面是否对爬虫容易理解非常重要,因为爬虫很大程度上会忽略用于表现的标记,而只注重语义标记. 
8. 便于团队开发和维护

### 2.1.2. 基本语法、常用标记
// PPT

### 2.1.3. html语义化
1. 根据结构化内容选择合适标签
   1. 是被功能区域/使用结构标签
   2. 将内容和功能展示分离
      1. CSS文件可以有更多样式
      2. 考虑重置式样式表
      3. 考虑用于布局的网格系统
   3. 考虑替代布局
2. 为什么？
   1. 有利于SEO(Search Engine Optimization)
   2. 开发维护体验好
   3. 用户体验好
   4. 更好的可访问性，方便任何设备对代码解析。

### 2.1.4. html5 新特性
1. 语义化的元素
2. 输入验证简化功能：`<input type=email required>`
3. 语法简化：简化了解析的标题`<!DOCTYPE html>`
4. 统一：在所有的语言中工作。
5. 减少对外部插件的需求(比如 Flash)：支持很多复杂的特性(视频音频图像)插件可能安装失败、被禁用、被屏蔽，或者成为被攻击的对象。
6. 默认的安全性：HTML为iframe元素添加了sandbox属性，防止不信任的Web页面某些操作。
7. 应用缓存：在浏览器中存储信息，而不是在cookie中，包含在每一个request中。
8. 平滑降级：旧浏览器中新的表单控件会**平滑降级**，将input $\rightarrow$ text
9. 不建议过多的使用div，因为其是无语言元素
10. audio&video标签
11. Canvas 像素级操作，放大缩小会变形
12. SVG 矢量量图，伸缩时细节不会发生变化，基于xml
13. 更多取代脚本的标记
14. 新元素：article section footer nav mark
15. 更优秀的错误处理
16. HTML5 应该独立于设备
17. 开发进程应对公众透明

## 2.2. CSS
$css \rightarrow css2 \rightarrow css2.1 \rightarrow css3$

1. 样式表的三个层次，按照从底层到高层的顺序，分别为
   1. 行内样式表:行内样式表位于开始标签中，只能够作用于单个标签的内容
   2. 文档样式表:文档样式表位于文档的头部领域，文档样式表则能够对文档的整个主体起作用
   3. 外部样式表:外部样式表是独立存储的，可以应用到任意数目文档的主体中，需要使用外部样式表的XHTML文档必须在本文档中指定所需的外部样式表。外部样式表可以独立创建为一个文本文件，文件的MIME类型为text/css。这些文件可以存储在Web中的任何计算机中。
2. 浏览器能够像获取其他文档那样米获取样式表文件。标签`<link>`用于指定外部样式表。
3. css由选择器+声明块组成。

### 2.2.1. why
1. **可分离性**：这个从文档中分离出文档的样式，保证CSS文档更小
2. **易维护性**：更便于维护和避免重复。
3. **可复用性**：可以使用相同的内容加以不同的样式实现不同的目的。
4. **访问时间**：使用类选择器节省用户访问时间。

### 2.2.2. CSS 2.1，3新特性
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Web-Front-End-development/img/exam1/4.png)

1. CSS 2.1：选择器、媒体类型、盒模型、视觉效果、产生内容、tables、分级媒体。
2. CSS 3：模块化、使用特定于浏览器的前缀、显著提高性能，比如圆角等。

### 2.2.3. CSS盒模型
1. 几乎所有的文档元素都可以具有边框。这些边框有各种不同的样式，如颜色和宽度等。
   1. 可以指定元素内容与其边框之间的距离，即内边距(padding)
   2. 还可以指定元素边框与其相邻元素之间的距离，即外边距(margin)
   3. 填充border

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Web-Front-End-development/img/exam1/1.png)

2. 元素总宽度 $=width + border_{left} + border_{right} + magin_{left} + magin_{right} + padding_{left} + padding_{right}$
3. 元素总高度 $=height + border_{top} + border_{bottom} + magin_{top} + magin_{bottom} + padding_{top} + padding_{bottom}$

### 2.2.4. 响应式网页设计，主要手段
1. 响应式网页设计(RWD，Responsive Web Design)，可以自动识别屏幕宽度、并作出相应调整网页，指页面布局(流式网格)，目标是解决设备多样化问题。
2. 优点：网站可用性大大提升、简化服务器端、易维护、只提供给搜索引擎一个入口、可支持未知设备。
3. 缺点：兼容设备导致性能低下、代码冗余(加载时间变长)，限制应用复杂性(折衷的设计方案)、用户混淆(改变了网站布局)
4. 主要手段：
   1. CSS媒体查询(不同屏幕分辨率，不同CSS规则)
   2. 网页头部添加viewport标签(控制窗口宽度)
   3. 不使用绝对大小，而使用相对大小:`width:20%/auto`、`px/em`
   4. 流动布局
   5. 图片自动缩放
   6. 渐进坚强
   7. 服务端组件的响应式设计

### 2.2.5. 优先级顺序和继承关系
1. 优先级顺序：
   1. 浏览器自带
   2. 外部link链接，`tag & @import`
   3. Style标签引入的CSS样式表
   4. 内联在HTML中，以`style`标签提供的
2. !important > ID > class > 元素选择器
3. 外联样式优先级低于内联样式
4. 内联样式优先级低于行间样式
5. 更多参考(重要)：<a href = "https://www.cnblogs.com/wangmeijian/p/4207433.html">css优先级计算规则</a>
6. 继承关系：TODO

### 2.2.6. 布局
1. Flex、Float和Grid
2. 圣杯布局：三列布局，中间宽度自适应，两边定宽；中间栏要在浏览器中优先展示渲染；允许任意列的高度最高实现：父元素设置padding，子元素三栏float：left, position：relative相对定位，负margin，main设置width：100%
3. 双飞翼布局：功能与圣杯相同，实现方式不同双飞翼布局比圣杯布局多使用了1个div，少⽤⼤致4个css属性(圣杯布局container的 padding-left和padding-right这2个属性，加上左右两个div⽤相对布局position: relative 及对应的right和left共4个属性，；⽽双飞翼布局⼦div里用margin-left和margin-right共2 个属性，比圣杯布局思路更直接和简洁⼀点。简单说起来就是：双⻜翼布局比圣杯布局多创建了⼀个div，但不⽤相对布局了。
4. flex弹性布局：首先将container块设置为⼀个Flex容器：display:flex 通过order属性设置排列顺序，数字越小越靠前，通过项目属性flex-grow设置main的放⼤比例，将空余的空间⽤main来填充，使三个项目不满一整行；默认为0，也就是对剩余空间不做处理 通过项目属性flex-basis 设置left和right的固定宽度

## 2.3. javascript 重要

### 2.3.1. 基本语法
> 可以写在body中、head中或外部文件中

```html
<!-- body -->
<body>
   <script>
      document.write("<h1>This is a heading</h1>");
      document.write("<p>This is a paragraph.</p>");
   </script>
</body>
<!-- head -->
<head>
   <script>
      function myFunction(){
         document.getElementById("demo").innerHTML="My First JavaScript Function";
      }
   </script>
</head>
<!-- 外部文件 -->
<script src="url" type="text/javascript">
   ! script commands and comments
</script>
```

1. JavaScript 拥有动态类型：这意味着相同的变量可用作不同的类型

### 2.3.2. 严格模式
1. 脚本或函数头使用添加`use strict;`的目的是指代码在严格条件下执行。
2. 为什么使用严格模式
   1. 消除js语法的一些不合理、不严谨的地方，减少怪异的行为
   2. 消除代码运行的不安全
   3. 提供编译器效应，增加运行效率
   4. 为未来版本的js做好铺垫
3. 严格模式限制：
   1. 变量必须声明后使用
   2. 函数参数不可以同名
   3. 不可以使用<a href = "https://blog.csdn.net/zwkkkk1/article/details/79725934">with</a>语句
   4. 不能对只读属性赋值
   5. 不能使用前缀0表示八进制
   6. 不可以删除不可删除属性
   7. 不可以使用delete prop删除变量，啊只能删除属性delete global[prop]
   8. eval不会从它的外层作用于引入变量
   9. eval和arguments不可以被重新赋值
   10. arguments不会自动反应函数参数变化
   11. 不能使用arguments`.callee`和`.caller`
   12. 禁止`this`指向全局对象
   13. 不能使用fn`.caller`和`.arguments`获取函数调用的堆栈
   14. 增加了保留字`protected`、`static`和`interface`

### 2.3.3. "first-class" functions
1. 头等函数(first-class function)是指在程序设计语言中，函数被当作头等公民。
2. 函数可以作为别的函数的参数、函数的返回值，赋值给变量或存储在数据结构中。在这样的语言中，函数的名字没有特殊含义，它们被当作具有函数类型的普通的变量对待。

### 2.3.4. 事件驱动编程
1. 正常调用函数

```html
<head>
   <script>
      function changetext(id){
         id.innerHTML="谢谢!";
      }
   </script>
</head>
<body>
   <h1 onclick="changetext(this)">请点击该文本</h1>
</body>
```

2. 事件驱动：onmouseover，onmouseout，onClick

```html
<div onmouseover="mOver(this)" onmouseout="mOut(this)">把鼠标移到上面</div>
<script>
   function mOver(obj){
      obj.innerHTML="谢谢"
   }
   function mOut(obj){
      obj.innerHTML="把鼠标移到上面"
   }
</script>
```

3. JS 是采用事件驱动的机制来响应用户操作的，也就是说当用户对某个 html 元素进行操作的时候，会产生一个事件，该事件会**驱动某些函数**来处理。在事件驱动的应用程序中，通常有一个主循环侦听事件，然后在检测到其中一个事件时触发回调函数。
   1. **松耦合的交互**，事件发布者和订阅者无须知道对方的存在。
   2. **多对多**的关系，多个事件发布者对应多个订阅者。
   3. 一个个事件发布出来，针对这些事件作出响应，这就是一个**业务场景**，每个步骤清晰自然。
   4. **事件发布可以带参数，事件处理者可以拿到关于该事件的任何数据**。
```js
$().trigger("advanced_search_load_complete");
$().bind("advanced_search_load_complete", function(){ ... });
```

### 2.3.5. 面向对象
1. 用JavaScript实现类JavaScritpt没有专门的机制实现类，这里是借助**它的函数允许嵌套**的机制来实现类的。一个函数可以包含变量，又可以包含其它函数，这样，变量可以作为属性，内部的函数就可以作为成员方法了。因此外层函数本身就可以作为一个类了。
2. 类声明：`function myClass() { //此处相当于构造函数 }`，这里 myClass就是一个类。其实可以把它看成类的构造函数。至于非构造函数的部分，以后会详细描述。
3. 类新建：`var obj1 = new myClass();`，JavaScript提供了一个方法可以获得对象实例。即new操作符。其实JavaScript中，类和函数是同一个概念，当用new操作一个函数时就返回一个对象。
4. 对象的成员的引用在JavaScript中引用一个类的属性或方法的方法有以下三种。
   1. 点号操作符：这是一种最普遍的引用方式，就不累赘。即如下形式：`对象名.属性名; 对象名.方法名;`
   2. 方括号引用：JavaScript中允许用方括号引用对象的成员。如下：`对象名["属性名"]; 对象名["方法名"];`
      1. 这里方括号内是代表属性或方法名的字符串，不一定是字符串常量。也可以使用变量。这样就可以使用**变量**传递属性或方法名。为编程带来了方便。在某些情况下，代码中不能确定要调用那个属性或方法时，就可以采用这种方式。否则，如果使用点号操作符，还需要使用条件判断来调用属性或方法。
      2. 另外，使用方括号引用的属性和方法名还可以以**数字**开头，或者出现**空格**，而使用点号引用的属性和方法名则遵循标示符的规则。但一般不提倡使用非标示符的命名方法。
   3. 迭代器遍历：`for item in obj`
5. prototype属性：每个构造函数有一个`prototype`属性，指向另一个对象，这个对象的所有属性和方法会被构造函数继承。

```js
// 每个实例对象的type和eat都是一样的，每次生成一些示例其实是重复的内容，多占用内存
functlon Cat(name,color){
   this.name = nane;
   this.color = color;
   this.type = "猫科动物";
   this.eat = function(){alert("吃老鼠");
};
// 使用prototype属性
function Cat(name ,color){
   this.name = name;
   this.color = color ;
)
Cat.prototype.type = "猫科动物";
Cat.prototype.eat = function(){alert("吃老鼠");
```

### 2.3.6. 匿名函数
1. 匿名函数就是声明一个函数不起名字。
2. 如果匿名函数只要一处调用，那么在调用处声明，调用完就销毁了

```js
// 例子1：声明方式1
$("div").each(function(index){alert(this)})
// 例子1：声明方式2：f1就是匿名函数
var f1 = function(index){alert(this)};
$("div").each(f1);
// 例子2：声明方式1
var double = function(x){return 2 * x;}
// 例子2：声明方式2
(function(x, y){
   alert(x + y);
})(2, 3);
```

<a href = "http://www.cnblogs.com/playerlife/archive/2012/10/17/2727683.html">js匿名函数更多参考</a>

### 2.3.7. 作用域、作用域链、闭包及其用途
1. 作用域是在运行时代码中的某些特定部分中变量、函数和对象的可访问性。
   1. 最大作用：隔离变量，不同作用域下同名变量不会有冲突。
   2. ES6后出现了块级作用域
   3. 全局作用域：
      1. 最外层函数和最外层函数外声明的变量
      2. **所有未定义直接复制的变量**
      3. 所有window对象的属性
   4. 函数作用域：
      1. 只能在函数中访问
      2. 函数中可以访问全局等外部的，但是外部不可以访问内部的
      3. 块语句，如if等不会创建新的作用域
   5. 块级作用域：使用let和const声明。
      1. 函数内部声明
      2. 代码块内声明

```js
// 代码块内声明
function getValue(condition) {
   if (condition) {
      let value = "blue";
      return value;
   } else {
      // value 在此处不可用
      return null;
   }
   // value 在此处不可用
}

// 禁止重复声明
var count = 30;
let count = 40; // Uncaught SyntaxError: Identifier 'count' has already been declared

// 不会抛出错误
var count = 30;
var condition = 1;
if (condition) {
   let count = 40;
   // 其他代码
}

// 循环中的绑定块作用域的妙用，如果使用var声明i的话，就会导致i成为全局边浪
for (let i = 0; i < btns.length; i++) {
    btns[i].onclick = function () {
      console.log('第' + (i + 1) + '个')
    }
  }
```

1. 作用域链
   1. 自由变量：当前的作用域没有定义的变量，找值则需要向父级作用域查找。
   2. 自由变量的取值要谨慎:
      1. 无论函数将在哪里调用，要到创建函数的那个作用域中取

```js
// 对比例1
var x = 10
function fn() {
  console.log(x)
}
function show(f) {
  var x = 20
  (function() {
    f() //10，而不是20
  })()
}
show(fn)
// 对比例2
var a = 10
function fn() {
  var b = 20
  function bar() {
    console.log(a + b) //30
  }
  return bar
}
var x = fn(),
  b = 200
x() //bar()
```

2. 闭包是可以读取其他函数内部变量的函数

```js
function f1(){
　　var n=999;
   // 匿名函数，本质也是闭包
　　nAdd=function(){n+=1;}
   // f2闭包函数
   function f2(){
　　　alert(n);
　　}
   return f2;
}
// f1被赋值被全局变量，于是也就不会在调用结束后被垃圾回收机制回收。
var result=f1();
result(); // 999
nAdd();
result(); // 1000

// 例子1
var name = "The Window";
var object = {
　　name : "My Object",
　　getNameFunc : function(){
　　　　return function(){
           // 函数声明时，向外查找function没有找到，则再往外直接到全局
　　　　　　return this.name;
　　　　};
　　}
};
alert(object.getNameFunc()());// "The Window"

// 例子2
var name = "The Window";
var object = {
　　name : "My Object",
　　getNameFunc : function(){
       // 向上查找找到this指本object
　　　　var that = this;
　　　　return function(){
　　　　　　return that.name;
　　　　};
　　}
};
alert(object.getNameFunc()());

// 例子3
var name="XL";
var person={
   name:"xl",
   showName:function(){
      console.log(this.name);
   }
}
person.showName();//  xl
//这里是person对象调用showName方法，很显然this关键字是指向person对象的，所以会输出name

var showNameA=person.showName;
showNameA();     //输出  XL
//这里将person.showName方法赋给showNameA变量，此时showNameA变量相当于window对象的一个属性，因此showNameA()执行的时候相当于window.showNameA(),即window对象调用showNameA这个方法，所以this关键字指向window

// this和调用时有关，而不是创建时
```

3. 闭包用途
   1. 实现私有成员
   2. 保护命名空间
   3. 避免污染全局变量
   4. 变量需要长期驻留内存
4. 详细参考
   1. <a href = "https://www.cnblogs.com/fundebug/p/10535230.html">作用域、作用域链</a>
   2. <a href = "http://www.ruanyifeng.com/blog/2009/08/learning_javascript_closures.html">学习Javascript闭包(Closure)</a>
   3. <a herf = "https://www.cnblogs.com/lisha-better/p/5684844.html">JS中的this指针(详细，推荐阅读)</a>

## 2.4. DOM

### 2.4.1. XHTML/XML与DOM树

#### 2.4.1.1. XHTML/XML
1. HTML 语法要求比较松散，这样对网页编写者来说，比较方便，但对于机器来说，语言的语法越松散，处理起来就越困难，对 于传统的电脑来说，还有能力兼容松散语法，但对于许多其他设备，比如手机，难度就比较大。因此产生了由 DTD 定义规则，语法要求更加严格的XHTML。
2. 最大的变化在于文档必须是良构的，所有标签必须闭合，也就是说开始标签要有相应的结束标签。另外，XHTML中所有的标签必须小写。在XHTML中，所有的参数值，包括数字，必须用双引号括起来。

#### 2.4.1.2. DOM
1. DOM的全称是 Document Object Model，也即文档对象模型。
2. HTML DOM 定义了访问和操作 HTML 文档的标准方法。
3. 在应用程序中，基于DOM的XML分析器将一个XML文档转换成一个对象模型的集合(通常称DOM树)，应用程序正是通过对这个对象模型的操作，来实现对XML文档数据的操作

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Web-Front-End-development/img/exam1/2.png)

4. XML DOM 定义了所有 XML 元素的对象和属性，以及访问它们的方法。
5. HTML DOM 定义了所有 HTML 元素的对象和属性，以及访问它们的方法。
6. HTML DOM 是关于如何获取、修改、添加或删除 HTML 元素的标准。

### 2.4.2. DOM0，DOM2事件流(捕获、目标和冒泡)

#### 2.4.2.1. DOM0
1. 通过javascript制定事件处理程序的传统方式。就是将一个函数赋值给一个事件处理属性。第四代web浏览器出现，至今为所有浏览器所支持优点，简单且具有跨浏览器的优势。这个了解下就好，现在也比较少使用这种方式绑定事件,也不支持一些新的事件。

```js
var btn = document.getElementById("btn");
btn.onclick = function(){
   alert(this.id);
}
// 取消绑定
btn.onclick = null;
```

2. 缺点：一个事件处理程序只能对应一个处理函数。

#### 2.4.2.2. DOM2
1. DOM2事件引进了一种全新的绑定事件方法，添加了一些新的事件。现在的浏览器都支持这种绑定方式，也建议使用这种绑定方式。

```js
var btn = document.getElementById("btn");
var hander = function(){
}
// 参数：事件处理属性名称、处理函数、是否再捕获时执行事件处理函数
addEventListener("click",handler,false/true);
removeEventListener("click",handler,false/true);
```

2. DOM2级的事件规定事件流包含三个阶段
   1. 事件捕获
   2. 目标阶段
   3. 事件冒泡阶段
3. `addEventListener`添加的事件处理程序，只能通过`removeEventListener`来删除。
4. 事件冒泡，事件开始时由最具体的元素( 文档中嵌套层次最深的那个节点)接受，然后逐级向上传播到较为不具体的节点(文档)。
5. 事件捕获，父节点更早收到事件，而具体的节点最后收到事件。
6. 事件处理过程
   1. document首先接收到click事件，然后顺着DOM树逐级**向下**传递事件(也就是所谓的事件捕获)
   2. 事件最终传递到目标节点(目标阶段)
   3. 最后事件由目标节点顺着DOM树逐级向上传播回document (事件冒泡)
   4. 需要留意的是目标节点(此处为`<button>`)在捕获阶段不会接收到事件，这意味着在捕获阶段，事件的传递从document到`<html>`再到`<body>`最后到`<div id= "wrap">`后就停止了;然后就是处于目标阶段，而在事件处理中目标阶段被看做冒泡阶段的一部分。
7. 当一个 DOM 事件触发时，它不是在触发的对象上只触发一次的，而是经历上述的三个阶段，即开始从文档的根节点流向目标对象， 然后在目标对向上被触发，之后再回溯到文档的根节点。

### 2.4.3. 观察者模式
1. 察者模式定义了一种一对多的依赖关系，让多个观察者对象同时监听某一个主题对象。这个主题对象在状态上发生变化时，会通知所有观察者对象，使它们能够自动更新自己。它主要用于实现分布式事件处理系统。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Web-Front-End-development/img/exam1/5.png)

```js
/*通知所有注册的观察者对象*/
public void nodifyObservers(String newState){
   for(Observer observer:list){
      observer.update(newState);
   }
}
```

## 2.5. Ajax

### 2.5.1. RIA Rich Internet Applications 丰富互联网应用程序
1. 是一种具有近似于传统桌面应用软件系统**功能和特性**的网络应用系统。
2. RIA系统最大的**特点**是将大部分处理任务都从**用户界面端移植到客户端**，仅保留一些必要数据与服务器端进行信息交互。
3. RIA系统的特性：
   1. 运行于浏览器中，不需要额外安装支持软件
   2. 在本地运行时，受安全沙箱全程保护。
4. 优点
   1. 无需安装
   2. 容易升级
   3. 可以通过Internet/intranet轻易获得
   4. 更加丰富的用户界面
   5. 响应速度更快的用户界面
   6. 客户端/服务端 负载平衡
   7. 异步通讯
   8. 网络效率
5. 缺点
   1. 搜索引擎不可见
   2. 专有(与开放标准相反)
   3. 完整性丧失(RIA通常无法与HTML很好地融合在一起)
   4. 软件开发的复杂性(什么东西要被缓存或不缓存再客户端计算机中？)
   5. RIA体系结构打破了网页范例
   6. 受限于安全沙箱
   7. 依赖于脚本支持
   8. 客户端运行速度受限

### 2.5.2. 同步、异步通信

#### 2.5.2.1. 同步
1. 同步请求/响应通信模型中，总是浏览器(与Web服务器、应用服务器或Web应用程序相对)发起请求(通过Web用户)。接着，Web服务器、应用服务器或Web应用程序响应进入的请求。在处理同步请求/响应对期间，用户不能继续使用浏览器。
2. 基本上所有新数据都需要刷新页面

#### 2.5.2.2. 异步
1. Web用户在当前异步请求被处理时还可以继续使用浏览器。一旦异步请求处理完成，异步响应就被通信(从Web服务器、应用服务器或Web应用程序)回客户机页面。典型情况下，在这个过程中，调用对Web用户没有影响；他们不需要等候响应。
2. 交换数据但是不需要刷新页面

### 2.5.3. Ajax请求
1. 通过在后台与服务器进行少量数据交换，AJAX 可以使网页实现异步更新。这意味着可以在不重新加载整个网页的情况下，对网页的某部分进行更新。
2. 传统的网页(不使用 AJAX)如果需要更新内容，必需重载整个网页面。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Web-Front-End-development/img/exam1/6.png)

### 2.5.4. Ajax优缺点
1. 优点
   1. 更好的交互性和响应能力，使用起来更让人愉快。
   2. 由于部分渲染，减少了与Web服务器的连接。
   3. 因为只加载需要更新页面的数据，而不是刷新整个页面，所以可以节省带宽，减少网络流量。
2. 缺点
   1. 返回和刷新按钮变得无用。
   2. 为此页面添加书签将变得无用。
   3. 需要在Web浏览器上启用JavaScript。
   4. 网络延迟可能会破坏可用性。
   5. 通过AJAX加载的数据不会被任何主要的搜索引擎索引。因此，使SEO不友好。违背URL和资源定位的初衷

### 2.5.5. 安全相关，SOP，跨域

#### 2.5.5.1. 安全相关
> XSS威胁

1. 跨站脚本(Cross site scripting，通常简称为XSS)是一种网站应用程序的安 全漏洞攻击，是代码注入的一种。 它允许恶意用户将代码注入到网页上，其他用户在观看网页时就会受到影响。指攻击者在网页中嵌入客户端脚本(例如JavaScript),当用户浏览此网页时，脚本就会在用户的浏览器上执行，从而达到攻击者的目的.这类攻击通常包含了HTML以及用户端脚本语言。
2. AJAX无法从本地存储的网页上运行，只能在存储在Web服务器上的网页上运行

#### 2.5.5.2. SOP
1. 同源政策：限制浏览器可以获取的资源，只能从同源网站获取内容(除了资源文件) 同源政策规定，AJAX请求只能发给同源的网址，否则就报错。"同源政策"越来越严格。目前，如果非同源，共有三种行为受到限制。
   1. Cookie、LocalStorage 和 IndexDB 无法读取。
   2. DOM无法获得。
   3. AJAX请求不能发送。

#### 2.5.5.3. 跨域问题
1. 当协议、子域名、主域名、端口号中任意一个不同时，都算作不同域
2. 实现跨域的方法
   1. CORS：服务器设置HTTP响应头中Access-Control-Allow-Origin值，解除跨域限制。
   2. nginx：反向代理
   3. Docker

### 2.5.6. 数据格式

#### 2.5.6.1. JSON
1. 由Douglas Crockford形式化和推广，它是一种**轻量级的、易于简化**的数据格式，使用JavaScript对象和数组文本语法编写。

#### 2.5.6.2. JSON-P JSON with Padding
1. 带填充的JSON
2. 当使用动态脚本标记插入时，JSON数据被视为另一个JavaScript文件，并作为本机代码执行。为了实现这一点，数据必须包装在回调函数中。
3. 由于JavaScript被当作本机数据来处理，因此它以本机JavaScript的速度被解析。
4. 避免使用与性能无关的JSON-P有一个原因：由于JSON-P必须是可执行的JavaScript，因此任何人都可以调用它，并使用动态脚本标记插入将其包含在任何网站中。
5. 不要在JSON-P中对任何敏感数据进行编码，因为您无法确保它保持私有，即使使用随机url或cookie。

# 3. 服务器端

## 3.1. Node.js 重要
1. Node.js是基于Chrome的JavaScript运行时构建的平台，可轻松构建快速，可扩展的网络应用程序。
2. Node.js使用事件驱动的**非阻塞I/O模型**，使其轻巧高效，非常适合**跨分布式**设备运行的数据密集型实时应用程序。

### 3.1.1. 特点，应用场景

#### 3.1.1.1. 特点
1. MVC分离
2. 现代语法和闭包使得更强大的扩展库成为可能。
3. 很多语言可以交叉编译在JS中
4. Node.js通过优化可以通过Web服务传递数据，并且仅传递数据，保证交付行为良好。
5. 支持JSON
6. 回调机制出色，避免使用线程：单线程上异步处理，而不是传统多线程
7. 适用于请求大量请求但是每个请求不需要大量计算能力的应用程序，并发问题很少。

#### 3.1.1.2. 应用场景
1. 网站
2. IM即时聊天
3. API
4. HTTP代理
5. 前端构建工具(脚手架)
6. 操作系统(NodeOS)
7. 跨平台打包工具
8. 小程序
9. 命令行工具
10. 反向代理

### 3.1.2. 基本原理
1. 异步I/O

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Web-Front-End-development/img/exam1/7.png)

2. 事件循环驱动

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Web-Front-End-development/img/exam1/8.png)

3. 不惜一切代价避免同步代码，因为阻塞了时间循环，意味着很多的回调。
4. 网上解释
   1. Node.js：单线程，异步I/O，事件驱动
   2. 应用程序的请求过程可以分为俩个部分：CPU运算和I/O读写
      1. CPU计算速度通常远高于磁盘读写速度，这就导致CPU运算已经完成，但是不得不等待磁盘I/O任务完成之后再继续接下来的业务。
      2. 所以I/O才是应用程序的瓶颈所在，在I/O密集型业务中，假设请求需要100ms来完成，其中99ms花在I/O上。
   3. 如果需要优化应用程序，让他能同时处理更多的请求，我们会采用**多线程**，同时开启100个、1000个线程来提高我们请求处理，当然这也是一种可观的方案。但是由于一个CPU核心在**一个时刻**只能做一件事情，操作系统只能通过将CPU切分为时间片的方法，让线程可以较为均匀的使用CPU资源。
   4. 操作系统在内核切换线程的同时也要切换线程的上下文，当线程数量过多时，时间将会被消耗在上下文切换中。所以在大并发时，多线程结构还是无法做到强大的伸缩性。那么是否可以另辟蹊径呢？！
   5. 我们先来看看单线程，《深入浅出Node》一书提到"单线程的最大好处，是不用像多线程编程那样处处在意状态的同步问题，这里没有死锁的存在，也没有线程上下文切换所带来的性能上的开销"，那么一个线程一次只能处理一个请求岂不是无稽之谈，先让我们看张图：

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Web-Front-End-development/img/exam1/9.png)

5. Node.js的单线程并不是真正的单线程，只是开启了单个线程进行业务处理(cpu的运算)，同时开启了其他线程专门处理I/O。当一个指令到达主线程，主线程发现有I/O之后，直接把这个事件传给I/O线程，不会等待I/O结束后，再去处理下面的业务，而是拿到一个状态后立即往下走，这就是"单线程"、"异步I/O"。
6. I/O操作完之后呢？Node.js的I/O 处理完之后会有一个回调事件，这个事件会放在一个事件处理队列里头，在进程启动时node会创建一个类似于While(true)的循环，它的每一次轮询都会去查看是否有事件需要处理，是否有事件关联的回调函数需要处理，如果有就处理，然后加入下一个轮询，如果没有就退进程，这就是所谓的"事件驱动"。这也从Node的角度解释了什么是"事件驱动"。在node.js中，事件主要来源于网络请求，文件I/O等，根据事件的不同对观察者进行了分类，有文件I/O观察者，网络I/O观察者。事件驱动是一个典型的生产者/消费者模型，请求到达观察者那里，事件循环从观察者进行消费，主线程就可以马不停蹄的只关注业务不用再去进行I/O等待。

# 4. 优化 重要

## 4.1. 基准测试/性能分析
1. 通过设计科学的**测试方法、测试工具和测试系统**，实现对一类测试对象的某项性能指标进行定量和可对比的测试
2. 延迟(传播、传输、处理、排队)和带宽
3. Web性能要点
   1. 延迟和带宽对Web性能的影响
   2. 传输协议(TCP)对HTTP的限制
   3. HTTP协议自身的功能和缺陷
   4. Web应用的发展趋势及性能需求
   5. 浏览器局限性和优化思路
4. 性能监控指标
   1. FP：首次绘制，页面第一次绘制的时间点：只要出现视觉变化，无论什么。
   2. FCP：首次内容绘制，完成对DOM中的一部分内容渲染的时间点：首次绘制来自DOM的内容。
   3. FMP：首次有意义绘制，页面关键元素的渲染时间，由开发者自行定义。
   4. 首屏时间：应用渲染完整个屏幕的时间。
   5. 用户可交互时间：DOMReady时间
   6. 总下载时间：页面所有资源加载完成的时间，一般统计window.onload时间，也可以是异步渲染全部完成的时间。
   7. 页面所有元素夹杂时间
   8. 第一个字节加载时间
   9. 页面渲染时间：瀑布流中两个指标Start Render和msFirstPaint
      1. Start Render：通过捕获页面加载的视频，实验室测量。
      2. msFirstPaint：是浏览器本身报告的测量。
   10. DOM元素数量
   11. 自定义指标
5. 相关工具

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Web-Front-End-development/img/exam1/10.png)


## 4.2. 基本原理
1. 浏览器核心优化策略
   1. 基于文档的优化(做法是优先获取资源，提前解析)
   2. 推测性优化(学习用户的导航模式，尝试预测用户的下一次操作，预先解析DNS、预先连接可能的目标)
2. web性能优化两个准则
   1. 消除或减少不必要的网络延迟
   2. 将需要传输的数据压缩至最少

## 4.3. 优化思路，技术，方法

### 4.3.1. 优化思路
1. 减少域名查找
2. 重用TCP连接
3. 最少次数的Http重定向
4. 使用内容分发网络
5. 避免不必要的资源请求
6. 在客户端贮藏部分资源
7. 资源传输前先压缩
8. 避免不必要的请求字节
9. 使请求和响应过程并行

### 4.3.2. 具体的优化方法
1. CSS：CSS放置在HTML顶部，减少CSS文件，避免绝对CSS。
2. Image：合适的图片大小，而不是浏览器调整
3. js：将js放在html的底部，尽量用外部js
4. 服务器优化：减少域名查找，数据压缩
5. html：标准兼容、去除空白符、结构尽量简单、做到浏览器和移动端的兼容
6. 针对HTTP1.x的优化
   1. 利用http管道
   2. 域名分片
   3. 打包资源以减少HTTP请求
   4. 父文档中嵌入小资源
2. HTTP2优化
   1. 少发数据，减少请求，减少传输数据量和不必要网络延迟，调整资源供给
   2. 每个来源一个链接(多个链接会抵消新协议中首部压缩和请求优先级的作用)，去掉不必要资源打包(不利于缓存，单个文件比较大)，利用服务器推送(充分使用缓存的机制)

# 5. 题型

## 5.1. 基本概念(所有课件中涉及的，不限于总结)

## 5.2. 简答题

## 5.3. 问答题

# 6. 补充

# 7. 正则表达式
<a href = "http://www.chinaz.com/program/2008/1020/41452.shtml">正则表达式</a>

