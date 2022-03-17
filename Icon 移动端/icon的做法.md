icon的各种做法

# img

设计师作图：

切图: ps -->高宽-->背景-->图标

裁剪：选中图层，图层右键复制，-->new-->图像-->裁剪，大小img--> canvas view

``<img src="/xxx"/>``

自适应宽高。只写一个就行

# background icon

如果得到的是一个png设计图, 技巧百度:如何选择想要的像素

不随着宽高改变变形

```html
<style>
    .icons > .icon.one{
        margin:5px 25px;
        border: 1px solid red;
        display: inline-block;
        width:100px;
        height:100px;/*200px*/
        background: red url(./one.png) no-repeat 0 0;
    }
    .icons > .icon.two{
        background: red url(./2.png);
    }
    .icons > .icon.three{
        background: red url(./3.png);
    }
    
</style>
<div class="icons">
    <div class="icon one">
        
    </div>
    <div class="icon two">
        
    </div>
    <div class="icon three">
        
    </div>
</div>
```

# background 合一

通过 https://css.spritegen.com/ 制作

# font icon

## iconfont--html形式

https://www.iconfont.cn/   Unicode

此网站选择 Unicode，生成@font-face 代码。

```html
<style>
@font-face{
    font-family: 'iconFontName'
}
</style>
<div style="font-family: iconFontName">
    Unicode 
</div>
```

## iconfont--css形式

```html
<style>
@font-face{
    font-family: 'iconFontName'
}
    .font::before{
        conent:'\unicode';
    }
</style>
<div class="font" style="font-family: iconFontName">
</div>
```

或者直接选择生成 fontclass形式

```html
<link rel="styleSheet" href="//at..." >

<span class="iconfont  icon-xxx"></span>
```



# svg icon  [优先使用]

https://www.iconfont.cn/  生成svg代码

```html
<svg>
    <use></use>
</svg>
```





# css

练习css技巧，每天一个小图标

[CSS ICON -- project by Wenting Zhang](https://cssicon.space/#/icon/bell)