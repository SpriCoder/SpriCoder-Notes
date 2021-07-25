lecture09-局域网交换与VLAN
---
1. 网桥和路由器一般是通过软件来完成的，基于操作系统的。
2. 交换机是基于硬件的。

<!-- TOC -->

- [1. 交换机](#1-交换机)
  - [1.1. 交换机基本功能](#11-交换机基本功能)
  - [1.2. 对称交换(Symmetric Switching)](#12-对称交换symmetric-switching)
  - [1.3. 非对称交换(Asymmetric Switching)](#13-非对称交换asymmetric-switching)
    - [1.3.1. 内存缓冲](#131-内存缓冲)
  - [1.4. 交换方式](#14-交换方式)
    - [1.4.1. 储存转发(Store-and-Forward，网桥、路由器等通过软件的设备)](#141-储存转发store-and-forward网桥路由器等通过软件的设备)
    - [1.4.2. Cut-through 直通](#142-cut-through-直通)
    - [1.4.3. Segment-free Switching 无碎片转发](#143-segment-free-switching-无碎片转发)
  - [1.5. 第二层交换机](#15-第二层交换机)
  - [1.6. 第三层交换机](#16-第三层交换机)
  - [1.7. 第四层交换机](#17-第四层交换机)
  - [1.8. 多层交换机总结](#18-多层交换机总结)
- [2. 生成树协议(STP, The Spanning-Tree Protocol)](#2-生成树协议stp-the-spanning-tree-protocol)
  - [2.1. 桥回路](#21-桥回路)
  - [2.2. 冗余造成了路由回路](#22-冗余造成了路由回路)
  - [2.3. 第二层路由回路](#23-第二层路由回路)
    - [2.3.1. 第二层路由回路-泛洪单播帧](#231-第二层路由回路-泛洪单播帧)
  - [2.4. 生成树协议 综述](#24-生成树协议-综述)
    - [2.4.1. STP决策顺序(Seqence)](#241-stp决策顺序seqence)
    - [2.4.2. BPDUs(Bridge Protocol Data Unit)](#242-bpdusbridge-protocol-data-unit)
    - [2.4.3. STP的BPDU帧](#243-stp的bpdu帧)
    - [2.4.4. Bridge Identification/BID](#244-bridge-identificationbid)
    - [2.4.5. 选举根交换机](#245-选举根交换机)
  - [2.5. 路径代价 Cost](#25-路径代价-cost)
  - [2.6. Five STP States 5个STP状态](#26-five-stp-states-5个stp状态)
  - [2.7. 初始STP收敛](#27-初始stp收敛)
    - [2.7.1. 步骤1：根交换机决定](#271-步骤1根交换机决定)
    - [2.7.2. 步骤2：选择根端口](#272-步骤2选择根端口)
    - [2.7.3. 步骤3：选择网段的指定端口(I)](#273-步骤3选择网段的指定端口i)
- [3. VLAN(Virtual Local Area Network 虚拟局域网)](#3-vlanvirtual-local-area-network-虚拟局域网)
  - [3.1. 为什么引入VLAN？](#31-为什么引入vlan)
  - [3.2. VLAN可以不通过路由器就隔离广播域吗？](#32-vlan可以不通过路由器就隔离广播域吗)
  - [3.3. 虚拟局域网介绍](#33-虚拟局域网介绍)
    - [3.3.1. 现有的共享局域网配置](#331-现有的共享局域网配置)
    - [3.3.2. LAN和VLAN之间的差异](#332-lan和vlan之间的差异)
    - [3.3.3. VLANs (IEEE 802.1q)](#333-vlans-ieee-8021q)
    - [3.3.4. 分组用户](#334-分组用户)
      - [3.3.4.1. 没有 VLAN 时的网络广播](#3341-没有-vlan-时的网络广播)
      - [3.3.4.2. 划分了VLAN的网络广播](#3342-划分了vlan的网络广播)
    - [3.3.5. VLAN 间通信](#335-vlan-间通信)
    - [3.3.6. VLAN 和第3层转发来控制广播域](#336-vlan-和第3层转发来控制广播域)
  - [3.4. VLAN的结构](#34-vlan的结构)
    - [3.4.1. 虚拟局域网通过骨干网(BackBone)](#341-虚拟局域网通过骨干网backbone)
    - [3.4.2. 在虚拟局域网中的路由器的作用](#342-在虚拟局域网中的路由器的作用)
    - [3.4.3. 在虚拟局域网中的帧的使用](#343-在虚拟局域网中的帧的使用)
      - [3.4.3.1. Frame Filiter 帧过滤](#3431-frame-filiter-帧过滤)
      - [3.4.3.2. Frame Tagging 帧标记](#3432-frame-tagging-帧标记)
    - [3.4.4. Frame Tagging – IEEE802.1Q and ISL](#344-frame-tagging--ieee8021q-and-isl)
  - [3.5. 虚拟局域网的实现](#35-虚拟局域网的实现)
    - [3.5.1. 端口、虚拟局域网和广播](#351-端口虚拟局域网和广播)
    - [3.5.2. 静态VLANS](#352-静态vlans)
    - [3.5.3. 动态VLANS](#353-动态vlans)
    - [3.5.4. 以端口为中心的VLAN](#354-以端口为中心的vlan)
    - [3.5.5. 以端口为中心的VLAN的优点](#355-以端口为中心的vlan的优点)
    - [3.5.6. 接入和骨干连接](#356-接入和骨干连接)
    - [3.5.7. 访问连接](#357-访问连接)
    - [3.5.8. 主干链路](#358-主干链路)
    - [3.5.9. 交换机29xx中的配置](#359-交换机29xx中的配置)
    - [3.5.10. VLAN配置](#3510-vlan配置)
    - [3.5.11. 添加VLAN示例](#3511-添加vlan示例)
    - [3.5.12. 验证VLAN](#3512-验证vlan)
    - [3.5.13. 删除VLAN](#3513-删除vlan)
  - [3.6. 在局域网之间的路由](#36-在局域网之间的路由)
    - [3.6.1. 子接口](#361-子接口)
    - [3.6.2. 配置VLAN间路由](#362-配置vlan间路由)
    - [3.6.3. 配置VLAN间路由](#363-配置vlan间路由)
- [4. VLAN题目备注](#4-vlan题目备注)

<!-- /TOC -->

# 1. 交换机

## 1.1. 交换机基本功能
1. 根据MAC地址建立和维护**交换表**(类似于网桥表)
2. 将帧切换出接口到目标

## 1.2. 对称交换(Symmetric Switching)
1. 对称交换可在具有相同带宽(10/10 Mbps或100/100 Mbps)的端口之间提供交换连接
2. 用户尝试访问其他网段上的服务器时，可能会导致瓶颈(对称交换可能会导致带宽不足)

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec09/1.png)

>多个客户端向服务器访问的话，服务器端口流量会比较阻塞(在对称切换中，双端的带宽是完全对称的)，这是一个瓶颈。

## 1.3. 非对称交换(Asymmetric Switching)
1. 通过将带有服务器的网段连接到更高带宽的端口(100 Mbps)，非对称交换(asymmetric switching)减少了服务器上潜在瓶颈的可能性
2. 非对称交换需要在交换器中进行内存缓冲
3. 非对称交换端口解决对称交换端口中的对称阻塞问题(进一步保证了服务器的稳定实现)

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec09/2.png)

### 1.3.1. 内存缓冲
1. 交换机中存储目标和传输数据的内存区域，直到可以将其切换出正确的端口为止。
   1. 基于端口(Port)的内存缓冲
      1. 数据包存储在每个端口的队列中
      2. 由于目标端口繁忙，一个数据包可能会延迟其他数据包的传输
      3. 其他端口存在不均衡的问题。
   2. 共享(Shared)内存缓冲
      1. 所有端口共享的公用内存缓冲
      2. 允许将数据包在一个端口上接收并在另一个端口上发送出去，而无需将其更改为其他队列。
      3. 需要自己记录端口的信息
2. 发生阻塞的时候，根据情况按照端口或者内存将包缓存下来

## 1.4. 交换方式

### 1.4.1. 储存转发(Store-and-Forward，网桥、路由器等通过软件的设备)
1. 交换机**接收整个帧**，最后将其计算为CRC，然后再将其发送到目的地
2. 接收后，校验，正确再发送

### 1.4.2. Cut-through 直通
1. 转发会增加延迟:通过使用直通切换方法可以减少它
2. 快速转发切换:仅在立即转发帧之前检查目标MAC(只看到帧的目的地址就转发，而不看帧的后面的部分)

### 1.4.3. Segment-free Switching 无碎片转发
3. 碎片释放:在转发帧之前读取前64个字节以减少错误:避免碰撞和帧碎片
4. Exmaple:(三种不同的查看方式)

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec09/3.png)

## 1.5. 第二层交换机
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec09/4.png)

1. 大规模集成电路,保证链路效率,低时延,低成本
2. 有一个MAC地址

## 1.6. 第三层交换机
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec09/5.png)

1. 基于硬件的帧转发机制，较高的帧转发性能，低时延
3. 较高速的计算
4. 每一个端口的代价低
5. 流控制
6. 安全性更高
7. 对数据流进行路由，生成MAC和IP的映射
8. MAC地址过来的时候直接根据表从二层进行通过

## 1.7. 第四层交换机
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec09/6.png)

1. 数据段在数据报里面，数据报在数据帧里面
2. 只要交换机可以看到数据帧的数据部分的首部
3. 可以根据端口主机的应用特点进行一定的流量控制
4. 和Net OS是不一样的,没有那么智能
5. 识别到前80个字节的数据报长度，对指定应用进行管理

## 1.8. 多层交换机总结
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec09/7.png)

1. 一般我们只是用二层交换机
2. 交换机可以简单识别第三层和第四层信息

# 2. 生成树协议(STP, The Spanning-Tree Protocol)

## 2.1. 桥回路
1. 出于各种原因，网络中可能会出现**环路**。
   1. 通常，网络中的环路是故意(deliberate)提供冗余的结果。
   2. 也可能由于配置错误而发生:在桥接网络中，环路可能是绝对灾难性的两个主要原因：
      1. 广播回路(广播风暴)，没有TTL
      2. 路由表的错误
2. 往往是**第二层交换机**的冗余导致的桥回路。
3. 接入层到核心层的接入往往**要有冗余**，这个区域是主干网(backbone)

## 2.2. 冗余造成了路由回路
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec09/8.png)

- 设备通过backbone和远端设备进行链接

## 2.3. 第二层路由回路
1. 广播和第2层循环可能是危险的组合。
2. 以太网帧没有TTL字段
3. 以太网帧开始循环后，它可能会继续下去，直到有人关闭其中一台交换机或断开链路为止(外部条件)
4. 交换机将抖动(flip flop)主机A的桥接表条目(创建极高的CPU利用率)。
5. 消耗CPU和内存

### 2.3.1. 第二层路由回路-泛洪单播帧
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec09/9.png)

- 过一段时间CAT-1和CAT-2没有收到Host-B的信息，删除表中的对应记录
- 在这之后，Host A发送给Host B信息，然后在CAT-1和CAT-2之间进行循环

## 2.4. 生成树协议 综述
1. 生成树协议的元素
   1. 主要功能：在**交换/桥接网络**中允许**冗余路径**，而不会因环路的影响而引起延迟。
   2. STP通过计算**稳定的生成树**网络拓扑来防止环路
   3. **生成树帧**(称为桥协议数据单元-BPDU)用于确定生成树拓扑
2. 在正常情况下禁用一些端口来防止出现冗余

### 2.4.1. STP决策顺序(Seqence)
1. 生成树始终使用相同的四步决策序列：
   1. 在拓扑里面最低的root BID(网桥标识)
   2. 找到 Root bridgh的最低路径成本
   3. 每个路径都会选择一个最低BID的sender 这个是针对一个链路的，详见例子
   4. 每个路径再指定一个最低的ID端口

### 2.4.2. BPDUs(Bridge Protocol Data Unit)
1. BPDU是交换机之间的流量；它们不承载最终用户(end-user)流量。
2. STP建立一个称为**根网桥的根节点**，生成的树源自根桥。
3. 不属于最短路径树的冗余连接将被阻止。(block 端口，不转发，但是接收)
4. 在阻塞的链接上收到的数据帧将被丢弃。
5. 交换机发送的允许形成无环逻辑拓扑的消息是BPDU

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec09/10.png)

- BPDU里面包含几个字段标识协议、版本、数据类型、标志等，记录它认可的Root BID(类似OSPF)、到BID最小的代价、发送的交换机的ID、从哪个端口发送
- 和OSPF不一样的:不一定以自己为根
- 这样在选举之后，冗余链路就被屏蔽掉了。

### 2.4.3. STP的BPDU帧
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec09/11.png)

- 注意前四个是很有意义的
- 默认交换机每2s发送一次BPDU
- 主要是维护最短的路径
- 接收到BPDU帧的时候，会比较根ID，计算，如果更优则接受，反之则不接受。
- 经过一段时间的传递后会全局稳定。

### 2.4.4. Bridge Identification/BID
1. 网桥ID(BID)：8个字节(2 + 6)
   1. 高阶BID子字段(2个字节)：网桥优先级
      1. 2<sup>16</sup>个可能的值：0-65,535(默认值：32,768)
      2. 通常以十进制格式表示
   2. 低阶子字段(6个字节)：分配给交换机的MAC地址，以十六进制格式表示
2. STP成本值：成本越低越好。

### 2.4.5. 选举根交换机
1. 交换机通过查找具有**最低BID**的交换机(通常称为根战争)来选择单个根交换机。
2. 如果所有交换机都使用默认的网桥优先级32768，则最低的MAC地址将作为平局。
3. 配置优先级来调整根桥

## 2.5. 路径代价 Cost
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec09/12.png)

1. 桥梁使用成本的概念来评估它们与其他桥梁的距离。
2. 和OSPF算法相同的，这个标准是比较合适的，比之前OSPF要新，用固定的数值除以带宽来获得代价

## 2.6. Five STP States 5个STP状态
1. 通过根据策略配置每个端口来建立状态
2. 然后，STP根据流量模式(traffic Patterns)和潜在环路(Protential Loops)修改状态
3. STP状态的默认顺序为：
   1. 阻塞:没有转发帧，听到了BPDU
   2. 监听:不转发任何帧，监听数据帧(确定自己可以参加的交换)，也会发送一些数据帧表示自己状态变了
   3. 学习:不转发帧，学习地址
   4. 转发:转发帧，学习地址
   5. 禁用:没有转发帧，没有听到BPDU

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec09/13.png)

>STP过程:Blocking -> 20s Listening -> 15s Learning -> 15s Fowarding或者Disabled

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec09/37.png)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec09/38.png)

- 2s可以调整
- 老化时间:保存的时间

## 2.7. 初始STP收敛
1. 当网络首次启动时，所有网桥都会混合使用BPDU信息来泛洪网络。(开始泛洪BPDU信息)
2. 立即，他们应用决策序列，允许他们BPDU进行PK，然后选择出来ROOT，从而形成整个网络的单个生成树。
```
(Step 1) 根交换机决定：选择一个根桥作为该网络的中心点
(Step 2) 选择根端口：所有剩余的网桥都会计算出一组根端口
(Step 3) 选择指定端口：其余所有网桥计算一组指定端口
```

- Root switch针对一个特定的交换机
- 根端口针对一个交换机
- 指定端口对应链路

### 2.7.1. 步骤1：根交换机决定
1. 宣布自己为根
2. 检查端口上收到的所有BPDU以及将在该端口上发送的BPDU
3.  对于每个到达的BPDU，如果其值小于为端口保存的现有BPDU
   1. 旧值被替换
   2. BPDU的发送者被接受为新的根

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec09/14.png)

- BC收到后将根修改为A
- 比如在BC链路中，B的MAC地址比较小，作为链路的Sender BID，这个port是指定端口。

### 2.7.2. 步骤2：选择根端口
1. 每个非根桥必须选择一个根端口。
   1. 桥的根端口是最接近根桥的端口。
   2. 根路径成本是到根网桥的所有链接的累积(cumulative)成本。
2. STP成本随着在端口上接收到BPDU而增加，而不是随着它们从端口发送出去而增加。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec09/15.png)

>B会把上面一个端口做为Root Port，虽然两个可达，但是上面一个更快，C也是同样

### 2.7.3. 步骤3：选择网段的指定端口(I)
1. 每个网段都有一个指定的端口：充当单个网桥/交换机端口，该端口既向该网段又向根网桥发送流量，也从该网段和根网桥接收流量。
2. 包含给定网段的指定端口的网桥/交换机称为该网段的指定网桥。
3. 所有网桥/交换机将阻止它们上未指定的端口，根网桥上的每个活动端口都将成为指定端口
4. 每个链路只有一个指定端口，一旦选定其他就block了

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec09/16.png)

- BC之间的，左边是指定端口(BID小)
- MAC地址唯一的
- Root Port都是上面的

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec09/17.png)

- AB和AC之间的链路的指定端口是A上面的端口。

# 3. VLAN(Virtual Local Area Network 虚拟局域网)

## 3.1. 为什么引入VLAN？
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec09/39.png)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec09/40.png)

## 3.2. VLAN可以不通过路由器就隔离广播域吗？
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec09/41.png)

## 3.3. 虚拟局域网介绍

### 3.3.1. 现有的共享局域网配置
1. 在典型的共享局域网中...
   1. 根据用户所插入(plug)的集线器对用户进行物理分组
   2. 路由器分割局域网并提供广播防火墙
2. 在虚拟局域网中
   1. 您可以按使用的功能，部门或应用程序对用户进行逻辑分组
   2. 通过专有软件进行配置

### 3.3.2. LAN和VLAN之间的差异
1. 虚拟局域网
   1. 在第2层和第3层工作
   2. 控制网络广播
   3. 允许用户由网络管理员分配。
   4. 提供更严格的网络安全性。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec09/18.png)

- 左边是基于地理位置划分成子网(传统局域网)
- VLAN是是通过逻辑位置进行划分
- VLAN1的报文不会发送给VLAN2(虽然连接在一个交换机上)

### 3.3.3. VLANs (IEEE 802.1q)
1. 特点
   1. 不限于物理交换机网段的网络设备或用户的**逻辑分组**。
   2. VLAN中的设备或用户可以按功能，部门，应用程序等进行分组，而**不管其物理网段的位置**如何。
   3. VLAN**创建一个不限于物理网段**的单个广播域，并且将其视为子网。
   4. VLAN设置是由网络管理员使用供应商的软件在交换机中完成的。
2. 优点:
   1. 限制广播包，提高带宽的利用率。
   2. 增强通信的安全性:其他VLAN用户网络收不到非本VLAN的报文，避免被监听
   3. 创建虚拟工作组：可以一个部门工作的人划分为一个VLAN，这样子即使他移动了办公位置，仍然能够正常办公
   4. 增强网络的健壮性：将一些网络故障限制在一个VLAN中

### 3.3.4. 分组用户
1. VLAN可以从逻辑上将用户划分为不同的子网(广播域)
2. 广播帧仅在具有相同VLAN ID的一个或多个交换机的端口之间切换。(VLAN ID属于端口)
3. 可以通过基于以下内容的软件对用户进行逻辑分组：
   1. 端口号
   2. MAC地址
   3. 使用的协议
   4. 使用的应用

#### 3.3.4.1. 没有 VLAN 时的网络广播
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec09/19.png)

>大家在一个交换机上不可以进行划分

#### 3.3.4.2. 划分了VLAN的网络广播
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec09/20.png)

>各自角色之间单独进行通信，虽然连接的是同一个交换机，如果不在同一个VLAN上，相互之间也不能通信

### 3.3.5. VLAN 间通信
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec09/21.png)

- 首先127.17.10.21询问网关地址(ARQ)
- 路由器帮忙转发(VLAN的交换需要路由器的支持)
- 交换机S2的不同端口在不同的VLAN，S1和S2、S1和S3之间是VLAN骨干

### 3.3.6. VLAN 和第3层转发来控制广播域
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec09/22.png)

>第三层交换机:为每一个网段设置一个SVI(switch virtual interface,虚拟交换机结构，也可以理解为子接口)，通过这个来进行不同网段之间的通信

## 3.4. VLAN的结构

### 3.4.1. 虚拟局域网通过骨干网(BackBone)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec09/23.png)

1. VLAN配置需要支持互连的路由器和交换机之间的骨干数据传输。
2. 骨干网是用于VLAN间通信的区域
3. 骨干网应该是高速链路，通常为100Mbps或更高
4. BackBone可以跑多个VLAN，是骨干网

### 3.4.2. 在虚拟局域网中的路由器的作用
1. 路由器提供不同VLAN之间的连接
2. 例如，您有VLAN1和VLAN2。
   1. 在交换机内，位于不同VLAN上的用户无法相互通信(VLAN的好处！)
   2. 但是，VLAN1上的用户可以向VLAN2上的用户发送电子邮件，但他们需要路由器才能执行此操作。

### 3.4.3. 在虚拟局域网中的帧的使用
1. 交换机根据帧中的数据做出过滤和转发决策。
2. 使用了两种技术
   1. 帧过滤：检查有关每个帧的特定信息(MAC地址或第3层协议类型),特定的VLAN记录或者映射
   2. 帧标记：在整个网络骨干网中转发时，在每个帧的标题中放置一个唯一的标识符。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec09/24.png)

#### 3.4.3.1. Frame Filiter 帧过滤
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec09/25.png)

- 收到帧转发后，发现都不在一个LAN上，然后通过Backbone转发
- Frame Table在交换机上传输

#### 3.4.3.2. Frame Tagging 帧标记
1. 帧标记实施过程：
   1. 在整个网络骨干网中转发时，在每个帧的标题中放置一个VLAN标识符。
   2. 每个开关都可以理解和检查标识符。
   3. 当帧离开网络骨干网时，交换机会在帧发送到目标终端站之前删除标识符。只和端口绑定，而不影响主机
2. 帧标记在第2层起作用，并且几乎不需要处理或管理开销。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec09/26.png)

3. 从主机到了交换机端口，交换机端口进行标记，然后进行转发。

### 3.4.4. Frame Tagging – IEEE802.1Q and ISL
1. IEEE802.1Q:IEEE标准，在标头中插入VLAN的标签以标识所属的VLAN。(帧标记)。
2. ISL(Inter-Switch Link)：思科专有。ISL在数据帧的前面添加一个26字节的标头，并在末尾附加一个CRC(4字节)。
3. 推荐用IEEE802.Q
4. 标记一般在BackBone上

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec09/27.png)

## 3.5. 虚拟局域网的实现

### 3.5.1. 端口、虚拟局域网和广播
1. 实现VLAN的两种方法
   1. 静态的
   2. 动态的
2. 每一个端口绑定给一个VLAN
   1. 确保不共享同一VLAN的端口不共享广播。
   2. 确保共享相同VLAN的端口将共享广播。
3. 实现途径:
   1. 基于端口的虚拟局域网
   2. 基于MAC地址的虚拟局域网
   3. 基于IP地址的虚拟局域网
   4. 基于上层协议的虚拟局域网

### 3.5.2. 静态VLANS
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec09/28.png)

1. 定义：静态VLAN是指将交换机上的端口管理性地分配给VLAN的时间
2. 优点：
   1. 安全，易于配置和监控
   2. 在控制移动的网络中效果很好
3. 端口是写死在交换机的端口上的

### 3.5.3. 动态VLANS
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec09/29.png)

>1. 一个服务器来配置VLAN的信息
>2. 交换机通过MAC地址或者哪一个协议，指定是哪一个VLAN

1. 当工作站最初连接到未分配的端口时，交换机会检查表中的条目，并使用正确的VLAN动态配置端口
2. 优点
   1. 添加或移动用户时减少管理(更多前期工作)
   2. 集中通知未授权用户

### 3.5.4. 以端口为中心的VLAN
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec09/30.png)

- 实际的网络是有层次的
- static的物理的接入层(physical Layer)
- 不同电脑在一个房间内
- 不同房间的不同电脑组成一个VLAN
- 路由器网关来处理

### 3.5.5. 以端口为中心的VLAN的优点
1. 同一VLAN中的所有节点都连接到同一路由器接口
2. 使管理更容易，因为...
   1. 通过路由器端口分配用户
   2. VLAN易于管理。
   3. 提供更高的安全性
   4. 数据包不会"泄漏"到其他域

### 3.5.6. 接入和骨干连接
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec09/31.png)

- 分为两类:
   1. 接入链路:通过一个VLAN报文
   2. 骨干链路:通过多个VLAN报文

### 3.5.7. 访问连接
1. 访问连接是仅作为一个VLAN成员的交换机上的连接。
2. 此VLAN被称为端口的本机VLAN，连接到端口的任何设备都完全不知道VLAN存在。

### 3.5.8. 主干链路
1. 主干链路能够支持多个VLAN。
2. 主干链路通常用于将交换机连接到其他交换机或路由器。
3. 交换机在快速以太网和千兆位以太网端口上都支持骨干链路。
4. 也存在访问和骨干链接
5. 一般Trunk就是BackBone

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec09/32.png)

>1. Sa和Sb上面连接使用单独的线，浪费
>2. 底下使用串行的线，不浪费端口

1. 骨干是支持多个VLAN的点对点链接
2. 骨干用于在两个实现VLAN的设备之间创建链接时节省端口
3. 骨干链路不属于特定的VLAN：充当交换机和路由器之间VLAN的通道。
4. 可以将骨干链路配置为传输所有VLAN或有限数量的VLAN。
5. 但是，骨干链路可能具有本地VLAN。
6. 如果骨干线链路由于任何原因失败，则骨干线的本地VLAN是该骨干线使用的VLAN。
7. native VLAN是不发送无标记的信息。

### 3.5.9. 交换机29xx中的配置
1. 在Cisco 29xx交换机上配置VLAN时，必须遵循以下准则：
   1. VLAN的最大数量取决于交换机本身。
   2. VLAN 1是出厂默认VLAN之一。(native VLAN往往是VLAN1，以及广播也是)
   3. VLAN 1是默认的以太网VLAN。
   4. 思科发现协议(CDP)和VLAN骨干协议(VTP)通告在VLAN 1上发送。
   5. 默认情况下，Catalyst 29xx IP地址在VLAN 1广播域中。

### 3.5.10. VLAN配置
1. 步骤1：创建VLAN所需的步骤。 如果需要，还可以配置VLAN名称。
```
Switch# vlan database
Switch(vlan)# vlan vlan_number
Switch(vlan)# exit
```
1. 步骤2：将VLAN分配给一个或多个接口：
```
Switch(config)# interface fastethernet 0/9 Switch(config-if)# switchport access vlan vlan_number
```

### 3.5.11. 添加VLAN示例
```
cat2950#vlan database
cat2950(vlan)#vlan 9 name switchlab90
VLAN 9 added:
   Name: switchlab90
cat2950(vlan)#?
VLAN database editing buffer manipulation commands:
    abort Exit mode without applying the changes
    apply Apply current changes and bump revision number
    exit Apply changes, bump revision number, and exit mode
    reset Abandon current changes and reread current database Adding a VLAN Example
cat2950(config)#interface fa 0/2
cat2950(config-if)# switchport access vlan 9
```

### 3.5.12. 验证VLAN
1. `Switch# show vlan [vlanid]`

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec09/33.png)

>剩下的是默认VLAN

### 3.5.13. 删除VLAN
1. 删除VLAN后，分配给该VLAN的所有端口都将变为非活动状态。 但是，端口将一直与删除的VLAN关联，直到分配给新的VLAN。
2. `switch(vlan)# no vlan vlanid  [name /vlan-name]`
```
cat2950(vlan)#no vlan 9
Deleting VLAN 9...
cat2950(vlan)#exit
APPLY completed.
Exiting....
cat2950#
```

## 3.6. 在局域网之间的路由
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec09/34.png)

1. 每个端口连接一个VLAN，每个IP和一个VLAN连接
2. 如下图，我们使用串口线，物理上是一个一个接口，划分成多个IP和子接口

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec09/1.jpg)

- 对比如下:接入方式不同

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec09/35.png)

### 3.6.1. 子接口
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/lec09/36.png)

1. 物理上一个，划分成Fa0/1、Fa0/2和Fa/3
2. 涉及到的是单臂路由

### 3.6.2. 配置VLAN间路由
1. Step1:识别界面.`Router(config)#interface fastethernet port-number. subinterface-number`
2. Step2:定义VLAN封装.(一般用dot1q)`Router(config-if)#encapsulation dot1q vlan-number`
3. Step3:为接口分配IP地址
`Router(config-if)#ip address ip-address subnet-mask`

### 3.6.3. 配置VLAN间路由
```
Sydney(config)#interface FastEthernet 0/0 
Sydney(config-if)#full duplex 全双工
Sydney(config-if)#no shut
Sydney(config-if)#interface FastEthernet 0/0.1

Sydney(config-subif)#encapsulation 802.1q 1
Sydney(config-subif)#ip address 192.168.1.1 255.255.255.0
Sydney(config-if)#interface FastEthernet 0/0.2

Sydney(config-subif)#encapsulation 802.1q 20
Sydney(config-subif)#ip address 192.168.2.1 255.255.255.0
Sydney(config-if)#interface FastEthernet 0/0.3

Sydney(config-subif)#encapsulation 802.1q 30
Sydney(config-subif)#ip address 192.168.3.1 255.255.255.0
```

1. 如果是Trunk Link:应该使用交叉线，而不是直通线
2. 如果是Access Link:直通线

# 4. VLAN题目备注
1. 同一VLAN中的两台主机可以跨越多台交换机
2. 必须是第三层及以上的交换机才能用来构建VLAN