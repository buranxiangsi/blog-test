# Vue3 新功能

- [组合式 API](https://v3.cn.vuejs.org/guide/composition-api-introduction.html)
    - 通过创建 Vue 组件，我们可以将界面中重复的部分连同其功能一起提取为可重用的代码段
    - setup
- [Teleport](https://v3.cn.vuejs.org/guide/teleport.html)
    - 父组件的逻辑子组件
    - 作为子组件将组件传送到父组件
    - 预防深度嵌套，拆分组件
- [片段](https://v3.cn.vuejs.org/guide/migration/fragments.html)
    - 支持组件包含多个根节点
    - 需在节点显示绑定 attribute `v-bind="$attrs"`
- [触发组件选项](https://v3.cn.vuejs.org/guide/component-custom-events.html)
    - emits 定义发出事件
- [来自 `@vue/runtime-core` 的 `createRenderer` API](https://github.com/vuejs/vue-next/tree/master/packages/runtime-core)，用于创建自定义渲染器
- [单文件组件组合式 API 语法糖 (``)](https://v3.cn.vuejs.org/api/sfc-script-setup.html)
- [单文件组件状态驱动的 CSS 变量 (`` 中的 `v-bind`)](https://v3.cn.vuejs.org/api/sfc-style.html#状态驱动的动态-css)
- [SFC `` 现在可以包含全局规则或只针对插槽内容的规则](https://github.com/vuejs/rfcs/blob/master/active-rfcs/0023-scoped-styles-changes.md)
- [Suspense](https://v3.cn.vuejs.org/guide/migration/suspense.html) 实验性



# 非兼容变更

## 全局API

createApp

```js
import { createApp } from 'vue'

const app = createApp({})

//cdn
const { createApp } = Vue

const app = createApp({})
```

- [全局和内部 API 已经被重构为支持 tree-shake](https://v3.cn.vuejs.org/guide/migration/global-api-treeshaking.html)

## 模板指令

- [组件上 `v-model` 用法已更改，以替换 `v-bind.sync`](https://v3.cn.vuejs.org/guide/migration/v-model.html)
    - prop:`value modelValue`
    - input: `update:modelValue`
    - `:title.sync='pagetitle'` => `v-model:title='pagetitle'`
- `<template v-for>` 和 `v-for` 节点上的key用法更改
- [在同一元素上使用的 `v-if` 和 `v-for` 优先级已更改](https://v3.cn.vuejs.org/guide/migration/v-if-v-for.html)
- [`v-bind="object"` 现在排序敏感](https://v3.cn.vuejs.org/guide/migration/v-bind.html)
- [`v-on:event.native` 修饰符已移除](https://v3.cn.vuejs.org/guide/migration/v-on-native-modifier-removed.html)
- [`v-for` 中的 `ref` 不再注册 ref 数组](https://v3.cn.vuejs.org/guide/migration/array-refs.html)

### 组件

- [只能使用普通函数创建函数式组件](https://v3.cn.vuejs.org/guide/migration/functional-components.html)
- [`functional` attribute 在单文件组件 (SFC) 的 `
- [异步组件现在需要使用 `defineAsyncComponent` 方法来创建](https://v3.cn.vuejs.org/guide/migration/async-components.html)
- [组件事件现在需要在 `emits` 选项中声明](https://v3.cn.vuejs.org/guide/migration/emits-option.html)

### 渲染函数

- [渲染函数 API 更改](https://v3.cn.vuejs.org/guide/migration/render-function-api.html)
- [`$scopedSlots` property 已移除，所有插槽都通过 `$slots` 作为函数暴露](https://v3.cn.vuejs.org/guide/migration/slots-unification.html)
- [`$listeners` 被移除或整合到 `$attrs`](https://v3.cn.vuejs.org/guide/migration/listeners-removed)
- [`$attrs` 现在包含 `class` 和 `style` attribute](https://v3.cn.vuejs.org/guide/migration/attrs-includes-class-style.html)

### 自定义元素

- [自定义元素检测现在在模板编译时执行](https://v3.cn.vuejs.org/guide/migration/custom-elements-interop.html)
- [特殊的 `is` attribute 的使用被严格限制在被保留的 `` 标签中](https://v3.cn.vuejs.org/guide/migration/custom-elements-interop.html#定制内置元素)

### 其他小改变

- `destroyed` 生命周期选项被重命名为 `unmounted`
- `beforeDestroy` 生命周期选项被重命名为 `beforeUnmount`
- [`default` prop 工厂函数不再可以访问 `this` 上下文](https://v3.cn.vuejs.org/guide/migration/props-default-this.html)
- [自定义指令的 API 已更改为与组件生命周期一致，且 `binding.expression` 已移除](https://v3.cn.vuejs.org/guide/migration/custom-directives.html)
- [`data` 选项应始终被声明为一个函数](https://v3.cn.vuejs.org/guide/migration/data-option.html)
- [来自 mixin 的 `data` 选项现在为浅合并](https://v3.cn.vuejs.org/guide/migration/data-option.html#mixin-合并行为变更)
- [Attribute 强制策略已更改](https://v3.cn.vuejs.org/guide/migration/attribute-coercion.html)
- [一些过渡的 class 被重命名](https://v3.cn.vuejs.org/guide/migration/transition.html)
- [`` 不再默认渲染包裹元素](https://v3.cn.vuejs.org/guide/migration/transition-group.html)
- [当侦听一个数组时，只有当数组被替换时，回调才会触发，如果需要在变更时触发，则必须指定 `deep` 选项](https://v3.cn.vuejs.org/guide/migration/watch.html)
- 没有特殊指令的标记 (`v-if/else-if/else`、`v-for` 或 `v-slot`) 的 `<template>` 现在被视为普通元素，并将渲染为原生的 `<template>` 元素，而不是渲染其内部内容。
- [已挂载的应用不会取代它所挂载的元素](https://v3.cn.vuejs.org/guide/migration/mount-changes.html)
- [生命周期的 `hook:` 事件前缀改为 `vnode-`](https://v3.cn.vuejs.org/guide/migration/vnode-lifecycle-events.html)

### [#](https://v3.cn.vuejs.org/guide/migration/introduction.html#被移除的-api)被移除的 API

- [`keyCode` 作为 `v-on` 修饰符的支持](https://v3.cn.vuejs.org/guide/migration/keycode-modifiers.html)
- [$on、$off 和 $once 实例方法](https://v3.cn.vuejs.org/guide/migration/events-api.html)
- [过滤器 (filter)](https://v3.cn.vuejs.org/guide/migration/filters.html)
- [内联模板 attribute](https://v3.cn.vuejs.org/guide/migration/inline-template-attribute.html)
- [`$children` 实例 property](https://v3.cn.vuejs.org/guide/migration/children.html)
- [`propsData` 选项](https://v3.cn.vuejs.org/guide/migration/props-data.html)
- `$destroy` 实例方法。用户不应再手动管理单个 Vue 组件的生命周期。
- 全局函数 `set` 和 `delete` 以及实例方法 `$set` 和 `$delete`。基于代理的变化检测已经不再需要它们了。

## [#](https://v3.cn.vuejs.org/guide/migration/introduction.html#官方的支持库)官方的支持库