名词分析总结
---

# 1. A

| 英文简称 | 英文全称 | 中文全称 | 备注 |
| -------- | -------- | -------- | ---- |
| ATM | Asynchronous Transfer Mode | 异步传输模式 | 具有分组交换和电路交换的优点，对应于OSI协议参考模型的第2层。ATM通过AAL层适配，将不同业务应用接纳进来。 |
| ANSI | American National Standards Institute | 美国国家标准协会 | 美国国家标准化中心，各界标准化活动都围绕着它进行 |
| AMI | Alternate Mark Inversion | 双极性码 | 二进制的0用0电平表示，二进制码的1交替的用+1和-1的半站空归零表示 |
| AM | Amplitude Modulation | 调幅 | 使载波的振幅按照所需传送信号的变化规律而变化，但频率保持不变的调制方法 |
| AP | Access Point | 接入点 | |
| ARS | Adaptive Rate Selection | 自适应速率选择 | |
| ARIN | American Registry For Internet Numbers | 美国互联网号码注册机构 | |
| ARP | Address Resolution Protocol | 地址解析协议 | 把ip地址解析为硬件地址，解决了同一个局域网上的主机或者路由器的ip地址和硬件地址的映射问题。ARP的高速缓存可以大大减少网络上的通信量。只针对同一网段 |
| API | Application Programming Interface | 应用程序接口 | |
| ARQ | Automatic Repeat-reQuest | 自动重传请求 | 是OSI模型中数据链路层的错误纠正协议之一 |
| ASCII | American Standard Code for Information Interchange | 美国信息交换标准码 | |
| AD | Administrative Distance | 管理距离 | |
| ABR | Area Border Router | 区域边界路由器 | |
| ADSL | Aysmmetric Digital Subscriber Line | 非对称数字用户线路 | 用数字技术对现有的模拟电话用户线进行改造，使它能承载宽带数字业务。ADSL下行带宽远远大于上行带宽，因此得名"非对称"。 |
| ATU | Access Termination Unit | 接入端接单元 | |
| ACL | Access Control Lists | 访问控制列表 | 是路由器和交换机接口的指令列表，用来控制端口进出的数据包 |
| ACK | Acknowledgement | 最大报文段长度 | 在数据通信中，接收站发给发送站的一种传输类控制字符，表示发来的数据已确认接收无误 |
| AES | Advanced Encryption Standard | 高级加密标准 | 是美国联邦政府采用的一种区块加密标准 |

# 2. B

| 英文简称 | 英文全称 | 中文全称 | 备注 |
| -------- | -------- | -------- | ---- |
| BSS | Basic Service Set | 基本服务集 | |
| BS | Base Station | 基站 | |
| BOOTP | BOOTstrap Protocol | 引导程序协议 | 向BOOTP服务器请求分配IP |
| BGP | Border Gateway Protocol | 边界网关协议 | |
| BDR | back-up designated router | 备份指定路由器 | 备份指定路由器，对DR的备份 |
| BPDU | Bridge Protocol Data Unit | 桥接数据单元 | 用于在STP中传递拓扑信息、选举等 |
| BID | Bridge Identification | 网桥标识 | 8字节，由优先级和交换机的MAC地址组成，用于选举根桥接器、根端口等 |
| BRI | Basic Rate Interface | 基本速率接口 | |
| B Channel | Barrier Channel | B信道 | 用于电路交换(circuit-switch)的数据，通过PPP或HDLC，B信道工作在64 kbps的速率下，用于传输数据和语音流量 |

# 3. C

| 英文简称 | 英文全称 | 中文全称 | 备注 |
| -------- | -------- | -------- | ---- |
| CSU | Channel Service Unit | 通信服务单元 | 将终端用户和本地数字电话环路相连的数字接口设备 |
| CDM | Code Division Multiplexing | 码分复用 | 常用的名词是码分多址 CDMA(Code Division Multiple Access)靠不同的编码来区分各路原始信号的一种复用方式 |
| CDMA | Code Division Multiple Access | 码分多址 | 是一种多路方式，多路信号只占用一条信道 |
| CSMA/CA | Carrier Sense Multiple Access with Collision Avoid | 带有冲突避免的载波侦听多路访问 | |
| CSMA/CD | Carrier Sense Multiple Access with Collision Detection | 带冲突检测的载波侦听多路访问 | "多点接入"就是说明这是总线型网络，"载波监听"就是用电子技术检测总线上有没有其他计算机也在发送。"碰撞检测"也就是"边发送边监听"，即适配器边发送数据边检测信道上的信号电压的变化情况，以便判断自己在发送数据时其他站是否也在发送数据。 |
| CRC | Cyclic Redundancy Check | 循环冗余校验 | |
| CTS | Clear To Send | 清除发送 | |
| CIDR | Classless Inter-Domain Routing  | 无类域间路由选择 | 无类域间路由，是一个在Internet上创建附加地址的方法，这些地址提供给服务提供商(ISP)，再由ISP分配给客户,(Tip: VLSM+CIDR就形成了划分子网时出现如  192.168.1.0/28  子网掩码255.255.255.240这样的形式) |
| CDP | Cisco Discovery Protocol | 思科发现协议 | |
| CPE | Customer Premise Equipment | 用户终端设备 | |
| CHAP | Challenge Handshake Authentication Protocol | 挑战握手认证协议 | 链路建立阶段结束之后，认证者向对端点发送"challenge"消息;对端点用经过单向哈希函数计算出来的值做应答;认证者根据它自己计算的哈希值来检查应答，如果值匹配，认证得到承认，否则连接应该终⽌止;经过一定的随机间隔，认证者发送一个新 challenge 给端点，重复步骤 1- 3。 |

