web service
---

# 1. 概述

## 1.1. A New Web Model
1. 一般用户使用Web的模式
   1. 浏览互相链接的文档
   2. 通过手工操作处理采购等商业事务
   3. 下载文件

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/web-serivce/1.png)

2. Web Service是使用Web的新模式
   1. 通过程序自动启动和处理商务事务，而并非使用浏览器
   2. 能够在一个分布式的计算环境中动态地描述、发布、发现和调用
   3. 基于Web Service的新型应用

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/web-serivce/2.png)

## 1.2. 面向服务架构的技术标准
1. SOA (Service Oriented Architecture)

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/web-serivce/3.png)

## 1.3. Web 服务
1. 可以在组织内部或者公司之间的异构计算资源中被共享、组合、使用和复用的商业资产
2. 是一个可编程的部件，提供一种易于通过Internet获取的商业服务
3. 可以是独立的，也可以连接在一起向外部世界提供更强大的系统功能
4. 是从分布式面向对象部件的系统向服务网络的逻辑演进，该服务网络提供一个能够跨企业集成的松散耦合的底层基础结构

## 1.4. What is a Web Service?
1. 一个能够使用XML消息通过网络来访问的Interface, 这个Interface描述了一组可访问的操作
   1. 由SOAP+WSDL包装的Object
   2. 适应松散耦合的网络环境，可通过Web访问，手段是SOAP Message
   3. 服务的行为、输入/输出都可使用WSDL描述

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/web-serivce/4.png)

## 1.5. Web services的特征
1. 良好的封装性
2. 松散耦合
3. 使用标准协议规范
4. 高度可集成能力

## 1.6. Web ServiceArchitecture Evolution
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/web-serivce/5.png)

## 1.7. Web Service与其他技术比较
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/web-serivce/6.png)

## 1.8. 考虑Web Services的理由
1. 业务上：需要与外部客户通信
2. 技术上：
   1. 应用需要与其它语言编写的客户程序通信
   2. 客户在防火墙之外
3. 管理上：管理托管web service 应用

## 1.9. 不适用Web Services
1. 客户程序与应用使用相同语言编写
2. 通信开销大
   1. 序列化或者远程访问开销大
   2. Web Services/XML 处理开销大
   3. Don’t Use XML to Communicate Unless You Really, Really Have To –Floyd Marinescu, The Middleware Company
3. Web Services/XML 是用于集成的

## 1.10. Web service应用场合
1. 适用场合
   1. 跨防火墙的通讯
   2. 应用程序集成
   3. B2B的集成
   4. 软件和数据重用
2. 不适用场合
   1. 单机程序
   2. 局域网的同构应用程序

# 2. web service 原理
1. Web Service 是为其它应用提供数据和服务的应用逻辑单元
2. 应用程序通过标准的Web 协议和数据格式获得Web Service，如HTTP、XML 和SOAP 等，每个Web Service 的实现完全独立
3. Web 服务是一个URL 资源，客户端可以通过编程方式请求得到它的服务，而不需要知道所请求的服务是怎样实现的，这一点与传统的分布式组件对象模型不同

## 2.1. web service模型
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/web-serivce/7.png)

## 2.2. web服务角色的相互关系
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/web-serivce/8.png)

1. "发布"是为了让用户或其他服务知道某个Web服务的存在和相关信息
2. "查找（发现）"是为了找到合适的Web 服务
3. "绑定"则是在提供者与请求者之间建立某种联系

## 2.3. 完整的web服务步骤
1. Web 服务提供者设计实现Web 服务，通过Web 服务中介者发布，在UDDI 注册中心注册；（发布）
2. Web 服务请求者向Web 服务中介者请求特定的服务，中介者根据请求查询UDDI 注册中心，为请求者寻找满足请求的服务；（发现）
3. Web 服务中介者向Web 服务请求者返回满足条件的Web 服务描述信息，该描述信息用WSDL 写成，各种支持Web 服务的机器都能阅读；（发现）
4. Web 服务请求者利用从Web 服务中介者返回的描述信息生成相应的SOAP 消息，发送给Web 服务提供者，以实现Web 服务的调用；（绑定）
5. Web 服务提供者按SOAP 消息执行Web 服务，并将服务结果返回给Web 服务请求者。（绑定）

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/web-serivce/9.png)

