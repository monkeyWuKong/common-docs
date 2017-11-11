
## 名词

### Web Service

Web service是一种服务导向架构的技术，通过标准的Web协议提供服务，目的是保证不同平台的应用服务可以互操作。根据W3C的定义，Web服务(Web service)应当是一个软件系统，用以支持网络间不同机器的互动操作。

网络服务通常是许多应用程序接口(API)所组成的，它们透过网络，例如Internet的远程服务器端，执行客户所提交服务的请求。无论定义还是实现，WEB服务过程中会由服务器提供一个机器可读的描述以辨识服务器所提供的WEB服务。

另外，虽然WSDL不是SOAP服务端点的必要条件，但目前基于Java的主流WEB服务开发框架往往需要WSDL实现客户端的源代码生成。一些工业标准化组织就在WEB服务定义中强制包含SOAP和WSDL。

webService三要素:
- SOAP, 
- WSDL (Web Services Description Language),
- UDDI( Universal Description Discovery and Integration )

soap用来传递信息的格式, WSDL 用来描述如何访问具体的接口, UDDI用来管理,分发,查询.

[WebService到底是什么](http://blog.csdn.net/wooshn/article/details/8069087/)

[百科-Web Service](http://baike.sogou.com/v598444.htm?fromTitle=webservice)

### SOA架构

[金蝶软件-浅析深究什么是SOA](http://blog.vsharing.com/fengjicheng/A1059842.html)

[面向服务架构](http://baike.sogou.com/v74965236.htm?fromTitle=%E9%9D%A2%E5%90%91%E6%9C%8D%E5%8A%A1%E6%9E%B6%E6%9E%84)

### SOAP

简单对象访问协议（Simple Object Access Protocol，SOAP），是一种轻量的、简单的、基于XML的协议，它被设计成在WEB上交换结构化的和固化的信息。

它是基于已经广泛使用的两个协议：HTTP和XML，所以业界把这种技术称为“它是第一个没有发明任何新技术的技术"。

SOAP简单的理解，就是这样的一个开放协议SOAP=RPC+HTTP+XML：采用HTTP作为底层通讯协议；RPC作为一致性的调用途径，ＸＭＬ作为数据传送的格式，允许服务提供者和服务客户经过防火墙在INTERNET进行通讯交互。

SOAP 使用 HTTP 传送 XML，尽管HTTP 不是有效率的通讯协议，而且 XML 还需要额外的文件解析（parse），两者使得交易的速度大大低于其它方案。但是XML 是一个开放、健全、有语义的讯息机制，而 HTTP 是一个广泛又能避免许多关于防火墙的问题，从而使SOAP得到了广泛的应用。但是如果效率对你来说很重要，那么你应该多考虑其它的方式，而不要用 SOAP。


资料：

[2001年-浅谈 SOAP](https://www.ibm.com/developerworks/cn/xml/x-sisoap/)

[百科-SOAP](http://baike.sogou.com/v641208.htm?fromTitle=soap)

[SOAP协议初级指南](http://www.cnblogs.com/meil/archive/2006/09/24/513283.html)

### WSDL

SOAP是用来最终完成Web服务调用的，而WSDL则是用于描述如何使用SOAP来调用Web服务的。

WSDL 是一种 **XML Application**，他将Web服务描述定义为一组服务访问点，客户端可以通过这些服务访问点对包含面向文档信息或面向过程调用的服务进行访问(类似远程过程调用)。WSDL首先对访问的操作和访问时使用的请求/响应消息进行抽象描述，然后将其绑定到具体的传输协议和消息格式上以最终定义具体部署的服务访问点。相关的具体部署的服务访问点通过组合就成为抽象的Web服务。

[IBM-WSDL:描述你的Web服务](https://www.ibm.com/developerworks/cn/webservices/ws-wsdl/index.html)

### UDDI

UDDI 是一种目录服务，企业可以使用它对 Web services 进行注册和搜索。UDDI，英文为 "Universal Description, Discovery and Integration"，可译为“通用描述、发现与集成服务”。

UDDI是一种规范，它主要提供基于Web服务的注册和发现机制，为Web服务提供三个重要的技术支持：

1. 标准、透明、专门描述Web服务的机制；
2. 调用Web服务的机制；
3. 可以访问的Web服务注册中心。

UDDI规范由OASIS（Organization for the Advancement of Structured Information Standards）标准化组织制定。

[IBM - 理解 UDDI](https://www.ibm.com/developerworks/cn/webservices/ws-featuddi/)

[WSDL 和 UDDI](http://www.w3school.com.cn/wsdl/wsdl_uddi.asp)

### JSON

JSON的优势在于:

1. JSON是纯文本格式，是独立于语言和平台的。

2. 生成和解析相对于XML而言要简单。

3. 读写的速度更快。


[知乎 - WEB开发中，使用JSON-RPC好，还是RESTful API好？](https://www.zhihu.com/question/28570307)

## thoughts

RPCful and RESTful = 面向过程与面向对象??

以不变应万变















