# HTML 常用标签
## a
1. 作用: 链接（内部，外部，邮箱/电话)
2. 属性
   1. href 包含url
      1. 网址
          1. https://google.com
          2. http://google.com
          3. //google.com
      2. 路径
         1. /a/b/c & a/b/c
         2. index.html & ./index.html 
      3.  伪协议
          1. javascript:代码;作用于点击后没有动作的标签
          2. mailto:邮箱
          3. tel:手机号
  1. target 在何处显示连接的资源
       1. _self 当前页加载
       2. _blank 新窗口打开
       3. _parent 加载到当前框架的父框架
       4. _top  加载响应进入顶层
2. download  下载
3. 3. rel=noopener  指定目标对象到链接对象的关系
## img
1. 作用：发出get请求，展示图片
2. 属性
   1. alt
   2. src
   3. height 宽高只写一个
   4. width
3. 事件
   1. onload
   2. onerror
4. 响应式
   ```CSS
   a{max-width: 100%}
   ```
5. 可替换元素replaced element
   1. 不由css控制，独立于css，只作用于位置
   2. iframe，video,embed,img
   3. 特定条件下被作为可替换元素，option，audio,canvas,object,applet.

## form
1. 作用：发送get/post请求，刷新页面
2. 属性
   1. action 处理表单提交的url
   2. method get/post提交表单
   3. autocomplete 浏览器自动补全
   4. target 提交后在哪里响应信息
### [input 参考MDN](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/input) 
1. 作用：让用户输入内容
2. 属性
   1. type
   2. name/...
3. 验证器 html5新增功能
## table
1. table
2. thead
3. tbody
4. tfoot
5. tr  行
6. td  列
7. th  表头（2个，行列开头）

## 其他标签
1. video
2. audio
3. canvas
4. svg
   