# 3. web service 关键技术

## 3.1. web service协议栈
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/web-serivce/10.png)

## 3.2. Web Service的关键技术
1. HTTP：基于文本的、"请求－响应"（request-response）型的协议
2. XML：描述数据的标准方法
3. SOAP：表示信息交换的协议
4. WSDL：Web服务描述语言
5. UDDI：通用描述、发现与集成，它是一种独立于平台的，基于XML语言的用于在互联网上描述商务的协议

### 3.2.1. HTTP
1. HTTP/1.1规定一个客户打开到服务器的一个连接，然后以专门的格式发送一个请求，服务器进行响应，同时如果必要则保持连接的打开状态
2. HTTP使用的普遍性及其固有的穿防火墙的能力使它成为主导的Web服务网络协议。
3. 由于HTTP是基于文本的协议而缺乏表示远程过程调用（RPC）消息参数值的机制

### 3.2.2. XML
1. XML允许数据被串行化为易于被任何平台解码的消息格式，提供了在网络应用之间交换结构化数据的机制
2. Web服务需要一种方法定义Web服务消息中使用的数据类型：XML Schema 规范
3. Web服务需要一种机制避免名字冲突，并允许一个程序只处理自己关心的元素：XML名称空间

### 3.2.3. Simple Object Access Protocol
1. SOAP是在松散的、分布的环境中使用XML交换结构化和类型化信息的一种简单协议
2. 本身并不定义任何应用语义,只定义了一种简单的以模块化的方式包装数据的机制, 可以使用任何底层传输协议，如HTTP、FTP、SMTP等，其中最常用的是HTTP协议
3. SOAP=RPC+HTTP+XML
   1. 采用HTTP作为底层通讯协议；
   2. RPC作为一致性的调用途径
   3. XML作为数据传送的格式
4. SOAP代表了xml-rpc的发展，已经被W3C作为一种Internet标准采纳

#### 3.2.3.1. SOAP特性
1. 为信息交换设计的轻量协议，用于在网络应用程序之间交换结构化数据，是一种基于XML的机制
2. 设计目标是简单性和可扩充性，SOAP中省略了在其它消息系统和分布式对象系统中常见的一些特性
3. 无用存储单元收集、消息批处理
4. SOAP没有定义一种编程模型或实现，而是定义了一个模块化的包装模型，并在模块内定义了编码数据的编码机制

#### 3.2.3.2. SOAP 与IIOP、JRMP
1. 应用范围
   1. IIOP for CORBA
   2. JRMP for RMI
   3. Soap for Web Service
2. 编码格式
   1. IIOP 和JRMP是二进制编码
   2. SOAP 使用XML封装信息
3. 效率
   1. SOAP比较低
   2. HTTP不是有效率的通信协议
   3. XML需要额外的文件解析

#### 3.2.3.3. SOAP的组成
1. SOAP封皮（Envelope），定义描述消息所包含信息的框架结构，即消息中包含什么信息、由谁来处理，是必需的还是可选的
2. SOAP编码规则（Encoding rules），定义了一个串行化机制，用于交换应用定义的数据类型的实例
3. SOAP RPC表示，定义如何表示远程过程调用和响应
4. SOAP绑定（binding），定义如何使用底层传输协议进行SOAP消息的交换

#### 3.2.3.4. SOAP消息
1. SOAP封皮（SOAP Envelope），描述SOAP消息的XML文档的顶点元素
2. SOAP消息头（SOAP Header），可选的，用来扩展其它诸如安全、事务等服务的重要机制
3. SOAP消息体（SOAP Body），定义了一个简单的机制来交换要发送给最终SOAP接收者的消息中的必要信息

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/web-serivce/11.png)

#### 3.2.3.5. SOAP消息交换模型
1. SOAP消息是单方向的，从一个发送者到一个接收者
2. SOAP消息交换模型要求接收到一个SOAP消息的应用程序执行下列操作
   1. 识别SOAP消息中意图供给本应用的部分，本应用可以作为SOAP中介将消息的其它部分传递给另外的应用
   2. 检验SOAP消息中指定的所有必须处理的部分，并进行相应的处理
   3. 如果SOAP应用不是消息的最终目的地，它应该在删除所有自己消耗的部分后将消息转发给消息要供给的下一个应用