# 4. D

| 英文简称 | 英文全称 | 中文全称 | 备注 |
| -------- | -------- | -------- | ---- |
| DoD | Department of Defense  | 国防部 | |
| DNS | Domain Name System | 域名系统 | 因特网上作为域名和IP地址相互映射的一个分布式数据库，将域名转化为IP地址，能够使用户更方便的访问互联网，而不用去记住能够被机器直接读取的IP数串。共分为三级域名、二级域名、顶级域名。因特网采用层次树状结构命名方法，由多个域名服务器共同完成。每个服务器接收到域名后尝试解析，如果不能解析则传给上一层服务器 |
| DSU | Data Service Unit | 数据服务单元 | 数字传输的一种设备，将DTE设备上的物理层接口适配到T1或者E1等通信设施上 |
| DSA | Digital Signature Algorithm | 数字签名算法 | 是数字签名标准的一个子集，表示了只用作数字签名的一个特定的公钥算法 |
| DSAP | Destination Service Access Point | 目标服务访问点 | |
| DSSS | Direct Sequence Spread Spectrum | 直接序列扩频 | |
| DS | Distribution System | 分发系统 | |
| DIFS | Distributed Inter-frame Spacing | 分布协调功能帧间间隔 | |
| DHCP | Dynamic Host Configuraion Protocol | 动态主机配置协议 | 是一个局域网的网络协议，使用UDP协议工作，主要有两个用途：给内部网络或网络服务供应商自动分配IP地址，给用户或者内部网络管理员作为对所有计算机作中央管理的手段 |
| DVP | Distance-Vector Protocols | 距离矢量协议 | 通过计算目标路由器与源路由器之间的距离矢量和来选择最佳路径，有频繁和周期性的更新，每次更新都将整张路由表发给周围的路由器，包括RIP, IGRP等 |
| DV | Distance-Vector | 距离矢量 | |
| DR | Designated Router | 指定路由器 | 指定路由器，在OSPF多路访问网络中，在同一个区域内被选举出来代表所有路由的路由。为了减少在同一个网段中几个邻居互相交换信息的数量 |
| DTE | Data Terminal Equipment | 数据终端设备| |
| DCE | Data Communication Equipment | 数据通信设备 | |
| DSL | Digital Subscriber Line | 数字用户线路 | 就是利用数字技术对现有的模拟电话用户线进行改造，使其能承载宽带业务,将0-4kHz的低端频谱留给传统电话使用，而把原来没有被利用的高端频谱留给用户上网使用 |
| DMT | DiscreteMultiTone | 多载波通信 | 我国当前正在采用的调制技术，"多音调"指的是"多载波"或"多子信道" |
| DSLAM | Digital Subscriber Line Access Multiplexer | 数字用户线接入复用器 | |
| DES | Data Encryption Standard | 数据加密标准 | 是一种使用密钥加密的块算法 |
| DNA | Digital Network Architecture | 数字网络架构 | |
| DNAT | Dynamic Network Address Translator | 动态网络地址转换 |
| DOS | Disk Operation System | 磁盘操作系统 | 是个人计算机上的一类操作系统 |
| DSS | Digital Signature Standard | 数字签名标准 | 美国政府用来指定数字签名算法的一种标准 |
| D Channel | Delta Channel | D 信道 | 信号信息(signaling information)，通过LAPD(Link Access Procedure of D-Channel，D信道链路规程)，D信道工作在16 kbps的速率下，用于告诉公用交换电话网络如何处理B信道 |
| DDR | dial-on-demand routing | 按需拨号路由 | DDR自动建立和释放电路交换请求，通过网络流量体现了透明的连接, DDR也通过负载阈值(load threshold)控制B信号的建立和释放 |

# 5. E

