Exam-final-考试试卷情况汇总
---

<!-- TOC -->

- [1. 试卷：2010年](#1-试卷2010年)
  - [1.1. 单选题](#11-单选题)
  - [1.2. 多选](#12-多选)
  - [1.3. 设备](#13-设备)
  - [1.4. 第一道大题](#14-第一道大题)
  - [1.5. 第二大题：编码汇总](#15-第二大题编码汇总)
- [2. 各层协议汇总](#2-各层协议汇总)
- [3. 无屏蔽双绞线](#3-无屏蔽双绞线)
- [4. 试卷：2013年](#4-试卷2013年)
  - [4.1. 单选题](#41-单选题)
  - [4.2. 多选题](#42-多选题)
  - [4.3. 大题:子网划分](#43-大题子网划分)
- [5. 试卷：2015年](#5-试卷2015年)
- [6. 试卷：2016年](#6-试卷2016年)
- [7. 试卷：2017年](#7-试卷2017年)
- [8. 试卷:2018年](#8-试卷2018年)
- [9. 试卷：2019年](#9-试卷2019年)
- [10. 报文格式总结](#10-报文格式总结)
  - [10.1. MAC帧格式](#101-mac帧格式)
  - [10.2. 无线网数据帧](#102-无线网数据帧)
  - [10.3. Ipv4报文](#103-ipv4报文)
  - [10.4. ARP请求](#104-arp请求)
  - [10.5. ICMP报文格式](#105-icmp报文格式)
  - [10.6. UDP报文格式](#106-udp报文格式)
  - [10.7. TCP报文格式](#107-tcp报文格式)
  - [10.8. HTTP报文结构](#108-http报文结构)
  - [10.9. OSPF报文](#109-ospf报文)
  - [10.10. PPP帧格式](#1010-ppp帧格式)
- [11. CCNA](#11-ccna)
- [12. 零散总结](#12-零散总结)
- [13. 名词解释](#13-名词解释)

<!-- /TOC -->

# 1. 试卷：2010年

## 1.1. 单选题
1. POP不是网络层协议
2. IP是Routed Protocol
3. 100BASETX:是屏蔽双绞线
4. 协议们:
   1. 802.1q:VLAN
   2. 802.2:LLC
   3. 802.3:MAC，覆盖了物理层和数据链路层下半层，是互联网的**核心协议**，通常指以太网
   4. 802.4:委员会定义了令牌总线标准是宽带网络标准
   5. 802.5:令牌环网
   6. 802.11:IEEE为无线网制定的标准
5. Hub:集线器
6. Transceiver:第一层设备
7. CIDR:无类间路由，提供路由聚集功能。
8. 在Root Bridge上，所有的端口都是Designed Ports.
9. 无线协议速度：
   1. 802.11：1M-2M
   2. 802.11b：2.4GHz 11M
   3. 802.11a：5GHz 54M
   4. 802.11n:下一代，100M
10. 无线局域网可以在有线以太网上运行(作为主干网)，但是不一定
11. The Basic Media Access Control Mechanism of 802.11b 是 CSMA/CA(注意不是CSMA/CD)
12. 同网段中的Host ID的全0或者全1不可以使用。
13. 固定的网络地址：
    1. OSPF hello:224.0.0.5
    2. OSPF DR和BDR的组播地址:224.0.0.6
    3. RIP v2:224.0.0.9
14. 以太网上的MAC机器使用CSMA/CD
15. 无线网中的MAC地址使用CSMA/CA

## 1.2. 多选
1. IP和IPX是Routed Protocols
2. 冲突域：共用同样的网线
3. 广播域：广播是否转发
4. ACL
   1. 如果没有找到ACL，则所有的流量都会被转发
   2. 配置了`access-list 1 deny host 192.168.10.1`，则来自子网，192.168.10.0/24网段都会被拒绝
   3. ACL如果不强调则为标准ACL，配置在目的地址。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/exam/2.png)
>一共由3个冲突域和2个广播域

5. MAC地址一共有48 bit
6. 以太网交换机通过MAC地址来过滤流量
7. IP地址不可以在以太网帧中找到
8. 路由器配置：
   1. startup放置在NVRAM中，而不是FLASH
   2. IOS的备份在ROM中
   3. 端口号可以在TCP和UDP帧中找到
9. number 1-100标准ACL，101-200扩展ACL
10. IP地址不出现在帧首部
11. 简单系统镜像-IOS，系统镜像(FLASH、TFTP、ROM)

## 1.3. 设备
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/exam/1.png)

## 1.4. 第一道大题
1. 找到路径，并且简要写帧的格式：注意MAC地址在到路由器之前时路由器的默认网关的地址(MACR1)
2. 注意：看清From和To是不一样的，IP一致没有变过

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/exam/3.png)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/exam/4.png)

## 1.5. 第二大题：编码汇总
1. 单极性编码：0电平表示0，正电平表示1

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec02/29.png)

2. 不归零电平编码：负电平表示0，正电平表示1

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec02/18.png)

3. 不归零反相编码：电平**翻转**表示1，不翻转表示0
4. 归零制码:负电平表示0，正电平表示1，后半部分归零电平

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec02/19.png)

5. 曼彻斯特编码：低到高表示0，高到底表示1

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec02/20.png)

6. 差分曼彻斯特：有跳变表示1，无跳变表示0

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec02/21.png)

# 2. 各层协议汇总
1. 物理层
2. 数据链路层：CSMA/CD、CSMA/CA
3. 网络层：
   1. ARP
   2. ICMP
   3. Routed Protocol：IP
   4. Routing Protocol
      1. Static Routing Protocol:
      2. Dynamic Routing Protocol:
         1. IGP:IGRP、EIGRP
            1. DVP:RIP
            2. LSP:OSPF
         2. EGP:BGP
4. 运输层:TCP、UDP、ARQ、NAT/PAT
5. 应用层
   1. 会话层：
   2. 展示层：JPEG、GIF
   3. 应用层：HTTP、FTP(20和21)、Telne、SMTP、POP、DNS、DHCP

# 3. 无屏蔽双绞线
1. 一类线：主要用于语音传输，不用于数据传输，只有两根线做双绞线，常用作电话的语音通信，并不做语音进行通信
2. 二类线：传输频率1MHz，用于语音和最高4Mbps的数据传输，常见于令牌网环网，不是很常用
3. 三类线：EIA/TIA568标准指定电缆，传输频率16MHz，用于语音传输及最高传输速率为10Mbps的数据传输，主要用于10BASE-T(10M带宽的双绞线)
4. 四类线：传输频率为20MHz，用于语音传输和最高传输速率16Mbps的数据传输，主要用于令牌网和 10BASE-T/100BASE-T
5. 五类线：增加了绕线密度，外套高质量绝缘材料，用于语音和数据传输(主要为100/1000BASE-T)，是最常用的以太网电缆
    + 和三类线相比，绞合度更高，抗干扰能力更强。
    + 从五类线开始进行了更加标准化的处理。
6. 超五类线(主要使用的)：衰减小，串扰少，具有更高的衰减/串扰比和信噪比、更小的时延误差，主要用于1000BASE-T
7. 六类线：传输频率为1MHz～250MHz，性能远高于超五类标准，适用于高于1Gbps的应用
8. 七类线：带宽为600MHz，可能用于今后的10G比特以太网。

# 4. 试卷：2013年

## 4.1. 单选题
1. IEEE 802.3不是网络层协议，是描述物理层和数据链路层的MAC子层的实现方法的。
2. 各类地址
   1. 0–127 Class A address A类地址
   2. 128-191 Class B address B类地址
   3. 192–223 Class C address C类地址
   4. 224–239 Class D – Multicast D类地址：多播：视频点播的原理也是组播(多播)
   5. 240–255 Class E - Research  E类地址：研究
3. PDU在不同层的名称
   1. 数据链路层:帧(frame)
   2. 网络层:包(packet)
   3. 传输层:数据段(Segment)
   4. 更高层次:报文(Message)
4. 无线局域网可以在有线以太网上运行(作为主干网)，但是不一定
5. 如果交换机不知道发送的报文的目的MAC地址，则会对所有端口泛红。
6. B信道是64kbps，D信道是16kbps，BRI是144kbps

## 4.2. 多选题
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/exam/5.png)

- 默认没有匹配的话,使用Deny Any,上题选B

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/exam/6.png)

- BC,DV在邻居之间相互交换信息,路由器不断更新它们内部的表.
- FTP使用TCP两个端口:21负责发起和建立双方的连接,20端口负责传输数据
- Telnet使用TCP/23号
- SMTP使用TCP/25号
- DNS使用UDP/53号
- TFTP使用UDP/69号
- SNMP使用161号
- HTTP使用TCP/80号
- HTTPS使用443号
- DHCP使用了UDP

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/exam/7.png)

- AC,PAP模式,中心路由器询问远端路由器密码,不限制次数,直到连接成功
- CHAP每一个路由器必须知道密码,中心路由器发起

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/exam/8.png)

- AE
- 为172.16.3.0这个网段设置了静态路由
- 使用了默认管理距离,这个并不会在最后使用

## 4.3. 大题:子网划分
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/exam/9.png)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/exam/10.png)

- hostID的全0和全1都不能使用，subnet全零可用

# 5. 试卷：2015年
1. 简述OSI模型和TCP/IP的相似和不同？
   1. 相似：
      1. 两者都有层次，网络专业人员都需要知道二者，通过分层方案完成具体实现
      2. 两个都有应用层，尽管他们有不同的服务。
      3. 两个都有相同的传输层和网络层
      4. 都采用了**分组交换**的技术，都是**基于报文**进行交换的。
   2. 不同：
      1. TCP/IP只有4层，而OSI有7层。
      2. TCP/IP协议是互联网发展的标准，在实际使用中。而OSI模型只是作为学习的指南
2. 子网划分：3位作为网络，5位作为主机
   1. 195.3.1.0 255.255.255.224
   2. 195.3.1.32 255.255.255.192
   3. 195.3.1.64 255.255.255.160
   4. 192.3.1.96 255.255.255.128
   5. 192.3.1.128 255.255.255.96
3. 最后一题(问题)：TCP的确认号是期望发送的下一个字节号

# 6. 试卷：2016年
1. 各种线的用法：
   1. 直通线：台式机和交换机，顺着插线
   2. 反转线：控制台线缆，一端的插脚1连接到另一端的插脚8；然后插脚2连接到插脚7，插脚3连接到插脚6，依此类推，两端是插脚对应是反着的
   3. 交叉线：两个台式机相连接(连接相同的设备)，电缆一端的Pair 2和Pair 3将在另一端反转，一端为T568-A的排序，另一端为T568-B的排序

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec02/10.png)

2. Ipv4和IPv6的区别
   1. Ipv4占有4位(32的地址)，Ipv6占有6位(128位地址)
   2. Ipv6的地址空间大于Ipv4
   3. Ipv6的路由表小于Ipv4
   4. Ipv6的安全性更强
3. 解决路由环路的方法
   1. 设置最大跳数：设置最大跳数为15，16即视为不可达
   2. 水平分割：从某个端口接受到的报文信息，在相同端口不再接受。
   3. 路由毒化：发生故障时，将不可达网路的跳数设置为16，然后进行毒性传播，之后达到最后一个后通过毒性逆转告知源头已经传播完成。
   4. 设置计时器：我们收到网络不可达信息时，启动计时器，如果在计时过程中没有找到一条更好的路径，则删除该条记录。
4. TCP建立连接的过程(重点)
   1. 客户机 -> 服务器:SYN = 1 seq = x
   2. 服务器 -> 客户机:SYN = 1,ACK = 1,seq = y,ack = x + 1
   3. 客户机 -> 服务器:ACK = 1,seq = x + 1 ack = y + 1
5. TCP解除连接的过程(重点)
   1. 客户机 -> 服务器:FIN = 1,seq = u
   2. 服务器 -> 客户机:ACK = 1,seq = v,ack = u + 1
   3. 服务器 -> 客户机:FIN = 1,ACK = 1,seq = w,ack = u + 1
   4. 客户机 -> 服务器:ACK = 1,seq = u + 1, ack = w + 1

# 7. 试卷：2017年
1. UTP特点：直径小、更便宜、更容易安装，必须要用中继器
2. NAT中的一个IP地址给多个用户使用连接到全局以太网，PAT
3. WildMask

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/exam/11.png)

4. 收邮件:POP3，发送邮件SMTP
5. 路由器Input端口没有？
6. 静态路由相比于动态路由的优点
   1. 快速收敛
   2. 不占用带宽
   3. 更安全
   4. 用更少的CPU
7. 为什么交换机学习不到广播地址：广播地址不是一个帧的源地址
8. 可靠性最高的拓扑是网型拓扑
9. RIP v2的特点
   1. 支持有类路由:可以携带子网掩码
   2. 使用主播地址进行发送广播:特定给RIP接受，避免了接受后发现没有启动RIP进程耽误时间
   3. 需要身份认证才确定是否继续进行接收。
10. 路由表更新：找到最短路径即可(图一和图三反了)
   - 最后一个不替换，因为是1+3
11. 报文 -> 数据段 -> 数据包 -> 数据帧 -> 位

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/exam/12.png)


# 8. 试卷:2018年
1. D
2. 数据封装过程:data -> segments -> packets -> frames -> bits
3. Socket:(Ip address, Port)
4. 静态路由优点：节省CPU，带宽，安全性
5. 使用了TCP的协议有:HTTP、FTP、SMTP(基于FTP)
6. 使用了UDP的协议有:RIP、DNS、SNMP、TFTP、DHCP
7. private ip address:私有网络地址
   1. 10.0.0.0 - 10.255.255.255
   2. 172.16.0.0 - 172.31.255.255
   3. 192.168.0.0 - 192.168.255.255

# 9. 试卷：2019年
1. 路由更新，给原表，按照相邻节点提供的表更新

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/47.png)

2. 不归零编码、曼彻斯特编码和差分曼彻斯特编码
3. 注意PING的方向
4. UDP报文解析
   1. 二进制表示:`0000 1100 0011 0010 0000 0000 0011 0101 0000 0000 0001 1100 1110 0001 0100 0110`
   2. 源端口：3122，目的端口：53
   3. 客户端发送
   4. 请求DNS服务

# 10. 报文格式总结

## 10.1. MAC帧格式
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec03/5.png)

>字节为单位
1. 前同步码:0x10101010|0x10101011
2. 目的地址(48bit)
3. 源地址(48bit)
4. 长度字段(16bit)
5. 数据(不定长)
6. FCS(32bit)

## 10.2. 无线网数据帧
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec03/13.png)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec03/14.png)

- 有时间窗口，超时重传

## 10.3. Ipv4报文
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/3.png)

>单位为bit
- 标志
  - DF(Don't fragement):是否允许做分片，0允许做分片,1不允许做分片
  - MF:MF为0表示最后一个分片,1是指后面还有分片
- 偏移：单位：8 bit为一单位

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/40.png)

## 10.4. ARP请求
1. ARP Request:

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/31.png)

2. ARP Checking:

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/32.png)

3. ARP Reply:

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/33.png)

4. ARP Caching:

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/34.png)

## 10.5. ICMP报文格式
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec04/61.png)

## 10.6. UDP报文格式
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec05/23.png)

>源端口(16 bit)、目的端口(16 bit)、长度(16 bit)、校验(data)(16 bit)、Data

## 10.7. TCP报文格式
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec05/2.png)

>单位bit

- 固定首部20字节
- 源地址(16 bit)、目的地址(16 bit)
- 确认号：期望收到对方的下一个报文段的数据的第一个字节的序号
- 特殊位
  - URG：1表示紧急，尽快传送
  - ACK：1表示确认号字段有效，反之无效
  - PSH：1表示尽快交付(将缓存部分全部交付)
  - RST：1表示TCP连接中出现严重差错，立即释放连接重建
  - SYN：1同步，表示连接请求
  - FIN：1表示发送端数据发送完毕，释放连接
- 填充字段：保证长度位4字节的倍数

## 10.8. HTTP报文结构
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec06/7.png)

