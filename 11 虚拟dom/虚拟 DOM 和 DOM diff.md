#### 虚拟 DOM 是什么

一个能代表DOM树的对象，通常含有标签名、标签上的属性、事件监听和子元素们，以及其他属性。

它在Vue和React上的表现形式：

```js
//Vue
const vNode = {
    tag: "div", //标签名 or 组件名
    data:{
        className: "red" //标签属性
        on: {
        click: ()=>{}//事件
        }
	},
    children: [ //子元素
            {type: 'span',...},
            {type: 'span',...}
        ],          
}

//React
const vNode = {
    key: null,
    props:{
        children: [ //子元素
            {type: 'span',...},
            {type: 'span',...}
        ],
        className: "red" //标签属性
        onClick: ()=>{} //事件
    },
    ref: null,
    type: "div", //标签名 or 组件名
}
```

##### 创建虚拟DOM   `React.createElement`

一开始

```js
createElement('div', {className:'red', onclick:()=>{}},[
    createElement('span', {}, 'span1'),
    createElement('span', {}, 'span2')
])
//vue 在render函数里得到h
h('div', {
    class: 'red',
    on:{
        click: () =>{}
    },
},[h('span',{},'span1'),h('span',{},'span1')])
```

React JSX 简化虚拟DOM

```html
<div className="red" onClick="{()=>{}}">
	<span>span1</span>
    <span>span1</span>
</div>
```

现在

```html
<!--VUE-->

<div class="red" @click="fn">
    <span>span1</span>
    <span>span1</span>
</div>

Vue通过vue-loader转为 h 形式

<!--React -->
<div className="red" onCilck={fn}>
    <span>span1</span>
    <span>span1</span>
</div>

React 通过babel转为createElement形式
```

#### 虚拟 DOM 的优点

1. 减少DOM操作
   - 虚拟DOM可以将多次操作合并为一次操作，减少次数
     - 添加1000个节点，却一个一个操作的时候
   - 虚拟DOM借助DOM diff可以把多余的操作省掉，减少范围
     - 你添加1000个节点，但只有10个是新增的时候。
2. 跨平台
   - 虚拟DOM可以变成DOM
   - 小程序
   - IOS应用
   - 安卓应用
   - 因为虚拟DOM本质上是一个JS对象

#### 虚拟 DOM 的缺点

- 虚拟DOM的对比算法。
- 需要额外的创建函数，如createElement或h，但可以通过JSX来简化成XML写法

#### DOM diff 是什么

- 是一个函数 patch

- patches = patch(oldVnode, newVNode)

- patches 运行的DOM操作

- ```
  [
    {type: 'INSERT', vNode: ... },
    {type: 'TEXT',  vNode: ... },
    {type: 'PROPS', propsPatch: [...]}
  ]
  ```

- 新旧DOM逐层对比

- 节点类型是组件看Component diff, 是组件看Element diff

- 类型不同删除旧的，替换成新的，类型相同而属性不同只更新属性。

#### DOM diff 的优点

- 保持完整的结构，有利于提升性能

#### DOM diff 的问题（key）

- 同级节点对比存在bug
- DOM diff 中的key问题



#### 总结

开发时使用`render`函数创建虚拟DOM，当节点/属性更新时，再次用`render`创建新的虚拟DOM，而`diff`是对比新旧虚拟DOM来更新。



参考链接

1. [React 源码剖析系列 － 不可思议的 react diff](https://zhuanlan.zhihu.com/p/20346379)
2. [React 虚拟 Dom 和 diff 算法](https://juejin.cn/post/6844903529161850893)

