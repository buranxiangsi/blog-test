# jQuery

> 它的基本设计思想和主要用法：选择某个网页元素，然后对其进行某种操作。

1. [jQuery 如何获取元素](#jQuery 如何获取元素)
2. [jQuery 的链式操作是怎样的](#jQuery 的链式操作是怎样的)
3. [jQuery 如何创建元素](#jQuery 如何创建元素)
4. [jQuery 如何移动元素](#jQuery 如何移动元素)
5. [jQuery 如何修改元素的属性](#jQuery 如何修改元素的属性)

### jQuery 如何获取元素

jQuery将一个选择表达式放进构造函数jQuery()，简写为$()，然后得到被选中得元素。（返回对象）

**选择表达式**：

1. cssx选择器

   ```js
   $(document) //选择整个文本对象
   $('myId')   //选择class为myID得div元素
   $('div.myClass')//选择class为myClass得div元素
   $('input[name=first]')//选择name属性等于first的input元素
   ```

   

2. jquery特有得表达式

   ```js
   $('a:first') //选择网页中第一个a元素
   $('tr:odd')//选择表格的奇数行
   $('#myForm :input') //选择表单中的input元素
   $('input[name=first]') //选择name属性等于first的input元素
   ```

3. 提供各种强大的过滤器，对结果进行筛选，缩小选择结果

   ```js
   　$('div').has('p'); // 选择包含p元素的div元素
   
   　$('div').not('.myClass'); //选择class不等于myClass的div元素
   
   　$('div').filter('.myClass'); //选择class等于myClass的div元素
   
   　$('div').first(); //选择第1个div元素
   
   　$('div').eq(5); //选择第6个div元素
   ```

   

### jQuery 的链式操作是怎样的

**选中网页元素，对它进行一系列操作，并且所有操作可以链接在一起，以链条的形式写出来，比如下面这条代码**

```js
$('div').find('h3').eq(2).html('Hello')
```

**等价于**

```js
$('div')//找到div元素
    .find('h3')//选择其中h3元素
	.eq(2) //选择第3个h3元素
    .html(hello) //将它的内容改为Hello
```



### jQuery 如何创建元素

创建：把新元素传入jquery

```js
$('<p>Hello</p>')

$('<li class="new">new list item</li>')

$('ul').append('<li>list item</li>')
```



### jQuery 如何移动元素

jQuery 提供两组方法，来操作元素在网页中的位置移动。一组方法是直接移动该元素，另一组方法是移动其他元素，使得目标元素达到我们想要的位置。

 1. .insertAfter()

    ```js
    $('div').insertAfter($('p'))  //把div元素移动到p元素后面  返回div元素
    ```

2. .after()

   ```js
   $('p').after($('div'))   //把p元素加到div元素的前面 //返回p元素
   ```

3.  四对操作方法

   ```js
   .insertAfter()和.after()  //在现存元素的外部，从后面插入元素
   
   .insertBefore()和.before()//在现存元素的外部，从前面插入元素
   
   .appendTo()和.append()    //在现存元素的内部，从后面插入元素
   
   .prependTo()和.prepend()  //在现存元素的内部，从前面插入元素　
   
   ```

   4. 提供各种强大的过滤器，对结果进行筛选，缩小选择结果

   ```js
   　$('div').has('p'); // 选择包含p元素的div元素
   
   　$('div').not('.myClass'); //选择class不等于myClass的div元素
   
   　$('div').filter('.myClass'); //选择class等于myClass的div元素
   
   　$('div').first(); //选择第1个div元素
   
   　$('div').eq(5); //选择第6个div元素
   
   //从结果集移动到附件相关的元素
   
   $('div').next('p'); //选择div元素后面的第一个p元素
   
   $('div').parent(); //选择div元素的父元素
   
   $('div').closest('form'); //选择离div最近的那个form父元素
   
   $('div').children(); //选择div的所有子元素
   
   $('div').siblings(); //选择div的同级元素
   
   ```

   

### jQuery 如何修改元素的属性

可以使用同一个函数，完成取值和修改属性（赋值）

```
$('h1').html() //html没有参数，表示取出h1的值
$('h1').html('Hello') //html有参数，表示对h1进行赋值
```