## 10.9. OSPF报文
- Hello报文

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec08/27.png)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec08/28.png)

## 10.10. PPP帧格式
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec10/10.jpg)

>数字的单位是字节
1. Flag: 01111110 标记：帧的开头或结尾，01111110，一位可能会连续接受到多个帧
2. Address：11111111，广播地址
3. Control：00000011，用户数据作为无序帧传输
4. Protocol: 数据字段中的协议类型
5. Data: 数据报，最大默认值为1500字节
6. FCS: 2或者4字节

# 11. CCNA
1. TCP/IP有4层，OSI有7层，TCP/IP协议套件没有会话层，TCP/IP是一个动态改变的互连网络协议的集合，顺序号用来确认、记录接受情况和拒绝重复。
2. RPC:远程透明访问,Remote-Procedure call，RPC提供了本地透明访问，和高可移植性。
3. 套接字允许多个应用程序使用相同的TCP/IP连接，传输层套接字为(IP,Port)
4. 窗口技术是用来进行流控制的
5. IP协议是一个从一个节点向另一个节点传输数据的网络层协议。
6. 传输层提供可靠性连接
7. UDP泛洪时，源地址不能变化。UDP报文首部没有紧急指针。
8. IP地址寻址是静态寻址的格式，需要手动配置IP地址
9. IP is described as an unreliable mechanism because it does not guarantee delivery √
10. 报文分段是为了保证报文更加适合传送，发生在路由器上
11. RARP是知道MAC地址，但是不知道IP地址
12. ICMP重定向是由网关完成的

