web app适配解决方案

- 流式布局，通过百分比定义宽度，px固定，导致有些页面元素拉长

- 固定页面宽度-超出部分留白-大屏幕手机下页面小

- 响应式做法-工作大，维护性难

- viewport进行缩放-页面元素会糊

- rem 通过根元素进行适配，能等比列适配所有屏幕，通过设置html的字体大小可以控制rem的大小

  ```html
  <button>REM-test</button>
  ```

  ```css
  html{
      font-size:20px;
  }
  button{
      width: 6rem;
      height: 3rem;
      line-height:3rem;
      font-size:1.2rem;
      display:inline-block;
      background:#06c;
      border-radius:.5rem;
      text-align:center;
  }
  ```

  

  