
# Table of Contents

-   [摘要（Abstract）](#org0db8dbe)
-   [备忘状态（Status of This Memo）](#orgb0cb1da)
-   [1 引论（Introduction）](#org39f0ea3)
    -   [1.1 Requirements Notation](#org0d3ff06)
    -   [1.2 句法标记 (Syntax Notation)](#org8e2ef47)
-   [2 体系结构（Architecture）](#orgdd453e7)
    -   [2.1 客户端/服务器通讯 (Client/Server Messaging)](#org089417b)
    -   [2.2 实现的差异性（Implementation Diversity）](#org903d3d3)
    -   [2.3 中间人 (Intermediaries)](#org86ee91c)
    -   [2.4 缓存 (Caches)](#orgc346344)
    -   [2.5 一致性和错误处理 (Conformance and Error Handling)](#orgbfd4ecc)
    -   [2.6 协议版本管理 (Protocol Versioning)](#orga558a35)
    -   [2.7 统一资源标识符 (Uniform Resource Identifiers)](#org050102c)
        -   [2.7.1 http URI Scheme](#org8d00096)
        -   [2.7.2 https URI Scheme](#orgce3a733)
        -   [2.7.3 http and https URI Normalization and Comparison](#org5f3a9aa)
-   [3 报文格式（Message Format）](#org8644818)
    -   [3.1 起始行 (Start Line)](#org957627d)
        -   [3.1.1 请求行 (Request Line)](#org386c1a2)
        -   [3.1.2 状态行 (Status Line)](#org3e53136)
    -   [3.2 头域 (Header Fields)](#org0f4dd4f)
        -   [3.2.1 域的可扩展性 (Field Extensibility)](#org839a087)
        -   [3.2.2 域的顺序 (Field Order)](#org9834eef)
        -   [3.2.3 空格 (Whitespace)](#orga4b9d50)
        -   [3.2.4 域解释 (Field Parsing)](#orgb8f7882)
        -   [3.2.5 域限制 (Field Limits)](#org902ee98)
        -   [3.2.6 域值的组成 (Field Value Components)](#org0f8e507)
    -   [3.3 报文体 (Message Body)](#org27d606a)
        -   [3.3.1 传输编码 (Transfer-Encoding)](#org5248f65)
        -   [3.3.2 内容长度 (Content-Length)](#orgc417d3f)
        -   [3.3.3 报文体的长度 (Message Body Length)](#org49c3093)
    -   [3.4 报文不完整的处理 (Handling Incomplete Messages)](#orgaebe17e)
    -   [3.5 报文解释的健壮性 (Message Parsing Robustness)](#org1e4e10d)
-   [4 传输编码（Transfer Codings）](#orgd5db07b)
    -   [4.1 Chunked Transfer Coding](#orge6ce133)
        -   [4.1.1 Chunk Extensions](#org5de3893)
        -   [4.1.2 Chunked Trailer Part](#org50ba17f)
        -   [4.1.3 Decoding Chunked](#orgc3f78b7)
    -   [4.2 Compression Codings](#orgf7f23d5)
        -   [4.2.1 Compress Coding](#org46e4b8b)
        -   [4.2.2 Deflate Coding](#org5923bd6)
        -   [4.2.3 Gzip Coding](#org19d009d)
    -   [4.3 TE](#orgfb316f0)
    -   [4.4 Trailer](#org53d7545)
-   [5 报文路由（Message Routing）](#org77574f5)
    -   [5.1 标识目标资源 (Identifying a Target Resource)](#orga306fad)
    -   [5.2 Connecting Inbound](#org5ec56fd)
    -   [5.3 请求目标 (Request Target)](#orgd1804be)
        -   [5.3.1 (origin-form)](#orgf834915)
        -   [5.3.2 (absolute-form)](#org153cebb)
        -   [5.3.3 (authority-form)](#org1c3638c)
        -   [5.3.4 (asterisk-form)](#orgc95d555)
    -   [5.4 主机 (Host)](#org4d0e8e5)
    -   [5.5 Effective Request URI](#org7ba40ee)
    -   [5.6 Associating a Response to a Request](#org06d22fe)
    -   [5.7 报文转发 (Message Forwarding)](#org066fec4)
        -   [5.7.1 Via](#orgad39f20)
        -   [5.7.2 Transformations](#org630ebc3)
-   [6 连接管理（Connection Management）](#orge2597b0)
    -   [6.1 连接 (Connection)](#org576bde0)
    -   [6.2 建立 (Establishment)](#org85c1699)
    -   [6.3 持久性 (Persistence)](#orgccd03a7)
        -   [6.3.1 (Retrying Requests)](#orgcd7c628)
        -   [6.3.2 (Pipelining)](#orgb9421fe)
    -   [6.4 并发性 (Concurrency)](#orgb618025)
    -   [6.5 失败和超时 (Failures and Timeouts)](#org4650cb9)
    -   [6.6 销毁 (Tear-down)](#orgf45cd65)
    -   [6.7 升级 (Upgrade)](#orgc0cff1a)
-   [7 ABNF 列表扩展：#rule（ABNF List Extension: #rule）](#orgb633ea2)
-   [8 INAN 考虑（IANA Considerations）](#org2c48e90)
    -   [8.1 Header Field Registration](#orgdf30041)
    -   [8.2 URI Scheme Registration](#org212ee20)
    -   [8.3 Internet Media Type Registration](#org76af6b3)
        -   [8.3.1 Internet Media Type message/http](#orga870e90)
        -   [8.3.2 Internet Media Type application/http](#org8ed9c5f)
    -   [8.4 Transfer Coding Registry](#org4d82db6)
        -   [8.4.1 Procedure](#org135cebe)
        -   [8.4.2 Registration](#org530f24a)
    -   [8.5 Content Coding Registration](#org4096af6)
    -   [8.6 Upgrade Token Registry](#org191505b)
        -   [8.6.1 Procedure](#orgf181bcc)
        -   [8.6.2 Upgrade Token Registration](#org2feb3f1)
-   [9 安全考虑（Security Considerations）](#org0af0d25)
    -   [9.1 Establishing Authority](#org1e3f6dc)
    -   [9.2 Risks of Intermediaries](#org2131912)
    -   [9.3 Attacks via Protocol Element Length](#org083cfbd)
    -   [9.4 Response Splitting](#org29b9a36)
    -   [9.5 Request Smuggling](#org5c43a6b)
    -   [9.6 Message Integrity](#org43c3f69)
    -   [9.7 Message Confidentiality](#org2e4dc40)
    -   [9.8 Privacy of Server Log Information](#orgce09664)
-   [10 感谢（Acknowledgments）](#orga72f474)
-   [11 参考资料（References）](#orgb9bc814)
-   [附录 A：HTTP 版本历史（Appendix A. HTTP Version History）](#orga723ab5)
-   [附录 B：收集的 ABNF（Appendx B. Collected ABNF）](#orgf6cbd21)
-   [索引（Index）](#org31a7d70)

Internet Engineering Task Force (IETF)                  R. Fielding, Ed.
Request for Comments: 7230                                         Adobe
Obsoletes: 2145, 2616                                    J. Reschke, Ed.
Updates: 2817, 2818                                           greenbytes
Category: Standards Track                                      June 2014
ISSN: 2070-1721


<a id="org0db8dbe"></a>

# 摘要（Abstract）

The Hypertext Transfer Protocol (HTTP) is a stateless application-level protocol for distributed, collaborative, hypertext information systems. This document provides an overview of HTTP architecture and its associated terminology, defines the "http" and "https" Uniform Resource Identifier (URI) schemes, defines the HTTP/1.1 message syntax and parsing requirements, and describes related security concerns for implementations.

This document is the first in a series of documents that collectively form the HTTP/1.1 specification:

1.  "Message Syntax and Routing" (this document)
2.  "Semantics and Content" [RFC7231]
3.  "Conditional Requests" [RFC7232]
4.  "Range Requests" [RFC7233]
5.  "Caching" [RFC7234]
6.  "Authentication" [RFC7235]

本 HTTP/1.1 规范淘汰了 RFC 2616 和 RFC 2145。


<a id="orgb0cb1da"></a>

# 备忘状态（Status of This Memo）

This is an Internet Standards Track document.

This document is a product of the Internet Engineering Task Force (IETF). It represents the consensus of the IETF community. It has received public review and has been approved for publication by the Internet Engineering Steering Group (IESG). Further information on Internet Standards is available in Section 2 of RFC 5741.

Information about the current status of this document, any errata, and how to provide feedback on it may be obtained at <http://www.rfc-editor.org/info/rfc7230>.


<a id="org39f0ea3"></a>

# 1 引论（Introduction）

The Hypertext Transfer Protocol (HTTP) is a stateless application-level request/response protocol that uses extensible semantics and self-descriptive message payloads for flexible interaction with network-based hypertext information systems. This document is the first in a series of documents that collectively form the HTTP/1.1 specification:

-   "Message Syntax and Routing" (this document)
-   "Semantics and Content" [RFC7231]
-   "Conditional Requests" [RFC7232]
-   "Range Requests" [RFC7233]
-   "Caching" [RFC7234]
-   "Authentication" [RFC7235]

This HTTP/1.1 specification obsoletes RFC 2616 and RFC 2145 (on HTTP versioning). This specification also updates the use of CONNECT to establish a tunnel, previously defined in RFC 2817, and defines the "https" URI scheme that was described informally in RFC 2818.

HTTP is a generic interface protocol for information systems. It is designed to hide the details of how a service is implemented by presenting a uniform interface to clients that is independent of the types of resources provided. Likewise, servers do not need to be aware of each client's purpose: an HTTP request can be considered in isolation rather than being associated with a specific type of client or a predetermined sequence of application steps. The result is a protocol that can be used effectively in many different contexts and for which implementations can evolve independently over time.

HTTP is also designed for use as an intermediation protocol for translating communication to and from non-HTTP information systems. HTTP proxies and gateways can provide access to alternative information services by translating their diverse protocols into a hypertext format that can be viewed and manipulated by clients in the same way as HTTP services.

One consequence of this flexibility is that the protocol cannot be defined in terms of what occurs behind the interface. Instead, we are limited to defining the syntax of communication, the intent of received communication, and the expected behavior of recipients. If the communication is considered in isolation, then successful actions ought to be reflected in corresponding changes to the observable interface provided by servers. However, since multiple clients might act in parallel and perhaps at cross-purposes, we cannot require that such changes be observable beyond the scope of a single response.

This document describes the architectural elements that are used or referred to in HTTP, defines the "http" and "https" URI schemes, describes overall network operation and connection management, and defines HTTP message framing and forwarding requirements. Our goal is to define all of the mechanisms necessary for HTTP message handling that are independent of message semantics, thereby defining the complete set of requirements for message parsers and message-forwarding intermediaries.


<a id="org0d3ff06"></a>

## 1.1 Requirements Notation

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in [RFC2119].

Conformance criteria and considerations regarding error handling are defined in Section 2.5.


<a id="org8e2ef47"></a>

## 1.2 句法标记 (Syntax Notation)

This specification uses the Augmented Backus-Naur Form (ABNF) notation of [RFC5234] with a list extension, defined in Section 7, that allows for compact definition of comma-separated lists using a '#' operator (similar to how the '\*' operator indicates repetition). Appendix B shows the collected grammar with all list operators expanded to standard ABNF notation.

The following core rules are included by reference, as defined in [RFC5234], Appendix B.1: ALPHA (letters), CR (carriage return), CRLF (CR LF), CTL (controls), DIGIT (decimal 0-9), DQUOTE (double quote), HEXDIG (hexadecimal 0-9/A-F/a-f), HTAB (horizontal tab), LF (line feed), OCTET (any 8-bit sequence of data), SP (space), and VCHAR (any visible [USASCII] character).

As a convention, ABNF rule names prefixed with "obs-" denote "obsolete" grammar rules that appear for historical reasons.


<a id="orgdd453e7"></a>

# 2 体系结构（Architecture）

HTTP was created for the World Wide Web (WWW) architecture and has evolved over time to support the scalability needs of a worldwide hypertext system.

<span class="underline">HTTP 是为万维网（WWW）而设计的，目前已发展成为支撑世界范围内超文本体系的基石。</span>

Much of that architecture is reflected in the terminology and syntax productions
used to define HTTP.

<span class="underline">用于定义 HTTP 协议的术语和句法的产品反映了这一体系结构的方方面面。</span>


<a id="org089417b"></a>

## 2.1 客户端/服务器通讯 (Client/Server Messaging)

HTTP is a stateless request/response protocol that operates by exchanging messages (Section 3) across a reliable transport- or session-layer "connection" (Section 6). 

<span class="underline">HTTP 是一个无状态的，通过请求和响应的方式来进行报文消息交换的通信协议，在可靠的传输
层或会话层之间进行报文互换。</span>

（译注：response 译作“响应”、“应答”，本文统一译为“响应”；message 译作“报文”、“消息”，这里统一译为“报文”，但在如果在某些情况下我认为译为“消息”更通俗的时候，我会特别标注为“消息”。）

An HTTP "client" is a program that establishes a connection to a server for the purpose of sending one or more HTTP requests.

<span class="underline">HTTP 客户端是一个用于与服务器建立连接，向其发送一个或多个 HTTP 请求的应用程序。</span>

An HTTP "server" is a program that accepts connections in order to service HTTP requests by sending HTTP responses.

<span class="underline">HTTP 服务器是一个接受客户端连接，接收 HTTP 请求，发送 HTTP 响应的应用程序。</span>

The terms "client" and "server" refer only to the roles that these programs perform for a particular connection. 

The same program might act as a client on some connections and a server on others. 

The term "user agent" refers to any of the various client programs that initiate a request, including (but not limited to) browsers, spiders (web-based robots), command-line tools, custom applications, and mobile apps. 

The term "origin server" refers to the program that can originate authoritative responses for a given target resource. 

The terms "sender" and "recipient" refer to any implementation that sends or receives a given message, respectively.

HTTP relies upon the Uniform Resource Identifier (URI) standard [RFC3986] to indicate the target resource (Section 5.1) and relationships between resources.

<span class="underline">HTTP 依靠“统一资源定位符（URI）标准【RFC3986】”来标识目标资源（Section 5.1）以及资源与资源之间的联系。</span>

Messages are passed in a format similar to that used by Internet mail [RFC5322] and the Multipurpose Internet Mail Extensions (MIME) [RFC2045] (see Appendix A of [RFC7231] for the differences between HTTP and MIME messages).

<span class="underline">报文通过类似于电子邮件【RFC5233】和多用途互联网邮件扩展类型（MIME）【RFC2045】的格式进行传输，而 HTTP 与 MIME 报文之间的区别在于两者传输格式上的不同。</span>

Most HTTP communication consists of a retrieval request (GET) for a representation of some resource identified by a URI.

<span class="underline">大多数 HTTP 的通讯是通过 URI 以检索请求（GET）的形式定位资源。</span>

In the simplest case, this might be accomplished via a single bidirectional connection (`=`) between the user agent (UA) and the origin server (O).

<span class="underline">用最简单的例子来说，可以经由一个在用户代理（UA）和源服务器（O）之间的双向连接来完成。</span>

         request   >
    UA ======================================= O
                                <   response

A client sends an HTTP request to a server in the form of a request message, beginning with a request-line that includes a method, URI, and protocol version (Section 3.1.1), followed by header fields containing request modifiers, client information, and representation metadata (Section 3.2), an empty line to indicate the end of the header section, and finally a message body containing the payload body (if any, Section 3.3).

TODO <span class="underline">客户端以请求报文（Request Message）的形式向服务器发送一个 HTTP 请求，请求报文的第一行叫做请求行（见 [3.1.1 Request Line](#org386c1a2)），请求行包含了该请求的方法，URI 和 协议版本。</span>

A server responds to a client's request by sending one or more HTTP response messages, each beginning with a status line that includes the protocol version, a success or error code, and textual reason phrase (Section 3.1.2), possibly followed by header fields containing server information, resource metadata, and representation metadata (Section 3.2), an empty line to indicate the end of the header section, and finally a message body containing the payload body (if any, Section 3.3).

A connection might be used for multiple request/response exchanges, as defined in Section 6.3.

The following example illustrates a typical message exchange for a GET request (Section 4.3.1 of [RFC7231]) on the URI "<http://www.example.com/hello.txt>":

Client request:

    GET /hello.txt HTTP/1.1
    User-Agent: curl/7.16.3 libcurl/7.16.3 OpenSSL/0.9.7l zlib/1.2.3
    Host: www.example.com
    Accept-Language: en, mi

Server response:

    HTTP/1.1 200 OK
    Date: Mon, 27 Jul 2009 12:28:53 GMT
    Server: Apache
    Last-Modified: Wed, 22 Jul 2009 19:15:56 GMT
    ETag: "34aa387-d-1568eb00"
    Accept-Ranges: bytes
    Content-Length: 51
    Vary: Accept-Encoding
    Content-Type: text/plain
    
    Hello World! My payload includes a trailing CRLF.


<a id="org903d3d3"></a>

## 2.2 实现的差异性（Implementation Diversity）

**When** considering the design of HTTP, it is easy to fall into a trap of thinking that all user agents are general-purpose browsers and all origin servers are large public websites.

<span class="underline">在考虑 HTTP 协议的设计时，很容易陷入一个误区，认为所有的用户代理都是通用的网页浏览器；所有的源服务器都是大型公共站点。</span>

That is not the case in practice.

<span class="underline">然而实践中并不是这么一回事。</span>

Common HTTP user agents include household appliances, stereos, scales, firmware update scripts, command-line programs, mobile apps, and communication devices in a multitude of shapes and sizes.

<span class="underline">一般的 HTTP 用户代理包含了家用电器、音响器材、磅秤、固件升级脚本、命令行程序、移动应用以及各种形状和尺寸的通信设备。</span>

Likewise, common HTTP origin servers include home automation units, configurable networking components, office machines, autonomous robots, news feeds, traffic cameras, ad selectors, and video-delivery platforms.

<span class="underline">同样，一般的 HTTP 源服务器包含家庭自动化元件、可配置的网络组件、办公设备、自主学习的机器人、新闻源、交通摄像头、广告选择器以及视频分发平台。</span>

**The** term "user agent" does not imply that there is a human user directly interacting with the software agent at the time of a request.

<span class="underline">术语“用户代理”并不是意味着在请求的时候有一个人类用户与软件代理进行直接交互。</span>

In many cases, a user agent is installed or configured to run in the background and save its results for later inspection (or save only a subset of those results that might be interesting or erroneous).

<span class="underline">在许多情况下，用户代理被安装或配置用于后台运行，以及保存其运行结果用于后续检验（或者只保存那些感兴趣的，或者错误的那部分）。</span>

Spiders, for example, are typically given a start URI and configured to follow certain behavior while crawling the Web as a hypertext graph.

<span class="underline">例如，爬虫，其典型应用是给定一个起始 URI，然后配置其抓取网页文本的后续行为。</span>

**The** implementation diversity of HTTP means that not all user agents can make interactive suggestions to their user or provide adequate warning for security or privacy concerns.

<span class="underline">HTTP 实现上的差异性，表现为不是所有的用户代理都能为用户提供交互性的建议或者对其关注的安全或隐私提供足够的警示。</span>

In the few cases where this specification requires reporting of errors to the user, it is acceptable for such reporting to only be observable in an error console or log file.

<span class="underline">例如，本规范规定了在某些情况下要求向用户报告错误，但在某些实现上，这些报告信息可能只输出到错误控制台或者日志文件里，这也是允许的。</span>

Likewise, requirements that an automated action be confirmed by the user before proceeding might be met via advance configuration choices, run-time options, or simple avoidance of the unsafe action; confirmation does not imply any specific user interface or interruption of normal processing if the user has already made that choice.

<span class="underline">同样，用户可以在用户代理里（例如在高级选项、运行时选项或者不安全操作中）预先配置接下来的默认行为，规范要求当遇到这些默认行为时需要用户确认，而这个确认并不意味着任一具体的用户接口，或者用户选择某一选项后正常流程的打断。</span>


<a id="org86ee91c"></a>

## 2.3 中间人 (Intermediaries)

HTTP enables the use of intermediaries to satisfy requests through a chain of connections.

<span class="underline">HTTP 支持中间人的功能，从而使请求能在通信链路各节点之间中转。</span>

There are three common forms of HTTP intermediary: proxy, gateway, and tunnel.

<span class="underline">HTTP 有三种中间人：代理，网关和隧道。</span>

In some cases, a single intermediary might act as an origin server, proxy, gateway, or tunnel, switching behavior based on the nature of each request.

在某些情况下，一个中间人可以依据当前接收到的请求来决定是以源服务器、代理、网关还是隧道的方式来处理。

         >             >             >             >
    UA =========== A =========== B =========== C =========== O
               <             <             <             <

**The** figure above shows three intermediaries (A, B, and C) between the user agent and origin server.

<span class="underline">上图展示了在用户代理（UA）和源服务器（O）之间的三个中间人（A、B 和 C）。</span>

A request or response message that travels the whole chain will pass through four separate connections.

<span class="underline">一个请求报文或者响应报文通过依次建立四个独立的连接走完整条链路。</span>

Some HTTP communication options might apply only to the connection with the nearest, non-tunnel neighbor, only to the endpoints of the chain, or to all connections along the chain.

<span class="underline">HTTP 的某些通信选项可能仅适用于通信链路上的某些节点上，例如离其最近的非隧道节点、链路的终点，或者适用于链路上的所有节点。</span>

Although the diagram is linear, each participant might be engaged in multiple, simultaneous communications.

<span class="underline">虽然上图以线性的方式展示这条链路（但并不一定是线性的），每个节点都可能在处理多个并行的通信。</span>

For example, B might be receiving requests from many clients other than A, and/or forwarding requests to servers other than C, at the same time that it is handling A's request.

<span class="underline">例如，B 在处理来自 A 的请求的同时，还可能接收到来自 A 之外的多个客户端的请求，并（或）将其转发这些请求到 C 之外的服务器。</span>

Likewise, later requests might be sent through a different path of connections, often based on dynamic configuration for load balancing.

<span class="underline">同样，后面接收到的请求可能被节点依据其负载均衡的策略发送至一个不同通信路径上。</span>

（译注：例如，来自 A 的请求被 B 转发到 D，而不是上图所示的 C。）

**The** terms "**upstream**" and "**downstream**" are used to describe directional requirements in relation to the **message flow**: <span class="underline">all messages flow from upstream to downstream.</span>

<span class="underline">术语“上行”和“下行”用于描述报文（消息）流的方向：所有的报文（消息）都从上行流到下行。</span>

The terms "**inbound**" and "**outbound**" are used to describe directional requirements in relation to the request route: "inbound" means toward the origin server and "outbound" means toward the user agent.

术语“入境”和“出境”用于描述请求经过路由的方向：“入境”意为经过路由器的数据流向源服务器，而“出境”意为经过路由器的数据流向用户代理。 

（译注：路由器是连接互联网的枢纽，数据流入互联网，这叫“入境”，例如文件上传；流出互联网，这叫“出境”，例如文件下载）。

**A** "proxy" is a message-forwarding agent that is selected by the client, usually via local configuration rules, to receive requests for some type(s) of [absolute URI](https://tools.ietf.org/html/rfc3986#page-27) and attempt to satisfy those requests via translation through the HTTP interface.

“代理”，一般是由客户端通过本地设置或规则所选定的，负责报文转发的中介。代理接收绝对 URI 类型的请求并试图经由 HTTP 接口转译来满足这些请求。

（译注：[Wikipedia 上对绝对 URI 的描述](https://en.wikipedia.org/wiki/HTTP_location)）

Some translations are minimal, such as for proxy requests for "http" URIs, whereas other requests might require translation to and from entirely different application-level protocols.

**TODO** 一些转译是以最低限度来进行的，例如

Proxies are often used to group an organization's HTTP requests through a common intermediary for the sake of security, annotation services, or shared caching. 

为了安全性、服务标识或者共享缓存，多个代理一般通过一个共同的中间人，将属于同一团体的 HTTP 请求进行分组。

Some proxies are designed to apply transformations to selected messages or payloads while they are being forwarded, as described in [Section 5.7.2](#org630ebc3).

某些代理被设计为对选定的报文或载荷在其被转发时进行转换（见 [5.7.2](#org630ebc3)）。

**A** "gateway" (a.k.a. "reverse proxy") is an intermediary that acts as an origin server for the outbound connection but translates received requests and forwards them inbound to another server or servers.

<span class="underline">“网关”（又称为“反向代理”），在 Outbound 通信时网关充当一个源服务器，将接收到的请求进行转译，然后转发到其他一个或多个服务器上。</span>

Gateways are often used to encapsulate legacy or untrusted information services, to improve server performance through "accelerator" caching, and to enable partitioning or load balancing of HTTP services across multiple machines.

<span class="underline">网关通常用于封装遗留或者非信任的信息，通过“加速器”缓存，以及在多机中开启分片或负载均衡来提升 HTTP 服务器的性能。</span>

**All** HTTP requirements applicable to an origin server also apply to the outbound communication of a gateway.

<span class="underline">HTTP 中所有对于源服务器的要求都适用于网关的出境通信（Outbound Communication）。</span> 

A gateway communicates with inbound servers using any protocol that it desires, including private extensions to HTTP that are outside the scope of this specification.

一个网关可以使用其喜欢的协议与入境网关通信，包括对 HTTP 的私有扩展（已经超出了本标准的范畴）。

However, an HTTP-to-HTTP gateway that wishes to interoperate with third-party HTTP servers ought to conform to user agent requirements on the gateway's inbound connection.

<span class="underline">但是，如果一个 HTTP-to-HTTP 的网关在 Inbound 时想跟第三方 HTTP 服务器交互的话应该遵循本标准对于用户代理的要求。</span>

**A** "tunnel" acts as a blind relay between two connections without changing the messages.

一个“隧道”在两个连接之间充当盲中继，即隧道并不会对报文进行更改。

（译注：Blind relay，盲中继，只是将字节从一个连接转发到另一个连接中去，不对 Connection 首部进行特殊的处理。）

Once active, a tunnel is not considered a party to the HTTP communication, though the tunnel might have been initiated by an HTTP request.

隧道在激活后，由 HTTP 请求来进行初始化，但隧道并不作为 HTTP 通信的一部分。

A tunnel ceases to exist when both ends of the relayed connection are closed.

在隧道两端的连接都关闭后，隧道将不复存在。

Tunnels are used to extend a virtual connection through an intermediary, such as when Transport Layer Security (TLS, [RFC5246]) is used to establish confidential communication through a shared firewall proxy.

隧道以中间人的方式用于扩展[虚连接](https://en.wikipedia.org/wiki/Virtual_circuit)，例如传输层安全协议（TLS，[[RFC5246](https://tools.ietf.org/html/rfc5246)]）通过一个共享的防火墙代理，用于建立保密通信。

**The** above categories for intermediary only consider those acting as participants in the HTTP communication.

以上这些类型的中间人仅仅认为是在 HTTP 通信中作为参与者。

There are also intermediaries that can act on lower layers of the network protocol stack, filtering or redirecting HTTP traffic without the knowledge or permission of message senders. 

这些中间人同样能工作在网络协议栈的底层，过滤或重定向 HTTP 流而不必了解报文发送者的权限或逻辑。

Network intermediaries are indistinguishable (at a protocol level) from a man-in-the-middle attack, often introducing security flaws or interoperability problems due to mistakenly violating HTTP semantics.

网络中间人并不能（在协议层面上）识别出（报文）是否来自于[中间人攻击](https://en.wikipedia.org/wiki/Man-in-the-middle_attack)，因此，有时会因为中间人的实现有误没有遵循 HTTP 语义从而引入了安全隐患或者互通问题。

**For** example, an "interception proxy" [RFC3040] (also commonly known as a "transparent proxy" [RFC1919] or "captive portal") differs from an HTTP proxy because it is not selected by the client.

例如，一个“拦截代理”（一般又叫作“透明代理” [[RFC1919](https://tools.ietf.org/html/rfc1919)] 或者“强制网络门户”、“捕获门户”）

（译注：强制网络门户，是一个在用户使用无线网络前，先被导向至的 Web 网页，它是使用公共访问网络的用户在被授予访问权限前必须访问和交互的页面。）

Instead, an interception proxy filters or redirects outgoing TCP port 80 packets (and occasionally other common port traffic).

而是，一个拦截代理（Interception Proxy）过滤或者重定向输出的于 TCP 80 端口的数据包（有时还包括其他一般端口的流量）。

Interception proxies are commonly found on public network access points, as a means of enforcing account subscription prior to allowing use of non-local Internet services, and within corporate firewalls to enforce network usage policies.

<span class="underline">拦截代理在公有网络访问点<sup><a id="fnr.1" class="footref" href="#fn.1">1</a></sup>里很常见，作为一种在允许使用非本地互联网服务之前的强制认证手段，同样常见于防火墙里，用于实施网络使用策略。</span>

**HTTP** is defined as a stateless protocol, meaning that each request message can be understood in isolation.

<span class="underline">HTTP 被定义为一个无状态的协议，意为每一个请求报文都能够被单独理解。</span>

（译注：源服务器或中间人能够完全理解每一个请求报文的含义，这种理解并不用基于该请求报文的前一个或多个请求报文的内容）

Many implementations depend on HTTP's stateless design in order to reuse proxied connections or dynamically load balance requests across multiple servers.

<span class="underline">许多依托于 HTTP 无状态设计的实现是为了复用代理连接或者通过多台服务器实现对请求的动态负载均衡。</span>

Hence, a server MUST NOT assume that two requests on the same connection are from the same user agent unless the connection is secured and specific to that agent.

<span class="underline">因此，除非是针对于特定代理的安全连接，一个服务器不能假设同一个连接里的两个请求是来自于同一个用户代理。</span>

Some non-standard HTTP extensions (e.g., [RFC4559]) have been known to violate this requirement, resulting in security and interoperability problems.

<span class="underline">某些非标准的 HTTP 扩展（例如 [[RFC4559](https://tools.ietf.org/html/4559)]）已经被发现违反了这一要求，结果就是引发安全性和互操作性的问题。</span>


<a id="orgc346344"></a>

## 2.4 缓存 (Caches)

**A** "cache" is a local store of previous response messages and the subsystem that controls its message storage, retrieval, and deletion.

<span class="underline">“缓存”，是一个保存上一个请求报文的本地存储，以及与之配套的子系统（控制其报文的存储、获取和删除）。</span>

A cache stores cacheable responses in order to reduce the response time and network bandwidth consumption on future, equivalent requests.

<span class="underline">缓存响应是为了减少将来的响应时间和网络带宽消耗。</span>

Any client or server **MAY** employ a cache, though a cache cannot be used by a server while it is acting as a tunnel.

<span class="underline">任何客户端或者服务器都可以使用缓存，但是，当服务器作为隧道（Tunnel）而使用时，不能使用缓存。</span>

**The** effect of a cache is that the request/response chain is shortened if one of the participants along the chain has a cached response applicable to that request.

<span class="underline">缓存的作用是缩短请求/响应链，表现为在一个有缓存参与的进请求/响应链中，如果链路中的某个缓存里保存了与该请求相匹配的响应报文。</span>

The following illustrates the resulting chain if B has a cached copy of an earlier response from O (via C) for a request that has not been cached by UA or A.

<span class="underline">下图的请求响应链的意思是，如果 B 保存了之前从源服务器 O （经过 C）返回的响应报文的副本，而这个响应没有缓存于用户代理 UA 或者 A 中，那么 B 就可以直接返回缓存的响应，而不用再转发至 C。</span>

         >             >
    UA =========== A =========== B - - - - - - C - - - - - - O
               <             <

**A** response is "cacheable" if a cache is allowed to store a copy of the response message for use in answering subsequent requests.

<span class="underline">如果一个缓存被允许去存储一个响应报文的副本用于应答随后的请求，那么这个响应报文可用于缓存。</span>

Even when a response is cacheable, there might be additional constraints placed by the client or by the origin server on when that cached response can be used for a particular request.

<span class="underline">即使一个响应可用于缓存，也可能存在一些由客户端或服务器设置的额外约束来规定在什么情况下所缓存的响应报文能够用于特定的请求。</span>

HTTP requirements for cache behavior and cacheable responses are defined in Section 2 of [RFC7234].

<span class="underline">HTTP 关于缓存的行为（cache behavior）以及可缓存的响应（cacheable reponses）的定义，见 [[RFC7234](https://tools.ietf.org/html/rfc7234)] 第二章。</span>

**There** is a wide variety of architectures and configurations of caches deployed across the World Wide Web and inside large organizations.

<span class="underline">多种多样的架构和配置的缓存被部署于万维网和大型组织中。</span>

These include national hierarchies of proxy caches to save transoceanic bandwidth, collaborative systems that broadcast or multicast cache entries, archives of pre-fetched cache entries for use in off-line or high-latency environments, and so on.

包括用于节省越洋带宽的国家级的代理缓存，广播或多路广播协作系统的缓存条目，用于离线或高延迟环境的预缓存档案条目等等。


<a id="orgbfd4ecc"></a>

## 2.5 一致性和错误处理 (Conformance and Error Handling)

**This** specification targets conformance criteria according to the role of a participant in HTTP communication.

<span class="underline">本规范为参与 HTTP 通信的角色制定一致性准则。</span>

Hence, HTTP requirements are placed on senders, recipients, clients, servers, user agents, intermediaries, origin servers, proxies, gateways, or caches, depending on what behavior is being constrained by the requirement.

<span class="underline">因此，HTTP 对一致性的要求着眼于发送端、接收端、客户端、服务端、用户代理、中间人、源服务器、代理、网关和缓存，取决于哪些行为被要求所约束。</span>

Additional (social) requirements are placed on implementations, resource owners, and protocol element registrations when they apply beyond the scope of a single communication.

<span class="underline">附加的要求着眼于实现、资源所有者以及应用于超出单一通信时的协议元素注册（Protocol element registrations）。</span>

**The** verb "generate" is used instead of "send" where a requirement differentiates between creating a protocol element and merely forwarding a received element downstream.

动词“生成”（Generate）之于“发送”（Send），用于区分“创建一个协议元素”之于“仅仅转发一个接收到的下行元素”。

**An** implementation is considered conformant if it complies with all of the requirements associated with the roles it partakes in HTTP.

<span class="underline">判断一个实现是否符合本规范，需要判断实现是否遵循了本规范中涉及到对参与 HTTP 通信的所有角色的所有要求。</span>

**Conformance** includes both the syntax and semantics of protocol elements.

<span class="underline">一致性包含协议元素（Protocol Elements）的句法及语义。</span>

A sender **MUST NOT** generate protocol elements that convey a meaning that is known by that sender to be false.

<span class="underline">发送端不能生成其明知是不正确的协议元素。</span>

（译注：不能将错就错）

A sender **MUST NOT** generate protocol elements that do not match the **grammar** defined by the corresponding ABNF rules.

<span class="underline">发送端不能生成与相关 ABNF 规则所定义的语法（Grammar）不匹配的协议元素。</span>

Within a given message, a sender **MUST NOT** generate protocol elements or **syntax** alternatives that are only allowed to be generated by participants in other roles (i.e., a role that the sender does not have for that message).

<span class="underline">在给定的报文中，发送端不能生成只允许在其他规则中生成的协议元素或相关句法（Syntax）替换品。</span>

（译注：Grammar 与 Syntax 的区别了解一下？）

**When** a received protocol element is parsed, the recipient **MUST** be able to parse any value of reasonable length that is applicable to the recipient's role and that matches the grammar defined by the corresponding ABNF rules.

<span class="underline">当一个接收到的协议元素被解释时，接收端必须能够解释任何适用于接收者这一角色以及与相关 ABNF 规则所定义的语法相匹配的、合理长度的值。</span>

Note, however, that some received protocol elements might not be parsed.

<span class="underline">需要注意的是，某些接收到的协议元素可能不被解释。</span>

（译注：出于兼容性考虑，当接收者的 HTTP 版本是 HTTP/1.0，假如接到到的报文版本是 HTTP/1.1，那么某些头域可能会被忽略。）

For example, an intermediary forwarding a message might parse a header-field into generic field-name and field-value components, but then forward the header field without further parsing inside the field-value.

<span class="underline">例如，一个中间人在转发报文时可能会将一个头域（Header-field）解释为域名（Field-name）和域值（Field-value），但转发头域时并没有再对域值进一步解释。</span>

**HTTP** does not have specific length limitations for many of its protocol elements because the lengths that might be appropriate will vary widely, depending on the deployment context and purpose of the implementation.

<span class="underline">HTTP 并没有对其协议元素作具体长度限制，因为“多少的长度才算合适”这个问题过于宽泛，需要依据具体的实现上下文和实现目的去决定。</span>

Hence, interoperability between senders and recipients depends on shared expectations regarding what is a reasonable length for each protocol element.

<span class="underline">因此，发送端和接收端之间的交互取决于它们“对于每一个协议元素，如何才算是合理长度”的共同期望。</span>

Furthermore, what is commonly understood to be a reasonable length for some protocol elements has changed over the course of the past two decades of HTTP use and is expected to continue changing in the future.

<span class="underline">此外，对于某些协议元素来说，多少才算是一个通俗合理的长度这个问题已经在过去二十多年来完全变更了，而且在将来仍会继续变更。</span>

**At** a minimum, a recipient **MUST** be able to parse and process protocol element lengths that are at least as long as the values that it generates for those same protocol elements in other messages.

<span class="underline">接收端必须能够最低限度地解释和处理协议元素的长度，至少和它在其他报文中生成的同样一个协议元素的长度一致。</span>

For example, an origin server that publishes very long URI references to its own resources needs to be able to parse and process those same references when received as a request target.

<span class="underline">例如，一个源服务器公布了一个非常长的 URI 来引用其自身资源，当它接收到以这个 URI 作为目标资源的请求时， 源服务器必须能够正确地解释和处理这个 URI。</span>

**A** recipient **MUST** interpret a received protocol element according to the semantics defined for it by this specification, including extensions to this specification, unless the recipient has determined (through experience or configuration) that the sender incorrectly implements what is implied by those semantics.

<span class="underline">接收端必须依据本规范（及其后续扩展）所定义的语义来转译其接收到的协议元素，除非接收端已经（通过经验或者配置）确定发送端并没有正确实现那些语义。</span>

For example, an origin server might disregard the contents of a received [Accept-Encoding](https://httpwg.org/specs/rfc7231.html#header.accept-encoding) header field if inspection of the [User-Agent](https://httpwg.org/specs/rfc7231.html#header.user-agent) header field indicates a specific implementation version that is known to fail on receipt of certain content codings.

<span class="underline">例如，源服务器接到一个请求报文，这个请求的 `Accept-Encoding` 报文头域表明发送端支持某些编码类型，源服务器检查这个请求的 User-Agent 的值获得这个用户代理的实现版本，（从过往的经验上）得知实际上这个用户代理并不能正确处理其声明的编码类型，于是源服务器可以忽略接收到的 `Accept-Encoding` 报文头域的内容。</span>

**Unless** noted otherwise, a recipient **MAY** attempt to [recover](https://en.wikipedia.org/wiki/Recovery_procedure) a usable protocol element from an invalid construct.

<span class="underline">除非另有说明，接收端可以尝试从一个不合法的报文结构中恢复出一个可用的协议元素。</span>

HTTP does not define specific error handling mechanisms except when they have a direct impact on security, since different applications of the protocol require different error handling strategies. 

<span class="underline">HTTP 协议在不用的应用场景上会有不同的错误处理策略的要求，因此，协议本身并没有定义具体的错误处理机制，除非这种错误直接影响到安全性。</span>

For example, a Web browser might wish to [transparently recover](https://en.wikipedia.org/wiki/Failure_transparency) from a response where the [Location](https://httpwg.org/specs/rfc7231.html#header.location) header field doesn't parse according to the ABNF, whereas a systems control client might consider any form of error recovery to be dangerous.

例如，一个网页浏览器接收到一个响应报文，响应报文的 Location 头域依据 ABNF 规则并不能合法解释到，于是浏览器可能希望进行透明恢复；但是对于一个系统控制客户端，可能认为任何方式的错误恢复都是危险的。

（译注，这里是拿“Web Browser”与所谓的“Systems Control Client”作对比。）


<a id="orga558a35"></a>

## 2.6 协议版本管理 (Protocol Versioning)

**HTTP** uses a "<major>.<minor>" numbering scheme to indicate versions of the protocol.

<span class="underline">HTTP 使用“<主版本>.<次版本>”的编号方式来表明协议的版本。</span>

This specification defines version "1.1".

<span class="underline">本规范定义了版本号“1.1”。</span>

The protocol version as a whole indicates the sender's conformance with the set of requirements laid out in that version's corresponding specification of HTTP.

<span class="underline">整体来说，协议版本表明了发送端遵循了哪一个版本的 HTTP 规范。</span>

**The** version of an HTTP message is indicated by an HTTP-version field in the first line of the message.

<span class="underline">HTTP 协议的版本通过在报文的第一行的 `HTTP-version` 域来指定。</span>

HTTP-version is case-sensitive.

需要注意的是\_，`HTTP-version` 是区分大小写的，以下是 HTTP-version 的 ABNF 规则。\_

    HTTP-version  = HTTP-name "/" DIGIT "." DIGIT
    HTTP-name     = %x48.54.54.50 ; "HTTP", case-sensitive 

**The** HTTP version number consists of two decimal digits separated by a "." (period or decimal point).

<span class="underline">HTTP 的版本号由 2 个十进制数组成，中间以英文句号“.”分隔。</span>

The first digit ("major version") indicates the HTTP messaging syntax, whereas the second digit ("minor version") indicates the highest minor version within that major version to which the sender is conformant and able to understand for future communication.

<span class="underline">第一个数字（主版本号）表明了 HTTP 报文的句法，第二个数字（次版本号）表明了发送端在接下来的通信中将会遵循以及能够理解的最高次版本。</span>

（译注：HTTP 版本用于 **发送端** 告诉接收端，使接收端了解发送端所使用或支持的 HTTP 版本。）

The minor version advertises the sender's communication capabilities even when the sender is only using a backwards-compatible subset of the protocol, thereby letting the recipient know that more advanced features can be used in response (by servers) or in future requests (by clients).

<span class="underline">次要版本号通告了发送端的通信能力，甚至当发送端仅仅使用协议的向后兼容的子集，因此让接收端了解更多高级功能能够被用于响应（作为服务器）或者用于接下来的请求（作为客户端）。</span>

（译注：接收端（Recipient）并不一定指的是源服务器，也可以是各种中间人（如代理、网关、隧道等），因此接收端既可能以服务器的身份向该发送端响应报文，也可以以中间人的身份转发报文出去）。

**When** an HTTP/1.1 message is sent to an HTTP/1.0 recipient [[RFC1945](https://tools.ietf.org/html/rfc1945)] or a recipient whose version is unknown, the HTTP/1.1 message is constructed such that it can be interpreted as a valid HTTP/1.0 message if all of the newer features are ignored.

<span class="underline">当一个 HTTP/1.1 报文被发送到一个 HTTP/1.0 接收端 [RFC1945] 或者一个接收端的版本号未知，HTTP/1.1 报文会被构建成一个能够被转译为一个合法的 HTTP/1.0 报文，如果忽略掉所有在 HTTP/1.1 新增的功能的话。</span>

（译注：也就是说，HTTP/1.1 是向后兼容的。）

This specification places recipient-version requirements on some new features so that a conformant sender will only use compatible features until it has determined, through configuration or the receipt of a message, that the recipient supports HTTP/1.1.

<span class="underline">本规范明确了接收端使用新功能的版本要求，以便于发送端可以仅仅使用兼容性功能与接收端通信，直到发送端（通过配置，或者解释接收到的报文）已经明确接收端支持 HTTP/1.1。</span>

（译注：发送端如何得知接收端支持 HTTP/1.1？一个办法是，发送端不管接收端是否支持，强制使用 HTTP/1.1；另一个办法是解释从接收端响应的报文，分析其是否真正实现了 HTTP/1.1。）

**The** interpretation of a header field does not change between minor versions of the same major HTTP version, though the default behavior of a recipient in the absence of such a field can change.

<span class="underline">对一个报文的头域的转译（Interpretation）并不会改变报文本身的协议主、次版本号，即使接收者的默认行为可能会因为缺少这些域而改变。</span>

Unless specified otherwise, header fields defined in HTTP/1.1 are defined for all versions of HTTP/1.x.

<span class="underline">除非具体说明，定义在 HTTP/1.1 版本的头域同样适用于所有 HTTP/1.x 版本。</span>

In particular, the Host and Connection header fields ought to be implemented by all HTTP/1.x implementations whether or not they advertise conformance with HTTP/1.1.

<span class="underline">特别是，`Host` 和 `Connection` 头域应该被所有版本（all HTTP/1.x）所实现，无论它们声明是否与 HTTP/1.1 版本一致。</span>

**New** header fields can be introduced without changing the protocol version if their defined semantics allow them to be safely ignored by recipients that do not recognize them.

<span class="underline">将来新的头域能够在不改变当前协议版本的情况下被引入，如果定义这些新头域的语义允许它们能够在接收者无法识别的情况下被其安全忽略（Safely ignored）。</span>

Header field extensibility is discussed in Section 3.2.1.

<span class="underline">头域的扩展（Extensibility）会在 [章节 3.2.1](#org839a087) 中讨论。</span>

**Intermediaries** that process HTTP messages (i.e., all intermediaries other than those acting as tunnels) **MUST** send their own HTTP-version in forwarded messages.

<span class="underline">处理 HTTP 报文的中间人（除了作为隧道的中间人） **必须** 在转发报文时发送它们自身的 `HTTP-version`。</span>

（译注：隧道作为盲中介，它并不会对报文本身作修改。）

In other words, they are not allowed to blindly forward the first line of an HTTP message without ensuring that the protocol version in that message matches a version to which that intermediary is conformant for both the receiving and sending of messages.

<span class="underline">换句话说，在以上中间人接收和发送报文的时候，它们并不允许在没有确保报文的版本与自身所使用的 HTTP 版本是否一致的情况下盲转发（Blindly Forwarding）HTTP 报文的首行。</span>

Forwarding an HTTP message without rewriting the HTTP-version might result in communication errors when downstream recipients use the message sender's version to determine what features are safe to use for later communication with that sender.

<span class="underline">当下行（Downstream）接收端使用报文的发送端版本来决定“对于接下来与之通信，什么功能能够安全使用”时，在没有重写 `HTTP-version` 的情况下直接转发一个 HTTP 报文可能会导致通信错误。</span>

**A** client **SHOULD** send a request version equal to the highest version to which the client is conformant and whose major version is no higher than the highest version supported by the server, if this is known.

<span class="underline">客户端所发送的请求报文版本 **应当** 等于其支持的最高版本，同时，客户端的主版本（Major Version）不能高于服务器支持的最高主版本号（如果客户端知道服务器的主版本号的话）。</span>

A client **MUST NOT** send a version to which it is not conformant.

<span class="underline">客户端 **不能** 发送自身不支持的协议版本。</span>

（译注：不能打肿脸充胖子。例如，当客户端最高仅支持 HTTP/1.0 时，请求行的 `HTTP-version` 域不能是 HTTP/1.1。）

**A** client **MAY** send a lower request version if it is known that the server incorrectly implements the HTTP specification, but only after the client has attempted at least one normal request and determined from the response status code or header fields (e.g., Server) that the server improperly handles higher request versions.

<span class="underline">如果客户端知道服务器没有正确实现 HTTP 规范，客户端 **可以** 向服务器发送较低版本的请求，但仅当客户端在至少发送一次正常（最高版本）请求未遂，并且依据服务器响应的报文（消息）状态码或者报文头域断定服务器不能正确处理更高版本的请求的情况下才被允许。</span>

**A** server **SHOULD** send a response version equal to the highest version to which the server is conformant that has a major version less than or equal to the one received in the request.

<span class="underline">服务器所发送的响应报文版本 **应当** 低于或等于其接收到的请求报文的主版本（Major Version）。</span>

A server **MUST NOT** send a version to which it is not conformant.

<span class="underline">服务器 **不能** 发送自身不支持的协议版本。</span>

A server can send a [505 (HTTP Version Not Supported)](https://httpwg.org/specs/rfc7231.html#status.505) response if it wishes, for any reason, to refuse service of the client's major protocol version.

<span class="underline">如果有必要，当服务器不支持客户端所声明的 HTTP 协议主版本时，服务器可以发送一个 505（HTTP 版本不支持）响应来拒绝来自客户端的请求服务。</span>

**A** server **MAY** send an HTTP/1.0 response to a request if it is known or suspected that the client incorrectly implements the HTTP specification and is incapable of correctly processing later version responses, such as when a client fails to parse the version number correctly or when an intermediary is known to blindly forward the `HTTP-version` even when it doesn't conform to the given minor version of the protocol.

<span class="underline">如果服务器知道或怀疑客户端没有正确实现 HTTP 规范而且不能够正确处理更高版本的响应的时候，服务器 **可以** 发送一个 HTTP/1.0 响应。例如，当客户端没有正确解释协议版本号，或者已知一个中间人即使自身没有实现给定的 `HTTP-version` 的次版本的规范（即不支持给定版本的 HTTP 协议）仍然盲目转发该 `HTTP-version` 等。</span>

Such protocol downgrades **SHOULD NOT** be performed unless triggered by specific client attributes, such as when one or more of the request header fields (e.g., [User-Agent](https://httpwg.org/specs/rfc7231.html#header.user-agent)) uniquely match the values sent by a client known to be in error.

<span class="underline">这些协议版本的降级行为 **不应该** 被执行除非服务器（或其他中间人）被特定客户端的特性所触发，例如当唯一匹配到客户端所发送的一个或多个请求头域（例如 [User-Agent](https://httpwg.org/specs/rfc7231.html#header.user-agent)）是已知会导致错误。</span>

**The** intention of HTTP's versioning design is that the major number will only be incremented if an incompatible message syntax is introduced, and that the minor number will only be incremented when changes made to the protocol have the effect of adding to the message semantics or implying additional capabilities of the sender.

<span class="underline">HTTP 版本编号的设计意图是：主版本号只会在引入不兼容的报文句法的情况下才会增加；次版本号只会在对协议的改动会引起语义的添加，或者赋予发送端新的能力时才会增加。</span>

However, the minor version was not incremented for the changes introduced between [[RFC2068](https://httpwg.org/specs/rfc7230.html#RFC2068)] and [[RFC2616](https://httpwg.org/specs/rfc7230.html#RFC2616)], and this revision has specifically avoided any such changes to the protocol.

<span class="underline">但是，从 [RFC2068] 到 [RFC2616] 的修订过程中，次版本号并没有增加（仍然是 HTTP/1.1），同时，本次修订已经明确避免对协议（版本号）的变动。</span>

**When** an HTTP message is received with a major version number that the recipient implements, but a higher minor version number than what the recipient implements, the recipient **SHOULD** process the message as if it were in the highest minor version within that major version to which the recipient is conformant.

<span class="underline">接收端接收到一个 HTTP 报文，如果接收端兼容该报文的主版本号，但不兼容其次版本号（接收端所支持的次版本号低于该报文所标识的次版本号），那么，接收端 **应当** 以其所能支持的最高次版本（前题是相同主版本）的方式来处理这个报文。</span>

A recipient can assume that a message with a higher minor version, when sent to a recipient that has not yet indicated support for that higher version, is sufficiently backwards-compatible to be safely processed by any implementation of the same major version.

TODO <span class="underline">当报文发送到接收端但没有指明其支持更高的版本，接收端可以假设这个报文带有更高的次版本，为所有具有相同主版本的实现去安全处理这些报文提供足够的向后兼容性。</span>


<a id="org050102c"></a>

## 2.7 统一资源标识符 (Uniform Resource Identifiers)

Uniform Resource Identifiers (URIs) [RFC3986] are used throughout HTTP as the means for identifying resources (Section 2 of [RFC7231]). URI references are used to target requests, indicate redirects, and define relationships.

统一资源标识符（URIs）[[RFC3986](https://tools.ietf.org/html/rfc3986)] 作为标识资源（[RFC7231] [第二章](https://tools.ietf.org/html/rfc7231#section-2)）的手段，普遍用于 HTTP 中。URI 引用（URI references）用于定位请求，标识重定向以及定义关联。

The definitions of "URI-reference", "absolute-URI", "relative-part", "scheme", "authority", "port", "host", "path-abempty", "segment", "query", and "fragment" are adopted from the URI generic syntax. An "absolute-path" rule is defined for protocol elements that can contain a non-empty path component. (This rule differs slightly from the path-abempty rule of RFC 3986, which allows for an empty path to be used in references, and path-absolute rule, which does not allow paths that begin with "//".) A "partial-URI" rule is defined for protocol elements that can contain a relative URI but not a fragment component.

`URI-reference`，`absolute-URI`，`relative-part`，`scheme`，`authority`，`port`，`host`，`path-abempty`，`segment`，`query` 和 `fragment` 是引用自 [[RFC3986](https://tools.ietf.org/html/rfc3986)]。`absolute-path` 规则用于定义能够包含一个非空路径的协议元素（这个规则在 RFC3986 中与 `path-abempty` 有些微的区别：`path-abempty` 允许在引用中使用空路径，而 `path-absolute` 规则不允许以“//”开头）。`partial-URL` 规则用于定义能包含一个相对 URI 但不能包含一个 `fragment` 的协议元素。

译注：【RFC3986】章节 3 有 URI 的完整图解，如下图所示：

      foo://example.com:8042/over/there?name=ferret#nose
      \_/   \______________/\_________/ \_________/ \__/
       |           |            |            |        |
    scheme     authority       path        query   fragment
       |   _____________________|__
      / \ /                        \
      urn:example:animal:ferret:nose

    URI-reference = <URI-reference, see [RFC3986], Section 4.1>
    absolute-URI  = <absolute-URI, see [RFC3986], Section 4.3>
    relative-part = <relative-part, see [RFC3986], Section 4.2>
    scheme        = <scheme, see [RFC3986], Section 3.1>
    authority     = <authority, see [RFC3986], Section 3.2>
    uri-host      = <host, see [RFC3986], Section 3.2.2>
    port          = <port, see [RFC3986], Section 3.2.3>
    path-abempty  = <path-abempty, see [RFC3986], Section 3.3>
    segment       = <segment, see [RFC3986], Section 3.3>
    query         = <query, see [RFC3986], Section 3.4>
    fragment      = <fragment, see [RFC3986], Section 3.5>
    
    absolute-path = 1*( "/" segment )
    partial-URI   = relative-part [ "?" query ]

Each protocol element in HTTP that allows a URI reference will indicate in its ABNF production whether the element allows any form of reference (URI-reference), only a URI in absolute form (absolute-URI), only the path and optional query components, or some combination of the above. Unless otherwise indicated, URI references are parsed relative to the effective request URI (Section 5.5).

HTTP 中的每一个允许 URI 引用的协议元素都会在它的 ABNF 产品中提及到这个元素允许哪种形式的引用：

1.  任何形式的引用（URI-reference）
2.  只能是绝对形式的引用（absolute-URI）
3.  只能是路径（path）和可选的查询（query）组成部分
4.  以上一个或多个组合

除非另有说明，URI 引用会解释为相关的“实际请求 URI”（[章节 5.5](#org7ba40ee)）。


<a id="org8d00096"></a>

### 2.7.1 http URI Scheme

The "http" URI scheme is hereby defined for the purpose of minting identifiers according to their association with the hierarchical namespace governed by a potential HTTP origin server listening for TCP ([RFC0793]) connections on a given port.

“http” 这个 URI scheme 专门为建造某种标识而定义的，这种标识的建造规则依据于其与监听给定端口号的 TCP 连接([[RFC0793](https://tools.ietf.org/html/rfc793)]) 的源服务器所管理的层级命名空间的关联。

（译注：[namespace](https://en.wikipedia.org/wiki/Namespace)，即命名空间，一般我们认为命名空间就是 Java、C# 等编程语言的语法规则，实际上，命名空间是一个广义的概念，它只是一组符号按一定的规则组合而成的用于关联一个对象的字符序列，这个字符序列就组成了一个命名空间（或者叫命名空间的名称），以便于通过这个命名空间来引用相关的对象。觉见的命名空间的例子有文件系统、Java 等编程语言的 namespace 关键字、计算机网络或分布式系统中对资源的命名等）

    http-URI = "http:" "//" authority path-abempty [ "?" query ] [ "#" fragment ]

The origin server for an "http" URI is identified by the authority component, which includes a host identifier and optional TCP port ([RFC3986], Section 3.2.2). The hierarchical path component and optional query component serve as an identifier for a potential target resource within that origin server's name space. The optional fragment component allows for indirect identification of a secondary resource, independent of the URI scheme, as defined in Section 3.5 of [RFC3986].

如上所示，对于一个“http” URI，源服务器被标记到 `authority` 部件里，`authority` 包含一个主机（host）标识和一个可选的 TCP 端口（[【RFC3986】，章节 3.2.2](https://tools.ietf.org/html/rfc3986#section-3.2.2)）。`path` 部件和可选的 `query` 部件组成一个标识符，对位于源服务器命名空间里的某个潜在目标资源进行标记。可选的 `fragment` 部件允许间接标记一个次要资源（Secondary Resource），不依赖于 URI scheme，见[【RFC3986】章节 3.5](https://tools.ietf.org/html/rfc3986#section-3.5) 。

（译注：按照[【RFC3986】章节 3.2](https://tools.ietf.org/html/rfc3986#section-3.2) 的解释，Authority 是“管理机构”的意思，由域名或 IP，加上一个可选的端口组成，通俗的讲，它的作用是相当于一个房屋的门牌，通过找门牌就可以找到这一间房屋。而 Path 相当于从房屋大门走到特定房间的路径。另外，Authority 除了“权威、权力”的意思以外，在其他文库管理方面还有其他有趣的意思<sup><a id="fnr.2" class="footref" href="#fn.2">2</a></sup>哦）

A sender **MUST NOT** generate an "http" URI with an empty host identifier. A recipient that processes such a URI reference **MUST** reject it as invalid.

发送端 **不能** 生成一个 `host` 为空的“http” URI。接收端 **必须** 以 URI 不合法的原因拒绝处理这种 URI。

If the host identifier is provided as an IP address, the origin server is the listener (if any) on the indicated TCP port at that IP address. If host is a registered name, the registered name is an indirect identifier for use with a name resolution service, such as DNS, to find an address for that origin server. If the port subcomponent is empty or not given, TCP port 80 (the reserved port for WWW services) is the default.

如果 `host` 标识符以 IP 地址的形式来提供，表示源服务器就是在那个 IP 地址对应的 TCP 端口的监听器；如果 `host` 是一个已注册的名称（可以理解为域名），所谓“已注册的名称”，是一个用于名称解释服务的间接标识，例如域名系统（DNS）用于查找源服务器的地址；如果 `port`
子部件为空或未提供，那么 TCP 默认使用 80（WWW 服务的保留端口）端口。

Note that the presence of a URI with a given authority component does not imply that there is always an HTTP server listening for connections on that host and port. Anyone can mint a URI. What the authority component determines is who has the right to respond authoritatively to requests that target the identified resource. The delegated nature of registered names and IP addresses creates a federated namespace, based on control over the indicated host and port, whether or not an HTTP server is present. See Section 9.1 for security considerations related to establishing authority.

需要注意的是，一个 URI 带有给定的 `authority` 部件并不意味着这个 URI 一定就是一个监听那个 `host` 以及对应 `port` 来等待连接的 HTTP 服务器。任务人都可以建造 URI。而 `authority` 决定的是谁有权力去响应这个定位目标资源的请求。注册域名和 IP 地址所代表的本质是，基于支配明确的 `host` 和 `port` 生成一个联合命名空间，无论最终呈现的是否是一个 HTTP 服务器。见[章节 9.1](#org1e3f6dc)。

When an "http" URI is used within a context that calls for access to the indicated resource, a client **MAY** attempt access by resolving the host to an IP address, establishing a TCP connection to that address on the indicated port, and sending an HTTP request message (Section 3) containing the URI's identifying data (Section 5) to the server. If the server responds to that request with a non-interim HTTP response message, as described in Section 6 of [RFC7231], then that response is considered an authoritative answer to the client's request.

当一个“http” URI 用于一个请求访问目标资源的上下文里，客户端 **可以** 尝试通过解释 `host` 获得 IP 地址，（通过对应的端口）建立一个 TCP 连接到这个地址，然后发送一个包含这个 URI 的识别数据（见[章节 5](#org77574f5)）的 HTTP 请求，从而访问到这个目标资源。如果服务器对这个请求响应了一个非过渡（non-interim）的 HTTP 响应报文（见[【RFC7231】章节 6](https://httpwg.org/specs/rfc7231.html#status.codes)），那么这个响应可认为是一个对客户端请求的权威应答（authoritative answer）。

Although HTTP is independent of the transport protocol, the "http" scheme is specific to TCP-based services because the name delegation process depends on TCP for establishing authority. An HTTP service based on some other underlying connection protocol would presumably be identified using a different URI scheme, just as the "https" scheme (below) is used for resources that require an end-to-end secured connection. Other protocols might also be used to provide access to "http" identified resources — it is only the authoritative interface that is specific to TCP.

虽然 HTTP 并不依赖其他传输协议，但“http” scheme 是特指基于 TCP 的服务的，这是因为名称委派处理（name delegation process?）需要依赖 TCP 来建立授权。一个基于其他多个底层通信协议的 HTTP 服务可能会被标识为使用一个不同的 URI scheme，类似于“https” scheme 是用于要求端到端安全的资源访问一样。其他协议可能也用于提供访问以“http”标识的资源，但这是唯一特定于 TCP 的授权接口。

The URI generic syntax for authority also includes a deprecated userinfo subcomponent ([RFC3986], Section 3.2.1) for including user authentication information in the URI. Some implementations make use of the userinfo component for internal configuration of authentication information, such as within command invocation options, configuration files, or bookmark lists, even though such usage might expose a user identifier or password. A sender **MUST NOT** generate the userinfo subcomponent (and its "@" delimiter) when an "http" URI reference is generated within a message as a request target or header field value. Before making use of an "http" URI reference received from an untrusted source, a recipient **SHOULD** parse for userinfo and treat its presence as an error; it is likely being used to obscure the authority for the sake of phishing attacks.

在 URI 的通用句法中有关授权（authority）方面还包含了一个已废弃的 `userinfo` 子部件（见[【RFC3986】章节 3.2.1](https://tools.ietf.org/html/rfc3986#section-3.2.1)），用于包含用户信息到 URI 里。某些实现将 `userinfo` 部件用于携带供内部使用的认证信息，例如命令调用的选项、配置文件或者书签列表，尽管这些用途可能会暴露用户名或密码。当发送端生成一个 HTTP 报文，包含以 `http` URI 引用作为一个请求目标或者报文头域里的值（例如头域 `Location`）时，发送端 **不能** 生成 `userinfo` 子部件（以及其“@”分隔符）。在使用一个接收自一个非受信的源的 `http` URI 引用时，接收者 **应当** 对 `userinfo` 进行解释并且对待它的出现当作一个错误，它的出现很可能带来网络钓鱼（Phishing Attach）的威胁。


<a id="orgce3a733"></a>

### 2.7.2 https URI Scheme

The "https" URI scheme is hereby defined for the purpose of minting identifiers according to their association with the hierarchical namespace governed by a potential HTTP origin server listening to a given TCP port for TLS-secured connections ([RFC5246]).

“https” 这个 URI scheme 专门为建造某种标识而定义的，这种标识的建造规则依据于其与监听给定端口号用于使用 TLS 安全协议进行 TCP 连接 ([【RFC5246】](https://tools.ietf.org/html/rfc5246)）的源服务器所管理的层级命名空间的关联。

All of the requirements listed above for the "http" scheme are also requirements for the "https" scheme, except that TCP port 443 is the default if the port subcomponent is empty or not given, and the user agent **MUST** ensure that its connection to the origin server is secured through the use of strong encryption, end-to-end, prior to sending the first HTTP request.

所有上文罗列过的对于“http” scheme 的要求同样适用于“https” scheme，除了没有明确指明端口号时“https”的默认端口是 443 而“http”的默认端口是 80，以及用户代理 **必须** 保证它与源服务器的端到端连接在发送第一个 HTTP 请求之前已经是使用强加密技术到达安全级别。

    https-URI = "https:" "//" authority path-abempty [ "?" query ] [ "#" fragment ]

Note that the "https" URI scheme depends on both TLS and TCP for establishing authority. Resources made available via the "https" scheme have no shared identity with the "http" scheme even if their resource identifiers indicate the same authority (the same host listening to the same TCP port). They are distinct namespaces and are considered to be distinct origin servers. However, an extension to HTTP that is defined to apply to entire host domains, such as the Cookie protocol [RFC6265], can allow information set by one service to impact communication with other services within a matching group of host domains.

需要注意的是，“https” URI scheme 依赖于 TLS 以及 TCP 来建立授权。通过“https” scheme 指向的资源与通过“https” scheme 指向的资源两者间并没有关系，即使它们的 `authority` 一样（有相同的 `host` 和相同的 TCP `port`）。它们的命名空间是有区别的，因此指向的是两个不同的源服务器。然而，后来的规范对 HTTP 进行了扩展来（使某些特性）适用于所有主机域名，例如 Cookie 协议[【RFC6265】](https://tools.ietf.org/html/rfc6265)，能够允许一个服务设置某些信息，通过一个关于主机域名的匹配规则集合来影响与其他服务的通信。

（译注：即使两个 URI 除了 scheme 不一样以外，其他各部件都一模一样，如 <http://www.example.com/path> 与 <https://www.example/path> 这两个 URI 并不一定指向同一个资源，因为这是两个是不同的 URI。）

The process for authoritative access to an "https" identified resource is defined in [RFC2818].

通过“https”标识来权威访问（Authoritative Access）<sup><a id="fnr.3" class="footref" href="#fn.3">3</a></sup>资源的过程定义于[【RFC2818】](https://tools.ietf.org/html/rfc2818)。


<a id="org5f3a9aa"></a>

### 2.7.3 http and https URI Normalization and Comparison

Since the "http" and "https" schemes conform to the URI generic syntax, such URIs are normalized and compared according to the algorithm defined in [Section 6 of {RFC3986}](https://tools.ietf.org/html/rfc3986#page-38), using the defaults described above for each scheme.

因为“http”和“https” schemes 都遵循 URI 通用句法，因此这些 URI 都可以依据定义于[【RFC3986】章节 6](https://tools.ietf.org/html/rfc3986#page-38) 的算法来进行标准化和对比。

If the port is equal to the default port for a scheme, the normal form is to omit the port subcomponent. When not being used in absolute form as the request target of an OPTIONS request, an empty path component is equivalent to an absolute path of "/", so the normal form is to provide a path of "/" instead. The scheme and host are case-insensitive and normally provided in lowercase; all other components are compared in a case-sensitive manner. Characters other than those in the "reserved" set are equivalent to their percent-encoded<sup><a id="fnr.4" class="footref" href="#fn.4">4</a></sup> octets: the normal form is to not encode them (see Sections 2.1 and 2.2 of [RFC3986]).

如果一个 scheme 的 `port` 等于其默认端口，那么其通常的形式是省略掉 `port` 子部件。当一个 `OPTIONS` 请求没有使用绝对形式（Absolute Form）作为请求目标（Request Target）时，一个空的 `path` 等价于绝对路径“`/`”，所以通常的形式是使用路径“`/`”来替换。`scheme` 和 `host` 是大小写不敏感的，通常使用小写。除了 `scheme` 和 `host` 以外的所有其外部件都是大小写敏感的。除了“保留”字符以外的所有字符都等价于它的 URL 编码（[Precent-encoded](https://en.wikipedia.org/wiki/Percent-encoding)，又叫百分号编码）形式（使用 `%` 加上两位的十六进制 0~F 字符表示）：一般形式是（如非必要）不要对它们进行编码（见[【RFC3986】章节 2.1 和 2.2](https://tools.ietf.org/html/rfc3986#section-2.1)）。

（译注：对于百分号编码还可以参考[这篇博文](https://www.cnblogs.com/DaoMuRen/p/5695030.html)。）

For example, the following three URIs are equivalent:

例如，以下三个 URI 是等价的：

    http://example.com:80/~smith/home.html
    http://EXAMPLE.com/%7Esmith/home.html
    http://EXAMPLE.com:/%7esmith/home.html


<a id="org8644818"></a>

# 3 报文格式（Message Format）

All HTTP/1.1 messages consist of a start-line followed by a sequence of octets in a format similar to the Internet Message Format [RFC5322]: zero or more header fields (collectively referred to as the "headers" or the "header section"), an empty line indicating the end of the header section, and an optional message body.

所有的 HTTP/1.1 报文的由一个“起始行（start-line）”以及随后的报头（Header），然后空一行（表明报头结束），最后是一个可选的报文体（Message Body）组合而成。其中报头由 0 个或多个报头域（Header Fields）组成，报头域的格式类似于
随后的一系列字符（octets，8位字节的字符）

    HTTP-message   = start-line
                     *( header-field CRLF )
                     CRLF
                     [ message-body ]

The normal procedure for parsing an HTTP message is to read the start-line into a structure, read each header field into a hash table by field name until the empty line, and then use the parsed data to determine if a message body is expected. If a message body has been indicated, then it is read as a stream until an amount of octets equal to the message body length is read or the connection is closed.

A recipient MUST parse an HTTP message as a sequence of octets in an encoding that is a superset of US-ASCII [USASCII]. Parsing an HTTP message as a stream of Unicode characters, without regard for the specific encoding, creates security vulnerabilities due to the varying ways that string processing libraries handle invalid multibyte character sequences that contain the octet LF (%x0A). String-based parsers can only be safely used within protocol elements after the element has been extracted from the message, such as within a header field-value after message parsing has delineated the individual fields.

An HTTP message can be parsed as a stream for incremental processing or forwarding downstream. However, recipients cannot rely on incremental delivery of partial messages, since some implementations will buffer or delay message forwarding for the sake of network efficiency, security checks, or payload transformations.

A sender MUST NOT send whitespace between the start-line and the first header field. A recipient that receives whitespace between the start-line and the first header field MUST either reject the message as invalid or consume each whitespace-preceded line without further processing of it (i.e., ignore the entire line, along with any subsequent lines preceded by whitespace, until a properly formed header field is received or the header section is terminated).

The presence of such whitespace in a request might be an attempt to trick a server into ignoring that field or processing the line after it as a new request, either of which might result in a security vulnerability if other implementations within the request chain interpret the same message differently. Likewise, the presence of such whitespace in a response might be ignored by some clients or cause others to cease parsing.


<a id="org957627d"></a>

## 3.1 起始行 (Start Line)

An HTTP message can be either a request from client to server or a response from server to client. Syntactically, the two types of message differ only in the start-line, which is either a request-line (for requests) or a status-line (for responses), and in the algorithm for determining the length of the message body (Section 3.3).

In theory, a client could receive requests and a server could receive responses, distinguishing them by their different start-line formats, but, in practice, servers are implemented to only expect a request (a response is interpreted as an unknown or invalid request method) and clients are implemented to only expect a response.

    start-line     = request-line / status-line


<a id="org386c1a2"></a>

### 3.1.1 请求行 (Request Line)

A request-line begins with a method token, followed by a single space (SP), the request-target, another single space (SP), the protocol version, and ends with CRLF.

    request-line   = method SP request-target SP HTTP-version CRLF

The method token indicates the request method to be performed on the target resource. The request method is case-sensitive.

    method         = token

The request methods defined by this specification can be found in Section 4 of [RFC7231], along with information regarding the HTTP method registry and considerations for defining new methods.

The request-target identifies the target resource upon which to apply the request, as defined in Section 5.3.

Recipients typically parse the request-line into its component parts by splitting on whitespace (see Section 3.5), since no whitespace is allowed in the three components. Unfortunately, some user agents fail to properly encode or exclude whitespace found in hypertext references, resulting in those disallowed characters being sent in a request-target.

Recipients of an invalid request-line SHOULD respond with either a 400 (Bad Request) error or a 301 (Moved Permanently) redirect with the request-target properly encoded. A recipient SHOULD NOT attempt to autocorrect and then process the request without a redirect, since the invalid request-line might be deliberately crafted to bypass security filters along the request chain.

HTTP does not place a predefined limit on the length of a request-line, as described in Section 2.5. A server that receives a method longer than any that it implements SHOULD respond with a 501 (Not Implemented) status code. A server that receives a request-target longer than any URI it wishes to parse MUST respond with a 414 (URI Too Long) status code (see Section 6.5.12 of [RFC7231]).

Various ad hoc limitations on request-line length are found in practice. It is RECOMMENDED that all HTTP senders and recipients support, at a minimum, request-line lengths of 8000 octets.


<a id="org3e53136"></a>

### 3.1.2 状态行 (Status Line)

The first line of a response message is the status-line, consisting of the protocol version, a space (SP), the status code, another space, a possibly empty textual phrase describing the status code, and ending with CRLF.

    status-line = HTTP-version SP status-code SP reason-phrase CRLF

The status-code element is a 3-digit integer code describing the result of the server's attempt to understand and satisfy the client's corresponding request. The rest of the response message is to be interpreted in light of the semantics defined for that status code. See Section 6 of [RFC7231] for information about the semantics of status codes, including the classes of status code (indicated by the first digit), the status codes defined by this specification, considerations for the definition of new status codes, and the IANA registry.

    status-code    = 3DIGIT

The reason-phrase element exists for the sole purpose of providing a textual description associated with the numeric status code, mostly out of deference to earlier Internet application protocols that were more frequently used with interactive text clients. A client SHOULD ignore the reason-phrase content.

    reason-phrase  = *( HTAB / SP / VCHAR / obs-text )


<a id="org0f4dd4f"></a>

## 3.2 头域 (Header Fields)

Each header field consists of a case-insensitive field name followed by a colon (":"), optional leading whitespace, the field value, and optional trailing whitespace.

    header-field   = field-name ":" OWS field-value OWS
    
    field-name     = token
    field-value    = *( field-content / obs-fold )
    field-content  = field-vchar [ 1*( SP / HTAB ) field-vchar ]
    field-vchar    = VCHAR / obs-text
    
    obs-fold       = CRLF 1*( SP / HTAB )
                   ; obsolete line folding
                   ; see Section 3.2.4

The field-name token labels the corresponding field-value as having the semantics defined by that header field. For example, the Date header field is defined in Section 7.1.1.2 of [RFC7231] as containing the origination timestamp for the message in which it appears.


<a id="org839a087"></a>

### 3.2.1 域的可扩展性 (Field Extensibility)

Header fields are fully extensible: there is no limit on the introduction of new field names, each presumably defining new semantics, nor on the number of header fields used in a given message. Existing fields are defined in each part of this specification and in many other specifications outside this document set.

New header fields can be defined such that, when they are understood by a recipient, they might override or enhance the interpretation of previously defined header fields, define preconditions on request evaluation, or refine the meaning of responses.

A proxy MUST forward unrecognized header fields unless the field-name is listed in the Connection header field (Section 6.1) or the proxy is specifically configured to block, or otherwise transform, such fields. Other recipients SHOULD ignore unrecognized header fields. These requirements allow HTTP's functionality to be enhanced without requiring prior update of deployed intermediaries.

All defined header fields ought to be registered with IANA in the "Message Headers" registry, as described in Section 8.3 of [RFC7231].


<a id="org9834eef"></a>

### 3.2.2 域的顺序 (Field Order)

The order in which header fields with differing field names are received is not significant. However, it is good practice to send header fields that contain control data first, such as Host on requests and Date on responses, so that implementations can decide when not to handle a message as early as possible. A server MUST NOT apply a request to the target resource until the entire request header section is received, since later header fields might include conditionals, authentication credentials, or deliberately misleading duplicate header fields that would impact request processing.

A sender MUST NOT generate multiple header fields with the same field name in a message unless either the entire field value for that header field is defined as a comma-separated list [i.e., #(values)] or the header field is a well-known exception (as noted below).

A recipient MAY combine multiple header fields with the same field name into one "field-name: field-value" pair, without changing the semantics of the message, by appending each subsequent field value to the combined field value in order, separated by a comma. The order in which header fields with the same field name are received is therefore significant to the interpretation of the combined field value; a proxy MUST NOT change the order of these field values when forwarding a message.

Note: In practice, the "Set-Cookie" header field ([RFC6265]) often appears multiple times in a response message and does not use the list syntax, violating the above requirements on multiple header fields with the same name. Since it cannot be combined into a single field-value, recipients ought to handle "Set-Cookie" as a special case while processing header fields. (See Appendix A.2.3 of [Kri2001] for details.)


<a id="orga4b9d50"></a>

### 3.2.3 空格 (Whitespace)

This specification uses three rules to denote the use of linear whitespace: OWS (optional whitespace), RWS (required whitespace), and BWS ("bad" whitespace).

The OWS rule is used where zero or more linear whitespace octets might appear. For protocol elements where optional whitespace is preferred to improve readability, a sender SHOULD generate the optional whitespace as a single SP; otherwise, a sender SHOULD NOT generate optional whitespace except as needed to white out invalid or unwanted protocol elements during in-place message filtering.

The RWS rule is used when at least one linear whitespace octet is required to separate field tokens. A sender SHOULD generate RWS as a single SP.

The BWS rule is used where the grammar allows optional whitespace only for historical reasons. A sender MUST NOT generate BWS in messages. A recipient MUST parse for such bad whitespace and remove it before interpreting the protocol element.

    OWS            = *( SP / HTAB )
                   ; optional whitespace
    RWS            = 1*( SP / HTAB )
                   ; required whitespace
    BWS            = OWS
                   ; "bad" whitespace


<a id="orgb8f7882"></a>

### 3.2.4 域解释 (Field Parsing)

Messages are parsed using a generic algorithm, independent of the individual header field names. The contents within a given field value are not parsed until a later stage of message interpretation (usually after the message's entire header section has been processed). Consequently, this specification does not use ABNF rules to define each "Field-Name: Field Value" pair, as was done in previous editions. Instead, this specification uses ABNF rules that are named according to each registered field name, wherein the rule defines the valid grammar for that field's corresponding field values (i.e., after the field-value has been extracted from the header section by a generic field parser).

No whitespace is allowed between the header field-name and colon. In the past, differences in the handling of such whitespace have led to security vulnerabilities in request routing and response handling. A server MUST reject any received request message that contains whitespace between a header field-name and colon with a response code of 400 (Bad Request). A proxy MUST remove any such whitespace from a response message before forwarding the message downstream.

A field value might be preceded and/or followed by optional whitespace (OWS); a single SP preceding the field-value is preferred for consistent readability by humans. The field value does not include any leading or trailing whitespace: OWS occurring before the first non-whitespace octet of the field value or after the last non-whitespace octet of the field value ought to be excluded by parsers when extracting the field value from a header field.

Historically, HTTP header field values could be extended over multiple lines by preceding each extra line with at least one space or horizontal tab (obs-fold). This specification deprecates such line folding except within the message/http media type (Section 8.3.1). A sender MUST NOT generate a message that includes line folding (i.e., that has any field-value that contains a match to the obs-fold rule) unless the message is intended for packaging within the message/http media type.

A server that receives an obs-fold in a request message that is not within a message/http container MUST either reject the message by sending a 400 (Bad Request), preferably with a representation explaining that obsolete line folding is unacceptable, or replace each received obs-fold with one or more SP octets prior to interpreting the field value or forwarding the message downstream.

A proxy or gateway that receives an obs-fold in a response message that is not within a message/http container MUST either discard the message and replace it with a 502 (Bad Gateway) response, preferably with a representation explaining that unacceptable line folding was received, or replace each received obs-fold with one or more SP octets prior to interpreting the field value or forwarding the message downstream.

A user agent that receives an obs-fold in a response message that is not within a message/http container MUST replace each received obs-fold with one or more SP octets prior to interpreting the field value.

Historically, HTTP has allowed field content with text in the ISO‑8859‑1 charset [ISO-8859-1], supporting other charsets only through use of [RFC2047] encoding. In practice, most HTTP header field values use only a subset of the US-ASCII charset [USASCII]. Newly defined header fields SHOULD limit their field values to US‑ASCII octets. A recipient SHOULD treat other octets in field content (obs‑text) as opaque data.


<a id="org902ee98"></a>

### 3.2.5 域限制 (Field Limits)

HTTP does not place a predefined limit on the length of each header field or on the length of the header section as a whole, as described in Section 2.5. Various ad hoc limitations on individual header field length are found in practice, often depending on the specific field semantics.

A server that receives a request header field, or set of fields, larger than it wishes to process MUST respond with an appropriate 4xx (Client Error) status code. Ignoring such header fields would increase the server's vulnerability to request smuggling attacks (Section 9.5).

A client MAY discard or truncate received header fields that are larger than the client wishes to process if the field semantics are such that the dropped value(s) can be safely ignored without changing the message framing or response semantics.


<a id="org0f8e507"></a>

### 3.2.6 域值的组成 (Field Value Components)

Most HTTP header field values are defined using common syntax components (token, quoted-string, and comment) separated by whitespace or specific delimiting characters. Delimiters are chosen from the set of US-ASCII visual characters not allowed in a token (DQUOTE and "(),/:;<=>?@[\\]{}").

    token          = 1*tchar
    
    tchar          = "!" / "#" / "$" / "%" / "&" / "'" / "*"
                   / "+" / "-" / "." / "^" / "_" / "`" / "|" / "~" 
                   / DIGIT / ALPHA
                   ; any VCHAR, except delimiters

A string of text is parsed as a single value if it is quoted using double-quote marks.

    quoted-string  = DQUOTE *( qdtext / quoted-pair ) DQUOTE
    qdtext         = HTAB / SP /%x21 / %x23-5B / %x5D-7E / obs-text
    obs-text       = %x80-FF

Comments can be included in some HTTP header fields by surrounding the comment text with parentheses. Comments are only allowed in fields containing "comment" as part of their field value definition.

    comment        = "(" *( ctext / quoted-pair / comment ) ")"
    ctext          = HTAB / SP / %x21-27 / %x2A-5B / %x5D-7E / obs-text

The backslash octet ("\\") can be used as a single-octet quoting mechanism within quoted-string and comment constructs. Recipients that process the value of a quoted-string MUST handle a quoted-pair as if it were replaced by the octet following the backslash.

    quoted-pair    = "\" ( HTAB / SP / VCHAR / obs-text )

A sender SHOULD NOT generate a quoted-pair in a quoted-string except where necessary to quote DQUOTE and backslash octets occurring within that string. A sender SHOULD NOT generate a quoted-pair in a comment except where necessary to quote parentheses ["(" and ")"] and backslash octets occurring within that comment.


<a id="org27d606a"></a>

## 3.3 报文体 (Message Body)

The message body (if any) of an HTTP message is used to carry the payload body of that request or response. The message body is identical to the payload body unless a transfer coding has been applied, as described in Section 3.3.1.

    message-body = *OCTET

The rules for when a message body is allowed in a message differ for requests and responses.

The presence of a message body in a request is signaled by a Content-Length or Transfer-Encoding header field. Request message framing is independent of method semantics, even if the method does not define any use for a message body.

The presence of a message body in a response depends on both the request method to which it is responding and the response status code (Section 3.1.2). Responses to the HEAD request method (Section 4.3.2 of [RFC7231]) never include a message body because the associated response header fields (e.g., Transfer-Encoding, Content-Length, etc.), if present, indicate only what their values would have been if the request method had been GET (Section 4.3.1 of [RFC7231]). 2xx (Successful) responses to a CONNECT request method (Section 4.3.6 of [RFC7231]) switch to tunnel mode instead of having a message body. All 1xx (Informational), 204 (No Content), and 304 (Not Modified) responses do not include a message body. All other responses do include a message body, although the body might be of zero length.


<a id="org5248f65"></a>

### 3.3.1 传输编码 (Transfer-Encoding)

The Transfer-Encoding header field lists the transfer coding names corresponding to the sequence of transfer codings that have been (or will be) applied to the payload body in order to form the message body. Transfer codings are defined in Section 4.

    Transfer-Encoding = 1#transfer-coding

Transfer-Encoding is analogous to the Content-Transfer-Encoding field of MIME, which was designed to enable safe transport of binary data over a 7-bit transport service ([RFC2045], Section 6). However, safe transport has a different focus for an 8bit-clean transfer protocol. In HTTP's case, Transfer-Encoding is primarily intended to accurately delimit a dynamically generated payload and to distinguish payload encodings that are only applied for transport efficiency or security from those that are characteristics of the selected resource.

A recipient MUST be able to parse the chunked transfer coding (Section 4.1) because it plays a crucial role in framing messages when the payload body size is not known in advance. A sender MUST NOT apply chunked more than once to a message body (i.e., chunking an already chunked message is not allowed). If any transfer coding other than chunked is applied to a request payload body, the sender MUST apply chunked as the final transfer coding to ensure that the message is properly framed. If any transfer coding other than chunked is applied to a response payload body, the sender MUST either apply chunked as the final transfer coding or terminate the message by closing the connection.

For example,

    Transfer-Encoding: gzip, chunked

indicates that the payload body has been compressed using the gzip coding and then chunked using the chunked coding while forming the message body.

Unlike Content-Encoding (Section 3.1.2.1 of [RFC7231]), Transfer-Encoding is a property of the message, not of the representation, and any recipient along the request/response chain MAY decode the received transfer coding(s) or apply additional transfer coding(s) to the message body, assuming that corresponding changes are made to the Transfer-Encoding field-value. Additional information about the encoding parameters can be provided by other header fields not defined by this specification.

Transfer-Encoding MAY be sent in a response to a HEAD request or in a 304 (Not Modified) response (Section 4.1 of [RFC7232]) to a GET request, neither of which includes a message body, to indicate that the origin server would have applied a transfer coding to the message body if the request had been an unconditional GET. This indication is not required, however, because any recipient on the response chain (including the origin server) can remove transfer codings when they are not needed.

A server MUST NOT send a Transfer-Encoding header field in any response with a status code of 1xx (Informational) or 204 (No Content). A server MUST NOT send a Transfer-Encoding header field in any 2xx (Successful) response to a CONNECT request (Section 4.3.6 of [RFC7231]).

Transfer-Encoding was added in HTTP/1.1. It is generally assumed that implementations advertising only HTTP/1.0 support will not understand how to process a transfer-encoded payload. A client MUST NOT send a request containing Transfer-Encoding unless it knows the server will handle HTTP/1.1 (or later) requests; such knowledge might be in the form of specific user configuration or by remembering the version of a prior received response. A server MUST NOT send a response containing Transfer-Encoding unless the corresponding request indicates HTTP/1.1 (or later).

A server that receives a request message with a transfer coding it does not understand SHOULD respond with 501 (Not Implemented).


<a id="orgc417d3f"></a>

### 3.3.2 内容长度 (Content-Length)

When a message does not have a Transfer-Encoding header field, a Content-Length header field can provide the anticipated size, as a decimal number of octets, for a potential payload body. For messages that do include a payload body, the Content-Length field-value provides the framing information necessary for determining where the body (and message) ends. For messages that do not include a payload body, the Content-Length indicates the size of the selected representation (Section 3 of [RFC7231]).

    Content-Length = 1*DIGIT

An example is

    Content-Length: 3495

A sender MUST NOT send a Content-Length header field in any message that contains a Transfer-Encoding header field.

A user agent SHOULD send a Content-Length in a request message when no Transfer-Encoding is sent and the request method defines a meaning for an enclosed payload body. For example, a Content-Length header field is normally sent in a POST request even when the value is 0 (indicating an empty payload body). A user agent SHOULD NOT send a Content-Length header field when the request message does not contain a payload body and the method semantics do not anticipate such a body.

A server MAY send a Content-Length header field in a response to a HEAD request (Section 4.3.2 of [RFC7231]); a server MUST NOT send Content-Length in such a response unless its field-value equals the decimal number of octets that would have been sent in the payload body of a response if the same request had used the GET method.

A server MAY send a Content-Length header field in a 304 (Not Modified) response to a conditional GET request (Section 4.1 of [RFC7232]); a server MUST NOT send Content-Length in such a response unless its field-value equals the decimal number of octets that would have been sent in the payload body of a 200 (OK) response to the same request.

A server MUST NOT send a Content-Length header field in any response with a status code of 1xx (Informational) or 204 (No Content). A server MUST NOT send a Content-Length header field in any 2xx (Successful) response to a CONNECT request (Section 4.3.6 of [RFC7231]).

Aside from the cases defined above, in the absence of Transfer-Encoding, an origin server SHOULD send a Content-Length header field when the payload body size is known prior to sending the complete header section. This will allow downstream recipients to measure transfer progress, know when a received message is complete, and potentially reuse the connection for additional requests.

Any Content-Length field value greater than or equal to zero is valid. Since there is no predefined limit to the length of a payload, a recipient MUST anticipate potentially large decimal numerals and prevent parsing errors due to integer conversion overflows (Section 9.3).

If a message is received that has multiple Content-Length header fields with field-values consisting of the same decimal value, or a single Content-Length header field with a field value containing a list of identical decimal values (e.g., "Content-Length: 42, 42"), indicating that duplicate Content-Length header fields have been generated or combined by an upstream message processor, then the recipient MUST either reject the message as invalid or replace the duplicated field-values with a single valid Content-Length field containing that decimal value prior to determining the message body length or forwarding the message.

**Note:** HTTP's use of Content-Length for message framing differs significantly from the same field's use in MIME, where it is an optional field used only within the "message/external-body" media-type.


<a id="org49c3093"></a>

### 3.3.3 报文体的长度 (Message Body Length)

The length of a message body is determined by one of the following (in order of precedence):

1.  Any response to a HEAD request and any response with a 1xx (Informational), 204 (No Content), or 304 (Not Modified) status code is always terminated by the first empty line after the header fields, regardless of the header fields present in the message, and thus cannot contain a message body.

2.  Any 2xx (Successful) response to a CONNECT request implies that the connection will become a tunnel immediately after the empty line that concludes the header fields. A client MUST ignore any Content-Length or Transfer-Encoding header fields received in such a message.

3.  If a Transfer-Encoding header field is present and the chunked transfer coding (Section 4.1) is the final encoding, the message body length is determined by reading and decoding the chunked data until the transfer coding indicates the data is complete.
    
    If a Transfer-Encoding header field is present in a response and the chunked transfer coding is not the final encoding, the message body length is determined by reading the connection until it is closed by the server. If a Transfer-Encoding header field is present in a request and the chunked transfer coding is not the final encoding, the message body length cannot be determined reliably; the server MUST respond with the 400 (Bad Request) status code and then close the connection.
    
    If a message is received with both a Transfer-Encoding and a Content-Length header field, the Transfer-Encoding overrides the Content-Length. Such a message might indicate an attempt to perform request smuggling (Section 9.5) or response splitting (Section 9.4) and ought to be handled as an error. A sender MUST remove the received Content-Length field prior to forwarding such a message downstream.

4.  If a message is received without Transfer-Encoding and with either multiple Content-Length header fields having differing field-values or a single Content-Length header field having an invalid value, then the message framing is invalid and the recipient MUST treat it as an unrecoverable error. If this is a request message, the server MUST respond with a 400 (Bad Request) status code and then close the connection. If this is a response message received by a proxy, the proxy MUST close the connection to the server, discard the received response, and send a 502 (Bad Gateway) response to the client. If this is a response message received by a user agent, the user agent MUST close the connection to the server and discard the received response.

5.  If a valid Content-Length header field is present without Transfer-Encoding, its decimal value defines the expected message body length in octets. If the sender closes the connection or the recipient times out before the indicated number of octets are received, the recipient MUST consider the message to be incomplete and close the connection.

6.  If this is a request message and none of the above are true, then the message body length is zero (no message body is present).

7.  Otherwise, this is a response message without a declared message body length, so the message body length is determined by the number of octets received prior to the server closing the connection.

Since there is no way to distinguish a successfully completed, close-delimited message from a partially received message interrupted by network failure, a server SHOULD generate encoding or length-delimited messages whenever possible. The close-delimiting feature exists primarily for backwards compatibility with HTTP/1.0.

A server MAY reject a request that contains a message body but not a Content-Length by responding with 411 (Length Required).

Unless a transfer coding other than chunked has been applied, a client that sends a request containing a message body SHOULD use a valid Content-Length header field if the message body length is known in advance, rather than the chunked transfer coding, since some existing services respond to chunked with a 411 (Length Required) status code even though they understand the chunked transfer coding. This is typically because such services are implemented via a gateway that requires a content-length in advance of being called and the server is unable or unwilling to buffer the entire request before processing.

A user agent that sends a request containing a message body MUST send a valid Content-Length header field if it does not know the server will handle HTTP/1.1 (or later) requests; such knowledge can be in the form of specific user configuration or by remembering the version of a prior received response.

If the final response to the last request on a connection has been completely received and there remains additional data to read, a user agent MAY discard the remaining data or attempt to determine if that data belongs as part of the prior response body, which might be the case if the prior message's Content-Length value is incorrect. A client MUST NOT process, cache, or forward such extra data as a separate response, since such behavior would be vulnerable to cache poisoning.


<a id="orgaebe17e"></a>

## 3.4 报文不完整的处理 (Handling Incomplete Messages)

A server that receives an incomplete request message, usually due to a canceled request or a triggered timeout exception, MAY send an error response prior to closing the connection.

A client that receives an incomplete response message, which can occur when a connection is closed prematurely or when decoding a supposedly chunked transfer coding fails, MUST record the message as incomplete. Cache requirements for incomplete responses are defined in Section 3 of [RFC7234].

If a response terminates in the middle of the header section (before the empty line is received) and the status code might rely on header fields to convey the full meaning of the response, then the client cannot assume that meaning has been conveyed; the client might need to repeat the request in order to determine what action to take next.

A message body that uses the chunked transfer coding is incomplete if the zero-sized chunk that terminates the encoding has not been received. A message that uses a valid Content-Length is incomplete if the size of the message body received (in octets) is less than the value given by Content-Length. A response that has neither chunked transfer coding nor Content-Length is terminated by closure of the connection and, thus, is considered complete regardless of the number of message body octets received, provided that the header section was received intact.


<a id="org1e4e10d"></a>

## 3.5 报文解释的健壮性 (Message Parsing Robustness)

Older HTTP/1.0 user agent implementations might send an extra CRLF after a POST request as a workaround for some early server applications that failed to read message body content that was not terminated by a line-ending. An HTTP/1.1 user agent MUST NOT preface or follow a request with an extra CRLF. If terminating the request message body with a line-ending is desired, then the user agent MUST count the terminating CRLF octets as part of the message body length.

In the interest of robustness, a server that is expecting to receive and parse a request-line SHOULD ignore at least one empty line (CRLF) received prior to the request-line.

Although the line terminator for the start-line and header fields is the sequence CRLF, a recipient MAY recognize a single LF as a line terminator and ignore any preceding CR.

Although the request-line and status-line grammar rules require that each of the component elements be separated by a single SP octet, recipients MAY instead parse on whitespace-delimited word boundaries and, aside from the CRLF terminator, treat any form of whitespace as the SP separator while ignoring preceding or trailing whitespace; such whitespace includes one or more of the following octets: SP, HTAB, VT (%x0B), FF (%x0C), or bare CR. However, lenient parsing can result in security vulnerabilities if there are multiple recipients of the message and each has its own unique interpretation of robustness (see Section 9.5).

When a server listening only for HTTP request messages, or processing what appears from the start-line to be an HTTP request message, receives a sequence of octets that does not match the HTTP-message grammar aside from the robustness exceptions listed above, the server SHOULD respond with a 400 (Bad Request) response.


<a id="orgd5db07b"></a>

# 4 传输编码（Transfer Codings）


<a id="orge6ce133"></a>

## 4.1 Chunked Transfer Coding


<a id="org5de3893"></a>

### 4.1.1 Chunk Extensions


<a id="org50ba17f"></a>

### 4.1.2 Chunked Trailer Part


<a id="orgc3f78b7"></a>

### 4.1.3 Decoding Chunked


<a id="orgf7f23d5"></a>

## 4.2 Compression Codings


<a id="org46e4b8b"></a>

### 4.2.1 Compress Coding


<a id="org5923bd6"></a>

### 4.2.2 Deflate Coding


<a id="org19d009d"></a>

### 4.2.3 Gzip Coding


<a id="orgfb316f0"></a>

## 4.3 TE


<a id="org53d7545"></a>

## 4.4 Trailer


<a id="org77574f5"></a>

# 5 报文路由（Message Routing）


<a id="orga306fad"></a>

## 5.1 标识目标资源 (Identifying a Target Resource)


<a id="org5ec56fd"></a>

## 5.2 Connecting Inbound


<a id="orgd1804be"></a>

## 5.3 请求目标 (Request Target)


<a id="orgf834915"></a>

### 5.3.1 (origin-form)


<a id="org153cebb"></a>

### 5.3.2 (absolute-form)


<a id="org1c3638c"></a>

### 5.3.3 (authority-form)


<a id="orgc95d555"></a>

### 5.3.4 (asterisk-form)


<a id="org4d0e8e5"></a>

## 5.4 主机 (Host)


<a id="org7ba40ee"></a>

## 5.5 Effective Request URI


<a id="org06d22fe"></a>

## 5.6 Associating a Response to a Request


<a id="org066fec4"></a>

## 5.7 报文转发 (Message Forwarding)


<a id="orgad39f20"></a>

### 5.7.1 Via


<a id="org630ebc3"></a>

### 5.7.2 Transformations


<a id="orge2597b0"></a>

# 6 连接管理（Connection Management）


<a id="org576bde0"></a>

## 6.1 连接 (Connection)


<a id="org85c1699"></a>

## 6.2 建立 (Establishment)


<a id="orgccd03a7"></a>

## 6.3 持久性 (Persistence)


<a id="orgcd7c628"></a>

### 6.3.1 (Retrying Requests)


<a id="orgb9421fe"></a>

### 6.3.2 (Pipelining)


<a id="orgb618025"></a>

## 6.4 并发性 (Concurrency)


<a id="org4650cb9"></a>

## 6.5 失败和超时 (Failures and Timeouts)


<a id="orgf45cd65"></a>

## 6.6 销毁 (Tear-down)


<a id="orgc0cff1a"></a>

## 6.7 升级 (Upgrade)


<a id="orgb633ea2"></a>

# 7 ABNF 列表扩展：#rule（ABNF List Extension: #rule）


<a id="org2c48e90"></a>

# 8 INAN 考虑（IANA Considerations）


<a id="orgdf30041"></a>

## 8.1 Header Field Registration


<a id="org212ee20"></a>

## 8.2 URI Scheme Registration


<a id="org76af6b3"></a>

## 8.3 Internet Media Type Registration


<a id="orga870e90"></a>

### 8.3.1 Internet Media Type message/http


<a id="org8ed9c5f"></a>

### 8.3.2 Internet Media Type application/http


<a id="org4d82db6"></a>

## 8.4 Transfer Coding Registry


<a id="org135cebe"></a>

### 8.4.1 Procedure


<a id="org530f24a"></a>

### 8.4.2 Registration


<a id="org4096af6"></a>

## 8.5 Content Coding Registration


<a id="org191505b"></a>

## 8.6 Upgrade Token Registry


<a id="orgf181bcc"></a>

### 8.6.1 Procedure


<a id="org2feb3f1"></a>

### 8.6.2 Upgrade Token Registration


<a id="org0af0d25"></a>

# 9 安全考虑（Security Considerations）


<a id="org1e3f6dc"></a>

## 9.1 Establishing Authority


<a id="org2131912"></a>

## 9.2 Risks of Intermediaries


<a id="org083cfbd"></a>

## 9.3 Attacks via Protocol Element Length


<a id="org29b9a36"></a>

## 9.4 Response Splitting


<a id="org5c43a6b"></a>

## 9.5 Request Smuggling


<a id="org43c3f69"></a>

## 9.6 Message Integrity


<a id="org2e4dc40"></a>

## 9.7 Message Confidentiality


<a id="orgce09664"></a>

## 9.8 Privacy of Server Log Information


<a id="orga72f474"></a>

# 10 感谢（Acknowledgments）


<a id="orgb9bc814"></a>

# 11 参考资料（References）


<a id="orga723ab5"></a>

# 附录 A：HTTP 版本历史（Appendix A. HTTP Version History）


<a id="orgf6cbd21"></a>

# 附录 B：收集的 ABNF（Appendx B. Collected ABNF）


<a id="org31a7d70"></a>

# 索引（Index）


# Footnotes

<sup><a id="fn.1" href="#fnr.1">1</a></sup> 访问点（AP, Access Point）一般翻译为“无线访问节点”，或“桥接器”。其主要在媒体存取控制层MAC中扮演无线工作站及有线局域网络的桥梁。

-   [百科：AccessPoint](https://baike.baidu.com/item/AccessPoint/6762525?fr=aladdin)
-   [Wikipedia: Wireless access point](https://en.wikipedia.org/wiki/Wireless_access_point)

<sup><a id="fn.2" href="#fnr.2">2</a></sup> Authority

Authority 在文档管理领域中还有“组织、建立规范统一的索引”的意思，例如 Authority Control，即规范控制，通常是指始终如一地使用和维护统一的名称、主题和题名等规范形式，而这些名称、主题和题名等在书目记录文档中用作标目。

-   [Wikisource: Authority Control](https://en.wikisource.org/wiki/Wikisource:Authority_control) is the practice of creating and maintaining index terms for bibliographic material in a catalogue, and is particularly useful for assigning unique identifiers to people, works or subjects. When applied to Wikisource, it means maintaining links to a set of standard external catalogues.
-   [Wikipedia: In library science, authority control](https://en.wikipedia.org/wiki/Authority_control#cite_note-tws2NovY333-7) is a process that organizes bibliographic information, for example in library catalogs by using a single, distinct spelling of a name (heading) or a numeric identifier for each topic. The word authority in authority control derives from the idea that the names of people, places, things, and concepts are authorized, i.e., they are established in one particular form.

<sup><a id="fn.3" href="#fnr.3">3</a></sup> Authoritative Access

权威访问，[【RFC7230】章节 5.7.2](https://tools.ietf.org/html/rfc7230#section-5.7.2) 有这样的描述：

    A proxy that transforms the payload of a 200 (OK) response can further inform downstream recipients that a transformation has been applied by changing the response status code to 203 (Non-Authoritative Information).

客户端接收到来自源服务器的状态码为 200 (OK) 的响应报文时，其中报文的 payload 没有被中间代理转换或更改过，那么这次访问就叫“权威访问”，那个无经过转换或更改的报文就叫“权威信息”。而当 200 (OK)  响应报文经过中间代理修改过时，这个报文就叫“非权威信息”，通常中间代理会将源服务器返回的 200 (OK) 状态码改为 203 (Non-Authoritative Information)。

-   [Section 5.7.2 of {RFC7230}](https://tools.ietf.org/html/rfc7230#section-5.7.2)
-   [Section 6.3.4 of {RFC7231}](https://tools.ietf.org/html/rfc7231#section-6.3.4)

<sup><a id="fn.4" href="#fnr.4">4</a></sup> Percent-encoded

百分号编码，也叫作 URL 编码。