#### 3.2.3.6. SOAP Message structure
1. Request/Response Message
   1. Request 调用远端对象的某个方法
   2. Response 返回该方法运行后的输出结果

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/web-serivce/12.png)

#### 3.2.3.7. A SOAP Request Message
```xml
<SOAP-ENV:Envelope xmlns:SOAP-ENV="http://{soaporg}/envelope/"SOAP-ENV:encodingStyle="http://{soaporg}/encoding/">
  <SOAP-ENV:Body>
    <m:QuoteStockPricexmlns:m="Some-URI">
      <Symbol>MSFT</Symbol>
    </m:QuoteStockPrice>
  </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

#### 3.2.3.8. A SOAP Response Message
```xml
<SOAP-ENV:Envelope xmlns:SOAP-ENV="http://{soaporg}/envelope/"SOAP-ENV:encodingStyle="http://{soaporg}/encoding/">
  <SOAP-ENV:Body>
    <m:QuoteStockPriceResponsexmlns:m="Some-URI">
      <Price>78.2</Price>
    </m:QuoteStockPriceResponse>
  </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

#### 3.2.3.9. SOAP隐藏了实现
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/web-serivce/13.png)

#### 3.2.3.10. 为什么SOAP会成功
1. Internet环境下实现技术的多样性使得早期的分布式技术无法实现普遍的互相连接
   1. DCOM –需要每个连接点都使用Windows
   2. CORBA –需要每个连接点都有ORB
   3. RMI –需要每个连接点都使用Java
2. SOAP是基于平台独立的选择
   1. 简单的XML格式
   2. 可以在任意平台采用任意技术
   3. 可以使用开放源代码资源

### 3.2.4. 消息协议
1. SOAP本身没有严格地归入Web服务
2. SOAP 可以作为一种对任何类型的远程对象或过程的访问机制使用，也可以只是一个简单的消息传递机制
3. W3C创建的XMLP（Extensible Markup Language Protocol）
   1. 类似于SOAP的XML消息协议，包括封皮、对象串行化方式、HTTP传输绑定以及进行远程过程调用的方式几个部分

### 3.2.5. Web Services Description Language
1. Web服务接口由WSDL定义
   1. 类似IDL, 不过是使用XML格式
2. 描述了服务的操纵信息
   1. 描述服务提供了什么功能
   2. 服务位于何处
   3. 服务如何调用
3. WSDL是早先技术的综合
   1. IBM's NASSL
   2. Microsoft's SDL

#### 3.2.5.1. WSDL
1. 以XML格式描述网络服务，将服务描述为在包含面向过程或面向文档信息的消息上进行操作的一组端点
2. 操作和消息抽象描述，然后绑定到具体的网络协议和消息格式以定义一个端点。相关的具体端点被组合成为抽象端点（服务）
3. WSDL 是可扩展的，允许描述任何端点和消息，而不考虑通信使用的消息格式或网络协议

#### 3.2.5.2. WSDL文档结构
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/web-serivce/14.png)

#### 3.2.5.3. WSDL的元素
1. 类型（Types）：使用某种类型系统的数据类型定义的容器
2. 消息（Message）：对要传送数据的一个抽象定义
3. 操作（Operation）：对服务支持动作的抽象描述
4. 端口类型（Port Type），一个或多个端点所支持的操作抽象集合
5. 绑定（Binding）：对特定端口类型的一个具体协议和数据格式规格
6. 端口（Port）：一个单独的端点，由一个绑定和一个网络地址组合在一起定义
7. 服务（Service）：一组相关的端点的集合

#### 3.2.5.4. 操作和消息的抽象
1. 一个Web服务由一组端口定义
2. 端口由绑定到一个具体协议和数据格式规范的一组抽象操作和消息定义
3. WSDL中端点和消息的抽象定义与其具体网络配置和数据格式绑定相分离
4. WSDL定义了一个公共的绑定机制，将特定的协议或数据格式或结构连接到抽象的消息、操作或端点，从而可对抽象定义复用

