Lecture06-应用层
---
1. 本节PPT包含5-7三层:
   1. The Session Layer 会话层
   2. The Presentation Layer 展示层
   3. The Application Layer 应用层

<!-- TOC -->

- [1. 第五层：The Session Layer 会话层](#1-第五层the-session-layer-会话层)
  - [1.1. 第五层的职责](#11-第五层的职责)
  - [1.2. 第五层的服务](#12-第五层的服务)
  - [1.3. 第五层设备](#13-第五层设备)
- [2. Layer 6 - The Presentation Layer 第六层 表示层](#2-layer-6---the-presentation-layer-第六层-表示层)
  - [2.1. 数据格式](#21-数据格式)
    - [2.1.1. 图形文件格式](#211-图形文件格式)
    - [2.1.2. 多媒体文件格式](#212-多媒体文件格式)
  - [2.2. 数据加密与压缩](#22-数据加密与压缩)
- [3. Layer 7:The Application Layer 应用层](#3-layer-7the-application-layer-应用层)
  - [3.1. 应用层职责](#31-应用层职责)
  - [3.2. 超文本传输协议 (HTTP，HyperText Transfer Protocol)](#32-超文本传输协议-httphypertext-transfer-protocol)
    - [3.2.1. 统一资源定位符 URL(Uniform Resource Locator)](#321-统一资源定位符-urluniform-resource-locator)
    - [3.2.2. HTTP](#322-http)
    - [3.2.3. HTTP 的报文结构(请求报文)](#323-http-的报文结构请求报文)
    - [3.2.4. HTTP 请求报文的一些方法](#324-http-请求报文的一些方法)
  - [3.3. HTML(HyperText Markup Language)](#33-htmlhypertext-markup-language)
  - [3.4. FTP(File Transfer Protocol) and TFTP(Trivial File Transfer Protocol)](#34-ftpfile-transfer-protocol-and-tftptrivial-file-transfer-protocol)
    - [3.4.1. 主进程工作步骤](#341-主进程工作步骤)
    - [3.4.2. FTP 的屏幕信息举例](#342-ftp-的屏幕信息举例)
  - [3.5. Telnet 协议](#35-telnet-协议)
  - [3.6. SMTP(Simple Mail Transfer Protocol) and POP(Post Office Protocol)](#36-smtpsimple-mail-transfer-protocol-and-poppost-office-protocol)
    - [3.6.1. MIME(Multipurpose Internet Mail Extensions) 增加 5 个新的邮件首部](#361-mimemultipurpose-internet-mail-extensions-增加-5-个新的邮件首部)
    - [3.6.2. MIME(Multipurpose Internet Mail Extensions) 和 SMTP 的关系](#362-mimemultipurpose-internet-mail-extensions-和-smtp-的关系)
  - [3.7. SNMP(Simple Network Management Protocol) 简单网络管理协议](#37-snmpsimple-network-management-protocol-简单网络管理协议)
  - [3.8. 域名系统(DNS, Domain Name System)](#38-域名系统dns-domain-name-system)
    - [3.8.1. Domain Name 域名](#381-domain-name-域名)
    - [3.8.2. TLD (Top Level Domain) TLD(顶级域)](#382-tld-top-level-domain-tld顶级域)
    - [3.8.3. Domain Name Server 域名服务器](#383-domain-name-server-域名服务器)
    - [3.8.4. 结合域名服务器查找IP地址](#384-结合域名服务器查找ip地址)
  - [3.9. 应用层:沟通的方式](#39-应用层沟通的方式)
  - [3.10. DHCP(Dynamic Host Configuration Protocol，动态主机配置协议)](#310-dhcpdynamic-host-configuration-protocol动态主机配置协议)
    - [3.10.1. DHCP概述](#3101-dhcp概述)
    - [3.10.2. DHCP过程](#3102-dhcp过程)
      - [3.10.2.1. DHCP工作过程](#31021-dhcp工作过程)
      - [3.10.2.2. 发现阶段](#31022-发现阶段)
      - [3.10.2.3. 响应阶段](#31023-响应阶段)
      - [3.10.2.4. 选择阶段](#31024-选择阶段)
      - [3.10.2.5. 租约确认阶段](#31025-租约确认阶段)
      - [3.10.2.6. 租期续约](#31026-租期续约)
      - [3.10.2.7. 租期释放](#31027-租期释放)
      - [3.10.2.8. DHCP报文结构](#31028-dhcp报文结构)
    - [3.10.3. DHCP报文类型](#3103-dhcp报文类型)
    - [3.10.4. DHCP欺骗及防范](#3104-dhcp欺骗及防范)
      - [3.10.4.1. DHCP欺骗原理](#31041-dhcp欺骗原理)
      - [3.10.4.2. DHCP欺骗攻击](#31042-dhcp欺骗攻击)
      - [3.10.4.3. DHCP欺骗防范](#31043-dhcp欺骗防范)

<!-- /TOC -->

# 1. 第五层：The Session Layer 会话层
1. TCP 控制传输，如果用户想要完成一定的数据控制，就会对应在会话层完成。

## 1.1. 第五层的职责
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec06/1.png)

1. 基于令牌进行交互发言，通过数据同步保证数据完整性(应用逻辑)
2. 进行数据分段、拼接，保证传输的有效。
3. 同步技术，保证故障恢复。

## 1.2. 第五层的服务
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec06/2.png)

1. 双向同步通讯？
   1. 全双工通信
   2. 半双工通信
   3. 单工通信
2. 双向交替控制？
   1. 会话连接、活动开始、数据校验(同步)
   2. 令牌转换等
3. 是否同步了您的会话的主题？

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec06/3.png)

1. **同步点(CheckPoint)**用于分隔会话的各个部分，以前称为对话(dialogues)
   1. 同步点:发送一定数据后设置同步点
   2. 次同步点:作为同步点的一个子集，进行数据校验
   3. 主同步点:按照主同步点进行校验确认
   4. 如果错误，恢复到上次都已经同步的主同步点
2. 对话分离(Seperation)是通信的有序启动，终止和管理
3. 尽量保证了通话的效率和可靠性。

## 1.3. 第五层设备
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec06/4.png)

1. Client-Server 客户端-服务器模式:通过会话实现

# 2. Layer 6 - The Presentation Layer 第六层 表示层
1. 表示层负责以接收**设备可以理解**的形式表示数据。
   1. 传送语法协商
   2. 接受语法协商
2. 表示层具有3个主要功能：
   1. 数据格式(format)
   2. 数据压缩(compression):早期网络比较慢，倾向于先压缩在发送
   3. 数据加密(encryption)
3. 协商编码方式可以在会话层中实现

## 2.1. 数据格式
1. 想象两个不同(dissimilar)的系统。
   1. 一种使用扩展二进制编码的十进制交换码(EBCDIC,Extended Binary Coded Decimal Interchange Code)格式化文本
   2. 另一种使用**美国信息交换标准码(ASCII)**格式化文本
   3. 选择大家都能识别的编码形式传输，保证大家都能理解

2. 第6层提供了这两种不同类型的代码之间的转换

### 2.1.1. 图形文件格式
1. 互联网通常使用两种二进制文件格式来显示图像：
   1. 图形交换格式(GIF，Graphic Interchange Format)
   2. 联合图像专家组(JPEG，Joint Photographic Experts Group)。
2. 任何具有读取器的GIF和JPEG文件格式的计算机都可以读取这些文件类型，而与计算机的类型无关。

### 2.1.2. 多媒体文件格式
1. 多媒体文件格式是另一种二进制文件，它存储声音，音乐和视频。
   1. 这些文件可以完全下载，然后播放，也可以在播放时下载。
   2. 后一种方法称为流音频。

## 2.2. 数据加密与压缩
1. 第6层负责数据加密：数据加密可在信息传输过程中保护信息。
2. 表示层还负责文件的压缩。

# 3. Layer 7:The Application Layer 应用层
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec06/5.png)

1. 上图中各层的一些协议和使用：对端口进行管理
2. 应用程序层(最接近用户)支持应用程序的通信组件。

## 3.1. 应用层职责
1. 确定并确定预期的通信合作伙伴的可用性
2. 同步合作的应用程序
3. 同步协作的应用
4. 建立有关错误恢复程序的协议
5. 控制数据完整性
6. 通过网络应用(network applications)为OSI模型的其余部分提供一个直接接口，或是通过独立应用提供非直接接口，如文字处理，电子表格，演示管理器(presentation managers)，网络重定向器
7. 不同应用不同情况

## 3.2. 超文本传输协议 (HTTP，HyperText Transfer Protocol) 
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec06/6.png)

1. 和电视的播放比较类似，通过浏览器界面切换内容，通过URL切换
2. 多源点传输，内容规范
3. 如何实现URL的转发:HTTP
4. 如何完成界面:html
5. 如何整合和查询:搜索引擎

### 3.2.1. 统一资源定位符 URL(Uniform Resource Locator)
1. 统一资源定位符 URL 是对可以从因特网上得到的资源的位置和访问方法的一种简洁的表示。
2. URL 给资源的位置提供一种抽象的识别方法，并用这种方法给资源定位。
3. 只要能够对资源定位，系统就可以对资源进行各种操作，如存取、更新、替换和查找其属性。
4. URL 相当于一个文件名在网络范围的扩展。因此 URL 是与因特网相连的机器上的任何可访问对象的一个指针。 
5. `<URL的访问方式>://<主机>:<端口>/<路径>`
   1. 访问方式:协议HTTPS 或者 HTTP
   2. 主机:域名的方式
   3. 端口对应进程
   4. 路径对应具体的文件

### 3.2.2. HTTP
1. HTTP 是**面向事务**的客户服务器协议。
2. HTTP 1.0 协议是**无状态**的(stateless)。
   1. 每一次请求是独立的，不记录上一次请求信息。
   2. Cookie是征求同意的存储(维持登录状态)，可以保证在多个应用之间维持登录状态。
3. HTTP 协议本身也是**无连接**的，虽然它使用了面向连接的 TCP 向上提供的服务。
4. 万维网浏览器就是一个 HTTP 客户，而在万维网服务器等待 HTTP 请求的进程常称为HTTP daemon， 有的文献将它缩写为 HTTPD。
5. HTTP daemon 在收到 HTTP 客户的请求后，把所需的文件返回给 HTTP 客户。

### 3.2.3. HTTP 的报文结构(请求报文)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec06/7.png)

1. 报文由三个部分组成，即开始行、首部行和实体主体。
2. 在请求报文中，开始行就是请求行。
3. 请求报文和应答报文的应答结构都是一样的
4. 应答码：
   1. 2xx:成功
   2. 3xx:重定向
   3. 4xx:错误
   4. 5xx:服务器内部错误

### 3.2.4. HTTP 请求报文的一些方法
| 方法(操作) | 意义                            |
| ------------ | ------------------------------- |
| OPTION       | 请求一些选项的信息              |
| GET          | 请求读取由URL所标志的信息       |
| HEAD         | 请求读取由URL所标志的信息的首部 |
| POST         | 给服务器添加信息(例如，注释)  |
| PUT          | 在指明的URL下存储一个文档       |
| DELETE       | 删除指明的URL所标志的资源       |
| TRACE        | 用来进行环回测试的请求报文      |
| CONNECT      | 用于代理服务器                  |

## 3.3. HTML(HyperText Markup Language)
1. 定义了许多用于排版的命令(标签)。
2. HTML 文档是一种可以用任何文本编辑器创建的 ASCII 码文件。
3. 仅当HTML文档是以.html或.htm为后缀时，浏览器才对此文档的各种标签进行解释。
4. 当浏览器从服务器读取HTML文档，针对HTML文档中的各种标签，根据浏览器所使用的显示器的尺寸和分辨率大小，重新进行排版并恢复出所读取的页面。
5. HTML用一对标签(一个开始标签和一个结束标签)或几对标签来标识一个元素。

## 3.4. FTP(File Transfer Protocol) and TFTP(Trivial File Transfer Protocol)
1. FTP是一种可靠的，面向连接的服务，它使用TCP传输文件。
   1.  FTP首先在客户端和服务器(端口21)之间建立**控制连接**
   2. 然后，建立第二个连接，这是计算机之间通过其传输数据的链接。(端口20)
2. TFTP是使用UDP的无连接服务(简化的FTP)
   1. 体积小，易于实施。更加方便
   2. 例如。 TFTP在路由器上用于传输配置文件和Cisco IOS映像
   3. 不支持交互，没有目录浏览功能
3. 互联网早期的时候，文件传输量是很大的。

### 3.4.1. 主进程工作步骤
1. 打开熟知端口(端口号为 21)，使客户进程能够连接上。(可以修改熟知端口)
2. 等待客户进程发出连接请求。
3. 启动从属进程来处理客户进程发来的请求。从属进程对客户进程的请求处理完毕后即终止，但从属进程在运行期间根据需要还可能创建其他一些子进程。
   1. 控制连接
   2. 数据连接:数据通信
   3. 需要建立上面两个连接才能完成传输
4. 回到等待状态，继续接受其他客户进程发来的请求。主进程与从属进程的处理是并发地进行。

### 3.4.2. FTP 的屏幕信息举例
```
用户要用FTP和远地主机(网络信息中心NIC上的主机)建立连接。域名:nic.ddn.mil
[01] ftp nic.ddn.mil
本地FTP发送的连接成功信息
[02] connected to nic.ddn.mil
从远地服务器返回的信息，220表示"服务就绪"
[03] 220 nic FTP server (Sunos 4.1)ready.
本地FTP提示用户键入名字。用户键入的名字表示"匿名"。用户只需键入anonymous即可(匿名)
[04] Name: anonymous
数字331表示"用户名正确"，需要口令
[05] 331 Guest login ok, send ident as password.
本地FTP提示用户键入口令。用户这时可键入guest作为匿名的口令，也可以键入自己的电子邮件地址，即耶鲁大学数学系名为xyz的主机上的abd(匿名密码是随意输入的)
[06] Password: abc@xyz.math.yale.edu
数字230表示用户已经注册完毕
[07] 230 Guest login ok, access restrictions apply.
"ftp>"是FTP的提示信息。用户键入的是将目录改变为包含RFC文件的目录
[08] ftp> cd rfc
字符"CWD"是FTP的标准命令，表示Change Working Directory
[09] 250 CWD command successful.
用户要求将名为rfc1261.txt的文件复制到本地主机上，并改名为nicinfo(get 获取到本地)
[10] ftp> get rfc1261.txt nicinfo
字符PORT是FTP的标准命令，表示要建立数据连接。200表示"命令正确"
[11] 200 PORT command successful.
数字150表示"文件状态正确，即将建立数据连接"
[12] 150 ASCII data connection for rfc1261.txt (128.36.12.27,1401) (4318 bytes).
数字226是"释放数据连接"，现在一个新的本地文件已经生成。
[13] 226 ASCII Transfer complete. local: nicinfo remote: rfc1261.txt 4488 bytes received in 15 seconds (0.3 Kbytes/s).
用户键入退出命令。
[14] ftp> quit
表示FTP工作结束
[15] 221 Goodbye. 
```

## 3.5. Telnet 协议
1. Telnet客户端软件提供了登录到运行Telnet服务器应用程序的远程Internet主机，然后从命令行执行命令的功能。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec06/8.png)

1. 输入参数，达成一致，对服务器进行操作。
2. 不同操作系统之间的快捷键和指令是有差异的，需要进行转换。
3. 基于Telnet的标准：virtual Terminal可视标准

## 3.6. SMTP(Simple Mail Transfer Protocol) and POP(Post Office Protocol)
1. 电子邮件服务器使用SMTP发送和POP接收邮件相互通信。
   1. SMTP (Simple Mail Transfer Protocol) SMTP(简单邮件传输协议)邮件发送，登录发送等操作
   2. POP3 (Post Office Protocol version 3) 邮件接收，邮件到达邮件服务端，由客户端和服务端联系接收邮件。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec06/9.png)
![SMTP_POP](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec06/session_presentation_and_application_layer__smtp_pop.png)

>发送者先登录到服务器，通过服务器根据SMTP传输到对应的服务器，然后用户登录后通过POP3协议收邮件到本地

### 3.6.1. MIME(Multipurpose Internet Mail Extensions) 增加 5 个新的邮件首部 
1. MIME-Version: 标志 MIME 的版本。现在的版本号是 1.0。若无此行，则为英文文本。
2. Content-Description: 这是可读字符串，说明此邮件主体是否是图像、音频或视频。
3. Content-Id: 邮件的惟一标识符。
4. Content-Transfer-Encoding: 在传送时邮件的主体是如何编码的。
5. Content-Type:说明邮件主体的数据类型和子类型。

### 3.6.2. MIME(Multipurpose Internet Mail Extensions) 和 SMTP 的关系
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec06/10.png)

1. MIME标准扩充了SMTP标准
2. 很多的文件(附件)并不是ASCII码的，我们需要用MIME将对应的文件进行转换(扩充)。过程如上图

## 3.7. SNMP(Simple Network Management Protocol) 简单网络管理协议
1. 简单网络管理协议(SNMP)是一种应用程序层协议，可简化网络设备之间的管理信息交换。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec06/11.png)

2. NMS(Network Management System):网管,通过下发请求对上网的所有的主机关于流量等等信息进行管理(监控)
3. 通过管理数据库(MIB)进行信息交流
4. 使用UDP通过广播进行实现。

## 3.8. 域名系统(DNS, Domain Name System)
1. 域名系统(DNS)是网络上的服务，该服务管理域名并响应客户端将域名转换为关联IP地址的请求。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec06/12.png)

2. 早期是用IP地址以及Host文件来进行访问

### 3.8.1. Domain Name 域名
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec06/13.png)

1. 使用`.`将字符串进行分隔开，字符串不应该太长
2. 越靠后域名级别越高
3. www就是对应到主机群

### 3.8.2. TLD (Top Level Domain) TLD(顶级域)
1. 国家TLD(nTLD)
   1. .cn(CHINA) 中国
   2. .us (United States) 美国
   3. .uk (United kingdom), etc. 英国等等
2. 通用TLD(gTLD)，最早的域包括：
   1. .com Enterprises and companies 企业和公司
   2. .net Network services providers 网络服务提供者
   3. .org Nonprofit organizations 非盈利组织
   4. .edu Educational facilities 教育机构
   5. .gov Governments (only for U.S.A) 政府(美国)
   6. .mil Military facilities (only for U.S.A) 军方(美军)
   7. .int International organizations 国际组织
3. Infrastructure domain 基础设施领域
   1. Only one: arpa, for resolving domain names reversely 仅一个：arpa，用于反向解析域名
4. Recently, new TLD domain added:
   1. .aero(航空运输企业)
   2. .biz (公司和企业)
   3. .cat (加泰隆人的语言和文化团体)
   4. .coop(合作团体)
   5. .info(各种资讯)
   6. .jobs(人力资源管理者)
   7. .mobi(移动产品与服务的用户和提供者)
   8. .museum (博物馆)
   9. .name   (个人)
   10. .pro (经过认证的专业人员)
   11. .travel  (旅游业)

### 3.8.3. Domain Name Server 域名服务器
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec06/14.png)

- 顶级域名底下的域名就是由顶级域名下面进行管理
- 根域名服务器存储位置，所以子服务器知道根服务器的地址即可

### 3.8.4. 结合域名服务器查找IP地址
1. DNS系统以层次(hierarchy)结构设置，该层次结构创建不同级别的DNS服务器。
2. 此级别的DNS服务器判断其自身是否能够将域名转换为关联的IP地址：
   1. 如果可以，则将结果返回给客户端
   2. 如果没有，它将请求发送到更高级别。(向上级请求)

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec06/15.png)

- 请求分为两种:
  - 能够应答
  - 不能够应答
- 递归地进行查找:具体过程在上图
- 下面递归，上面迭代

## 3.9. 应用层:沟通的方式
1. 通信处理发生的一种方式：(无上下文，请求后就断开)
   1. 当浏览器打开时，它将连接到默认页面，并且该页面的文件将传输到客户端。
   2. 处理完成后，连接断开
2. 第二种方式：(有上下文)
   1. 作为Telnet和FTP，建立与服务器的连接并保持该连接，直到执行所有处理。
   2. 当用户确定他/她已完成时，客户端将终止连接。
3. 所有的交流活动都属于这两类之一。

## 3.10. DHCP(Dynamic Host Configuration Protocol，动态主机配置协议)
1. DHCP服务器可以是服务器

### 3.10.1. DHCP概述
1. 一个协议软件在使用之前先作正确协议配置，具体配置内容取决于协议。
2. 接到因特网的计算机的协议软件需要配置的项目包括：
   1. IP 地址
   2. 子网掩码
   3. 默认路由器的 IP 地址
   4. 域名服务器的 IP 地址
3. Dynamic Host Configuration Protocol可以高效地分配IP地址
   1. 局域网的网络协议
   2. 使用UDP来实现
4. 目前一般都是自动获取IP地址，而不需要手动去获取IP地址等信息

### 3.10.2. DHCP过程

#### 3.10.2.1. DHCP工作过程
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec06/16.png)

1. AB是两个Server
2. Client先Discover去搜索
3. Server返回一个Offer报文
4. Client选择优先返回的Offer来优先服务
5. Client进行广播，告知到底服务了谁
6. 然后B返回一个Ack报文
7. 到了时间之后，选择release或者续租
8. AB的信息不对称不同步(局域网的地址B分配完成了但是A不知道，广播里面会携带分配的地址信息，告知A进行同步)

#### 3.10.2.2. 发现阶段

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec06/17.png)

- DHCP Client开始并不知道DHCP Server的 ip 地址,因此以广播的方式发出DHCP Discover报文
- 广播携带地址是MAC地址

#### 3.10.2.3. 响应阶段

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec06/18.png)

- DHCP Server在IP地址池中查找合法的IP地址通过DHCP Offer报文提供给DHCP Client

#### 3.10.2.4. 选择阶段

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec06/19.png)

- DHCP Client选择一个DHCP Offer报文(一般 选择最先收到的DHCP Offer报文)，向网络发送一个DHCP Request广播数据包，所有的Server进行同步

#### 3.10.2.5. 租约确认阶段

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec06/20.png)

- DHCP Server接收到DHCP Request消息后，以DHCP ACK消息向DHCP Client广播成功的确认；出错则广播否定确认消息DHCP NAK

#### 3.10.2.6. 租期续约

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec06/21.png)

- 在租期中，DHCP Client直接向为其提供IP地址的DHCP Server发送DHCP Request消息，收到回应的DHCP ACK消息后，DHCP Client根据所提供的新的租期以及其它更新的 TCP/IP 参数更新自己的配置，IP租用更新完成

#### 3.10.2.7. 租期释放
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec06/22.png)

- 当DHCP Client不再需要使用分配IP地址时，就会主动向 DHCP Server发送Release报文，告知不再需要分配IP地址，DHCP Server会释放被绑定的租约
- 到时间后，Server会主动询问，如果没有应答会自动释放

#### 3.10.2.8. DHCP报文结构
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec06/23.png)

1. op:报文类型，1请求，2应答
2. HTYPE:硬件地址类型，1表示10M以太网地址
3. HLEN:以太网地址长度，10M为6
4. Hops:是否使用代理服务器进行处理

### 3.10.3. DHCP报文类型
1. DHCP Discover：发现
2. DHCP Offer：提供
3. DHCP Request：告知决定
4. DHCP ACK：租约确认
5. DHCP NAK：租约不确认
6. DHCP Release：释放租约
7. DHCP Decline:收到Ack后，Client告诉服务器不接受
8. DHCP Inform:客户端向服务器端请求详细信息

### 3.10.4. DHCP欺骗及防范

#### 3.10.4.1. DHCP欺骗原理
1. 客户端以广播的方式来寻找服务器，并且只接收第一个到达的服务器提供的网络配置参数。
2. 非授权的DHCP服务器先应答，客户端最后获得的网络参数即是非授权的，客户端即被欺骗。(恶意服务器把自己作为默认网关)
3. 在实际应用DHCP的网络中，基本上都会采用DHCP中继，因此本网络的非授权DHCP服务器一般都会先于其余网络的授权DHCP服务器的应答(由于网络传输的延迟)，在这样的应用中，DHCP欺骗更容易完成。

#### 3.10.4.2. DHCP欺骗攻击

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec06/24.png)

1. 首先PC发出请求
2. 然后将DHCP请求发送出去
3. 伪装者收到后，DHCP伪装者给出应答

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec06/25.png)

- DHCP Server也会给出应答，但是可能比伪装者慢
- 这样子A收到的就是伪装者的报文

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec06/26.png)

- A发出去的网关就是B，所以A上网的请求就发送给B，B转发给默认网关上网，然后返回信息给B
- B再把返回的信息给A
- 很隐蔽的安全问题
- 除了服务器不应该启动DHCP进程

#### 3.10.4.3. DHCP欺骗防范
1. 在交换机上启用DHCP Snooping功能 DHCP Snooping技术通过建立和维护DHCP Snooping绑定表过滤不可信任的DHCP信息:比如B的DHCP不能通过认证，交换机拒绝进行转发
   1. 在交换机的全局配置模式中启用DHCP Snooping:`switch (config)# ip dncp snooping`
   2. 在交换机的全局配置模式中开启需要启用DHCP Snooping 的VLAN":`switch (config)# ip dhcp snooping vlan vlan号`
   3. 在端口配置子模式中将授权DHCP服务器所连的端口设为信任端口(缺省都是非信任的端口):就是连接到DHCP Server的端口:`switch (config-if)# ip dhcp snooping trust`