# DOM事件  7-8

- js无法操作dom

- 浏览器在window上加了一个document

- js用document操作网页

- API

- document.querySelector('#id')

- document.querySelectorAll('.red')[0]

- 兼容IE用 getElement(s)ByXXX

- 获取特定元素

- document.documentElement——html

- document.head——head

- document.body——body

- window——窗口（窗口不是元素）监听

- document.all——所有元素，第六个falsy值

- 获取的元素是对象，元素 有6层原型链

- x.nodeType **记住13**

- **1 元素 Element，标签  Tag**

- **3 文本 Text**

- 8 注释 Comment

- 9 文档  Document

- 11  文档片段 DocumentFragment

- 增删改查

- 增

- document.createElement('div|style|script|li')——标签节点

- document.createTextNode('text') ——文本节点

- div.appendChild(text,node接口) ——标签插入文本` element接口  div.innerText='text' div.textContent='text'`

- 1个元素不能出现在两个地方，除非复制一份 div.cloneNode()

- 删

- parentNode.removeChild(childNode) ——旧

- childNode.remove()——新

- 改属性

- div.className= "newdiv"——改class

- div.classList.add('newdiv')——改class

- div.style=' color:blue;'——改style

- div.style.width = '100px'——改style

- diy.style.backgroundColor = 'white' 大小写

- div.dataset.x = 'xx' 改data-* 属性

- 读属性

- div.classList / a.href

- div.getAttribute('class') /a.getAttribute('href')

- 改事件处理

- div.onclick(默认null)——升级版——div.addEventListener

- div.onclik调用方式 fn.call(div,event)

- 改内容

- div.innerText = 'xxx' ——文本内容

- div.textContent = 'xxx'

- div.innerHTML = 'xxx' ——html内容

- div.innerHTML = '' ——改标签，先清空

- div.appendChild(div) ——再加内容

- 查

- node.parentNode | node.parentElement——查父元素

- node.parentNode.parentNode——查祖元素

- node.childNodes | node.children——查子元素

- node.parentNode.childNodes | node.parentNode.children——查兄弟元素

- node.firstChild

- node.lastChild

- node.previousSibling

- node.nextSibling

- 遍历 

- DOM操作跨线程

- 跨线程通信

- 自动同步  id  dataset：{x:test}

- js——property——属性，div1的虽有属性，支持字符串，布尔等类型

- 渲染引擎——attribute——属性，渲染引擎div对应标签的属性 ，只支持字符串

- **封装**

- 库——提供给其它人的工具代码 jQuery

- API——库暴露出来的函数或属性

- 框架——当库变得很大，需要学习才能看懂，Vue React

- 对象风格，也叫命名空间风格，比如window.dom

- **原生js封装DOM库**

- **jQuery风格（链式风格）**重新封装

- 闭包 & 链式操作 （闭包访问外部变量，api操作elements）

- 返回api对象  return api

- 是一个不需要加new的构造函数

- jQuery对象代指jQuery函数构造出来的对象

- const div2 = $('.div')  <u>命名风格</u>  $div2——jQuery对象

- DOM    对象只能使用  DOM API querySelector  appendChild 

- jQuery 对象只能使用  jQuery的API find each 

- `jQuery.__proto__===jQuery.prototype` 共用属性|函数

- `const api = Object.create(jQuery.prototype)`  。创建一个对象，这个对象的`__proto__`是括号里的东西,`const api = {__proto__:}`。

- jQuery.fn =  jQuery.prototype = {}  别名  $ = jQuery

- 设计模式——漂亮且通用的代码

- 不用new的构造函数

- **重载**  $(支持多种参数)

- 用闭包隐藏细节

- **getter**/**setter**  $.div.text()可读也可写

- **别名** $.fn 是$.prototype 的

- **适配器**，针对不同浏览器使用不同代码

- 学习设计模式——总结，重写，写得好的地方抽象出来

- 学习

- 理解原理

- 做1-2个项目

- 写博客

- **<u>捕获与冒泡</u>**

- 事件捕获：从外向内找监听函数

- 事件冒泡：从内向外找监听函数

- addEventListener('click', fn, bool)  默认冒泡bool不传或为falsy，bool为true，为捕获。

- e 对象，结束就消失。

- e.target  用户操作的元素

- e.currentTarget=this 程序员监听的元素

- `div > span {文字}`

- e.target = span

- e.currentTarget = div

- 特例

- 不考虑父子同时被监听，只有一个div被监听，fn分别在捕获和冒泡阶段监听click事件，用户点击元素就是开发者监听的，此时就是——谁先监听谁先执行

- 捕获不可以取消，冒泡可以取消

- e.stopPropagation()  中断冒泡 一般用于封装某些独立组件

- 不可取消冒泡事件——scroll  event——滚动条document上

- scroll  event   查看mdn解释

- Bubbles  该事件是否冒泡  yes

- Cancelable  开发者是否可以取消冒泡  no

- 阻止scroll event，取消特定元素wheel  touchstart的默认动作

- js  `addEventListener('wheel',(e)=>{e.preventDefault()})`

- css `overflow:hidden `  直接取消滚动条 `::-webkit-scrollbar{width:0 !important}`

- 触屏 手机`addEventListener('touchstart',(e)=>{e.preventDefault()})`

- 浏览器自带事件——100多种，在mdn上查询

- 自定义事件

- 事件委托

- 省监听数（内存），监听动态元素

- 封装事件委托

- ```js
  function on(eventType, element, selector, fn){
      if(!(element instanceof Element)){
          element = document.querySelector(element)
      }
      element.addEventListener(eventType, (e)=>{
          const t = e.target
          if(t.matches(selector)){
              fn(e)
          }
      })
  }
  
  function on(eventType, element, selector, fn){
     if(!(element instanceof Element)){
          element = document.querySelector(element)
      }
      element.addEventListener(eventType, e=>{
          let el = e.target
          while(!el.matches(selector)){
              if(element===el){
                  el = null
                  break
              }
              el = el.parentNode
          }
          el && fn.call(el, e, el)
      })
      return element
  }
  
  on('click', '#div1', 'button', ()=>{
      console.log(e)
  })
  ```

- js不支持事件，js调用了dom 提供的addEventListener

- 问

- 如何当js支持事件，请手写一个事件系统

