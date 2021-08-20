### v-model

自定义

```vue
<Input v-model="value"/>
<!--等价于-->
<Input :value="value" @input="value = $event" />
```

```vue
<template>
   <input :value="value" @input="onInput" />
   <!--等价于，methods可删掉-->
   <input :value="value" @input="$emit('input',$event.target.value)"
</template>

<script>
export default{
    name: 'Input',
    props:{
        value:{
            type:String
        }
    },
    //第二个时可以删除。
    methods:{
        onInput(e){
            const value = e.target.value
            this.$emit('input', value)
        }
    }
}

</script>
```

