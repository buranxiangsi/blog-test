#### js通过document(Document Object Model)操作网页

#### 获取元素/标签

```js
window.idxxx/idxxx
//兼容IE
document.getElementById('idxxx')

document.getElementsByTabName('id')[0]

document.getElementsByClassName('red')[0]
//工作中使用
document.querySelector('#idxxx')

document.querySelectorAll('.red')[0]

```



#### 获取特定元素

```js
//HTML元素
document.documentElement
//head元素
document.head
//body
document.body
//窗口
window
//all
document.all //第六个falsy值

//看原型链
console.dir(div1)

```

#### [节点  元素](https://developer.mozilla.org/zh-CN/docs/Web/API/Node/nodeType)

- x.nodeType得到1个数字

- 1 表示元素 Element 也叫标签Tag

- 2 表示文本Text

- ```js
  var type = node.nodeType;//语法
  ```

##### 增

```js
//创建一个标签节点
let div1 = document.createElement('div')
document.createElement('style')
document.createElement('script')
document.createElement('li')

//创建一个文本节点
text1 = document.createTextNode('Hi')

//在标签里面插入文本
div1.appendChild(text1)
div1.innerText='Hi'
div1.textContent='Hi'


```

##### 删

```js
//旧方法
parentNode.childChild(childNode)

//新方法
childNode.remove()
```

##### 改

```js
//写标准属性
//改class
div.className = 'red blue'
div.classList.add('red')

//style
div.style='width: 100px; color: blue;'
div.style.width='200px'
//大小写
div.style.backgroundColor='white'
//data-*属性
div.dataset.x = 'xxx'

//都标准属性
div.classList/ a.href
div.getAttribute('class')
a.getAttribute('href')


//改事件处理函树
div.onclick //默认为null
//改为函数fn 调用fn.call(div,event) div会被当作this，event则包含了点击时间的所有信息
div.addEventListener //div.onclick的升级版


//改内容
//文本
div.innerText = 'xxx'
div.textContent= 'xxx'
//html
div.innerHtml = '<strong>Hi</strong>'
//改标签
div.innerHtml = '' //先清空
div.appendChild(div2) //再加内容

//改父元素
newParent.appendChild(div)

```

##### 查

```js
//查父元素
node.parentNode
node.parentElement
//查祖父元素
node.parentNode.parentNode
//查子代
node.ChildNOdes
node.children
//查兄弟姐妹
node.parentNOde.childNodes //排除自己
node.parentNode.children //排除自己

//查老大
node.firstChild
//查老幺
node.lastChild
//查上一个哥哥/姐姐
node.previousSibling
//查下一个弟弟/妹妹
node.nextSibling

```

