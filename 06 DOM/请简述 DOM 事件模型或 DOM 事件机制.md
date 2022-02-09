### DOM 事件模型或 DOM 事件机制

DOM 事件模型(DOM Event Model)主要描述事件(Event)接口本身以及DOM节点中的事件注册接口、事件监听接口，以及展示了多种事件接口之间相互关联的较长示例。

#### 事件监听(绑定API)：

**EventTarget.addEventListener('click', fn, bool)**   

- bool为空，默认false，冒泡
- bool为true，捕获
- W3C 定义先捕获再冒泡。
- 捕获不可取消，但冒泡可以
- e.stopPropagation()中断冒泡，用于封装独立组件
- Bubbles 表示是否冒泡
- Cancelable是否支持开发者取消冒泡
- scroll不支持取消冒泡，禁用scroll，wheel/touchstart

#### 事件接听的2个阶段。

1. 事件捕获——从外向内找监听函数，从父元素传递到子元素
2. 事件冒泡——从内向外找监听函数，从子元素传递到父元素



### target 与 currentTaget

- e.target 用户操作的元素
- e.currentTaget 程序员监听的元素
- 只有一个div监听时，用户点击的元素就是开发者监听的（特例）





#### 事件委托

由于事件会在冒泡阶段向上传播到父节点，因此可以把子节点监听函数定义在父节点上，由父节点的监听函数同意处理多个子元素的的事件。

- 节省监听数，省内存
- 监听动态元素

```html
<div id="myId">
    <button>click1</button>
    <button>click2</button>
    <button>click3</button>
</div>
```

```js
myId.addEventListener('click',(e) => {
    const t = e.target
    if(t.tagName.toLowerCase()==='button'){
        console.log('你点击了button')
    }
})
```



#### 封装事件委托

```js
on('click','#myId', 'button', ()=>{
    console.log('你点击了button')
})

//封装
function on(eventType, element, selector, fn){
    if(!(element instanceof Element)){
        element = document.querySelector(element)
    }
    element.addEventListener(eventType,(e)=>{
        const t = e.target
        if(t.matches(selector)){
            fn(e)
        }
    })
}
```