| 英文简称 | 英文全称 | 中文全称 | 备注 |
| -------- | -------- | -------- | ---- |
| EIA | Electronic Industies Alliance | 电子工业联盟 | 美国电子行业标准制定者之一 |
| EMI | Electromagnetic interference | 电磁干扰 | |
| ESS | Extended Service Set | 扩展服务集 | |
| EIGRP | Enhanced Interior Gateway Routing Protocol | 增强内部网关路由协议 | 增强内部网关协议，也是一种LSP和DVP混合的协议 |
| EGP | Exterior Gateway Protocols | 外部网关协议 | 在自治网络间交换路由的协议 |
| EBCDIC | Extended Binary Coded Decimal Interchange Code | 扩展二进制编码的十进制交换码 | |
| EEPROM | Electronically Erasable Programmable Read-only Memort | 电子可擦可编程制度存储器 | |

# 6. F

| 英文简称 | 英文全称 | 中文全称 | 备注 |
| -------- | -------- | -------- | ---- |
| FTP | File Transfer Protocol | 文件传输协议 | FTP是可靠的，面向连接的服务。基于TCP 20和21端口，工作流程：首先通过套接字建立控制连接，然后建立数据连接，通过数据连接传输数据 |
| FDM | Frequency Division Multiplexing | 频分复用 | 用户在分配到一定的频带后，在通信过程中自始至终都占用这个频带 |
| FM | Frequency Modulation | 调频 | 是一种以载波的瞬时频率变化来表示信息的调制方式，通过利用载波的不同频率来表达不同的信息 |
| FDDI | Fiber Distributed Data Interface | 逻辑环拓扑 | |
| FCS | Frame Check Sequences | 帧检验序列码 | |
| FTTH | Fiber To The Home | 光纤到家 | |
| FTTB | Fiber To The Building | 管线到大楼 | |
| FTTC | Fiber To The Curb | 光纤到路边 | |

# 7. G

| 英文简称 | 英文全称 | 中文全称 | 备注 |
| -------- | -------- | -------- | ---- |
| GIF | Graphic Interchange Format | 图形交换格式 | |
| gTLD | Generic Top Level Domain | 通用顶级域 | |

# 8. H

| 英文简称 | 英文全称 | 中文全称 | 备注 |
| -------- | -------- | -------- | ---- |
| HTTP | Hypertext Transfer Protocol | 超文本传输协议 | 物理层的 PDU是数据位(bit)，数据链路层的 PDU是数据帧(frame)，网络层的PDU是数据包(packet)，传输层的 PDU是数据段(segment)，其他更高层次的PDU是数据(data) |
| HTML | HyperText Markup Language | 超文本标记语言 | |
| HDLC | High-Level Data Link Control | 高级数据链路控制 | 是一个在同步网上传输 数据、面向比特的数据链路层协议，它是由国际标准化组织(ISO)根据IBM公司的SDLC(Synchronous Data Link Control)协议扩展开发而成的 |
| HFC | Hybird Fiber Coax | 混合光纤同轴电缆 | 是在目前覆盖面很广的有线电视网 CATV 的基础上开发的一种居民宽带接入网(没错，就是有线通) |
| HDSL | High Speed Digital Subscriber Line | 高速数字用户线 | |

# 9. I

| 英文简称 | 英文全称 | 中文全称 | 备注 |
| -------- | -------- | -------- | ---- |
| ISP | Internet Service Providers | 互联网服务提供商 | 向广大用户综合提供互联网接入业务、信息业务、和增值业务的电信运营商 |
| ICP | Internet Content Provider | 互联网内容提供商 | 向广大用户综合提供互联网信息业务和增值业务的电信运营商 |
| ISO | Internet Organization for Standardization | 国级标准化组织 | |
| IP | Internet Protocol | 网际互联协议 | 由network ID与host ID组成,0-127 Class A address,128-191 Class B address,192-223 Class C address,224-239 Class D-Multicast,240-255 Class E-Research |
| ISDN | Integrated Services Digital Network | 综合业务数字网 | 以电话综合数字网为基础发展成的通信网，能提供端到端的数字连接，用来承载包括话音和非话音在内的多种电信业务。 |
| IEEE | Institute of Electrica and Electronics Engineers | 电气与电子工程师学会 | IEEE主要关注以太网技术标准的制订。IEEE的工作重点是以传统以太网为基础，研究制定应用于城域网的新型以太网技术标准 |
| IEEE MAC Sub_layer | Institute of Electrica and Electronics Engineers MAC Sub_layer | 电气与电子工程师学会的MAC子层划分 | IEEE将数据链路层分成LLC (Logical Link Control，逻辑链路控制)和MAC(Media Access Control，介质访问控制)两个子层。MAC控制各个host对media的使用权。MAC子层定义了frame如何在物理线上运输，处理物理地址，定义网络拓扑和网线使用规则。|
| IGP | Interior Gateway Protocols | 内部网关协议 | 是一个在自治网络内网关间交换路由的协议 |
| IGRP | Interior Gateway Routing Protocol | 内部网关路由协议 | |
| ICMP | Internet Control Message Protocol | 因特网控制报文协议 | 是为了提高IP数据报交付成功的机会，允许主机或路由器报告差错情况和提供有关异常情况报告的协议，运行在IP层 |
| IOS | Internet Operating System | 互联网操作系统 | |
| IS-IS | Intermediate System-to-Intermediate System | 中间系统到中间系统协议 | 中间系统到中间系统，是一种LSP和DVP混合的协议 |
| IETF | The Internet Engineering Task Force | 国际互联网工程任务组 | |
| Internet | Internet | 互联网 | 互联网；指当前全球最大的、最开放的由众多网络相互连接而成的特定互连网，它采用TCP/IP协议族作为通信的规则，且其前身是美国的ARPANET |
| internet | internet | 互连网 | 泛指多个计算机网络互连而成的计算机网络 |
| ILD | injection laser diode | 注入式激光二极管 | |
| IFP | Inter-Frame Space | 帧间间隔 | |

