lecture04-网络层原理与技术
---

1. 为什么我们不用硬件地址进行通信?
   1. (设备数量问题)因为设备比较多，供应商也比较多
   2. (规格问题)不同供应商的解决方案不同，所以使用硬件地址进行通信的通用性比较低。
   3. (寻址问题)全球设备太多，如果使用硬件设备，那么进行定位比较复杂
2. 因为如上情况我们选择使用IP地址(逻辑地址)。
3. 本章比较重要，期末占比会比较大。

<!-- TOC -->

- [1. 网络层概述](#1-网络层概述)
  - [1.1. 第三层职责](#11-第三层职责)
  - [1.2. 第三层设备](#12-第三层设备)
- [2. IP地址和子网划分](#2-ip地址和子网划分)
  - [2.1. 第三层数据报格式](#21-第三层数据报格式)
  - [2.2. IPv4报文主要结构](#22-ipv4报文主要结构)
    - [2.2.1. 首部部分](#221-首部部分)
    - [2.2.2. 版本号](#222-版本号)
    - [2.2.3. 首部长度](#223-首部长度)
    - [2.2.4. 服务类型](#224-服务类型)
    - [2.2.5. 总长度](#225-总长度)
    - [2.2.6. 标识](#226-标识)
    - [2.2.7. 标志](#227-标志)
    - [2.2.8. 片偏移](#228-片偏移)
    - [2.2.9. 生存时间](#229-生存时间)
    - [2.2.10. 协议](#2210-协议)
    - [2.2.11. 首部检验和](#2211-首部检验和)
  - [2.3. 网络层地址](#23-网络层地址)
    - [2.3.1. 网络地址：用来标识网段](#231-网络地址用来标识网段)
    - [2.3.2. 主机ID：IP地址后面占据1-3个字节](#232-主机idip地址后面占据1-3个字节)
  - [2.4. IP地址](#24-ip地址)
    - [2.4.1. 分类](#241-分类)
    - [2.4.2. 主机的数量](#242-主机的数量)
    - [2.4.3. 保留(Reserved)地址](#243-保留reserved地址)
    - [2.4.4. 专用地址空间](#244-专用地址空间)
  - [2.5. 子网划分](#25-子网划分)
    - [2.5.1. 子网划分的基本概念](#251-子网划分的基本概念)
    - [2.5.2. 我们可以借多少位？](#252-我们可以借多少位)
    - [2.5.3. 子网划分的副产品：地址浪费](#253-子网划分的副产品地址浪费)
    - [2.5.4. 子网掩码](#254-子网掩码)
    - [2.5.5. 计算子网](#255-计算子网)
      - [2.5.5.1. 第一步](#2551-第一步)
      - [2.5.5.2. 第二步](#2552-第二步)
      - [2.5.5.3. 第三步](#2553-第三步)
      - [2.5.5.4. 第四步](#2554-第四步)
      - [2.5.5.5. 第五步](#2555-第五步)
    - [2.5.6. 计算子网网络地址](#256-计算子网网络地址)
  - [2.6. 实践:IP寻址问题](#26-实践ip寻址问题)
- [3. 第三层设备](#3-第三层设备)
  - [3.1. 路径选择](#31-路径选择)
  - [3.2. IP地址](#32-ip地址)
  - [3.3. 路由器端口](#33-路由器端口)
  - [3.4. 路由器发送的过程](#34-路由器发送的过程)
  - [3.5. 路由器端口示例](#35-路由器端口示例)
  - [3.6. IP地址分配](#36-ip地址分配)
  - [3.7. ARP Protocol ARP协议](#37-arp-protocol-arp协议)
    - [3.7.1. Address Resolution Protocol 地址解析协议](#371-address-resolution-protocol-地址解析协议)
    - [3.7.2. ARP示例](#372-arp示例)
    - [3.7.3. ARP表的缓存](#373-arp表的缓存)
    - [3.7.4. ARP的操作](#374-arp的操作)
      - [3.7.4.1. ARP request](#3741-arp-request)
      - [3.7.4.2. ARP Checking](#3742-arp-checking)
      - [3.7.4.3. ARP reply](#3743-arp-reply)
      - [3.7.4.4. ARP Caching](#3744-arp-caching)
    - [3.7.5. ARP 目的地址为本地](#375-arp-目的地址为本地)
    - [3.7.6. 网络交流](#376-网络交流)
      - [3.7.6.1. 默认网关](#3761-默认网关)
      - [3.7.6.2. Proxy ARP 代理ARP](#3762-proxy-arp-代理arp)
    - [3.7.7. Destination not local ARP对应目的方不是本地](#377-destination-not-local-arp对应目的方不是本地)
    - [3.7.8. ARP Flowchart ARP流程图](#378-arp-flowchart-arp流程图)
- [4. 网络层设备](#4-网络层设备)
  - [4.1. 面向连接的网络服务](#41-面向连接的网络服务)
  - [4.2. 无连接的网络服务](#42-无连接的网络服务)
  - [4.3. 电路交换(Circuit switched)](#43-电路交换circuit-switched)
  - [4.4. 报文交换(Packet Switched)](#44-报文交换packet-switched)
- [5. 网络协议操作](#5-网络协议操作)
  - [5.1. Routed protocol 被动可路由协议](#51-routed-protocol-被动可路由协议)
  - [5.2. Non-routable protocol 不可路由协议](#52-non-routable-protocol-不可路由协议)
  - [5.3. 被动可路由协议的寻址](#53-被动可路由协议的寻址)
  - [5.4. 路由协议的分类:静态、动态](#54-路由协议的分类静态动态)
    - [5.4.1. 静态路由和动态路由的区别](#541-静态路由和动态路由的区别)
    - [5.4.2. Routing protocol 主动路由协议(Routing)](#542-routing-protocol-主动路由协议routing)
  - [5.5. 被动路由协议和主动路由协议](#55-被动路由协议和主动路由协议)
  - [5.6. 动态路由协议的分类：内部网关协议和外部网关协议](#56-动态路由协议的分类内部网关协议和外部网关协议)
  - [5.7. 内部网关协议的分类：DVP and LSP](#57-内部网关协议的分类dvp-and-lsp)
    - [5.7.1. 距离矢量协议(DVP)的示例](#571-距离矢量协议dvp的示例)
    - [5.7.2. RIP(Routing Information Protocol) DV的代表](#572-riprouting-information-protocol-dv的代表)
    - [5.7.3. 链路状态协议(LSP)](#573-链路状态协议lsp)
    - [5.7.4. OSPF(Open Shortest Path First)](#574-ospfopen-shortest-path-first)
    - [5.7.5. IGRP (Interior Gateway Routing Protocol) and EIGRP (Enhanced IGRP)](#575-igrp-interior-gateway-routing-protocol-and-eigrp-enhanced-igrp)
- [6. VLSM(Variable Length Subnet Mask) 可变长度子网掩码](#6-vlsmvariable-length-subnet-mask-可变长度子网掩码)
  - [6.1. 经典路由和可变长度子网掩码](#61-经典路由和可变长度子网掩码)
    - [6.1.1. 经典路由(Classful routing) 无子网掩码](#611-经典路由classful-routing-无子网掩码)
    - [6.1.2. 可变长度子网掩码(Variable-Length Subnet Masks) 有子网掩码](#612-可变长度子网掩码variable-length-subnet-masks-有子网掩码)
  - [6.2. VSLM 可变长度子网掩码](#62-vslm-可变长度子网掩码)
  - [6.3. 为什么使用VLSM](#63-为什么使用vlsm)
  - [6.4. VLSM优缺点](#64-vlsm优缺点)
    - [6.4.1. VLSM的优点](#641-vlsm的优点)
    - [6.4.2. VLSM的缺点](#642-vlsm的缺点)
  - [6.5. 支持VLSM的路由协议](#65-支持vlsm的路由协议)
  - [6.6. VLSM的表示法](#66-vlsm的表示法)
  - [6.7. VLSM的例子](#67-vlsm的例子)
    - [6.7.1. 划分背景](#671-划分背景)
    - [6.7.2. 第一步:满足珀斯的主机需求](#672-第一步满足珀斯的主机需求)
    - [6.7.3. 第二步:为吉隆坡划分子网](#673-第二步为吉隆坡划分子网)
    - [6.7.4. 第三步:为悉尼和新加坡进行分配地址](#674-第三步为悉尼和新加坡进行分配地址)
    - [6.7.5. 第四步:为之间的路由地址进行划分](#675-第四步为之间的路由地址进行划分)
  - [6.8. VLSM: 例子总结](#68-vlsm-例子总结)
  - [6.9. 路由聚集(Route Aggregation)](#69-路由聚集route-aggregation)
  - [6.10. 路由聚集的例子](#610-路由聚集的例子)
  - [6.11. 如何进行路由聚集](#611-如何进行路由聚集)
  - [6.12. 路由聚集的优点](#612-路由聚集的优点)
  - [6.13. 路由隔离的其他内容](#613-路由隔离的其他内容)
- [7. 因特网控制报文协议 ICMP](#7-因特网控制报文协议-icmp)
  - [7.1. ICMP 报文的格式](#71-icmp-报文的格式)
  - [7.2. 两种ICMP报文](#72-两种icmp报文)
  - [7.3. 目的站不可到达](#73-目的站不可到达)
  - [7.4. ICMP 差错报告报文的数据字段的内容](#74-icmp-差错报告报文的数据字段的内容)
  - [7.5. 不应发送 ICMP 差错报告报文的几种情况](#75-不应发送-icmp-差错报告报文的几种情况)
  - [7.6. PING (Packet InterNet Groper)](#76-ping-packet-internet-groper)

<!-- /TOC -->

# 1. 网络层概述
1. 对于不同帧使用同一的方案进行处理
2. 第三层希望通过**路由选择算法**进行路径的选择和转发，对第二层是透明的。
3. 第三层只能避免拥塞，但是要到第四层(运输层)才能完成流量控制(第三层不能完成流量控制)

## 1.1. 第三层职责
1. 通过网络移动数据：不同网段之间的通信，不同的广播域，两个广播域之间的进行了划分，互不干扰，不是广播的通信以及对另一个网段的广播需要能传达给对方。
2. 使用分层寻址方案(与MAC寻址相反，后者平坦)
3. 细分网络并控制流量(flow)：一步步进行细化，越近了解的越多:IP地址是一致的，也就是可以忽略物理层的不同。(具体原因在开头已经分析过了)
4. 减少交通拥堵，基于IP做分段和传达，用来减少拥塞
5. 与其他网络交谈

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/1.png)

6. 在上面我们可以发现，对于不同数据链路层的帧，第三层基于IP地址，来实现跨介质的逻辑理解和连通。
7. 第三层负责进行连通和传达，数据可靠性由终端设备(第四层及以上)来进行保证(不然会带来比较大的计算量)。

## 1.2. 第三层设备
1. 路由器
   1. 互连网段或网络(不同网段的分割)
   2. 根据IP地址做出合理的决定
   3. 确定最佳路径，根据路由表。
   4. 将数据包从入站端口切换到出站端口
2. 如果A网段的设备向路由器发送了一个B网段的广播地址，那么路由器会进行转发，然而如果A网段设备发送的是本网段的广播地址，路由器则不会进行转发。(广播域划分)

# 2. IP地址和子网划分
 
## 2.1. 第三层数据报格式
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/2.png)

1. IP地址在报文中占据一部分(32bit一个IP地址)

## 2.2. IPv4报文主要结构
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/3.png)

### 2.2.1. 首部部分
>首部部分：上面蓝框部分的整体是首部部分

### 2.2.2. 版本号
>版本号:占 4 bit，指IP协议的版本。目前的 IP 协议版本号为 4 (即 IPv4)(6也就对应IPv6)

### 2.2.3. 首部长度
>首部长度:占 4 bit，可表示的最大数值是15个单位(一个单位为 4 字节) 因此IP的首部长度的最大值是60字节。
1. 因为首部长度是不确定的，所以我们需要进行标识。(用来方便读取)
2. 首部长度的32 bit为一行，也就是4个字节为一个单位
3. 所以IP报文首部字段长度为15行。

### 2.2.4. 服务类型
>服务类型:占8bit，用来获得更好的服务，这个字段以前一直没有被人们使用。
1. 比较早:延时、可靠性、代价等标志位。
2. 现在:区分服务:前6个bit表示区分服务码，后2个bit作为保留(这1个字节也就不怎么使用了)

### 2.2.5. 总长度
>总长度:占 16 bit，指**首部和数据**之和的长度，单位为字节，因此数据报的最大长度为 65535 字节(由于放到帧里面，所以大多数不比1500字节长)。总长度必须不超过最大传送单元 MTU。

### 2.2.6. 标识
>标识(identification):占 16 bit，它是一个计数器，用来产生数据报的标识。
1. 他只是为了做报文分片的问题，因为路由器可能连接的是不同网络，比如有线帧和无线帧。
2. 接收方依据标识号进行合并(相同标识号的报文是一个大报文，可以合并的)

### 2.2.7. 标志
>标志占 3 bit，最高位为 0 
1. 让发送方对报文进行控制，让中间路由器对其进行控制
2. DF(Don't fragement):是否允许做分片，0允许做分片,1不允许做分片
3. MF:MF为0表示最后一个分片,1是指后面还有分片

### 2.2.8. 片偏移
>片偏移(13 bit)指出：较长的分组在分片后某片在原分组中的相对位置。片偏移以8个字节为偏移单位。
1. 相同标识号，然后根据片偏移进行重拍(先发未必先到)，偏移比较小的更靠前
2. 因为16-3 = 13，2^3 = 8(因为单位是字节，所以用13位就可以补齐)
3.  例子(计算偏移量):偏移是字节为单位

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/40.png)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/4.png)

### 2.2.9. 生存时间
>生存时间(8 bit)记为 TTL (Time To Live) 数据报在网络中可通过的**路由器数**的最大值。
1. 是通过计数的方式来进行统计
2. 最大值是255(最多经过255个路由器)
3. 路由器每转发一次，就会对生存时间-1
4. 减小为0后，就会丢弃掉，并且通知给发送方我已经丢弃掉这个报文。
5. 防止在环上进行传输，避免由于回路问题，造成过大的网络资源浪费

### 2.2.10. 协议
>协议(8 bit)字段指出此数据报携带的数据使用何种协议以便目的主机的IP层将数据部分上交给哪个处理过程
1. 有的协议是上层的
2. 有的协议是第三层协议
3. 具体协议的情况如下

### 2.2.11. 首部检验和

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/5.png)

>首部检验和(16 bit)字段:只检验数据报的首部，不包括数据部分。这里不采用 CRC 检验码而采用简单的计算方法。算法过程如下(比较形式化的问题，并不能解决数据报错误的形式)

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/6.png)

1. 源地址和目的地址都各占 4 字节
2. 15 * 4: 15行，每行4字节

## 2.3. 网络层地址
1. IP地址为32位长(Ipv4中)
2. 它们以点分十进制格式表示为四个八位字节：133.14.17.0
3. IP地址包含两个组成部分：
   1. 网络ID
   2. 主机ID

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/7.png)

### 2.3.1. 网络地址：用来标识网段
1. 原来由ARIN(美国互联网号码注册机构，www.arin.net)分配，现在已经换了
2. 标识设备所连接(attached)的网络
3. 可以由前三个八位位组(octets)中的一个，两个或三个来标识

### 2.3.2. 主机ID：IP地址后面占据1-3个字节
1. 由网络管理员分配
2. 识别该网络上的特定设备
3. 可以由最后三个八位位组中的一个，两个或三个来标识

## 2.4. IP地址
1. 不同的类地址为地址的网络部分和主机部分保留不同数量的位

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/8.png)

2. N是Net ID,H 是 Host ID

### 2.4.1. 分类

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/9.png)

1. IP地址主要通过第一个字节进行划分
2. 0–127 Class A address A类地址
3. 128-191 Class B address B类地址
4. 192–223 Class C address C类地址
5. 224–239 Class D – Multicast D类地址：多播：视频点播的原理也是组播(多播)
6. 240–255 Class E - Research  E类地址：研究

### 2.4.2. 主机的数量
1. 每个类别的最大主机数量各不相同。(不包含网络号)
   1. A类拥有16,777,214个可用主机(2<sup>24</sup> – 2)
   2. Class B has 65,534 available hosts (2<sup>16</sup> – 2) B类具有65,534个可用主机(2<sup>16</sup> – 2)
   3. Class C has 254 available hosts (2<sup>8</sup> – 2) C类具有254个可用主机(2<sup>8</sup> –2)
2. 为什么每一类地址中都要减去2？
   1. 每个网络中的第一个地址都保留用于该网络地址
   2. 最后一个地址是为广播地址保留的。

### 2.4.3. 保留(Reserved)地址
1. 网络地址:在地址的主机部分中以二进制0结尾的IP地址
   1. A类网络地址示例：113.0.0.0
   2. 网络上的主机只有具有相同网络ID的其他主机才能直接通信。(用来确定是不是在一个网段里面)
2. 广播地址:用于将数据发送到网络上的所有设备。(一般是一个网段之间的)
   1. 广播IP地址在地址的主机部分中以二进制1结尾。
   2. B类地址的广播地址的示例:176.10.255.255 (decimal 255 = binary 11111111)
3. Class A
   1. 99.0.0.0: a reserved network number
   2. 99.255.255.255: a broadcast number
4. Class B
   1. 156.1.0.0: a reserved network number
   2. 156.1.255.255: a broadcast number
5. Class C
   1. 203.1.17.0: a reserved network number
   2. 203.1.17.255:a broadcast number

### 2.4.4. 专用地址空间
>1. 10.0.0.0 - 10.255.255.255
>2. 172.16.0.0 - 172.31.255.255
>3. 192.168.0.0 - 192.168.255.255
1. 有某些IP地址范围保留用于专用IP寻址方案(Schemas)。上述地址都是用作局域网的内部网段。
2. IP地址耗尽及其解决方案
   1. NAT
   2. CIDR
   3. IPv6(最终解决方案)
3. 发展过程:网络位数小于24，使得其可以组成超网。
4. 多个网段进行划分，保留足够的个人子网网段划分

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/10.png)

## 2.5. 子网划分
1. 网络管理员有时需要将网络划分为较小的网络，称为**子网**，以提供**额外的灵活性**.
2. 从主机字段借来的位被指定为子网字段(Subnet Fields)
3. ABC类网的主机数量比较大,会造成浪费，因为avalible的很多，很少能够用满。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/11.png)

4. 从Host中借位进行子网划分
5. 子网掩码:是由发送方提供。
6. 大的子网划分为小的子网来提高灵活性和利用率。

### 2.5.1. 子网划分的基本概念
1. 子网是网络的较小部分
   1. 提供寻址灵活性。(小的局域网可以完成隔离)
   2. 子网划分只需要本网段网络管理员进行处理即可，每一个子网也是一个网络(子网只是一个逻辑形式)
2. 子网地址通常由网络管理员在本地分配:每一个子网也是一个Net，实际上是和Net是一个标准的
3. 子网减少了广播域:使得广播域变小，提高网络利用率，避免接受到大量的无用的广播，广播只能在对应子网中进行广播。

### 2.5.2. 我们可以借多少位？
1. 可以借用的最小位数是2

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/12.png)

1. 借用的最小位数是2，为什么？
   1. I如果只借用1位以创建一个子网，那么您将只有一个网络号-.0网络-和广播号-.1网络，没有可以使用的专用网络。
   2. 两位的时候，01和10给Host，00给网络ID，11位广播地址
   3. 全0可能导致误判
2. 可以借用的最大位数可以是保留至少2位主机号的任何数字(给Host至少保留2位，因为1位的话，要么一个是NET无法使用，要么一个是广播地址)
   1. A类网络 20位
   2. B类网络 14位
   3. C类网络 6位
3. 互联网早期时，计算机比较少，没有划分子网。

### 2.5.3. 子网划分的副产品：地址浪费
1. 我们必须在所需的子网数，每个子网可接受的主机以及地址的浪费之间取得平衡(strike a balance)。
   1. hostID里面的全0和全1不能使用
   2. subnet不可以使用全0和全1
   3. 借用4位是最高效率的，提升了划分灵活性，影响了效率

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/13.png)

### 2.5.4. 子网掩码
1. 别名:扩展网络前缀
2. 定义我们用来构建网络的位数，以及描述主机地址的位数
   1. Class A 255.0.0.0
   2. Class B 255.255.0.0
   3. Class C 255.255.255.0

### 2.5.5. 计算子网
1. 我们有一个C类网络：223.14.17.0
2. 我们需要完成如下划分
   1. 划分成13个子网
   2. 每个子网有10个主机

#### 2.5.5.1. 第一步
1. 确定默认的子网掩码
2. C类网络的默认子网掩码是：255.255.255.0

#### 2.5.5.2. 第二步
1. 通过从主机ID借用位来计算子网和主机的实际数量
2. 我们对每一个子网需要借用4位来满足一个子网有10台可用的主机。

#### 2.5.5.3. 第三步
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/14.png)

1. 我们为每个子网获得16个可能的子网和16个可能的主机，因为：
   1. 对于**借用的4位**，每个位可以是1或0，从而有24或16种可能的组合。
   2. 4个剩余主机位也是如此。
2. 重要：每个子网上只有14个可用子网和主机。(一般情况下，而可用的是15个可用子网，因为0号子网可用)
   1. 因为您不能使用第一个和最后一个子网。
   2. 因为您不能使用每个子网中的第一个和最后一个地址。
   3. 对于每个，一个是广播地址，一个是网络地址。

#### 2.5.5.4. 第四步
1. 确定子网掩码。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/15.png)

1. 其中X表示用于子网划分的借用位。
2. 将X的位值相加，得到子网掩码的最后一个八位位组十进制值：128 + 64 + 32 + 16 = 240
3. 子网掩码是：255.255.255.240
4. 子网掩码用于显示IP地址中的子网和主机地址字段

#### 2.5.5.5. 第五步
1. 确定主机地址的范围
   
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/16.png)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/17.png)

1. 16个子网，14个可用子网
2. 每个子网16个主机，14个可用主机

### 2.5.6. 计算子网网络地址
1. 第一步：将IP主机地址转换为二进制。
2. 第二步：将子网掩码转换为二进制。
3. 第三步：使用布尔运算符AND将两者进行运算。
4. 第四步：将网络二进制地址转换为点分十进制。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/18.png)

1. 这是子网的网络地址
2. 它可以帮助确定路径：用来确定是否是一个网段，是否可以通过网关进行转发

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/19.png)

1. 为了找到子网的网络ID，路由器必须采用IP地址和子网掩码，并且在逻辑上将它们取和
2. 路由器根据运算的结果进行计算
3. 上图中的子网掩码255.255.255.0是255.255.0.0借用了8位产生的(而不要理解成为C类地址的子网掩码)

## 2.6. 实践:IP寻址问题
1. Given 195.137.92.0 and needing 8 usable subnets, find the subnetwork numbers, the ranges of host numbers, and subnetwork broadcast numbers. 给定195.137.92.0并且需要8个可用子网，请找到子网号，主机号范围和子网广播号。
2. IP Address is a class C. Default subnet mask is 255.255.255.0. We need to extend the network number by enough bits to give 8 usable subnets. IP地址是C类。默认子网掩码是255.255.255.0。 我们需要将网络号扩展足够的位数以提供8个可用子网。
3. Stealing 2 bits yields 2 usable subnets, stealing 3 bits yields 6 usable subnets, so we must steal 4 bits to get 14 usable subnets, of which we needed 8. 借用2位会产生2个可用子网，借用3位会产生6个可用子网，因此我们借用4位才能获得14个可用子网，其中我们需要8个可用地址。
4. This makes the subnet mask 255.255.255.240. So the Network number is 195.137.92.NNNN HHHH where Ns stand for network extension bits (subnets) and Hs stand for host numbers. 这将使子网掩码为255.255.255.240。 因此，网络号为195.137.92.NNNN HHHH，其中Ns代表网络扩展位(子网)，Hs代表主机号。
5. Next we must number the subnets; there are 16 combinations of 4 bit binary numbers but they retain their place value within the last octet. 接下来，我们必须为子网编号。 4位二进制数有16种组合，但它们在最后一个八位位组中保留其位置值。
6. 借用4-6位都可以，因为并没有规定子网中主机数量，而为什么是6位是因为一个子网中最少用2位给主机。

# 3. 第三层设备
1. 第三层的路由器
2. 路由器的两个功能:
   1. 路径选择
   2. 路由转发:将报文转发取出

## 3.1. 路径选择
1. 路由器用于根据链路带宽，跳数，延迟 … 
2. 选择数据包到达目的地的路径中的下一跳。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/20.png)

4. Internet 核心层的冗余链路是很必要的(相对于路径选项消耗，其可靠性和稳定性更加重要)
5. 路由器根据路由规范，选择他当时认为最为合适的路径

## 3.2. IP地址
1. IP地址是用软件实现的，是指设备所在的网络。
2. 路由器连接网络，每个网络必须具有唯一的网络号才能成功进行寻找路径。
3. 唯一的网络号包含在分配(incorporated)给该网络上每个设备的IP地址中
4. IP地址是逻辑的，是我们配置的。(不同于MAC地址)
5. IP地址是有层次，做转发的依据是网段而不是具体的IP，同一网段设备都有相同的IP地址，也就是我们只要到达网段即可

## 3.3. 路由器端口
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/21.png)

1. 路由器端口记录了网段的IP地址(和连接的地方是相同的)

## 3.4. 路由器发送的过程
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/22.png)

1. A5主机发送报文给B5主机，这个报文的IP地址是B5所在的IP地址，形成帧，然后放上总线。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/23.png)

2. 路由器收到帧，然后进行理解，看到报文，知道目的地是B5(解封装)

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/24.png)

3. 检查自己的路由表，找到目的地对应的端口

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/25.png)

4. 在B1端口进行转发，形成新的帧

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/26.png)

1. 形成一个全新的帧，这个帧的MAC地址是B1的MAC的地址。

## 3.5. 路由器端口示例

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/27.png)

1. 接口是路由器连接到网络的附件，在IP路由中也可以称为端口。
2. 这个IP地址往往被作为这个网络的网关
3. 每个接口必须具有一个单独的唯一网络地址。
   1. 比如上图中S1和S2不能是相同的IP地址
   2. 路由器的连接的网段一定要是不同的

## 3.6. IP地址分配
1. 静态地址分配(Static addressing)
   1. 为每个单独的设备配置一个IP地址
   2. 您应该保留非常细致的记录，因为如果使用重复的IP地址，可能会出现问题。
   3. 需要知道规范，然后根据上下文，通过命令行进行分配地址
2. 动态地址分配(Dynamic addressing)
   1. 有几种不同的方法可用于动态分配IP地址：
      + RARP: Reverse Address Resolution Protocol. RARP：反向地址解析协议。发起请求
      + BOOTP: BOOTstrap Protocol. BOOTP：BOOTstrap协议。用于工作栈
      + DHCP: Dynamic Host Configuration Protocol. (比较多用) DHCP：动态主机配置协议
3. IP地址和掩码处理后得到网络地址，保证每个网段中的主机的网段地址应该是一致的，不然会出现错误的。

## 3.7. ARP Protocol ARP协议

### 3.7.1. Address Resolution Protocol 地址解析协议
1. 为了使设备进行通信，发送设备需要目标设备的**IP地址和MAC地址**。
2. ARP使计算机能够查找与IP地址关联的计算机的MAC地址。
3. 目的方IP地址 -> 目的方MAC地址
4. 需要知道对方的MAC地址，来形成数据地址。

### 3.7.2. ARP示例

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/28.png)

1. source主机访问destination
2. 不知道目的主机在哪里

### 3.7.3. ARP表的缓存
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/29.png)

1. 可以通过lookup命令进行。
2. 在RAM里面，如果ARP没有本条目的对应MAC地址。
3. MAC地址在ARP中是有时效性的。到时间不更新不激活就会删除

### 3.7.4. ARP的操作
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/30.png)

1. 使用ARP机制
2. 上图中是一个示意图
3. 此时ARP table中没有缓存
4. 图问题:目的MAC地址应该在前面，源MAC地址字后面

#### 3.7.4.1. ARP request
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/31.png)

1. 向目的方请求MAC地址
2. 命令如图：就是找谁是这个主机，你的MAC地址是啥
3. 将MAC地址设置为全1，作为广播发送

#### 3.7.4.2. ARP Checking
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/32.png)

1. 10.0.2.5发现不是自己的主机，那么解析到这里丢掉就行，同样会记录下来对应的发送方的MAC地址。(攻击原理)
2. 10.0.2.9发现自己的MAC地址，然后形成ARP应答
3. 同时10.0.2.9会同时记录下A主机的MAC地址，更新到自己ARP地址中去(会记录对方的)

#### 3.7.4.3. ARP reply
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/33.png)

1. 向A主机进行MAC地址应答

#### 3.7.4.4. ARP Caching
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/34.png)

1. A的主机就会把对应的条目写到ARP Table中
2. 然后再次形成一个数据帧发送出去即可。

### 3.7.5. ARP 目的地址为本地
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/35.png)

1. ARP请求是本网段形成的，是一个广播就可以。
2. 如果目的主机不在本网段中，那么不能跨网段进行广播

### 3.7.6. 网络交流
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/36.png)

1. 如何与不在同一物理网段上的设备通信？如下是两种解决方案。
   1. Default gateway 默认网关
   2. Proxy ARP 代理ARP

#### 3.7.6.1. 默认网关
1. 为了使设备与另一网络上的另一设备通信，您必须为其提供**默认网关**。
2. **默认网关是路由器上连接到源主机所在网段的接口的IP地址。**
3. 为了使设备将数据发送到另一个网段上的设备的地址，源设备将数据发送到**默认网关**。
4. 192.168.0.0和192.168.0.1接入到路由器，如果网关错误是无法进行转发的。自己搭建拓扑需要手动配置。
   1. 由网关对对应报文进行转发，默认网关就是
   2. THPCP Server进行动态生成
5. 帧被发送到另一个不通过网段的链路无意义
6. 发送报文到另一个网段，需要路由器把对应端口的网关的MAC告诉你，然后通过网关进行转发。

#### 3.7.6.2. Proxy ARP 代理ARP
1. 代理ARP是ARP的一种变体(variation)。
2. 如果源主机未配置默认网关。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/37.png)

1. 发送ARP请求，然后路由器给你一个ARP的reply，告诉你MAC地址(一般为本端口的IP地址)

### 3.7.7. Destination not local ARP对应目的方不是本地
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/38.png)

1. 路由器会把Router MAC的地址给你(连接本网段的MAC地址)

### 3.7.8. ARP Flowchart ARP流程图
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/39.png)

1. ARP攻击：有一个机器恶意发送无用帧，然后会将cache写满(解决就是一段时间不处理，然后等待ARP记录中的记录失效)
2. ARP学习是收到不同的帧，对帧进行保存
3. 每一个ARP是有声明期的

# 4. 网络层设备

## 4.1. 面向连接的网络服务
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/41.png)

1. 面向连接的网络服务
   1. 就是任何发送数据的行为之前，先要建立好连接，协商好参数才会开始传输，所有数据进行有序传输
   2. 网络情况导致数据出现问题，需要接受方进行一定处理来保证数据正确
2. 传输过程中要保持连接距离，只有完成传输后才能断开连接。
3. 传输比较可靠，代价高。

## 4.2. 无连接的网络服务
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/42.png)

1. 他们分别对待每个数据包。
2. IP是**无连接系统**。
3. 不要求发送方和接收方在发送前先建立一个连接(不打招呼)。
4. 系统不需要进行大量的数据保留，不需要很多的缓存
5. 局域网使用的比较多，可靠性比较低，不处理报文丢失
6. 可靠网中，少量报文使用无连接是可以提高效率的(常用于比较小型的，并且可靠性相对比较高的网络)

## 4.3. 电路交换(Circuit switched)
1. 面向连接与电路交换。
   1. 但是，这两个词并不相同
   2. 要先建立一个虚电路关系，之后报文走对应的虚电路。
2. 面向连接：首先与接收者建立连接，然后开始数据传输。
3. 所有数据包依次在同一通道上传播，或更常见的是在同一虚拟电路上传播。
4. 问题:电路的利用效率低，一个人用了别人就不能用了(虚电路可能是分段建立，可能局部可以复用，但是整体不可以复用)。
5. 虚电路要强于面向连接的，传输更加可靠，保证**传输先后关系**。

## 4.4. 报文交换(Packet Switched)
1. 无连接网络与数据包交换:这两个词都不一样
2. 当数据包从源传递到目标时，它们可以：
   1. 切换到其他路径。(每一报文有各自的发送方和接收方，可以根据当前的网络情况，进行路由选择)
   2. 乱序到达。
3. 设备根据**各种标准**为每个数据包**确定路径**。某些标准可能因分组而异。
4. 将原始数据分为很多的子报文(单位)，每个子报文(单位)自己选择路径进行发送。
5. 大部分的Connetionless network都是基于packet switched进行实现，控制网络拥塞。
6. 出现问题时候，我们只需要重传对应部分的报文就可以(不用重传全部数据)

# 5. 网络协议操作
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/43.png)

1. 存在冗余，A转发给B是由当前网络状态处理。
2. ABC之间都是通过帧进行计算的。

## 5.1. Routed protocol 被动可路由协议
1. 为网络层提供支持的协议称为路由协议或可路由协议。
2. IP是网络层协议，因此，它可以通过互联网络进行路由。

## 5.2. Non-routable protocol 不可路由协议
1. 不可路由协议是不支持第3层的协议。
2. 这些不可路由协议中最常见的是NetBEUI。
   1. 直接根据目的方的地址在局域网中进行生成定位
   2. 这个协议不支持第三层，也就是跨局域网是不可以的。
   3. NetBEUI是一种小型，快速且高效的协议，仅限于在一个网段上运行。
   
## 5.3. 被动可路由协议的寻址
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/44.png)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/45.png)

1. 路由器连接三个网段(列出来的是网络号)
2. 将目的主机和掩码进行逻辑AND操作，得到对应的网段
3. 然后请求路由表可以发现E2端口为目的网段
4. 再次将报文封装转发给对应的主机
5. 路由表是存储在内存中的

## 5.4. 路由协议的分类:静态、动态
1. 静态路由：网络管理员在路由器中手动输入路由信息。
2. 动态路由
   1. 路由器可以在运行过程中互相学习信息。
   2. 使用路由协议更新路由信息。
   3. RIP, IGRP, EIGRP, OSPF …
   4. 人工维护的代价比较大

### 5.4.1. 静态路由和动态路由的区别
1. 静态路由
   1. 用于**隐藏**部分网络。安全(不必进行路由表的交换)
   2. 测试网络中的特定链接。
   3. 用于仅在到达目标网络的路径时维护路由表。
2. 动态路由
   1. 维护路由表。
   2. 以路由更新的形式及时分发信息。
   3. 依靠路由协议共享知识。
   4. 路由器可以调整以适应不断变化的网络状况。
   5. 打开后会启动**进程**，按照不同的协议，和网上的不同设备学习信息，然后根据**算法**生成路由表

### 5.4.2. Routing protocol 主动路由协议(Routing)
1. 路由协议确定路由协议遵循的到达目的地的路径。
2. 是用来构建路由表的，所以叫做routing
3. 公平、简单、适应变化等特点

## 5.5. 被动路由协议和主动路由协议
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/46.png)

1. Routed Portocol用于路由器之间，用来保证路由器之间连通(完成转发)，保证路由器有效连通。
2. Routing Protocol用于做各自的路由表的生成：路由器彼此交换信息。
3. Routing Protocol 决定 Routed Protocals

## 5.6. 动态路由协议的分类：内部网关协议和外部网关协议
1. 内部网关协议(Interior Gateway Protocols，RIP，IGRP，EIGRP，OSPF)：可在自治系统(autonomous system，大的单位或者管理方)中使用，该系统是一个主管部门下的路由器网络，例如公司(corporate)网络，学区的网络或政府机构的网络。
2. 外部网关协议(Exterior Gateway Protocols，EGP，BGP)：用于在自治系统之间路由数据包。
3. 自治系统是**逻辑**的划分,而未必是物理层次的划分。
4. 通过BGP，让其他自治系统了解自己的自治系统中的网段。
5. 内部网关协议和外部网关协议的区别：
   1. 一个单位对自己内部的网络管理负责，用一些协议。
   2. IGP是内部确定的管理规则，BGP(EGP)标准来沟通不同自己系统。

## 5.7. 内部网关协议的分类：DVP and LSP
1. 距离矢量协议(Distance-Vector Protocols，RIP, IGRP):
   1. 从**邻居**的角度查看网络拓扑。(注意不基于全局)
   2. 在路由器之间添加距离向量。(根据跳数来决定，经过一个路由器+1一次)
   3. 经常定期(periodic)更新。
   4. 将路由表的**副本**传递到邻居路由器。
2. 链路状态协议(Link State Protocols, OSPF):
   1. 获取整个网络拓扑的通用视图。(全局的视角，会有代价)
   2. 计算到其他路由器的最短路径。(基于带宽计算出来的cost，形成cost拓扑图，然后计算出对应的路径代价作为评判依据)
   3. **事件**触发的更新。
   4. 将链接状态路由更新传递给其他路由器。

### 5.7.1. 距离矢量协议(DVP)的示例
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/47.png)

1. 初始的时候，各自持有的是黑色的部分(直连的线路)
2. 定时路由表会相互交换给邻居，下一时刻C学习到B，B学习到AC，A学习到B，在下一刻进行再次的转发。
3. DVP只知道到达一个网段的最少跳数(但是不知道最佳路径)。
4. 会生成路由回路

### 5.7.2. RIP(Routing Information Protocol) DV的代表
1. 最受欢迎。(实现算法简单，更加靠谱)
2. 基于距离矢量的内部网关协议。
3. 唯一的指标是跳数。
4. 最大跳数为15。(评判依据简单，是一个短板)
5. 每30秒更新一次(广播)，可以修改。
6. 并非总是选择最快的路径(而是走跳数最短的路径)。
7. 产生大量的网络流量。
8. RIP v2是RIP v1的改进版本
   + RIP v1用地址广播
   + RIP v2用主播地址广播，支持身份认证、路由等，比较安全，常用

### 5.7.3. 链路状态协议(LSP)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/48.png)

>上图中的Routing table应该叫做初始时刻的Routing Table(本图的问题)
1. 彼此交换连接情况，交换的是**Link state**而不是路由表，包含link的信息，以NetID作为主键(无相同网段)，包含的是link上的路由器邻接关系、链路类型(4种)、链路带宽，会指定谁连接了谁，这个条目就被称为Database(表)。这样子就不仅仅知道链路，还知道更多的全局信息。
2. LSP操作过程:
   1. 相互交换彼此学到对应的Tpological Database(是全局的信息)
   2. 之后使用SPF算法，以自己为根，通过最短路径优先算法，生成以自己为根的树
   3. 根据这一个树再生成路由表(了解全局的信息)，逻辑是树的逻辑。
3. LSP不是进行定时进行交换的，而是初始的时候进行交换，稳定之后，根据**事件触发**的时候才会更新数据。
   1. 更新后发送给所有的路由器，需要将Database发送给所有的路由器
   2. 收到的路由器的，根据database更新自己的树，然后再次生成路由表。
4. LSP是指从所有可达的道路上找到代价最小的路径。
5. 全局可能会比较大，考虑负载进行处理
6. 但是没有路由回路，单域内一般不超过20个路由器
7. 路由表一般只保存一个最优的转发点的(负载均衡)

### 5.7.4. OSPF(Open Shortest Path First)
1. 最短路径优先协议，是基于链路状态的内部网关协议，消耗CPU和内存。
2. 指标由**带宽**，速度，流量，可靠性和安全性组成，本科阶段只考虑带宽的。
3. 事件触发的更新。
4. 最快和什么有关？(最快指的是带宽)
   1. 和实时各条链路上的通信冗余有关，也和管理方案有关，简单来说是和带宽有关
   2. 带宽表示为代价，带宽和代价成**反比**。

### 5.7.5. IGRP (Interior Gateway Routing Protocol) and EIGRP (Enhanced IGRP)
1. 思科知识产权的。
2. 基于距离矢量的内部网关协议。
3. IGRP最大跳数为255。
4. EIGRP指标由**带宽(bandwidth)，负载(load)，延迟(delay)和可靠性(reliability)**组成。加权进行运算
5. 每90秒更新一次。
6. EIGRP是IGRP的高级版本，它是**混合**路由协议(不全是根据跳数来计算)。
7. IOS 12.0以后，不支持IGRP，在模拟器中还可以。
8. EIGRP是可以的，和华为等路由器是不兼容的。(因为知识版权是思科独有的)

# 6. VLSM(Variable Length Subnet Mask) 可变长度子网掩码

## 6.1. 经典路由和可变长度子网掩码

### 6.1.1. 经典路由(Classful routing) 无子网掩码
1. 有类的路由协议要求单个网络使用相同的子网掩码。
2. 例如：网络192.168.187.0必须仅使用一个子网掩码，例如255.255.255.0。
3. 会造成网络号的浪费(为了规格一致，为了保证标准一致，会浪费一些网络号)，比如路由器之间的网络没有必要给很多的hostID。
4. 特定的情况:将路由器端口的掩码作为目的网络的掩码，可以进一步完成细化

### 6.1.2. 可变长度子网掩码(Variable-Length Subnet Masks) 有子网掩码
1. VLSM只是一项功能，它允许单个自治系统的网络具有不同的子网掩码。
2. 有效的解决网络号浪费的问题

## 6.2. VSLM 可变长度子网掩码
1. 使用VLSM，网络管理员可以在主机少的网络上使用长掩码，而在主机多的子网上使用短掩码。(提供了很高的灵活性)
2. 如果路由协议允许VLSM
   1. 在路由网络连接上使用30位子网掩码255.255.255.252
   2. 用户网络的24位掩码255.255.255.0
   3. 或者，对于最多1000个用户的网络，甚至是22位掩码255.255.252.0。(保留10位)
3. 在CIDR的基础上发展的，报文中包含有子网掩码。

## 6.3. 为什么使用VLSM
1. VLSM允许组织在同一网络地址空间内使用多个子网掩码。
2. 实施VLSM通常被称为"子网划分"，可用于最大化寻址效率。
3. VLSM是有助于缩小IPv4和IPv6之间差距的修改(modifications)之一。

## 6.4. VLSM优缺点

### 6.4.1. VLSM的优点
1. 高效使用IP地址
2. 更好的路由聚合(aggregation):构建超网

### 6.4.2. VLSM的缺点
1. 会导致地址空间的浪费:广播地址和网络号都无法被使用。
   1. 过去，建议不要使用第一个和最后一个子网。但是我们可以使用Cisco IOS ver12.0中的子网0。
   2. 从IOS ver12.0起，Cisco路由器默认使用零子网。
   3. 如果想要禁止零子网，使用该指令:`router(config)#no ip subnet-zero()`

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/50.png)

>上图解释了子网长度相同会造成怎样的浪费(在路由器所在的子网段我们只需要满足2个主机，也就是需要2位的主机号就可以完成操作)
>每一个位置都需要30个主机,有7个子网可以使用(全零可以使用，而全一不可以使用)

## 6.5. 支持VLSM的路由协议
1. 开放式最短路径优先(OSPF)
2. Integrated Intermediate System to Intermediate System (Integrated IS-IS) 集成中间系统到中间系统(集成IS-IS)
3. 增强型内部网关路由协议(EIGRP)
4. RIP v2
5. 静态路由

## 6.6. VLSM的表示法
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/51.png)

1. 斜杠的含义是指前面多少位保留给网络位
2. 此时也就是/30就可以满足路由器之间的网络连通所需(减少浪费)，剩下的网络地址可以在以后网络进行扩展
3. 这个例子中不使用VLSM还是可以进行解决的

## 6.7. VLSM的例子
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/52.png)

### 6.7.1. 划分背景
1. 已分配192.168.10.0/24的C类地址。
   1. 珀斯，悉尼和新加坡与吉隆坡建立WAN连接。
   2. 珀斯需要60个主机
   3. KL需要28个主机
   4. 悉尼和新加坡分别需要12位房东。
2. 先划分成大的子网，然后进一步进行划分，然后在慢慢进行细化
3. 为了计算VLSM子网，各个主机首先从地址范围分配最大的需求。需求级别应从最大到最小列出。

### 6.7.2. 第一步:满足珀斯的主机需求
1. 在此示例中，珀斯需要60个主机号。
2. 使用6位，因为2<sup>6</sup> – 2 = 62个可用主机地址。因此，将从第四个八位位组开始使用2位来表示/26的扩展网络前缀，其余6位将用于主机地址。
3. 在地址192.168.10.0/24上应用VLSM可得到：
   1. 192.168.10.00 hh hhhh /26
   2. 255.255.255.192 (1100 0000)

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/53.png)

4. 第一个给Perth使用，剩下的用作保留未使用的

### 6.7.3. 第二步:为吉隆坡划分子网
1. 吉隆坡需要28台主机号。192.168.10.63/26之后的下一个可用地址是192.168.10.64/26。
2. 由于需要28个主机，因此主机地址需要5位，即25 –2 = 30个可用主机地址。
3. 因此，将需要5位来表示主机，而将使用3位来表示扩展网络前缀/27
4. 在地址192.168.10.64/26上应用VLSM可得到：
   1. 192.168.10.010 hhhhh /27
   2. 255.255.255.224 (1110 0000)
   3. 三个子网再借用一位

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/54.png)

### 6.7.4. 第三步:为悉尼和新加坡进行分配地址
1. 现在，悉尼和新加坡分别需要12位主机号。 下一个可用地址从192.168.10.96/27开始。
2. 由于需要12个主机，因此主机地址需要4位，即24 = 16、16 – 2 = 14个可用地址。
3. 因此，需要4位来表示主机，对于/28的扩展网络前缀需要4位。
4. 在地址192.168.10.96/27上应用VLSM可得到：
   1. 192.168.10.0110 hhhh /28
   2. 255.255.255.240 (1111 0000)

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/55.png)

### 6.7.5. 第四步:为之间的路由地址进行划分
1. 现在为WAN连接分配地址。请记住，每个WAN连接都需要两个IP地址。下一个可用的子网是192.168.10.128/28。
2. 由于每个WAN链路需要2个网络地址，因此主机地址需要2位，即22 –2 = 2个可用地址。
3. 因此，需要2位来表示链接，并需要6位来表示扩展网络前缀/30。
4. 在192.168.10.128/28上应用VLSM可得到：
   1. 192.168.10.011000 hh /30
   2. 255.255.255.252 (1111 1100)

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/56.png)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/57.png)

5. 通过上述方法，从主机需求量大的部分入手，到主机需求量小的部分是很好的方法。

## 6.8. VLSM: 例子总结
1. 重要的是要记住，只有未使用的子网才能进一步划分子网。
2. 如果使用了子网中的任何地址，则该子网不能再进行子网划分。
3. 一般是从主机多大到主机少(路由间网络)进行划分

## 6.9. 路由聚集(Route Aggregation)
1. 使用无类域间路由(CIDR，Classless InterDomain Routing)和VLSM不仅可以防止地址浪费，而且还可以促进路由聚合或汇总。
2. 多个路由条目汇聚成小的路由条目
3. 比如如下图就是讲3个/24的子网合并成一个/16的网络高速远端
4. 优点:聚集之后我们只需要知道一个网段就可以，也就是远端的路由表就会变少

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/58.png)

## 6.10. 路由聚集的例子
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/59.png)

1. 多层聚集

## 6.11. 如何进行路由聚集
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/60.png)

>如何进行计算:将尽可能多的位进行聚集，将之后的不通过的位置，作为Host位，就得到了上图的结果

## 6.12. 路由聚集的优点
1. 减少路由表条目的数量。
2. 可用于隔离拓扑更改(聚集之后，只能得到大的网段的信息，因为小的网段的拓扑变化会比较频繁，导致路由表进行不断地计算，只公告比较高聚集后的路由的网段信息)

## 6.13. 路由隔离的其他内容
1. 为了使聚合正常工作，请以分层方式(hierarchical fashion)仔细分配地址，以便汇总的地址将共享相同的高位。
2. VLSM允许路由聚合，并且通过将聚合完全基于左侧共享的高阶位来灵活地增加，即使网络不连续也是如此。
3. 路由聚集需要严谨，不能让A和B两个端口的聚集后的网络号相同
4. VLSM是不做连续性检验的，也就是就算不连续也会进行聚集
5. 全0子网会在题目中说是否可用
6. 全1子网尽量不要使用

# 7. 因特网控制报文协议 ICMP
1. ICMP (Internet Control Message Protocol)：为了提高 IP 数据报交付成功的机会(消息管理和协商)
2. ICMP 允许主机或路由器**报告**差错情况和提供有关异常情况的报告
3. ICMP 只是IP层的协议
4. ICMP 报文作为IP层数据报的数据，加上数据报的首部，组成 IP 数据报发送出去
5. 一般路由器在丢弃报文的时候(处理之前已经提到的情况)，都会返回一个ICMP差错报文。

## 7.1. ICMP 报文的格式
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/61.png)

1. 前四个字节是一样的(格式化的)
2. 后面都是个根据类型

## 7.2. 两种ICMP报文
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/62.png)

1. 查询报文:一般这种情况不是很多
2. 差错报告报文:一般这种类型会多一些

## 7.3. 目的站不可到达
1. **网络**不可到达(net unreachable)
2. **主机**不可到达(host unreachable)
3. **协议**不可到达(protocol unreachable)
4. **端口**不可到达(port unreachable)
5. **源路由选择**不能完成(source route failed)
6. 目的网络**不可知**(unknown destination network)
7. 目的主机**不可知**(unknown destination host)
8. 不可知是完全不可以解析，不可达是可以解析但是不可以到达

## 7.4. ICMP 差错报告报文的数据字段的内容
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/63.png)

1. 一般会把原始的IP数据报文的数据报首部 + 8字节(数据的，可能会包含端口信息)作为ICMP的数据部分
2. ICMP的前8个字节的是确定的(前4个字节是类型，校验位，后面四个字节是确定的)
3. 然后添加一个首部作为IP数据报进行发送。

## 7.5. 不应发送 ICMP 差错报告报文的几种情况
1. 对 ICMP 差错报告报文不再发送 ICMP 差错报告报文
2. 对第一个分片的数据报片的所有后续数据报片都不发送 ICMP 差错报告报文(就是每次传送只要发送一次就够了)
3. 对具有多播地址的数据报都不发送 ICMP 差错报告报文
4. 对具有特殊地址(如127.0.0.0或0.0.0.0)的数据报不发送 ICMP 差错报告报文
   1. 127.0.0.0:逻辑回路地址
   2. 0.0.0.0:确认路由地址

## 7.6. PING (Packet InterNet Groper)
1. PING 是用ICMP的"Echo request"和"Echo reply"消息来实现的
2. PING 用来测试两个主机之间的连通性，一般是用来检查局域网的连通性：PING不通，不仅仅是发送不过去，有可能是应答不回来。
3. PING 使用了ICMP回送请求与回送回答报文
4. PING 是应用层直接使用网络层ICMP的例子，它没有通过运输层的TCP或UDP