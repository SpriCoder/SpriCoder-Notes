Socket 编程
---

<!-- TOC -->

- [1. Socket简介](#1-socket简介)
- [2. Socket分类](#2-socket分类)
  - [2.1. 有连接的客户/服务器时序图](#21-有连接的客户服务器时序图)
  - [2.2. 无连接的客户/服务器时序图](#22-无连接的客户服务器时序图)
- [3. Socket常用函数](#3-socket常用函数)
  - [3.1. socket()函数](#31-socket函数)
  - [3.2. bind()函数](#32-bind函数)
  - [3.3. listen()和connect()函数](#33-listen和connect函数)
  - [3.4. accept()函数](#34-accept函数)
  - [3.5. read()、write()等](#35-readwrite等)
  - [3.6. close()操作](#36-close操作)
- [4. Linux的阻塞和非阻塞IO](#4-linux的阻塞和非阻塞io)
- [5. Java Socket API](#5-java-socket-api)
  - [5.1. 示例](#51-示例)
  - [5.2. TCP套接字](#52-tcp套接字)
    - [5.2.1. ServerSocket类](#521-serversocket类)
    - [5.2.2. Socket类](#522-socket类)
  - [5.3. 套接字传输数据](#53-套接字传输数据)
    - [5.3.1. 写入数据](#531-写入数据)
    - [5.3.2. 写出数据](#532-写出数据)
- [6. TCP套接字编程示例](#6-tcp套接字编程示例)
  - [6.1. Java示例](#61-java示例)
- [7. UDP](#7-udp)
  - [7.1. DatagramSocket类](#71-datagramsocket类)
  - [7.2. DatagramPacket类](#72-datagrampacket类)
  - [7.3. UDP套接字编程示例](#73-udp套接字编程示例)
  - [7.4. Java示例](#74-java示例)

<!-- /TOC -->

# 1. Socket简介
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/tec03/1.png)

1. 不在一个主机上，通过socket来满足需求，封装不同网络主机的请求

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/tec03/2.png)

2. 处理不同的细节存在一定的难度，Socket我们可以屏蔽一些底层设计。

# 2. Socket分类
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/tec03/3.png)


1. 流套接字:可靠
2. 数据报套接字:广播、简单
3. 原始套接字:保证IP完整性

## 2.1. 有连接的客户/服务器时序图
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/tec03/4.png)

1. 客户端一般是发起方

## 2.2. 无连接的客户/服务器时序图
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/tec03/5.png)

1. 动作一致

# 3. Socket常用函数
1. 这里的函数使用C作为演示。

## 3.1. socket()函数
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/tec03/6.png)

1. 协议簇:指定具体的协议
2. socket类型:
3. protocol协议:具体用什么协议
4. type和protocol是必须对应的
5. 返回一个描述符(在协议空间，但没有绑定IP地址)

## 3.2. bind()函数
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/tec03/7.png)

## 3.3. listen()和connect()函数
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/tec03/8.png)

## 3.4. accept()函数
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/tec03/9.png)

1. 空指针作为返回的协议地址(因为不知道是谁来进行请求的)

## 3.5. read()、write()等
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/tec03/10.png)

## 3.6. close()操作
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/tec03/15.png)

# 4. Linux的阻塞和非阻塞IO
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/tec03/11.png)

1. 文件描述符fd:是进程中文件的唯一索引
2. 套接字默认是阻塞模式，我在写别人不能写(修改阻塞态)

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/tec03/12.png)

1. count个字节的数据
2. 返回值:
   1. `>0`
   2. `0`
   3. `-1`：错误码进入errno
3. 阻塞模式:如果建立连接后则长时间占用文件，而非阻塞模式则会返回-1，判断EAGAIN
4. 使用read调用来读取指定长度的数据(阻塞模式)
   1. nread表示不是很重要的错误
   2. 返回读了多少
   3. bufp:下次开始读是从哪里开始读

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/tec03/13.png)

5. 使用read调用来读取指定长度的数据(非阻塞模式)

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/tec03/14.png)

# 5. Java Socket API
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/tec03/16.png)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/tec03/17.png)

## 5.1. 示例
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/tec03/18.png)

## 5.2. TCP套接字
1. Socket和ServerSocket

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/tec03/19.png)

### 5.2.1. ServerSocket类
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/tec03/20.png)

### 5.2.2. Socket类
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/tec03/21.png)

1. 主动连接；Socket

## 5.3. 套接字传输数据

### 5.3.1. 写入数据
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/tec03/22.png)

### 5.3.2. 写出数据
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/tec03/23.png)


# 6. TCP套接字编程示例
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/tec03/24.png)

## 6.1. Java示例
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/tec03/25.png)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/tec03/26.png)

1. Java进行了比较好的封装

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/tec03/27.png)

# 7. UDP
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/tec03/28.png)

## 7.1. DatagramSocket类
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/tec03/30.png)

## 7.2. DatagramPacket类
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/tec03/29.png)

## 7.3. UDP套接字编程示例
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/tec03/31.png)

## 7.4. Java示例
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/tec03/32.png)

1. 数据报最大1024字节

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Internet-computing/img/tec03/33.png)
