# 前后端分离之AJAX，异步，回调，Promise



#### AXA使用XMLHttpRequest对象与服务器通信，就是使用JS发送和接收数据。

- AJAX是浏览器上的功能
- window上的XMLHttpRequest构造函数
- JS是通过它发请求，收响应



##### 步骤

- 创建HttpRequest对象

  ```js
  Request = new XMLHttpRequest();
  ```

- 调用对象的open方法

  ```js
  Request.open('GET', 'test.html');// get方法和路径
  ```

- 监听对象的onload/onreadystatechange&onerror事件

  ```js
  Request.onreadystatechange =() =>{
      //回调callback 写给别人调用的函数
  };
  ```

- 调用对象的send方法

  ```js
  Request.send();
  ```

- [具体例子参考MDN](https://developer.mozilla.org/zh-CN/docs/Web/Guide/AJAX/Getting_Started#step_3_%E2%80%93_%E4%B8%80%E4%B8%AA%E7%AE%80%E5%8D%95%E7%9A%84%E4%BE%8B%E5%AD%90)

  

#### 异步：不能直接得到结果——**以AJAX为例**

- <code>Request.send() </code>之后不能直接得到<code>response</code>

- 在<code>readyState=4</code>以后，浏览器**回**头**调**用<code>request.onreadystatechange</code>函数，才能得到<code>response</code>

- 可以尝试延迟网络，<code>console.log()</code>打出结果

- **回调** <code>callback</code>   写给别人调用的函数，比如ajax的<code>request.onreadystatechange</code>函数

- 异步和回调的关系

  - 异步任务在得到结果时通知js取结果
  - js留一个函数地址给浏览器
  - 异步任务完成时浏览器调用函数地址，同时把结果作为参数传给该函数
  - 这个函数是我写给浏览器调用的，所以是回调函数

- 区别

  - 异步任务需要用到回调函数来通知结果
  - 但回调不一定只用在异步任务里，还可以用在同步任务里
  - array,forEach(n=>console.log(n))同步回调

- 判断异步同步函数

  - 函数的返回值处于

  - [setTimeout]()
  - AJAX
  - AddEventlistener

  

封装ajax

```js
ajax = (method, url, options)=>{
    const {success,fail} = options //析构赋值,等价于以下两行
    //const success = options.success
    //const fail = options.fail
    const request = new XMLHttpRequest()
    request.open(method,url)
    request.onreadystatechange = () =>{
        if(request.readyStatechange===4){
            if(request.status < 400){
                success.call(null,request,request.response)
            }else if{
                fail.call(null, request, request.status)
            }
        }
    }
    request.send()
}

ajax('GET', '/xxx',{
    success(response){}, fail: (request, status) =>{}
})
```

#### Promise 写法 <code>return new Promise((resolve,reject)=>{})</code>

```js
ajax('GET', '/xxx')
    .then((response)=>{},(request,status)=>{})


ajax = (method, url, options)=>{
    return new Promise((resolve, reject)=>{//Promise
        const {success,fail} = options
        const request = new XMLHttpRequest()
        request.open(method,url)
        request.onreadystatechange = () =>{
            if(request.readyStatechange===4){
                if(request.status < 400){
                    resolve.call(null,request,request.response)
                }else if{
                    reject.call(null, request, request.status)
                }
            }
        }
        request.send()
        
    })
}

```

**Promise**之前的方法

```js
//方法1 回调接受2个参数
fs.readFile('/1.txt',(error, data)=>{
    if(error){
        console.log('error')
        return 
     }
    console.log(data.toString())
})

//方法2 写2个回调
ajax('get','/1.json', data=>{},error=>{})

ajax('get','/1.json',{
    success: ()=>{}, fail: ()=>{}
})
```

1.  以上方法不规范

2. 容易出现回调地狱

3. 难以进行错误处理

   

#### 参考链接：

1. [AXAJ  MDN](https://developer.mozilla.org/zh-CN/docs/Web/Guide/AJAX/Getting_Started)
2. [XMLHttpRequest  MDN](https://developer.mozilla.org/en-US/DOM/XMLHttpRequest)
3. [XML MDN](https://developer.mozilla.org/zh-CN/docs/Web/XML/XML_Introduction)
4. [JSON中文官网](http://json.org/json-zh.html)
5. [ajax库Axios](https://juejin.cn/post/6844903569745788941)
6. [Promise](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise)