# 12. 零散总结
1. CSMA/CD工作过程:先听后发，边听边发，冲突停止，延迟重发

| 层次       | 特点                     | 关键字                   | 备注         |
| ---------- | ------------------------ | ------------------------ | ------------ |
| 物理层     | 二进制传输               | 信号和介质               | 属于数据流层 |
| 数据链路层 | 介质访问                 | 帧和介质访问控制         | 属于数据流层 |
| 网络层     | 路径选择                 | 路径选择，最优路径       | 属于数据流层 |
| 传输层     | 终端到终端通信           | 可靠性，流控制，错误纠正 | 属于数据流层 |
| 会话层     | 进程之间通信如何用户交流 | 对话和交流               | 属于应用层   |
| 展示层     | 展示(语法传送、语法协商、连接管理)                     | 标准                     | 属于应用层   |
| 应用层     | 给用户展示交互接口       | 浏览                     | 属于应用层   |

2. IP报文首部最短20字节，最长60字节
3. CRC计算式异或运算，结果 + 余数

# 13. 名词解释
1. (2010)IEEE MAC Sub-Layer:数据连接层分为两个小层LLC和MAC。MAC是指Media Access Control，控制各个Host对Media的使用权。MAC子层定义了Frame如何在物理线上运输，处理物理地址，定义网络拓扑和网线使用规则。
2. (2010,2015)Split Horizon:水平分割，避免路由回路出现和加快路由汇聚的方法，指一个路由不允许把从一个路由那里得到的路由信息再传回去，该条路由信息只能单方向传输。
3. (2010)Flow Control:对数据的传输进行控制，检查，发现出错后的处理。
4. (2010)Socket：是网络联网的一个接口，表示为(IP 地址，端口)，一个连接表示为(Socket_source, Socket_des)
5. (2010,2013,2015,2016)DNS:Domain Name System,域名系统，分为三级域名、二级域名和顶级域名，通过DNS服务器将域名转化为IP地址，然后进行访问。
6. (2010,2013,2015,2016,2017,2018)TDM,Time Division Multiplexing：时分复用，在一条线上传输多个用户信息时，将网线的使用时间分段分配给各个用户，达到多路复用的效果。
7. (2010)ADSL：Asymmetric Digital Subscriber Line:非对称用户数字电话线路，对模拟电话数据线进行改造，使其能够承受宽带的业务，上行带宽和下行带宽不同。
8. (2010)Computer Virus:病毒，编制或者在计算机程序中插入破坏计算机功能或破坏数据，影响计算机使用并且能够自我复制的一组计算机指令或者程序代码
9. (2013)Full Duplex:全双工,通信的双方可以同时发送和接收信息.
10. (2013)OSI reference Model:OSI将计算机网络体系结构划分为以下七层:物理层、数据链路层、网络层、运输层、会话层、表示层和应用层
11. (2013,2015,2016,2017,2018)CSMA/CD:Carrier Sense Multiple Access with Collision Detection,载波监听多点接入碰撞检测。多点接入表示是总线网络，载波监听就是用电子技术监测总线上有没有其他计算机也在发送。碰撞检测就是边发送边监听，即适配器边发送数据边检测信道上的信号电压的变化情况，以便判断自己在发送数据时其他站是否也在发送数据。
12. (2013)STP(Spanning Tree Protocol):生成树协议，该协议可应用于在网络中建立树形拓扑，消除网络中的环路，并且可以通过一定的方法实现路径冗余，但是不时一定要实现路径冗余
13. (2013,2015,2017)RARP(Reverse Address Resolution Protocol),反向地址解析协议，发出要反向解析的物理地址并希望返回对应的IP地址。
14. (2015,2016,2017,2018,2019)PPP:Point to Point Protocol,点对点协议,是为在同等单元之间传输数据包这样的简单链路设计的数据链路层协议，是数据链路层使用最多的一种协议。这种链路提供全双工操作，并按照顺利传递数据包。特点为：简单；只检测差错而不纠正差错，不进行流量控制；支持多种网络层协议.
15. (2015)UDP:User Datagram Protocol，用户数据包协议，是OSI参考模型中一种无连接的传输层协议，提供面向事务的简单不可靠、无连接、无确认、无流控制的信息传送服务
16. (2015,2018)HTTP:HypeText Transfer Protocol,超文本传输协议，HTTP 是**面向事务**、**无状态**、**无连接**的客户服务器协议。
17. (2016,2017)FTP：File Transfer Protocol:文件传输协议，FTP是可靠的，面向连接的服务。基于TCP,20和21端口，工作流程：首先通过套接字建立控制连接，然后建立数据连接，通过数据连接传输数据
18. (2017,2018)CHAP:Challenge Handshake Authentication Protocol,挑战握手认证协议，链路建立阶段结束之后，认证者向对端点发送"challenge"消息;对端点用经过单向哈希函数计算出来的值做应答;认证者根据它自己计算的哈希值来检查应答，如果值匹配，认证得到承认，否则连接应该终⽌止;经过一定的随机间隔，认证者发送一个新 challenge 给端点，重复步骤 1- 3。
19. (2017,2018,2019)ICMP：Internet Control Message Protocol,互联网报文控制协议，是为了提高IP数据报交付成功的机会，允许主机或路由器报告差错情况和提供有关异常情况报告的协议，运行在IP层
20. (2018,2019)SMTP:Simple Mail Transfer Protocol,简单邮件传输协议，它是一组用于由源地址到目的地址传送邮件的规则，由它来控制信件的中转方式。SMTP协议属于TCP/IP协议族，它帮助每台计算机在发送或中转信件时找到下一个目的地。通过SMTP协议所指定的服务器,就可以把E-mail寄到收信人的服务器上了，整个过程只要几分钟。SMTP服务器则是遵循SMTP协议的发送邮件服务器，用来发送或中转发出的电子邮件。用于: 用户代理把邮件传送到服务器；在邮件服务器之间的传送
21. (2018,2019)ARP,Address Resolution Protocol,地址解析协议，把ip地址解析为硬件地址，解决了同一个局域网上的主机或者路由器的ip地址和硬件地址的映射问题。ARP的高速缓存可以大大减少网络上的通信量。只针对同一网段
22. (2019)HTML:HypeText Markup Language,超文本标记语言，定义了许多用于排版的命令(标签)是一种可以用任何文本编辑器创建的 ASCII 码文件。
23. (2019)CIDR:Classless Inter-Domain Routing,无类域间路由选择，是一个在Internet上创建附加地址的方法，这些地址提供给服务提供商(ISP)，再由ISP分配给客户,(Tip: VLSM+CIDR就形成了划分子网时出现如  192.168.1.0/28  子网掩码255.255.255.240这样的形式)
24. (2019)ISP,Internet Service Provider,互联网服务提供商，向广大用户综合提供互联网接入业务、信息业务、和增值业务的电信运营商
25. (2019)URL:Uniform Resource Locator,统一资源定位符，是对可以从因特网上得到的资源的位置和访问方法的一种简洁的表示。