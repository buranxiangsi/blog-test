## this 浅析

- 函数的`this`关键字在`Javascript`中的表现略有不同
- 严格模式和非严格模式之间也有差别
- 函数的调用方式决定了`this`的值
- `ES5`引入`bind`方法设置函数`this`的值
- 箭头函数不提供自身的`this`绑定

## 语法



```js
this
```



- ###### 全局上下文
  - 无论是否在严格模式下，在全局执行环境中(函数体外部)，this指向全局对象。

- 函数上下文
  - 函数内部，`this`的值取决于函数被调用的方式。
  - 非严格模式,`this`值不是由该调用设置的，`this`指向全局对象
  - 严格模式，进入执行环境没有设置`this`值，`this`保持`undefined`

- 类上下文
  - 在类的构造函数中，`this`是一个常规对象，
  - 类中所有非静态方法都会被添加到`this`的原型中。
  - 静态方法不是`this`属性，是类自身的属性

- ###### 派生类

  - ###### 派生类的构造函数没有初始的`this`绑定。

  - ###### 在构造函数调用`super()`会生成一个`this`绑定。

  - ###### 并相当于执行此代码`this = new Base()`，base为基类

  - ###### `super` 关键字用于访问和调用一个对象的父对象上的函数。



## 函数上下文中的this

```js
var obj = {a: 'Custom'};

var a = 'Global';

function whatsThis() {
  return this.a;  
}

whatsThis();       //   Global
whatsThis.call(obj); //Custom
whatsThis.apply(obj); //Custom
```

- `call()` 方法使用一个指定的`this`值和单独给出的一个或多个参数来调用一个函数

- `apply()` 方法调用一个具有给定`this`值的函数，以及以一个数组（或类数组对象）的形式提供的参数

- ```js
  function.call(thisArg, arg1,arg2)
  
  ```

## this和对象转换

```js
function add(c,d){
    return this.a+this.b+c+d
}
var o = {a:1, b:3}
add.call(o, 5, 7) //16,
add.apply(o, [10,20])//34
```

- 

```js
function f(){
    return this.a
}
var g = f.bind({a:"a1"})
console.log(g())

var h = g.bind({a: 'yoo'})
console.log(h())

var o = {a:37, f:f, g:g, h:h};
console.log(o.a, o.f(), o.g(), o.h())
```

- `bind()` 方法创建一个新的函数，在 `bind()` 被调用时，这个新函数的 `this` 被指定为 `bind()` 的第一个参数，而其余参数将作为新函数的参数，供调用时使用。

- ```js
  function.bind(thisArg[, arg1[, arg2[, ...]]])
  //它创建一个和function具有相同函数体和作用域的函数，新函数中，this将永久被绑定到bind的第一个参数。
  ```

## 箭头函数

- 在箭头函数中 `this` 与封闭词法环境的this保持一致。

- 箭头函数不会创建自己的this，它只会从自己的作用域链的上一层继承this

```js
// 全局函数中this被设置为全局对象
var globalObject = this;
var foo = (() => this);
console.log(foo() === globalObject); // true

//作为对象的一个方法调用
var obj = {foo: foo};
console.log(obj.foo() === globalObject); // true
//call设定this
console.log(foo.call(obj) === globalObject); // true
//bind设定this
foo = foo.bind(obj);
console.log(foo() === globalObject); // true

//函数内部
var obj ={
    bar: function(){
        var x = (() => this)
        return this
    }
}
//作为obj对象的方法调用bar，把它this绑定到obj
var fn =obj.bar()
console.log(fn()===obj)//ture
//引用obj方法，调用箭头函数后，this指向window
var fn2 = obj.bar
console.log(fn2()()==window)//true
```

## 作为对象的方法

函数作为对象的方法被调用时，`this`被设置为调用函数的对象。

```js
var o = {
  prop: 37,
  f: function() {
    return this.prop;
  }
};

console.log(o.f()); // 37
//o.f被调用时，函数内的this将绑定到o对象


//不受函数定义的方式或位置的影响

var o = {prop: 37};
function independent() {
  return this.prop;
}

o.f = independent;
console.log(o.f()); // 37


//this的绑定只受最接近的成员引用的影响
o.b = { g: independent, prop: 42}
console.log(o.b.g())

//原型链中的this
//该方法存在于一个对象的原型链上，那么 this 指向的是调用这个方法的对象，
var o = {
  f: function() {
    return this.a + this.b;
  }
};
var p = Object.create(o);
p.a = 1;
p.b = 4;

console.log(p.f()); // 5

//getter 与 setter 中的 this
//用作 getter 或 setter 的函数都会把 this 绑定到设置或获取属性的对象。
function sum() {
  return this.a + this.b + this.c;
}
var o = {
  a: 1,
  b: 2,
  c: 3,
  get average() {
    return (this.a + this.b + this.c) / 3;
  }
};
Object.defineProperty(o, 'sum', {
    get: sum, enumerable: true, configurable: true});

console.log(o.average, o.sum); // logs 2, 6
```



## 作为构造函数

当一个函数用作构造函数时（使用`new`关键字），它的`this`被绑定到正在构造的新对象。

```js
function C(){
  this.a = 37;
}

var o = new C();
console.log(o.a); // logs 37


function C2(){
  this.a = 37;
  return {a:38}; //设置返回代码，与this绑定的默认对象被丢弃
}

o = new C2();
console.log(o.a); // logs 38
```

