css——flex

弹性盒子布局

元素根据窗口大小变化而自动伸长或缩短，使得整个页面格式保持不变

css 属性

- `flex` 有主轴和交叉轴，假设x为主轴()，y为交叉轴，
- `flex-directioin`确定主轴是x轴方向，y轴垂直于x轴，`flex-direction`值有`row`|`row-reverse`|`column`|`column-reverse`，
- 水平属性`justify-content`|垂直属性`align-items`受`felx-direction`影响
- flex 为`flex-basis|flex-grow|flex-shrink` 缩写，
- order指定元素顺序







- `flex`
- `flex-direction` 确定主轴方向
- `flex-wrap` 换行
- `flex-flow`  2，3缩写属性
- `flex-basis` 定义分配多于空间之前，项目占据的大小，
- `flex-grow` 子项目放大比例，默认值为零
- `flex-shrink` 子项目缩小比例，默认值为1
- `order `指定元素顺序

对齐属性

- `align-content` 行之间的距离
- `align-items` 纵向对齐Y轴
  - `flex-start`: 元素与容器的顶部对齐。
  - `flex-end`: 元素与容器的底部对齐。
  - `center`: 元素纵向居中。
  - `baseline`: 元素在容器的基线位置显示。
  - `stretch`: 元素被拉伸以填满整个容器。
- `justify-content` 横向对齐X轴
  - `flex-start`: 元素和容器的左端对齐。
  - `flex-end`: 元素和容器的右端对齐。
  - `center`: 元素在容器里居中。
  - `space-between`:元素之间保持相等的距离。
  - `space-around`:元素周围保持相等的距离。
- `align-self` 控制单个元素对齐
- `row-gap`
- `column-gap`
- `gap`
- `place-content`





[flex游戏](http://flexboxfroggy.com/#zh-cn)