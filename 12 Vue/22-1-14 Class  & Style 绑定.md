# Class  & Style 绑定

## 绑定HTML Class

##### 对象语法

```html
<div :class="{active:isActive}"></div>
<!--active的class是否存在取决 isActive的truthiness (真值)-->
```

注：[Truthy](https://developer.mozilla.org/zh-CN/docs/Glossary/Truthy)(真值)

- 在js中，真值指在布尔值上下文中，转换后的值为真的值
- 除 假值 `false` `0` `-0` `0n` `“”` `null` `undefined` `NAN` 以外

###### 动态切换class

```html
<div class="static" 
     :class="{active: isActive, 'text-danger': hasError}">
</div>
<!--普通class和动态class可以共存-->
```

```js
data(){
    return {
        isActive:true,
        hasError:false
    }
}
```

渲染结果

```html
<div class="static active"></div>
```

###### 数据对象与模板分开

```html
<div :class="classObject"></div>
```

```js
data(){
    return{
        classObject:{
            active:true,
            'text-danger':false
        }
    }
}
```

###### 绑定一个返回对象的计算属性

```html
<div :class="classObject"></div>
```

```js
data(){
    return{
        isActive:true,
        error:null
    }
},
computed:{
    classObject(){
        return{
            active:this.isActive && !this.error,
            'text-danger': this.error && this.error.type === "fatal"
        }
    }
}
```

##### 数组语法

```html
<div :class="[activeClass, errorClass]"></div>
```

```js
data(){
    return {
        activeClass:'active',
        errorClass:'text-danger'
    }
}
```

渲染结果

```html
<div class="active text-danger"></div>
```

​	切换class

```html
<div :class="[isActive ? activeClass : '', errorClass]">
    <!--始终添加errorClass， isActive为真值时添加-->
</div>

<div :class="[{ active: isActive }, errorClass]"></div>
```

#### 组件上使用

声明组件

```js
const app = Vue.createApp({})
app.component('myComponent',{
    template:`<p class="foo bar">Hi!</p>`
})
```

使用时添加class

```html
<div id="app">
    <myComponent class="baz boo"></myComponent>
</div>
```

渲染结果

```html
<p class="foo bar baz boo">Hi</p>
```

带数据绑定class

```html
<myComponent :class="{ active:isActive}"></myComponent>
<!--isActive 为真值，Html 渲染结果-->
<p class="foo bar active">Hi</p>
```

组件有多个根元素，定义哪部分接收这个class 使用 $attrs 组件property执行此操作

```html
<div id="app">
    <myComponent class="baz"></myComponent>
</div>
```

```js
const app = Vue.createApp({})

app.component('myComponent', {
    templete:`
     <p :class="$attrs.class">Hi</p>
     <span>This is child component</span>
     `
})
```

### `$attrs` 扩展

非`prop`的`attribute`是指传向一个组件，但是，该组件并没有相应的 props 或`emits`定义的`attribute`，比如：`class` `style`  `id`的attribute

1. Attribute 继承 ：当组件返回单个根节点时，非prop的attribute 将自动添加到根节点的attribute中。

```js
app.component('date-picker',{
    template:`<div class="date-picker">
		<input type="datetime-local" />
    </div>`
})

```

通过 `data-status` attribute 定义 `date-picker`组件的状态，将应用于根节点——`div.date-picker`

```html

<!--具有非prop的attribute的date-picker组件-->
<data-picker data-status="activated"></data-picker>

<!--渲染后-->
<div class="data-picker" data-status="activated">
    <input type="datetime-local"/>
</div>
```

事件监听器同样如此。

```html
<date-picker @change="submitChange"></date-picker>
```

```js
app.component('date-picker', {
    created(){
        console.log(this.$attrs)// $attrs = {onChange:()=>{}}
    }
})
```

当一个具有change事件的html元素作为date-picket 的根元素时。

```js
app.component('date-picker',{
    templete:`
     <select>
      <option value="1">1</option>
      <option value="2">2</option>
      <option value="3">3</option>
     </select>
  `
})
change事件监听器从父组件传递到子组件，它在原生select的change事件上触发，无需显式从date-picker发出事件
```

显式发出事件

```html
<div id="date-picker" class="demo">
  <date-picker @change="showChange"></date-picker>
</div>
```

```js
const app = Vue.createApp({
  methods: {
    showChange(event) {
      console.log(event.target.value) // 将打印所选选项的值
    }
  }
})
```



2. 禁用 Attribute 继承，组件选项中设置`inheritAttrs:false`, 使用组件的 `$attrs` property 将attribute应用到其他元素上

   property包含组件`props `  和 `emits` property中未包含的所有属性，例如 `class ` `style` `v-on` 监听器等。

```js
app.component('date-picker',{
    inheritAttrs:false,
    template:`<div class="date-picker">
		<input type="datetime-local" v-bind="$attrs" />
    </div>`
})
```

`data-status ` attribute 将应用于`input`元素

```html
<!-- date-picker 组件使用非 prop 的 attribute -->
<data-picker data-status="activated"></data-picker>

<!--渲染后-->
<div class="data-picker">
    <input type="datetime-local"  data-status="activated"/>
</div>
```

3. 多个根节点上的 Attribute 继承

多个根节点组件需要显式绑定 `&attrs`

```html
<component id="component" @click="cangeValue"></component>
```

```js
// 这将发出警告
app.component('component', {
    templete:`
    <header>...</header>
    <main>...</main>
    <footer>...</footer>
    `
})

// 没有警告，$attrs 被传递到 <main> 元素
app.component('component', {
    templete:`
    <header>...</header>
    <main v-bind="$attrs">...</main> 
    <footer>...</footer>
    `
})
```

$attrs 应用总结

传递非props 和emits 的attribute，主要应用于禁止attribute继承，传递到非根节点的元素，以及多个根节点attribute继承上。

- 单个根节点  不禁用Attribute 继承，非prop将自动添加到根节点
- 事件监听器 $attrs 将change事件添加到子节点
- 单个根节点  禁用Attribute 继承 应用于根节点之外的元素  需绑定使用，v-bind=“$attrs”
- 多个根节点 Attribute 继承 无法自动添加，需要显式绑定到根节点之外的元素

## 绑定内联样式

#### 对象语法

`:style` js对象

```html
<div :style="{color:activeColor, fontSize: fontSize + 'px'}"></div>

直接绑定对象

<div :style="styleObject"></div>
```

```js
data(){
    return{
        activeColor:'red',
        fontSize: 30
    }
}

直接绑定对象
data(){
    return{
        styleObject:{
            color:'red',
            fontSize:'13px'
        }
    }
}
```

#### 数组语法

```html
<div :style="[baseStyles, overridingStyles]"
```

自动添加前缀。

多重值

```html
<div :style="{display:['-webkit-box' -ms-flexbox','flex']}"
 >
    浏览器不支持带前缀的flexbox，就只会渲染最后一个。
</div>
```



