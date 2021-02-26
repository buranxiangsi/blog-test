# 1. CSS概念
层叠样式表 (Cascading Style Sheets，缩写为 CSS），是一种 样式表 语言，用来描述 HTML 或 XML（包括如 SVG、MathML、XHTML 之类的 XML 分支语言）文档的呈现。

# 2. 语法
css语法1：选择器+声明（属性：属性值）

```
    Selector {
        Properties: Property value;
    }

    selector:选择器
    Properties:属性
    Property value：属性值

```
css语法2：@语法
```html

    @charset:"utf-8"

    @import url(xxx.css)

    @media(min-width:100px)and(max-width:200px){
    语法1
    }
```
# 调试法
1. border=js中log调试法
2. 有bug时在上下行添加border
   ```css
   border: 1px solid red;
   ```
   
# 文档流
1. 脱离文档流：float/position：absolute/fixed
2. margin合并
   1. 左右不重叠，上下重叠
   2. 父子/兄弟合并
      1. 父子合并阻止方法
         1. padding/block
         2. overflow:hidden
         3. display:flex;
      2. 兄弟合并符合预期，阻止合并的方法：inline-block

# 盒模型（CSS basic box model）
1. html标签都是盒子，一层一层包裹。
2. 由margin，border，padding，content组成
3. box-sizing：
   1. content-box 标准盒模型，W3C标准
    ```html
    <div class="content-box">content box</div>
    <div class="border-box">content box</div>
    
    ```
    ```CSS
    
    /*width=content*/

    .content-box{
        box-sizing: content-box;
        width: 100px;
        height: 50px;
        padding: 10px;
        border: 5px solid red;
        margin: 15px;
    }
    ```
   1. border-box IE盒模型，<b>推荐使用</b>
    ```css
   /*width=content+padding+border*/

   .border-box{
       box-sizing: border-box;
       width: 100px;
       height: 50px;
       padding: 10px;
       border: 5px solid red;
       margin: 15px;
   }
    ```

参考文档
1. [盒模型 MDN](https://developer.mozilla.org/zh-CN/docs/Learn/CSS/Building_blocks/The_box_model)
2. [盒模型 知乎](https://zhuanlan.zhihu.com/p/110617108)