# 10. J

| 英文简称 | 英文全称 | 中文全称 | 备注 |
| -------- | -------- | -------- | ---- |
| JPEG | Joint Photographic Experts Group | 联合图像专家组 | |

# 11. K

| 英文简称 | 英文全称 | 中文全称 | 备注 |
| -------- | -------- | -------- | ---- |

# 12. L

| 英文简称 | 英文全称 | 中文全称 | 备注 |
| -------- | -------- | -------- | ---- |
| LAN | Local Area Networks | 局域网 | 是指在某一区域内由多台计算机互联成的计算机组 |
| LLC | Logical Link Control | 逻辑链路控制 | 是局域网中数据链路层的上层部分。用户的数据链路服务通过LLC子层为网络层提供统一的接口。逻辑上标志不同的协议类型并且封装起来。处理差错通知，网络拓扑和流控制。 |
| LSP | Link State Protocols | 链路状态协议 | 每个路由器都了解整个网络的拓扑结构，利用算法计算两个路由之间的最短路径，更新由事件触发，每次更新都只向周围的路由器传递路由表的更新信息，包括OSPF等 |
| LSA | Link-state Advertisement | 逻辑链路广播 | |
| LS | Link-State | 链接状态 | |
| ISL | Inter-Switch Link | 交换链路内协议 | 思科的专利，再封装一遍帧，加上VLAN的信息 |
| LAPB | Link Access Procedure, Balanced | 平衡的链路访问程序 | |
| LCP | Link Control Protocol | 链路控制协议 | 建立链路，配置连接选项，检测链路质量。 |
| LED | light-emitting diode | 发光二极管 | |

# 13. M

| 英文简称 | 英文全称 | 中文全称 | 备注 |
| -------- | -------- | -------- | ---- |
| MAC | Media Access Control | 介质访问控制 | OSI模型中，数据链接层的子层。MAC地址是OSI模型中对应数据链路层的地址，每个网络位置都有一个唯一的编号。定义了物理线路上怎样传输帧。解决了物理地址问题，定义网络拓扑和流水线 |
| MTU | Maximal Transfer Unit | 最大传输单元 | |
| MSL | Maximum Segment Lifetime | 报文最长存活时间 | |
| MIME | Multipurpose Internet Mail Extensions | 多用途互联网邮件扩展类型 | |
| MSS | Maximum Segment Size | 最大报文段长度 | 用于在TCP连接建立时，收发双方协商通信时每一个报文段所能承载的最大数据长度 |


# 14. N

| 英文简称 | 英文全称 | 中文全称 | 备注 |
| -------- | -------- | -------- | ---- |
| NAP | Network Access Point| 互联网接入点 | 是因特网的路由选择层次体系中的通信交换点 |
| NIC | Network Interface Controller | 网络接口控制器 | |
| NRZ | Non-Return to Zero | 不归零制码 | 信号电平的一次反转代表1，电平不变化表示0，并且在表示完一个码元后，电压不需回到0 |
| NAV | Network Access Vector | 网络分配向量 | NAV 指出了信道处于忙状态的持续时间 |
| NAT | Network Address Translation | 网络地址转换 | 网络地址转换，将网络内部的私有IP地址转换为公有IP地址以节省IP地址的方法。只能一对一映射 |
| NVRAM | Non-volatile Random Access Memory | 非易失随机存取存储器 | 非易失性RAM，用来存储存储备份或启动配置文件，关机或重启后信息不会丢失 |
| NBMA | Nonbroadcasr Multi-access | 非广播多路复用 | |
| NCP | Network Layer Protocol | 网络层协议 | 选择和配置 3 层协议 |
| Network | Network | 网络 | 网络是一个由对象、设备或人组成的错综复杂的系统 |
| NFS | Network File System | 网络文件系统 | |
| NSA | National Security Agency | 美国国家安全局 | 是美国政府机构中最大的情报部门，专门负责收集和分析外国及本国通讯资料 |
|NMS | Network Management System | 网管 | 通过下发请求对上网的所有的主机关于流量等等信息进行管理(监控) | 
# 15. O

