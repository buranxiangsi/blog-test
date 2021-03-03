# JS对象的基本用法

对象（object）就是一组“键值对”（key-value）的集合，是一种无序的复合数据集合。

```js
var obj = {
  foo: 'Hello',
  bar: 'World',
  [xx]: 1111// [xx]变量:加[]是变量
};

// 键名是字符串；引号省略，只能写标识符，但它也是字符串。

```



## 1. 声明对象的两种语法

```js
let obj = { 'name': name, age: 18}
let obj = new Object({'name': name})

//区别：第二种是规范写法，但普遍使用第一种，因为简便
```

## 2. 如何删除对象的属性

```js
let obj = { p: 1}
delete obj.p //true
Object.keys(obj) //[]

delete.obj['p']
```



## 3. 如何查看对象的属性

```js
Object.key(obj) //查看自身的属性
console.dir(obj) //查看自身和共有属性
obj.hasOwnProperty('toString') //判断属性是自有属性还是共有属性

obj['key'] 
obj.key
```



## 4. 如何修改或增加对象的属性

1. 直接赋值

   ```js
   obj['name'] = 'jack'
   ```

   

2. 批量赋值

   ```js
   Object.assign(obj, {p1:1, key:value})
   ```

3. 增加修改共有属性（最好不要这么做。）

   ```js
   obj.__proto__['toString'] = 'xxx'
   Object.prototype['toString'] = 'xxx'//推荐此方法
   //__proto__代码不建议写
   ```

4. 改原型

   ```js
   obj__proto__=common
   let obj=Object.create(common)//推荐此方法
   //__proto__代码不建议写
   ```

5.  增基本同上，已有属性则改，没有属性则增。
6. 每个对象都有原型，对象的原型也是对象，<code>obj={}</code>

## 5. 'name' in obj 和 obj.hasOwnProperty('name')的区别

1. in 运算符检查对象是否包含某个属性。检查键名。

2. 'name' in obj

   ```js
   var obj = { 'name': name };
   'p' in obj // true
   'toString' in obj // true
   
   //in运算符的一个问题是，它不能识别哪些属性是对象自身的，哪些属性是继承的。就像上面代码中，对象obj本身并没有toString属性，但是in运算符会返回true，因为这个属性是继承
   ```

   

3.  obj.hasOwnProperty('name')

   ```js
   var obj = {};
   if ('toString' in obj) {
     console.log(obj.hasOwnProperty('toString')) // false
   }
   
   //使用对象的hasOwnProperty方法判断是否为对象自身的属性
   ```

   