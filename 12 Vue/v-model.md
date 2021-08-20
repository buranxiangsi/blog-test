## v-model

v-model 默认使用 `modelValue` 作为  prop 和  `update:modelValue` 作为事件。

- emits   在组件上定义发出的事件
- vue3 同一组件可使用多个v-model 进行双向绑定
- 自定义 v-model 修饰符

试用代码的在线网址:

- [CodeSandbox](https://codesandbox.io/s/agitated-perlman-sj6jo?file=/src/App.vue)
- [Codepen](https://codepen.io/team/Vue/pen/GRoPPrM) *

### 组件中使用

#### 1

```vue
<Input v-model="input"/>
<!--是以下的简写-->
<Input
  :modelValue="input"
  @update:modelValue="input = $event"
/>
```

```vue
<template>
   <!--
    vue3 
    v-model 的  prop attrs   vlaue 变更为 modelValue
                event        input 变更为 update:modelValue
    -->
   <input :value="modelValue" @input="$emit('update:modelValue',$event.target.value)"
</template>

<script>
export default{
    name: 'Input',
    props:{
        modelValue:{
            type:String
        }
    },
    emits:['update:modelValue']
   }
}

</script>
```

#### 2

```vue
<template>
   <!--
    vue3 
    v-model 的 prop attrs   vlaue 变更为 modelValue

    -->
   <input v-model="value"/>
</template>

<script>
export default{
    name: 'Input',
    props:{
        modelValue:{
            type:String
        }
    },
    emits:['update:modelValue'],
    computed:{
        value:{
            get(){
                return this.modelValue
            },
            set(value){
                this.$emit('update:modelValue',value)
            }
        }
    }
   }
    
}

</script>
```

### 自定义

v-model 参数，通过向v-model传递 参数 修改 默认名称(modelValue, update:mdoelValue)

```vue
<myComponent v-model:title="title"></myComponent>
<!--是以下的简写-->
<myComponent :title="title" @update:title="title = $event" ></myComponent>
```

```vue
myComponent.vue
<template>
  <input type="text" :value="title" @input="$emit('update:title', $event.target.value)" />
</template>
<script>
export default {
  props: {title:String},
  emits: ["update:title"],
};
</script>
```