| 英文简称 | 英文全称 | 中文全称 | 备注 |
| -------- | -------- | -------- | ---- |
| OSI | Open System Interconnection | 开发式系统互联 | OSI将计算机网络体系结构(architecture)划分为以下七层：物理层、数据链路层、网络层、传输层、会话层、表示层、应用层 |
| OSI/RM | Open System Interconnection Reference Model | 开放式系统互联引用 | "开放"是指非独家垄断的，因此只要遵循OSI标准，一个系统就可以和位于世界上任何地方的，也遵循这同一标准的其他任何系统进行通信。OSI将计算机网络体系结构(architecture)划分为以下七层：物理层、数据链路层、网络层、传输层、会话层、表示层、应用层 |
| OUI | Organizational Unique Identifier | 组织唯一标识符 | |
| OFDM | Orthogonal Frequency Division Multiplexing | 正交频分复用 | 将信道分成若干正交子信道，将高速数据信号转换成并行的低速子数据流，调制到在每个子信道上进行传输 |
| OSPF | Open Shortest Path First | 开发式最短路径优先 | 基于分布式的链路状态协议，适用于大型互联网。OSPF只在链路状态发生变化时，才用向本自治系统内的所有路由器，用洪泛法发送与本路由器相邻的所有路由器的链路状态信息，最终了解全网的拓扑结构图。 |
| OC | Optical Carrier | 光载波 | |

# 16. P

| 英文简称 | 英文全称 | 中文全称 | 备注 |
| -------- | -------- | -------- | ---- |
| PM | Phase Modulation | 调相 | 载波的相位对其参考相位的偏离值随调制信号的瞬时值成比例变化的调制方式，称为相位调制，或称调相 | 
| PING | Packet Internet Groper | 因特网包探测器 | 用于测试网络连接量的程序。使用了ICMP回送请求和回送回答报文，是应用程序直接使用网络层ICMP的例子，没有通过TCP/UDP |
| PAT | Port Address Translation | 端口地址转换 | 是对网络地址转换(NAT)的扩展，它允许本地网(LAN)上的多个设备映射到一个单一的公共IP地址 |
| POP3 | Post Office Protocol 3 | 邮局协议3 | 用于从服务器读取邮件。本协议主要用于支持使用客户端远程管理在服务器上的电子邮件 |
| POST | Power On Self Test | 开机自检 | |
| PVC | Permanent Virtual Circuit | 永久虚拟电路 | |
| PPP | Point-to-Point Protocol | 点对点协议 | 是为在同等单元之间传输数据包这样的简单链路设计的数据链路层协议，是数据链路层使用最多的一种协议。这种链路提供全双工操作，并按照顺利传递数据包。特点为：简单；只检测差错而不纠正差错，不进行流量控制；支持多种网络层协议 |
| PAP | Password Authentication Protocol | 密码认证协议 | 远程节点不不停的在链路路上反复发送⽤用户名/密码，直到验证通过或者连接终⽌止。不不健壮的身份认证协议，使⽤用明⽂文发送密码。连接建立前只有一次认证。 |
| PRI | Primary Rate Interface | 主速率接口 | 提供23B + D(T1或者叫DS1线路，美国和日本地区)或30B + D(E1 线路，欧洲地区)，B信道和D信道都工作在64 kbps的速率下 |
| PDU | Protocol Data Unit | 协议数据单元 | 是指对等层次之间传递的数据单位。 物理层的 PDU是数据位(bit)，数据链路层的 PDU是数据帧(frame)，网络层的PDU是数据包(packet)，传输层的 PDU是数据段(segment)，其他更高层次的PDU是数据(data) |
| PDU | Packet Data Unit | 分组数据单元 | |
| PID | Port Identification | 端口ID | 2字节，由优先级和端口号组成，用于选举根端口和指派端口等 |
| Proxy ARP | Proxy Address Resolution Protocol | 代理地址解析协议 | 是通过使用一个主机(通常为router)，来作为指定的设备对另一设备的ARP请求作出应答。代理ARP是ARP协议的一个变种。 对于没有配置缺省网关的计算机要和其他网络中的计算机实现通信，网关收到源计算机的ARP请求会使用自己的MAC地址与目标计算机的IP地址对源计算机进行应答。代理ARP就是将一个主机作为对另一个主机ARP进行应答 |

