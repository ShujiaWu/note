# HTTP1.0、HTTP1.1 和 HTTP2.0 的区别

> 超文本传输协议（HTTP，HyperText Transfer Protocol)是互联网上应用最为广泛的一种网络协议。所有的WWW文件都必须遵守这个标准。设计HTTP最初的目的是为了提供一种发布和接收HTML页面的方法。

## HTTP 各版本发布时间

1991  ==>  HTTP/0.9

1996  ==>  HTTP/1.0

1999  ==>  HTTP/1.1

2015  ==>  HTTP/2.0

## HTTP的基本优化

影响一个 HTTP请求的因素主要有两个: **带宽** 和 **延迟**。

带宽：即网络传输速率。

延迟：
* 浏览器阻塞

    浏览器对于同一个域名，同时只能有 4 个连接（不同浏览器内核会有所差异），超过浏览器最大连接数限制，后续请求就会被阻塞。

* DNS查询

    域名需要通过DNS解析成IP，浏览器才能与服务器建立连接。通过缓存DNS解析结果来减少这个查询的时间。

* 建立连接

    HTTP是基于TCP协议的，TCP连接需要三次握手才能完成。每次的三次握手过程在高延迟场景下影响较明显。

## HTTP1.0 和HTTP 1.1 的区别

* 缓存处理

    HTTP 1.0 : 使用If-Modified-Since,Expires来做为缓存判断的标准。

    HTTP 1.1 : 引入了更多的缓存空中策略,Entity tag，If-Unmodified-Since, If-Match, If-None-Match。

* 带宽优化及网络连接的使用

    HTTP 1.0 : 存在带宽浪费现象,只能获取完整的资源对象,不支持断点续传。

    HTTP 1.1 : 引入了rang头域,允许返回资源对象的某个部分,状态码为206(partial Content)。

* 错误通知的管理:

    HTTP 1.1 : 新增了24个错误状态响应码。

* Host头处理

    HTTP 1.0 : 认为每台服务器都绑定一个唯一的IP地址。

    HTTP 1.1 : 请求消息和响应消息都支持Host头域，如果没有Host则会报告一个错误（400 Bad Request），支持一台服务器上存在多个虚拟主机。

* 长连接

    HTTP 1.0 : 不支持长连接

    HTTP 1.1 : 支持长连接（PersistentConnection）和请求流水线（Pipelining）处理，在一个TCP连接上可以传送多个HTTP请求和响应，减少建立和关闭连接的消耗和延迟。默认状态下是开启`Connection:keep-alive`。

## HTTP 和 HTTPS

* HTTPS 需要到 CA 申请证书
* HTTP协议运行在TCP之上，所有传输的内容都是明文，HTTPS运行在SSL/TLS之上，SSL/TLS运行在TCP之上，所有传输的内容都经过加密的。
* HTTP和HTTPS使用的是完全不同的连接方式，用的端口也不一样，前者是80，后者是443。
* HTTPS可以有效的防止运营商劫持，解决了防劫持的一个大问题。

**HTTP :** HTTP --> TCP

**HTTPS :** HTTP --> SSL/TLS --> TCP

## SPDY : HTTP 1.x的优化

`SPDY` 是google在2012年提出的方案用于优化HTTP 1.x请求延迟和解决HTTP 1.x的安全性。

* 降低延迟

    采用 `多路复合(multiplexing)`,让多个请求共享一个TCP连接.解决浏览器阻塞的问题,降低延迟提高带宽利用率.

* 请求优先级

    SPDY允许对每个请求设置优先级,对重要的请求优先响应,用于解决多路复合带来的关键请求呗阻塞的问题.

* header压缩

    对header进行压缩减少请求时的包大小.

* 基于HTTPS的加密传输协议

    提高数据传输的可靠性

* 服务端推送

    服务端可以在一个请求后将相应的其他的资源推送给客户端,客户端在下次请求时可以直接从缓存中获取到。

HTTP --> SPDY --> SSL --> TCP

## HTTP 2.0 : SPDY的升级版

* HTTP 2.0 支持明文 HTTP 传输， SPDY 强制使用 HTTPS

* HTTP 2.0 消息头的压缩算法是 `HPACK`, SPDY使用的是`DEFLATE`。

## HTTP 2.0 和 HTTP 1.x的比较

* 新的二进制格式：HTTP 1.x 的解析是基于文本。HTTP 2.0 是基于二进制的。

* 多路复用：即连接共享，即每一个request都是使用作连接共享机制的。一个request对应一个id，这样一个连接上可以有多个request，每个连接的request可以随机的混杂在一起，接收方可以根据request的 id将request再归属到各自不同的服务端请求里面。

* header压缩：HTTP2.0使用encoder来减少需要传输的header大小，通讯双方各自cache一份header fields表，既避免了重复header的传输，又减小了需要传输的大小。

* 服务器推送：HTTP 2.0 具有与SPDY一样的服务器推送功能。