#### 3.2.5.5. WSDL Example
1. OMG-IDL为：

```java
interface FooSample{
  long foo(long arg);
}
```

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<definitions name="FooSample" >
  <types>
    <schema targetNamespace="http://tempuri.org/xsd"
    xmlns="http://www.w3.org/2001/XMLSchema" xmlns:SOAP-ENC="http://schemas.xmlsoap.org/soap/encoding/"xmlns:wsdl="http://schemas.xmlsoap.org/wsdl/" elementFormDefault="qualified" >
    </schema>
  </types>
  <message name="Simple.foo">
    <part name="arg" type="xsd:int"/>
  </message>
  <message name="Simple.fooResponse">
    <part name="result" type="xsd:int"/>
  </message>
  <portTypename="SimplePortType">
    <operation name="foo" parameterOrder="arg" >
      <input message="wsdlns:Simple.foo"/>
      <output message="wsdlns:Simple.fooResponse"/>
  </operation>
  </portType>
</definitions>
```

```xml
<?xml version="1.0" encoding="UTF-8" standalone="no"?>
<SOAP-ENV:Envelope SOAP-ENV:encodingStyle="http://schemas.xmlsoap.org/soap/encoding/" xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/">
  <SOAP-ENV:Body>
    <m:foo xmlns:m="http://tempuri.org/message/">
    <arg>5131953</arg>
    </m:foo>
  </SOAP-ENV:Body>
</SOAP-ENV:Envelope>

<?xml version="1.0" encoding="UTF-8" standalone="no"?>
<SOAP-ENV:Envelope SOAP-ENV:encodingStyle="http://schemas.xmlsoap.org/soap/encoding/" xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/">
  <SOAP-ENV:Body>
    <SOAPSDK1:fooResponse mlns:SOAPSDK1="http://tempuri.org/message/">
    <result>5131953</result>
    </SOAPSDK1:fooResponse>
  </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

### 3.2.6. Universal Description, Discovery and Integration(UDDI)
1. 在哪里以及如何找到需要的信息？
2. 一套基于internet为Web服务提供信息注册中心的标准规范
3. UDDI规范在底层协议的基础上又定义了一层规范，使不同企业能够以相同的方式描述自己提供的服务和查询对方提供的服务
4. IT业界和商业界的领导者的合作

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/web-serivce/15.png)

#### 3.2.6.1. Service Provider
1. 提供e-Business Service
2. 通过Service Registry发布(Publish)其提供的可用的Service

#### 3.2.6.2. Service Registry
1. 为Service的发布和定位提供支持
2. 类似电话黄页

#### 3.2.6.3. Service Requestor
1. 通过Service Registry发现(Find)需要的Service
2. 绑定(Bind) Service Provider提供的Service, 并实施调用

#### 3.2.6.4. Where is SOAP and WSDL?
1. WSDL:Publish的内容、Find的返回结果和Bind的信息都是WSDL描述的服务信息
2. SOAP:Service Registry的访问(Publish/Find)、Service的访问都是通过SOAP Message实现

#### 3.2.6.5. How UDDI works
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/web-serivce/16.png)

#### 3.2.6.6. Problems UDDI Solves
| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/web-serivce/17.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/web-serivce/18.png) |
| ----------------------------- | ----------------------------- |

#### 3.2.6.7. UDDI Vision and Process
1. 从现有的标准(standard)开始
   1. TCP/IP, HTTP, XML
   2. Industry-specific schemas
   3. Shared vision of open protocols
2. 通过Web Service的形式实施和拓展
   1. Common web services "stack"
   2. Shared implementation to avoid confusing customer
   3. Public specs, open service, inclusive process
3. 将转变为一个标准实体组织
   1. Manage design process for 3 revs
   2. License control and IP to a 3rd party

#### 3.2.6.8. 信息结构
1. 商业实体（Business entity）:描述商业信息，如名称、类型等
2. 商业服务（Business service）:已发布的Web服务的集合
3. 绑定模板（Binding template）:访问信息，如URL
4. 技术规范（tModel）:对服务类型的技术规格说明，如接口定义、消息格式、消息协议、安全协议等

