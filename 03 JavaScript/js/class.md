# class 类

- 类是用于创建对象的模板
- 类是特殊的函数
- 类不像函数声明，函数声明会提升，类声明不会。
- 先声明类，再访问它，否则会报错
- `ReferenceError`(引用错误)对象代表当一个不存在的变量被引用时发生的错误。

## 定义类的两种方法



类声明

```js
class Rectangle {
    constructor(height,width){
        this.height = height
        this.width = width
    }
}

```

类表达式

```js
// 匿名类
let Rectangle = class{
    constructor(height, width){
        this.height = height
        this.width = width
    }
}
console.log(Rectangle.name)
//命名类
let Rectangle = class Rectangle2{
   constructor(height, width){
        this.height = height
        this.width = width
    }
}
console.log(Rectangle.name)
```

## 类体和方法定义

类体是一对花括号`{}` 中的部分，它是定义类成员的位置，比如方法或构造函数。

### 严格模式

- 类声明和类表达式的主体都执行在**严格模式**下，比如：构造函数，静态方法，原型方法，getter和setter

  非严格模式：`sloppy mode`

  严格模式：限制JS变体

  - 脚本开启严格模式

    ```js
    "use strict"
    var  v = "hello world"
    ```

  - 函数开启严格模式

    ```js
    function strict(){
        'use strict'
    }
    ```

  - 作用

    - 将过失错误转换成异常
    - 简化变量的使用
    - 让`eval`和`arguments`变得简单
    - 安全的`js`
    - 未未来的版本铺平道路

### 构造函数

- 构造函数 `constructor` 是一个特殊的方法，它用于创建和初始化一个有 `class` 创建的对象，类只能有1个构造函数

  类包含多个`constructor`，将报错`SyntaxError`：对象代表尝试解析语法上不合法的代码的错误。

  `super` 关键字用来调用一个父类的构造方法，没有显示指定，则会添加默认的`constructor` 

  ```js
  class Polygon {
      constructor() {
          this.name = "Polygon";
      }
  }
  
  class Square extends Polygon {
      constructor() {
          super();
      }
  }
  ```

  不指定构造方法，则使用默认构造函数

  对于基类 默认构造函数是

  ```js
  constructor
  ```

  对于派生类

  ```js
  constructor(...args){
  	suprt(...args)
  }
  ```

  

### 原型方法

方法定义:ECMAScript 2015开始，对象初始器中引入了一种更简短定义方法的语法，把方法名直接赋给函数的简写方式。方法定义不是构造函数

```js
const obj = {
    a:"foo",
    foo(){
        return this.a
    }
}
console.log(obj.foo())

//该方法支持计算的属性名作为方法名
var bar = {
    foo0: function(){return 0},
    foo1(){ return 1}
    ['foo'+2]() {return 2}
}
console.log(bar.foo0())//0
console.log(bar.foo1())//1
console.log(bar.foo2())//2
```

语法

```js
var obj = {
  property( parameters… ) {},
  *generator( parameters… ) {},//生成器方法
  async property( parameters… ) {},//async方法
  async* generator( parameters… ) {},//async生成器方法

  // with computed keys:
  [property]( parameters… ) {},
  *[generator]( parameters… ) {},
  async [property]( parameters… ) {},

  // compare getter/setter syntax:
  get property() {},
  set property(value) {}
};
```

简写方法和`getter`和`setter`类似

```js
var obj = {
    foo: function(){
        ...
    },
    bar: function(){
        ...
    }
}
        
//可简写为
var obj = {
    foo(){//命名函数
        ...
    },
    bar(){
        ...
    }
}
```

#### 示例

```js
class R{
    constructor(h,w){
        this.h = h
        this.w =w
    }
    //getter
    get area(){
        return this.calcArea()
    }
    //method
    calcArea(){
        return this.h*this.w
    }
}
const s = new R(10,10)
console.log(s.area)
```



### 静态方法

`static ` 关键字定义一个类的静态方法。

调用静态方法不需要实例化该类，但不能通过一个类实例调用静态方法

```js
class Point{
    constructor(x,y){
        this.x = x
        this.y = y
    }
    static distance(a,b){
        const dx = a.x -b.x
        const dy = a.y -b.y
        return Math.hypot(dx,dy)
    }
}
const p1 = new Point(5, 5);
const p2 = new Point(10,10);
p1.displayName;
// undefined
p1.distance;
// undefined

console.log(Point.displayName);// "Point"
console.log(Point.distance(p1, p2));// 7.0710678118654755
```

### 用原型和静态方法绑定this

当调用静态或原型方法时没有指定 *this* 的值，那么方法内的 *this* 值将被置为 **`undefined`**。

```js
class Animal {
  speak() {
    return this;
  }
  static eat() {
    return this;
  }
}

let obj = new Animal();
obj.speak(); // Animal {}
let speak = obj.speak;
speak(); // undefined

Animal.eat() // class Animal
let eat = Animal.eat;
eat(); // undefined

//基于函数的语法来实现，this的值在非严格模式下，方法调用会发生自动装箱，初始值为undefined，this值会被设为全局对象
//严格模式下，this值保留传入状态
function Animal(){
    Animal.prototype.speak = function(){
        return this
    }
    Animal.eat = function(){
        return this
    }
}

let obj = new Animal()
let speak = obj.speak
speak() // global object

let eat = Animal.eat;
eat(); // global object
```

### 实例属性

实例的属性必须定义在类的方法里：

```
class Rectangle {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
}
```

静态的或原型的数据属性必须定义在类定义的外面。

```
Rectangle.staticWidth = 20;
Rectangle.prototype.prototypeWidth = 25;
```

### 字段声明

```js
//公有字段
class Rectangle {
  height = 0;
  width;
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
}

//私有字段
class Rectangle {
  #height = 0;
  #width;
  constructor(height, width) {
    this.#height = height;
    this.#width = width;
  }
}
```

### 使用`extends`扩展子类

`extends `关键字在类声明或类表达式中用于创建一个类作为另一个类的子类

```js
class Animal {
    constructor(name){
        this.name= name
    }
    speak(){
        console.log(`${this.name} makes a noise.`)
    }
}

class Dog extends Animal{
    constructor(name){
        super(name)
    }
    speak(){
        console.log(${this.name} barks.)
    }
}
var d = new Dog('jack')
d.speak()//jack

//继承基于函数的类
function Animal(name){
    this.name= name
}
Animal.prototype.speak = function(){
    console.log(this.name+ 'makes a noise')
}
class Dog extends Animal{
    speak(){
        suprt.speak()
        console.log(this.name+ 'barks.')
    }
}
var d = new Dog('jack')
d.speak()//jack

//类不能继承常规对象(不可构造的)，如需继承，改用Object.setPrototypeOf()

var Animal = {
    speak(){
        console.log(this.name+' noise')
    }
}
class Dog{
    constructor(name){
        this.name=name
    }
}
Object.setPrototypeOf(Dog.prototype, Animal)
```



### Species

在派生数组类myArray返回array对象，species方法允许你覆盖默认的构造函数

### super

调用对象的父对像上的函数

### Mix-ins/混入

抽象子类或者mix-ins是类的模板

```js
//一个以超类作为输入的函数和一个继承该超类的子类作为输出可以用于在ECMAScript中实现混合：
var calculatorMixin = Base => class extends Base {
  calc() { }
};

var randomizerMixin = Base => class extends Base {
  randomize() { }
};

//使用 mix-ins 的类可以像下面这样写：
class Foo { }
class Bar extends calculatorMixin(randomizerMixin(Foo)) { }
```