# 17. Q

| 英文简称 | 英文全称 | 中文全称 | 备注 |
| -------- | -------- | -------- | ---- |

# 18. R

| 英文简称 | 英文全称 | 中文全称 | 备注 |
| -------- | -------- | -------- | ---- |
| RZ | Return to Zero | 归零制码 | 是信号电平在一个码元之内都要恢复到零的编码方式 |
| RARP | Reverse Address Resolution Protocol | 反向地址解析协议 | ARP为IP到MAC的转换，而RARP为MAC到IP的转换，向RARP服务器请求分配IP。主要流程：发出要反向解析的物理地址并希望返回其对应的IP地址。发送主机发送一个本地的 RARP 广播，在此广播包中，声明自己的 MAC 地址并且请求任何收到此请求的 RARP 服务器分配一个 IP 地址。 本地网段上的 RARP服务器收到此请求后，检查其 RARP 列列表，查找该 MAC 地址对应的 IP 地址。 如果存在，RARP服务器器就给源主机发送一个响应数据包并将此 IP 地址提供给对方主机使用; 如果不存在，RARP服务器对此不做任何的响应。 源主机收到从 RARP 服务器的响应信息，就利用得到的 IP 地址进行通讯;如果一直没有收到 RARP 服务器的响应信息，表示初始化失败。 |
| RIP | Routing Information Protocol | 路由信息协议 | 分布式基于距离向量的路由选择协议，只适用于小型网络。按固定的时间间隔与相邻路由器交换信息。交换的信息是自己当前的路由表，即到达本自治系统中所有网络的(最短)距离，以及到每个网络应经过的下一跳路由器。但是不知道全网的拓扑结构。 |
| RAM | Random Access Memory | 随机存取存储器 | |
| ROM | Read-only Memory | 只读存储器 | |
| RPC | Remote Procedure Call | 远程过程调用 | 透明访问远程程序，就好像本地一样 |
| RFI | Radio Frequency Interference | 射频干扰 | |
| RADSL | Rate-Adaptive Digital Subscriber Line | 速率自适应DSL，是ADSL的一个子集，可自动调节线路速率 |


# 19. S

| 英文简称 | 英文全称 | 中文全称 | 备注 |
| -------- | -------- | -------- | ---- |
| SMTP | Simple Mail Transfer Protocol | 简单邮件传输协议 | 它是一组用于由源地址到目的地址传送邮件的规则，由它来控制信件的中转方式。SMTP协议属于TCP/IP协议族，它帮助每台计算机在发送或中转信件时找到下一个目的地。通过SMTP协议所指定的服务器,就可以把E－mail寄到收信人的服务器上了，整个过程只要几分钟。SMTP服务器则是遵循SMTP协议的发送邮件服务器，用来发送或中转发出的电子邮件。用于: 用户代理把邮件传送到服务器；在邮件服务器之间的传送 |
| SONET | Synchronous optical network | 同步光网络 | 美国的光传送网标准 |
| SDH | Synchronous Digital Hierarchy | 同步数字系列 | SONET应用在美国和加拿大，SDH应用在世界其他国家 | 
| STP | Shielded Twisted Pair | 屏蔽双绞线 | 是一种广泛用于数据传输的铜质双绞线 |
| STP | Spanning Tree Protocol | 生成树协议 | 该协议可应用于在网络中建立树形拓扑，消除网络中的环路，并且可以通过一定的方法实现路径冗余，但不是一定可以实现路径冗余 |
| ScTP | Screened Twisted Pair | 屏蔽双绞线 | 是一种广泛用于数据传输的铜质双绞线。// 注意，这里的2,3两种虽然都是屏蔽双绞线，但是它们的结构略有不同，详见第2章ppt的7、8两页。此处的ScTP不是著名的**SCTP协议** |
| STDM | Statistic Time Division Multiplexing | 统计时分复用 | 是一种根据用户实际需要动态分配线路资源的时分复用方法 |
| SSAP | Source Service Access Point | 源服务访问点 |
| SSID | Service Set Identifier | 服务集标识符 | |
| SIFS | Short Interframe Space | 短帧间间隔 | |
| SCTP | Stream Control Transmission Protocol | 流控制传输协议 | 进行视频和音频的传输 |
| SNMP | Simple Network Management Protocol | 简单网络管理协议 | 由一组网络管理的标准组成，包含一个应用层协议(application layer protocol)、数据库模型(database schema)和一组资源对象。该协议能够支持网络管理系统，用以监测连接到网络上的设备是否有任何引起管理上关注的情况。 |
| SPF | Shortest Path First | 最短路径优先算法 | 最短路径算法，这个算法其实就是Dijkstra算法，是LSP中计算路径的一种方式 |
| SVC | Switched Virtual Circuits | 交换虚拟电路 | | 
| SQL | Structured Query Language | 结构化查询语言 | |
| SCP | Session Control Protocol | 会话控制协议 | |
| SDSL | Single-line Digital Subscriber Line | 1对线的数字用户线 | |
| SLIP | Serial Line Internet Protocol | 串行线路网际协议 | 只支持IP协议、不支持动态IP分配、不支持认证、不支持压缩、不支持检错 |
| SPID | Service Profile Identifier | 服务档案标识符 | 用来标识用户身份，并且配置线路(就是用户名)，14位数字 |
| STS | Synchronous Transport Signal | 同步传输信号 | |
| STM | Synchronous Transfer Module | 同步传输模块 | 
| SRA | Seamless Rate Adaptation | 无缝速率自适应技术 | |