#### 3.2.6.9. UDDI的三类信息
1. 白页，包括企业的名称、地址、联系方式和企业标识，并允许其它公司按照名称查找目录
2. 黄页，包括基于标准分类法的行业类别
3. 绿页，包括了关于该企业所提供的Web服务的技术信息，其形式可能是一些指向文件或URL的指针，而这些文件或URL是为服务发现机制服务的

#### 3.2.6.10. 编程接口
1. UDDI规范提供了编程接口，允许商业注册一个Web服务，以及查找指定Web服务的注册。一旦想要的Web服务被确定，将提供一个指向WSDL文档所在位置的指
2. 查询API
   1. 构造搜索和浏览UDDI注册信息的程序
   2. Web服务出错处理
3. 发布API:创建各种类型的工具，以直接与UDDI注册中心进行交互，便于企业技术人员管理发布信息

#### 3.2.6.11. UDDI and SOAP
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/web-serivce/19.png)

# 4. 大众点评第三方团购券案例
1. 大众点评第三方团购券是在用户支付后，由系统实时请求第三方服务器生成券码而成的团购券；
2. 第三方服务器使用了Web Service技术，大众点评券系统需要根据其接口实现信息交互；
3. 本案例以阳光绿洲酒店团购举例

## 4.1. 系统分析
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/web-serivce/20.png)

## 4.2. 开发环境与技术
1. JDK1.5+Eclipse-jee
2. Maven+Jenkins+GitHub
3. 技术框架：Spring+Struts2+iBATIS
4. Axis2

## 4.3. 阳光绿洲系统(服务端)开发
1、 建立服务端JavaEE项目，实现生成券码方法

```java
public class SunOasisReceipt{//其他代码省略
  public String getEleInterface(String reqString) {
    reqString= URLDecoder.decode(DESCrypto.decrypt(des, reqString), "UTF-8");//解密reqString
    try {
      Document document= DocumentHelper.parseText(reqString);
      Node root = document.selectSingleNode("business_trans");
      Node result = root.selectSingleNode("result");
      String id = result.selectSingleNode("id").getText();
      Node orderNode= root.selectSingleNode("order");
      String thirdPartyOrderId= orderNode.selectSingleNode("order_num").getText();
      String req_seq= root.selectSingleNode("req_seq").getText();
      String serialNumber= receiptBiz.getReceiptSerial(order.getOrderId());
    } catch (Exception e) {
      logger.error("Exception:",e);
    return "";
    }
    String xml=buildContentByOrder(thirdPartyOrderId, req_seq, serialNumber);
    String encodeXml= DESCrypto.encrypt(des, xml);//加密结果
    return encodeXml;
  }
}
```

## 4.4. 发布Web Service
1. 打包Service，设定服务名称、所用类名和输出路径，并选择Apache Axis2的服务进行发布
2. 浏览器打开服务页面，将会生成对应的wsdl

## 4.5. WSDL文档
```xml
<?xml version="1.0" encoding="UTF-8" ?>
<wsdl:definitions xmlns:wsdl="http://schemas.xmlsoap.org/wsdl/"xmlns:typens="http://tempuri.org/xsd" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/wsdl/soap/" xmlns:stk="http://schemas.microsoft.com/soap-toolkit/wsdl-extension" xmlns="http://schemas.xmlsoap.org/wsdl/">
  <message name="getEleInterface"><part name="reqString" type="xsd:String"/></message>
  <portTypename="SimplePortType">
    <operation name="getEleInterface" parameterOrder="reqString" >
      <input message="wsdlns:Simple. getEleInterface"/>
      <output message="wsdlns:Simple. getEleInterfaceResponse"/>
    </operation>
  </portType>
  <service name="SunOasisReceiptService">
    <port name="SunOasisReceipt_Port" binding="mh:SunOasisReceipt_Binding">
      <soapbind:addresslocation="https://www.sunoasis-haefel.org/jwsbook/po" />
    </port>
  </service>
</definitions>
```

## 4.6. 大众点评券服务生成券流程
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/web-serivce/21.png)

