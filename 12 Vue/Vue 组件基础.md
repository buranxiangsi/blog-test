# Vue 组件基础

## 全局注册与局部注册

```js
app.component('myComponent',{...})
                             
components:{
  Mycomponent
}
```



## Props 传递数据

通过props向子组件传递数据

组件A

```vue
<template>
  <h1>{{title}}</h1>
</template>
<script>
    export default{
        name: 'ComponentA',
        props: {
            title: String
        }
    }
</script>
```

App.vue

```vue
<template>
  <ComponentA titile='ComponentA'></ComponentA>
</template>
<script>
    import ComponentA from './ComponentA'
    export default{
        name: 'App',
        components:{
            ComponentA
        },
      
    }
</script>
```

## 监听事件

`v-on` `@` 监听子组件

```html

```

子组件调用内置 `$emit` 方法并传入事件名称来触发一个事件

```html

```



## 插槽

## 动态组件