# 20. T

| 英文简称 | 英文全称 | 中文全称 | 备注 |
| -------- | -------- | -------- | ---- |
| TCP | Transmission Control Protocal | 传输控制协议 | 一种面向连接的、可靠的、基于字节流的传输层通信协议，不支持单播和组播 |
| TFTP | Trivial File Transfer Protocol | 一般文本传输协议 | TCP/IP协议族中的一个用来在客户机与服务器之间进行简单文件传输的协议，提供不复杂、开销不大的文件传输服务。无连接的服务。基于UDP，小且容易实现 |
| TDM | Time Division Multiplexing | 时分复用 | 采用同一物理连接的不同时段来传输不同的信号，达到多路传输的目的 或者是 时分复用是将时间划分为一段段等长的时分复用(TDM)帧，每个时分复用的用户在每个 TDM 帧中占用固定序号的时隙 |
| TIA | Telecommunications Industry Association | 电信工业协会 | 是全方位的服务性国家贸易组织 | 
| TTL | Time To Live | 生存时间 | |
| TPDU | Transport Protocol Data Unit | 传送协议数据单元 | |
| TLD | Top Level Domain | 顶级域 | 国家TLD:`.cn .us .uk`,通用TLD:`.com .net .org .edu .gov .mil .int .aero .biz .cat .coop .info .jobs .mobi .museum .name .pro .travel`,基础TLD:`.arpa`,提供域名反查服务 |

# 21. U

| 英文简称 | 英文全称 | 中文全称 | 备注 |
| -------- | -------- | -------- | ---- |
| UDP | User Datagram Protocol | 用户数据包协议 | 是OSI参考模型中一种无连接的传输层协议，提供面向事务的简单不可靠、无连接、无确认、无流控制的信息传送服务 |
| UTP | Unshielded Twisted Pair | 无屏蔽双绞线 | 由8根不同颜色的线分成4对绞合在一起，无金属屏蔽材料；线缆不需要接地，因此便于在线缆末端加上连接器；价格低廉；直径小，因此安装简单且更适合安装在管道中；和其他铜传输介质具有一样的数据传输速率；使用RJ连接器后极大地降低了噪音的影响。 |
| UL | Underwriters Laboratories | 美国保险商安全标准 | |
| URL | Uniform Resource Locator | 统一资源定位符 | |
| UIB | User Interface Box | 用户接线盒 | |

# 22. V

| 英文简称 | 英文全称 | 中文全称 | 备注 |
| -------- | -------- | -------- | ---- |
| VLSM | Variable Length Subnet Masks | 可变长度子网掩码 | 规定了一个网络在划分子网时的不同部分使用不同的子网掩码，更有效的使用IP地址；使用路由汇总的能力更强 |
| VLAN | Virtual Local Area Network | 虚拟局域网 | 是一组逻辑上的设备和用户，这些设备和用户并不受物理位置的限制，可以根据功能、部门及应用等因素将它们组织起来，相互之间的通信就好像它们在同一个网段中一样，由此得名虚拟局域网。用于划分逻辑子网。工作在第二层和第三层。**可以分割广播域** |
| VTP | VLAN Trunking Protocol | VLAN中继协议 | |
| VPN | Virtual Private Network | 虚拟专用网络 | |
| VDSL | Very High Speed Digital Subscriber Line | 甚高速数字用户线 |


# 23. W

| 英文简称 | 英文全称 | 中文全称 | 备注 |
| -------- | -------- | -------- | ---- |
| WAN | Wide Area Networks| 广域网 | 指一种跨地区的数据通讯网络,通常包含一个国家或地区 |
| WDM | Wavelength Division Multiplexing | 波分复用 | 就是光的频分复用 |
| WSP | Wireless Session Protocol | 无线会话协议 | |
| WSP | WAN Service Provider | WAN服务提供者 | |


