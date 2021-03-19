## 如何理解js的继承

- js的继承只有一种结构：对象。
- js的对象都是位于原型链顶端的Object的实例



#### 基于原型链的继承

继承属性

```js
let f = function(){
	this.a = 1
    this.b = 2
}

let o = new f()

f.prototype.b = 3
f.prototype.c = 4

console.log(o.a)//1
console.log(o.b)//2
console.log(o.c)//4
console.log(o.d)//undefiend
```

继承方法

在js中，任何函数都可以添加到对象上最为对象的属性。当继承的函数被调用时，this指向继承函数。

```js
var o ={
    a: 2,
    m: function(){
		return this.a +1
	}
}

console.log(o.m())//3  this指向o

var p = Object.create(o)//p 是一个继承o的对象
p.a=4 //创建自身属性
console.log(p.m())//5  this指向p  this.a=p.a
```



#### 基于class的继承

```js
class Rectangle{ //声明
    constructor(height, width){//构造函数
        this.height = height
        this.width = width
    }
    
    get area(){
        return this.calcArea()
    }
    calcArea(){
        return this.height * this.width
    }
}

const square = new Rectangle(10,10)
console.log(aquare.area)//100
```



#### 参考

[链接 继承](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Inheritance_and_the_prototype_chain)