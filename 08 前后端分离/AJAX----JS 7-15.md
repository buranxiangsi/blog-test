# AJAX----JS

- 用js发请求和收响应

- AJAX是浏览器上的功能

- 浏览器在window上加了一个 `XMLHttpRequest`  构造函数

- js 通过 `XMLHttpRequest` 发请求，收响应

- AJAX加载css | js |HTML  | JSON

- <u>创建 HttpRequest对象</u>

- <u>调用对象的open方法</u>

- <u>监听对象的 onload(**onreadystatechange**) & onerror 事件</u>

- <u>调用对象的send 方法</u>

- onreadystatechange 当结果下载之后， 浏览器调用函数获得结果——回调(callback)g写给别人用的函数

- window.JSON

- JSON.parse  将json语法字符串转换成js对应类型的数据

- JSON.stringify  js数据转换成JSON字符串  

- 加载分页

- **异步与同步**

- 同步：能直接拿到结果

- 异步：不能直接拿到结果——轮询/回调

- 关联：异步任务需要在得到结果时通知js来拿结果

- 区别：需要用回调函数来通知结果

- 回调也可以用到同步任务里

- 判断同步异步

- 异步函数的返回值处于 `setTiimeout   AJAX(XMLHttpRequest)  AddEventListener`  内部

-  异步任务不能拿到结果

- 我们传一个回调给异步任务

- 异步任务完成时调用回调

- 调用的时候把结果作为参数。

- **Promise**

- 使用promise的原因

- 不够规范

- 容易出现回调地狱

- 很难进行错误处理

- AJAX封装

- ```js
  ajax('get', '/xxx')//返回一个含有.then()方法的对象
      .then((response)=>{}, (request)=>{})//回调
  ajax = (method, url, options)=>{
      return new Promise((resolve, reject)=>{  //类似jQuery  return Promise对象
          const {success, fail} = options
          const request = new XMLHttpRequest()
          request.open(method, url)
          request.onreadystatechange = ()=>{
              if(request.readyState === 4){
                  //成功调用resolve， 失败调用reject
                  if(request.status < 400){
                      resolve.call(null, request.response) //成功
                  }else if(request.status >= 400){
                      reject.call(null, request)  //失败
                  }
              }
          }
          request.send()//上传数据 
      })
  }
  //post不能上传
  //不能设置请求头 request.setRequsetHeader(key, value)
  ```

- `return new Promise((resolve, reject)=>{...})`  异步任务回调转变成promise回调

- `.then(success, fail)`  传入成功和失败函数

- 库

- jQuery.ajax

- axios   ——  最新的AJAX库

- **跨域 | CORS | JSONP**

- 同源策略：限制数据访问，能引用

- 源 =  协议 + 域名 + 端口号

- CORS 跨域资源共享

- 设置响应头

- Access-Control-Allow-Origin: url

- 具体语法查看MDN

- JSONP——IE

- referer  检查

- 封装JSONP

- ```js
  function jsonp(url){
      return new Promise((resolve, reject)=>{
          const random = 'Name' + Math.random()
          window[random] = data =>{resolve(data)}
          const script = document.createElement("script")
          script.src = `${url}?callback=${random}`
          script.onload = ()=>{
              script.remove()
          }
          script.onerror = ()=>{
              reject()
          }
          document.body.appendChild(script)
      })
  }
  
  jsonp('url')
      .then((data)=>{
      console.log(data)
  })
  ```

- 读不到状态码，script标签，不支持cors

- 静态服务器  Static Server

- 处理错误：`try(){}catch(){}`

- 动态服务器  

- 区别

- 是否请求了数据库，请求数据库是动态服务器

- ```js
  //读取数据
  fs.readFileSync('./xx.json').toString()
  JSON.parse() //反序列化，得到数组
  
  //存储数据
  JSON.stringify  //序列化，得到字符串
  fs.weiteFileSync('./xx.json', data)

- 用户注册

- 前端

- 写一个form，让用户填name  password

- 监听submit事件

- 发送post请求 ，数据位于请求体

- 后端

- 接收post请求

- 获取请求体中的name和password

- 读取数据，查看是否有匹配的name和password——用户登录

- 匹配，**标记**(Cookie)为已登录——用户登录

- 存储数据

- Cookie 

-  服务器下发给浏览器的一段字符，相当于公园门票

- 浏览器必须保存这个Cookie，

- 之后发起相同二级域名请求时，浏览器必须附上Cookie

- set-Cookie  响应头  MDN

- 防篡改用户id

- 加密 安全漏洞，加密后的内容可无限期使用，  解决 JWT

- 把信息隐藏在服务器——会话 session

- 隐藏在session里，加一个随机id，把id发给浏览器，后端读取session[id]

- session  保存用户信息

- 有时效性