# 24. X

| 英文简称 | 英文全称 | 中文全称 | 备注 |
| -------- | -------- | -------- | ---- |

# 25. Y

| 英文简称 | 英文全称 | 中文全称 | 备注 |
| -------- | -------- | -------- | ---- |

# 26. Z

| 英文简称 | 英文全称 | 中文全称 | 备注 |
| -------- | -------- | -------- | ---- |

# 27. 其他名词简单解释
1. Frame Relay；帧中继；是一种用于连接计算机系统的面向分组的通信方法。它主要用在公共或专用网上的局域网互联以及广域网连接。大多数公共电信局都提供帧中继服务，把它作为建立高性能的虚拟广域连接的一种途径。
2. Data；数据；数据是二进制序列的表示。
3. Protocol；协议；协议定义消息传输和传递的详细方式。
4. Data Packets；数据分组；为了传输方， 计算机数据通常被分解成小的、易传输的单元，称为数据分组。
5. Symmetric Switching: 对称交换。交换机上所有端口带宽一样
6. Asymmetric Switching: 非对称交换。不同端口带宽不同
7. Store-and-Forward: 储存转发式交换。交换机收到帧后，先校验CRC再转发
8. Cut-through: 直通式交换。不校验就转发
9. Fast forward Switching: 快速转发交换。只查看目的MAC地址后就转发。
10. Fragment Free: 免碎片。转发前查看帧前64字节以减少线路上噪声造成的错误。
11. L2 Switching: Layer 2 Switching，二层交换
12. L3 Switching: Layer 3 Switching，三层交换
13. L4 Switching: Layer 4 Switching，四层交换
14. Multilayer Switching: 多层交换
15. backbone: 主干。用于VLAN间的通信。
16. Frame Filtering: 帧过滤。阻止不符合条件的帧。
17. Frame Tagging: 帧标记。在每个要被在主干线路上转发的帧的头部加上一个独特的标签，用来标识它来自哪一个VLAN。离开主干线路时被去除。
18. Static VLAN: 静态VLAN。直接指派端口所属的VLAN。
19. Dynamic VLAN: 动态VLAN。当有新的节点插入端口时，交换机查表来动态配置这个端口所属的VLAN
20. Port-Centric VLAN: 以端口为中心的VLAN。同一VLAN下的所有节点接入到同一个路由器接口上，或者反过来说，接入同一个路由器端口的节点被划分到同一个VLAN下。
21. Access Link: 接入链路。其上只有一个VLAN的链路。这个VLAN被称为这个链路对应的端口的本地VLAN。
22. Trunk Link: Trunk链路(就这么叫吧，硬要叫的话是 主干链路)。其上有多个VLAN的链路。用于连接交换机与交换机或路由器。(总之其实就是一根线上多个VLAN的帧在跑，所以这些帧得打上标签标识它来自于哪一个VLAN，不然就搞混了。到达对面的交换机之后再根据标签把这些帧转发到对应的VLAN里面去。Trunk链路最大的好处只是省端口和方便配置，以牺牲一点性能为代价。)
23. Trunk链路也可以有本地VLAN，即在trunk链路因为一些原因失败的时候使用的VLAN。
24. Routing Between VLANs: VLAN间路由
25. Infrastructure Mode：基础建设模式
26. Toll Network ：长途通信网
27. CO Switch ：中心局交换机
28. 流量控制Flow Control：让发送方的发送速率不要太快，要让接收方来得及接收。
29. 拥塞控制Congestion Control：防止过多的数据注入到网络中，这样可以使网络中的路由器或链路不致过载。
30. Socket:TCP连接的端点，表示为(IP address：port)。一个连接表示为(socket_sourse,socket_des)
31. Computer virus病毒：编制者在计算机程序中插入的破坏计算机功能或者数据的代码，能影响计算机使用，能自我复制的一组计算机指令或者程序代码
32. simplex transmission：单工。只能有一个方向的通信，没有反⽅方向的交互。
33. half-duplex transmission：半双工。信号可双向传输，但不能同时发送或同时接收。
34. full-duplex transmission：全双工。通信的双方可同时发送和接收消息，信号可同时双向传输。
35. Split horizon：水平分割是一种避免路由环路的出现和加快路由汇聚的技术。水平分割法的规则和原理是路由器从某个接口接收到的更新信息不允许再从这个接口发回去。
36. 冲突域(物理分段)：连接在同一导线上的所有工作站的集合，或者说是同一物理网段上所有节点的集合或以太网上竞争同一带宽的节点集合。
37. 广播域：接收同样广播消息的节点的集合。
