# 前后端分离之AJAX



#### AXA使用XMLHttpRequest对象与服务器通信，就是使用JS发送和接收数据。

- AJAX是浏览器上的功能
- window上的XMLHttpRequest构造函数
- JS是通过它发请求，收响应



### 步骤

- 创建HttpRequest对象

  ```js
  httpRequest = new XMLHttpRequest();
  ```

- 调用对象的open方法

  ```js
  httpRequest.open('GET', 'test.html');// get方法和路径
  ```

- 监听对象的onload/onreadystatechange&onerror事件

  ```js
  httpRequest.onreadystatechange = alertContents;
  ```

- 调用对象的send方法

  ```js
  httpRequest.send();
  ```

  

- [具体例子参考MDN](https://developer.mozilla.org/zh-CN/docs/Web/Guide/AJAX/Getting_Started#step_3_%E2%80%93_%E4%B8%80%E4%B8%AA%E7%AE%80%E5%8D%95%E7%9A%84%E4%BE%8B%E5%AD%90)



#### 参考链接：

1. [AXAJ  MDN](https://developer.mozilla.org/zh-CN/docs/Web/Guide/AJAX/Getting_Started)
2. [XMLHttpRequest  MDN](https://developer.mozilla.org/en-US/DOM/XMLHttpRequest)
3. [XML MDN](https://developer.mozilla.org/zh-CN/docs/Web/XML/XML_Introduction)
4. [JSON中文官网](http://json.org/json-zh.html)

