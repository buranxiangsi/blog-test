CSS 伪元素和伪类

伪元素：是一个附加至选择器末的关键词，允许你对被选择元素的特定部分修改样式。——MDN的说法。

伪类：添加到选择器的关键字，指定要选择的元素的特殊状态。可以在一个选择器中同时一起写多个伪类。——MDN的说法。

- 常用的伪类以及写法  [MDN](https://developer.mozilla.org/zh-CN/docs/Web/CSS/Pseudo-classes)

```css
:active
:focus
:link
:visited
:first-child
:lang
```

- 常用的伪元素及写法 [MDN]()

```css
::after
::before
::first-letter 选择首行首字母
::first-line  选择首行
```

CSS3 区分了伪元素和伪类的写法，但因为兼容性，伪元素也可以写一个冒号。

**伪元素与伪类的对比，伪元素和伪类与元素和类的对比**

```html
<div class="box1">
   <p>使用伪类和伪元素</p>
   <ul>
    <li>第一个li</li>
    <li>第二个li</li>
  </ul>
  </div>

  <div class="box2">
    <p>不使用伪类和伪元素达成以上效果</p>
   <ul>
     <li class="red"><span>第</span>一个li</li>
     <li><span>第</span>二个li</li>
  </ul>
  </div>
```

css

```css
li{
  margin: 20px;
}
.box1 li:first-child{
  color:red;
}
.box1 li::first-letter{
  background: green;
}


.box2 .red{color:red;}
.box2 li span {background:green;}
```

结果

![结果对比](C:\Users\luo\Desktop\1.png)



总结：

- 伪类和伪元素都需要选择器，都用来添加特殊效果
- 伪类是添加一个实际的类达成效果
- 伪元素是添加一个实际的元素达成的效果

参考链接：[详解 CSS 属性 - 伪类和伪元素的区别 - SegmentFault 思否](https://segmentfault.com/a/1190000000484493)

