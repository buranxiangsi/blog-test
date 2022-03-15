# Node.js http模块

HTTP 核心模块是 Node.js 网络的关键模块。

引入

```js
const http = require('http')
```

## 属性

- `http.METHODS`  列出所有支持的HTTP方法
- `http.STATUS_CODES` 列出状态码和描述
- ``http.globalAgent``  指向Agent对象的全局实例，用于管理HTTP客户端链接的持久性和复用。



## 方法

### http.createServer()  

返回 `http.Server` 类的新实例。

```js
const server = http.createServer((req, res) => {
  //使用此回调处理每个单独的请求。
})

```

### http.request()

发送HTTP请求到服务器，并创建 `http.ClientRequest` 类的实例

### http.get()

似于 `http.request()`，但会自动地设置 HTTP 方法为 GET，并自动地调用 `req.end()`。



## 类

- `http.Agent`
- `http.ClientRequest`
- `http.Server`
- `http.ServerResponse`
- `http.IncomingMessage`

