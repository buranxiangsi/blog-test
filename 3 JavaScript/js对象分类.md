# JS对象分类

## 1.  类型 VS 类

- 类型

  - 类型是JS数据的分类，有7种（四基两空一对象）

  

- 类
  - 类是针对对象的分类，有无数种
  - Array、function、Date等等

#### 对象需要分类

1.  很多对象拥有一样的属性和行为，需要把它们分为同一类。
2.   但还是有很多对象拥有其他的属性和行为，所以需要不同的分类。

```js
// 1 正方形，三个属性：边长、面积、周长
let square = {
    width: 5,
    getArea(){
		return this.width * this.width
	},
	getLength(){
		return this.width * 4
	}
}
// 2 for循环

let squareList = []
for(let i = 0; i<12; i++){
	squareList[i] = {
		width: 5,
		getArea(){
			return this.width * this.width
		},
		getLength(){
			return this.width * 4
		}
	}
}

// squareList[1].getArea()

// 3 width 长度不一样
let squareList = []
let widthList = [5,6,5,6,5,6,5,6,5,6,5,6]
for(let i = 0; i<12; i++){
    squareList[i] = {
        width: widthList[i],
        getArea(){
        	return this.width * this.width
        },
       	 getLength(){
       	 	return this.width * 4
        }
    }
}

// 4  借助原型，节省内存
let squareList = []
let widthList = [5,6,5,6,5,6,5,6,5,6,5,6]

let squarePrototype = {
    getArea(){
    	return this.width * this.width
    },
    getLength(){
    	return this.width * 4
    }
}

for(let i = 0; i<12; i++){
    squareList[i] = Object.create(squarePrototype)
    squareList[i].width = widthList[i]
}

// 5 把代码抽离到一个函数里，然后调用函数

let squareList = []
let widthList = [5,6,5,6,5,6,5,6,5,6,5,6]

function createSquare(width){ //此函数叫构造函数
	let obj = Object.create(squarePrototype)
	// 以squarePrototype为原型创建空对象
	obj.width = width
	return obj
}

let squarePrototype = {
    getArea(){
    	return this.width * this.width
    },
    getLength(){
    	return this.width * 4
    }
}

for(let i = 0; i<12; i++){
	squareList[i] = createSquare(widthList[i])
	// 创建square
}

// 6 但函数和原型还是分散的，组合在一起
let squareList = []
let widthList = [5,6,5,6,5,6,5,6,5,6,5,6]

function createSquare(width){
    let obj = Object.create(createSquare.squarePrototype) // NO
    obj.width = width
    return obj
}

createSquare.squarePrototype = { 
    // 把原型放到函数上
    getArea(){
    return this.width * this.width
	},
    getLength(){
    return this.width * 4
	},
    constructor: createSquare //方便通过原型找到构造函数
}

for(let i = 0; i<12; i++){
    squareList[i] = createSquare(widthList[i])
    console.log(squareList[i].constructor)
    // constructor可以知道谁构造了这个对象
}

// 7 函数和原型的结合，new操作符重写
let squareList = []
let widthList = [5,6,5,6,5,6,5,6,5,6,5,6]
function Square(width){
	this.width = width
}

Square.prototype.getArea = function(){
	return this.width * this.width
}

Square.prototype.getLength = function(){
	return this.width * 4
}

for(let i = 0; i<12; i++){
    squareList[i] = new Square(widthList[i])
    console.log(squareList[i].constructor)
}

/* 重点
new X()自动做了四件事
1. 自动创建空对象
2. 自动为空对象关联原型，原型地址指定为X.prototype
3. 自动将空对象最为this关键字运行空对象
4. 自动return this
5. new 后面的函数使用名词 词性规则
6. 其它函数一般使用动词开头 词性规则

构造函数X——构造对象
1. X函数本身负责给对象本身添加属性
2. X.prototype对象负责保存对象的共用属性。
3. 所有构造函数，首字母大写  大小写
4. 所有被构造出来的对象，首字母小写 大小写


*/
```



### ES6 引入了class

```js
class Circle{
    constructor(radius){
        this.radius = radius
    }
    getArea(){
        return Math.pow(this.radius,2) * Math.PI
    }
    getLength(){
        return this.radius * 2 * Math.PI
    }
}

let circle = new Circle(5)
circle.radius
circle.getArea()
circle.getLength()
```



## 原型和共有属性的关系

1. 共有属性的集合是原型。
2. 原型是指向共有属性的地址。



## 构造函数公式

结论: 你是谁构造的，你的原型就是谁的prototype属性对应的对象

```
对象.__proto__ ===  其构造函数.prototype
```

```
let x = {}
x.__proto__ === Object.prototype  //true
```



###  题

1 . 关于「原型」，正确的是（多选）下文中的 x 均代表普通对象。

```
1.  「x 的原型」等价于「x.__proto__ 所指的对象」 ，有时为了方便，我们可以认为「x 的原型」等价于「x.__proto__ 」
2.  一个对象的原型指的是这个对象与其他同类对象的公有属性的集合，比如 obj1 和 ob2 同时拥有 toString / valueOf，那么 toString / valueOf 等属性组成的对象，就是 obj1 和 obj2 的原型，这个原型的地址一般储存在构造函数的 prototype 里
3.  x.__proto__和 Object.prototype 存储着同一个对象的地址，这个对象就是 x 的原型
4.  每个对象都有原型，但除了「根对象 Object.prototype」比较特殊，Object.prototype 这个对象的原型为空 null
```



2. 关于 prototype 属性，正确的有

------

```
1.  所有函数一出生就有一个 prototype 属性
2.  所有 prototype 一出生就有一个 constructor 属性
3.  所有 constructor 属性一出生就保存了对应的函数的地
4.  如果一个函数不是构造函数，它依然拥有 prototype 属性，只不过这个属性暂时没什么用
5.   如果一个对象不是函数，那么这个对象一般来说没有 prototype 属性，但这个对象一般一定会有 __proto__ 属性
```



3. 请使用 class和属性，写一个 Person 构造函数，要求以下代码运行通过：

```js
function Person(你来补全代码){
    你来补全代码
}

class Person {
    你来补全代码
}

let person = new Person('frank', 18)
person.name === 'frank' // true
person.age === 18 // true
person.sayHi() // 打印出「你好，我叫 frank」

let person2 = new Person('jack', 19)
person2.name === 'jack' // true
person2.age === 19 // true
person2.sayHi() // 打印出「你好，我叫 jack」

//答案
//class
class Person {
    
    constructor(name,age){
        this.name = name
        this.age = age 
    }
    
    sayHi(){
        return '你好，我叫'+ this.name
        //console.log('你好，我叫'+ this.name)
        //console.log(`你好，我是${this.name}`)
    }
    

}

//peototype
function Person(name, age){

    this.name = name
    this.age = age
}

Person.prototype.sayHi = function(){
 
   return '你好，我叫' + this.name
    //console.log('你好，我叫'+ this.name)
    //console.log(`你好，我是${this.name}`)
}

```





###### 参考链接：

1. [方应杭：你可以不会 class，但是一定要学会 prototype](https://zhuanlan.zhihu.com/p/35279244)
2. [方应杭：JS 的 new 到底是干什么的？](https://zhuanlan.zhihu.com/p/23987456)
3. [方应杭：JS 中 **proto** 和 prototype 存在的意义是什么？](https://www.zhihu.com/question/56770432/answer/315342130)
4. [饥人谷整理的 ES6 所有新特性](http://frankfang.github.io/es-6-tutorials/)