## 4.7. 大众点评(客户端)发券流程
```java
public booleanissueThirdReceiptApply(Order order) {
  if (!init()) {
    logger.error("阳光绿洲-初始化配置失败！orderId= " + order.getOrderId());
    return false; 
  }
  boolean flag;//该任务是否正确处理标志
  try {
    List<Receipt> receiptList= receiptBiz.findByOrderID(order.getOrderId());
    receiptList= getReceiptListUsefull(receiptList); // 排除不需要发券的券
    if (CollectionUtils.isEmpty(receiptList)) {
      logger.error("处理第三方验票任务错误，没有找到该订单未处理的团购券，OrderID:"+ order.getOrderId());
      return false;
    }
    flag = getThirdReceiptByOrder(order, receiptList);
  } catch (Exception ex) {
    logger.error("处理第三方验票任务错误－－阳光绿洲－－生成券任务错误，OrderID：" + order.getOrderId() + "ex:" ,ex);
    flag = false;
  }
  return flag;
}
private booleangetThirdReceiptByOrder(Order order, List<Receipt> receiptList) {
  DealGroupVerifydealGroupVerify= getDealGroupVerify(order.getProduct().getProductId());
  String req_seq= getReqSeq();
  String xml = buildRequestContentByOrder(order, dealGroupVerify, req_seq);
  booleanflag = false;
  String response = "";
  try {
    String encodeXml= DESCrypto.encrypt(des, xml);//URLEncoder.encode(xml,"UTF-8")
    for (Receipt receipt: receiptList) {
      ThirdReceiptCodereceiptCode= thirdReceiptCodeDAO.findThirdReceiptCodeByReceiptId(receipt.getReceiptID());
      if (receiptCode== null || receiptCode.getThirdReceiptId() <= 0) {
        thirdReceiptCodeDAO.insertThirdReceiptCode(receipt.getReceiptID(), null, null, THIRD_PARTY_ID, null, req_seq);
      } else {
        req_seq= receiptCode.getSeqId(); //使用之前的seqid
      }
    }
    long start = new Date().getTime();
    response = getEleInterface(organization, encodeXml);//WebService调用
    response = URLDecoder.decode(DESCrypto.decrypt(des, response), "UTF-8");
    flag = parseResponseByOrder(response, order);//将结果转化并存储信息
    thirdVerifyLogDAO.insertThirdVerifyLog(THIRD_PARTY_ID, ThirdVerifyLogTypeEnum.GetThirdReceipt.getValue(), new Date().getTime() -start, 1, xml, response, 1, req_seq, String.valueOf(order.getOrderId()));
  } catch (Exception e) {
    logger.info("处理第三方验票任务错误，请求发送电子票失败，OrderID:" + order.getOrderId() + "req_seq:" + req_seq);
    String exMessage= "req_seq:" + req_seq+ "\t error message:" + ex.getMessage();
    thirdVerifyLogDAO.insertThirdVerifyLog(THIRD_PARTY_ID, ThirdVerifyLogTypeEnum.GetThirdReceipt.getValue(), new Date().getTime() -start, 0, xml, response, 1, exMessage, String.valueOf(order.getOrderId()));
    return false;
  }
  return flag;
}
```

## 4.8. 通过axis调用webservice实现
```java
private String getEleInterface(String organization, String xml) {
  String result = "no result!";
  Service service= new Service();
  try {
    Call call= (Call) service.createCall();
    call.setTargetEndpointAddress(url);// 远程调用路径
    call.setOperationName("getEleInterface");// 调用的方法名
    // 设置参数名:
    call.addParameter("organization", // 参数名
    XMLType.XSD_STRING,// 参数类型:String
    ParameterMode.IN);// 参数模式：'IN' or 'OUT'
    call.addParameter("xml", XMLType.XSD_STRING, ParameterMode.IN);
    // 设置返回值类型：
    call.setReturnType(XMLType.XSD_STRING);// 返回值类型：String
    result = (String) call.invoke(new Object[]{organization, xml});// 远调
  } catch (RemoteExceptione) {
    logger.error("RemoteException:" ,e);
  } catch (ServiceExceptione) {
    logger.error("ServiceException:" ,e); }
  return result;
}
```

## 4.9. 发布大众点评券服务
1. 在Jenkins上构建项目
2. 打包项目jar包，发布到服务器