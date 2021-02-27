# CSS布局(CSS layout)

1. 布局 把页面分成一块一块，按左中右、上中下等排列。
2. 分类
   1. 固定宽度布局
   2. 不固定宽度布局，文档流原理
   3. 响应式布局（pc固定，手机不固定)
3. 布局方式
   1. 兼容IE9 float布局,固定宽度，不响应
   2. 不兼容IE9，不兼容最新浏览器，flex布局
   3. 不兼容IE9， 兼容最新浏览器， grid布局
   <i>1,2必要时使用负margin</i>

## 1. float 
   1. 父元素加.chearfix
   ```css
        .clearfix::after{
            content:"";
            display:block;
            clear: both;

        }

        /*float 脱离文档流，父元素没有宽度，加以上代码保持宽度*/
   ```
   2. 子元素
   ```CSS
        div {
            float: left/right;
            width: 100px;
        }
   ```
## 2. flex布局
1. container items
   ```css
        .container{
            display: flex;
            flex-direction: row/column;
            justify-content: content/space-between;
            flex-wrap: wrap;
            align-items: center;
        }
   ```

## 3. Grid 布局
1. container items
   ```css
    .container{
        display: grid | inline-grid;
        grid-template-columns: 100px 100px 100px;
        grid-template-rows: 30px 30px 30px;
        grid-gap: 10px;
    }
   ```

# CSS 定位 position
## ```position: relative | absolute | fixed | sticky; ```
1. relative 用于位移，和absolute配合使用
2. absolute 子元素固定，祖先元素relative，相对于不是static的最近的祖先元素定位。
3. fixed 相对于视口定位，尽量不用于手机。
4. sticky 粘滞定位，在文档流中滚动，于顶部停滞。兼容性差，用于导航。
   
## 层叠上下文 The stacking context
1. z-index 每个层叠上下文你是一个新的作用域，同一作用域的z-index可比较。
2. flex
3. opacity
4. transform
   

   







<ul>
<li>[flex游戏](https://flexboxfroggy.com/#zh-cn)</li>
<li>[grid游戏](https://cssgridgarden.com/#zh-cn)</li>
<li>[c层叠上下文](https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_Positioning/Understanding_z_index/The_stacking_context)</li>
</ul>