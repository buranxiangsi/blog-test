1. 如何发请求
   1. chrome地址栏
   2. curl命令
2. 响应
   1. node.js http模块
   ```
   path  不带查询参数的路劲 /x
   query 查询参数的对象形式{a:`1`}
   queryString 查询参数的字符串形式
   pathWithQuery 带查询参数的路劲
   request 请求对象
   response 响应对象
   ```
# HTTP 基础概念
## 请求
- 请求动词 路径+查询参数 协议名/版本
- host： 域名或IP
- Accept: text/html
- Content-Type: 请求体的格式
- 回车
- 请求体
```
    请求行、请求头、请求体
    请求动词 GET/POST
```
  
## 响应
- 协议名/版本 状态码 状态字符串
- Content-Type 响应体的格式
- 回车
- 响应体
  ```
    三部分: 状态行、状态头、状应体
    常见的状态码：200、404
  ```

## 用curl构造请求
```
curl -v http://127.0.0.1:8888
```

1. 设置请求动词```-X POST```
2. 设置路径和查询参数 ``` 在url后面加 ```
3. 设置请求头 ```-H'Name:Value' / --header'Name:Value'```
4. 设置请求体 ```-d'内容' / --data'内容'```
   

## Node.js 请求响应
### 请求
- 读取请求动词 request.method
- 读取路径     request.url /path   /query
- 读取请求头   request.headers['Accept']

### 响应
- 设置响应状态码 request.statusCode = 200
- 设置响应头     response.setHeader('Content-Type','text/html')
- 设置响应体     response.write('内容') 可追加
  