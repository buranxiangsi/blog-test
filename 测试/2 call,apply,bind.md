# call、apply、bind 的用法

1. [call](# call)         语法     <code>function.call(thisArg, arg1,arg2 ...)</code>
2. [apply](# apply)     语法     <code>function.apply(thisArg, [argsArray])</code>
3. [bind](# bind)       语法     <code>function.bind(thisArg[, arg1[, arg2[, ...]]])</code>



## call

使用一个指定的this值和参数来**调用一个函数**

使用调用者提供的this值和参数调用该函数的返回值。

1.  **继承**  调用父构造函数，使用call方法实现继承

```js
function Product(name, price){
    this.name = name
    this.price= price
}
function.Food(name, price){
    Product.call(this, name, price)
    this.catefory = 'food'
}

let food = new Food('面', '20')
```

2. 调用匿名函数

```js
let animals = [
  { species: 'Lion', name: 'King' },
  { species: 'Whale', name: 'Fail' }
];
for (let i = 0; i < animals.length; i++) {
  (function(i) {
    this.print = function() {
      console.log('#' + i + ' ' + this.species
                  + ': ' + this.name);
    }
    this.print();
  }).call(animals[i], i);
}
```

3. 调用匿名函数并指定上下文的this

```js
function greet() {
  var reply = [this.animal, 'typically sleep between', this.sleepDuration].join(' ');
  console.log(reply);
}

var obj = {
  animal: 'cats', sleepDuration: '12 and 16 hours'
};

greet.call(obj);  // cats typically sleep between 12 and 16 hours
```





## apply

**调用一个具有给定`this`值的函数**，以及以一个数组（或[类数组对象](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Indexed_collections#working_with_array-like_objects)）的形式提供的参数.

返回有指定`this`值和参数的函数的结果。

1. 将数组各项添加到另一个数组

   ```js
   let array = ['a', 'b']
   let elements = [0,1,2]
   array.push.apply(array, elements)
   console.log(array)//['a','b',0,1,2]
   ```

2. apply和内置函数

   ```js
   const numbers = [5,6,2,3,7]
   const max = Math.max.apply(null, numbers) 
   console.log(max) // 7 
   ```

## bind

`bind()` 方法**创建一个新的函数**，在 `bind()` 被调用时，这个新函数的 `this` 被指定为 `bind()` 的第一个参数，而其余参数将作为新函数的参数，供调用时使用。

返回原函数的拷贝，并拥有指定的<code>this</code>值和初始参数

```js
const module = {
  x: 42,
  getX: function() {
    return this.x;
  }
};

const unboundGetX = module.getX;
console.log(unboundGetX());
//  undefined

const boundGetX = unboundGetX.bind(module);
console.log(boundGetX());
//  42

```

创建绑定函数，含有同样的this值

```js
this.x =9 
var module = {
    x: 81
    getX: function(){return this.x}
}

module.getX() //81

var retrieveX = module.getX
retrieveX() //9

var boundGetX = retrieveX.bind(module)
boundGetX()//81


```

## 总结

- call，apply是调用一个函数，call接受this和参数，apply接受this和参数数组。都返回函数执行的结果。
- bind 创建一个函数，返回函数的拷贝，拥有指定的this值和初始参数
- 三者都改变函数执行的this指向（指新不指旧），改变函数执行的上下文。

