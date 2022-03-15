# HTTP

## 概述

- 超文本传输协议：用于传输超媒体文档（例如 HTML）的应用层协议。
- 为浏览器和服务器之间通信设计
- 无状态协议——服务器不会保留数据（状态）
- 基于TCP/IP层，但可以在任何可靠的传输层上使用
- **client-serve**  在web上进行数据交换

### 基于HTTP的组件系统

- 客户端：user-agent ——任何能够为用户发起行为的工具，一般是浏览器

- 服务端：web-server——服务并提供客户端请求的文档

- 代理：Proxies：

  客户和服务器之间由许多其它设备转发HTTP消息，大多出现在传输层，网络层，和物理层上，其中**表现在应用层上的被称为代理**。

  - 作用：
  - 缓存：可公开可私有，比如浏览器缓存
  - 过滤：比如反病毒扫描，比如家长控制
  - 负载均衡：让多个服务器服务不同的请求
  - 认证：对不通过的资源进行权限管理
  - 日志记录：存储历史信息

### HTTP能够控制的

- 缓存
- 开放同源限制  2010年
- 认证
- 代理和隧道
- 会话

### HTTP报文

- 请求报文

  ![](https://mdn.mozillademos.org/files/13687/HTTP_Request.png)

  - HTTP的method(GET POST)
  - path 路径
  - HTTP协议版本号
  - headers

- 响应报文

  ![](https://mdn.mozillademos.org/files/13691/HTTP_Response.png)

  - HTTP协议版本号
  - 状态码
  - 状态信息
  - HTTP header
  - 可选项	

### HTTP API：

**XMLHttpRequest**



## 缓存

*缓存的种类以及配置  headers*

缓存是一种保存资源副本并在下次请求时直接使用该副本的技术，当 web 缓存发现请求的资源已经被存储，它会拦截请求，返回该资源的拷贝，而不会去源服务器重新下载。因此减少等待的时间和网络流量，加速响应。缓解服务器的压力，提提升性能。

### 私有(浏览器缓存)

只能用于单独用户，浏览器缓存用户通过HTTP下载的所有文档，具备向前向后导航，保存网页，查看源码，离线浏览的功能

### 共享缓存

被多个用户使用

### 缓存操作的目标

常见HTTP缓存只能存储GET响应，关键包括request method和目标url

- 请求成功的响应，GET请求，状态码为200
- 永久重定向，状态码301
- 错误响应，状态码404的页面
- 不完全响应：206
- 除了 GET 请求外，如果匹配到作为一个已被定义的cache键名的响应。

### 缓存控制

HTTP/1.1定义 **Cache-control** 头 区分对缓存机制的支持情况

- 没有缓存             `Cache-Control: no-store` 
- 缓存但重新验证 `Cache-Control: no-cache` 服务器验证请求是否过期
- 私有和公共缓存 `Cache-Control: private|public`
- 过期                    `Cache-Control: max-age=31536000`
- 验证方式            `Cache-Control: must-revalidate`

### 新鲜度

**缓存驱逐**：缓存只有有限的空间用于存储资源副本，所以缓存会定期地将一些副本删除。

另一方面资源更新，由于HTTP是C/S模式的协议，双方为资源约定一个过期时间。过期后，缓存请求附加`If-None-Match`头，发给服务器，服务器返回304状态码，表示没过期，过期则返回资源。

有特定头信息的请求会计算缓存寿命，比如`Cache-control: max-age=N` 不含这个属性时则查看是否包含`Expires` 属性，前两者都没有，则查找Last-Modified信息

**Steve Souders** 称之为 `revving` 的技术，不频繁更新文件的会使用特定的命名方式：在URL后面（通常是文件名后面）会加上版本号。被视为完全新的独立资源，期限一年以上，弊端是引用资源的的地方都需要更新，解决办法是采用自动化构建工具，低频更新的（js/css）变动，用在高频变动的html里做入口的改动。

### 缓存验证

触发验证：

- 用户点击刷新按钮
- 缓存响应头 `Cache-control: must-revalidate`
- 浏览器偏好设置Advanced->Cache为强制验证缓存

### ETags

ETags作为缓存的一种强校验器，如果资源请求的响应头里含有ETag, 客户端可以在后续的请求的头中带上 [`If-None-Match`](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/If-None-Match) 头来验证缓存。

[`Last-Modified`](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Last-Modified) 响应头可以作为一种弱校验器。

当向服务端发起缓存校验的请求时，服务端会返回 [`200`](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/200) ok表示返回正常的结果或者 [`304`](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/304) Not Modified(不返回body)表示浏览器可以使用本地缓存文件。304的响应头也可以同时更新缓存文档的过期时间。

### Vary响应

[`Vary`](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Vary) HTTP 响应头决定了对于后续的请求头，如何判断是请求一个新的资源还是使用缓存的文件。有利于内容服务的动态多样性。

`Vary: User-Agent`  头  缓存服务器需要通过UA判断是否使用缓存的页面。

## Cookie

HTTP Cookie（也叫 Web Cookie 或浏览器 Cookie）是**服务器发送**到用户浏览器并保存在本地的一小块数据，它会在浏览器下次向同一服务器再发起请求时被携带并发送到服务器上。

用途

- 会话状态管理 登录状态，购物车，游戏分数
- 个性化设置  用户自定义设置，主题
- 浏览器跟踪行为，跟踪分析用户行为

现在直接存储到本地，使用storage API 或者 IndexedDB

### 创建

`Set-Cookie: <cookie名>=<cookie值>`

### 定义生命周期

会话期：浏览器关闭自动删除

持久性：过期时间Expires   有效期`Max-Age`

`Set-Cookie: id=a3fWa; Expires=Wed, 21 Oct 2015 07:28:00 GMT;`

### 限制访问

- `Secure` 属性 只通过被 HTTPS 协议加密过的请求发送给服务端，
- `HttpOnly` 属性 仅作用于服务器。

### Cookie 作用域

- Domain 属性  指定了哪些主机可以接受 Cookie。
- Path 属性         标识指定了主机下的哪些路径可以接受 Cookie



## CORS

## 安全

## 消息

## 会话

## 连接管理