# API 之 实例property

### $data

- type:Object
- 组件实例正在侦听的数据对象，组件实例代理了对其data对象property的访问

### $props

- type:Object
- 当前组件接收的props对象

### $el

- type:any
- 组件实例正在使用的DOM元素，追踪组件在DOM的位置，使用模板引用直接访问DOM元素

### $options

- type:Object
- 当前组件实例的初始化选项，在选项中包含自定义property时使用

### $parent

- type: Vue instance
- 可读
- 父实例

### $root

- type: Vue instance
- 可读
- 当前组件树的根组件实例

### $slots

- type:{[name:string]:(…args:any[])=>Array(VNODE)|undefined}
- 可读
- 以编程方式访问通过插槽分发的内容

### $refs

- type:Object
- 可读
- 持有注册过`ref `attribute的所有DOM元素和组件实例
- 参考
- [slot组件](https://v3.cn.vuejs.org/api/built-in-components.html#slot)
- [通过插槽分发内容](https://v3.cn.vuejs.org/guide/component-basics.html#通过插槽分发内容)
- [渲染函数 - 插槽](https://v3.cn.vuejs.org/guide/render-function.html#插槽)

## [#](https://v3.cn.vuejs.org/api/instance-properties.html#refs)$refs

### $attrs

- type: Object
- 可读
- 包含父作用域不为组件props或自定义事件的attribute绑定和事件



# 插槽 扩展or基础

内容分发的API

```html
<!--使用-->
<todo-button>
  Add todo
</todo-button>

<!--Button组件模板-->
<button class="btn-primary">
  <slot></slot>
</button>

<!--渲染-->
<button class="btn-primary">
  Add todo
</button>
```

插槽可以包含任何模板代码： HTML，组件

### 渲染作用域

插槽可以访问与模板其余部分相同的实例 property，不能访问`todo-button` 的作用域。

**规则**：父模板的内容在父级作用域中编译，子模板的内容在子作用域中编译。

### 备用内容

为插槽指定备用内容，其内容会在没有提供内视的时候被渲染。

### 具名插槽

需要多个插槽时,`<slot>`有一个特殊的attribute:name，给不同的插槽分配独立ID

```html
<div class="container">
    <header>
        <slot name="header"></slot>
    </header>
    <main>
        <slot></slot>
    </main>
    <footer>
        <slot name="footer"></slot>
    </footer>
</div>
```

在template元素上使用v-slot指令

```html
<base-layout>
    <template v-slot:header>
        <h1>Here might be a page title</h1>
    </template>
    
     <template v-slot:default>
        <p>A paragraph for the main content.</p>
        <p>And another one.</p>
     </template>

      <template v-slot:footer>
        <p>Here's some contact info</p>
      </template>
</base-layout>
```

渲染结果

```html
<div class="container">
  <header>
    <h1>Here might be a page title</h1>
  </header>
  <main>
    <p>A paragraph for the main content.</p>
    <p>And another one.</p>
  </main>
  <footer>
    <p>Here's some contact info</p>
  </footer>
</div>
```



### 作用域插槽

让插槽访问子组件才有的数据

```js
app.component('todo-list',{
    data(){
        return{
            items:['Feed a cat','Buy milk']
        }
    },
    template:`
       <ul>
         <li v-for="(item, index) in items">{{item}}</li>
       </ul>
     `
})
```

把`{{item}}`  替换为 `<slot>` 以便在父组件上对其定义,使item在父级提供的插槽内容上可用，可以添加一个`<slot>`元素并将其作为一个attribute绑定。

```html
<ul>
    <li v-for="(item.index) in items">
      <slot :item="item"></slot>
    </li>
</ul>
```

绑定在 `<slot>` 元素上的attribute 被成为插槽prop,现在，在父级作用域中，可以使用带值的 `v-slot` 定义我们提供的插槽prop的名字

```html
<todo-list>
    <template  v-slot:defaut="slotProps">
        <i class="fas fa-check"></i>
        <span class="green">{{slotProps.item}}</span>
    </template>
</todo-list>
```



### 独占默认插槽的缩写语法

在上诉情况下，当被提供的内容只有默认插槽时，组件的标签才可以被当作插槽的模板来使用。

```html
<todo-list v-slot:default="slotProps">
  <i class="fas fa-check"></i>
  <span class="green">{{ slotProps.item }}</span>
</todo-list>
更简便的写法：
<todo-list v-slot="slotProps">
  <i class="fas fa-check"></i>
  <span class="green">{{ slotProps.item }}</span>
</todo-list>
```

默认插槽的缩写语法不能和具名插槽混用。多个插槽时，使用完整的template语法。

### 解构插槽prop

```html
<todo-list v-slot="{item}">
    <i class="fas fa-check"></i>
    <span class="green">{{ item }}</span>
</todo-list>
```

重命名

```html
<todo-list v-slot="{item:todo}">
    <i class="fas fa-check"></i>
    <span class="green">{{ todo }}</span>
</todo-list>
```

定义备用内容

```html
<todo-list v-slot="{item='Placeholder'}">
    <i class="fas fa-check"></i>
    <span class="green">{{ item }}</span>
</todo-list>
```

### 动态插槽名

动态指令参数也可以用在`v-slot`上

```html
<base-layout>
  <template v-slot:[dynamicSlotName]>
    ...
  </template>
</base-layout>
```

### 具名插槽的缩写

- `v-slot:header` 缩写为 `#header`
- 该缩写有参数时才有用