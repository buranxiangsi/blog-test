# 展开语法与剩余参数

展开语法，与`Object.assign()`行为一致，执行的都是浅拷贝

可以在函数调用/数组构造时, 将数组表达式或者string在语法层面展开；还可以在构造字面量对象时, 将对象表达式按key-value的方式展开。

## 语法

函数调用

```js
myFunction(...iterableObj)
```

字面量数组构造或字符串

```js
[...iterableObj, '4', ...'hello',6]
```

构造字面量对象时，进行克隆或者属性拷贝

```js
let objClone = {...obj}
```



## 在函数调用时使用展开语法

等价于apply

```js
function myFunction(x,y,z){}
var args = [0,1,2]
myFunction.apply(null, args)

//展开语法
function myFunction(x,y,z){}
var args = [0,1,2]
myFunction.apply(...args)
```

## 在new表达式中应用

使用new调用构造函数时，不能直接使用数组+apply的方式。

```js
var dateFields = [1970,0,1]
var d = new Date(...dateFields)
```

## 构造字面量数组时使用展开语法

```js
var o = ['1','2']
var a = [...o,'3', '4']
```

数组拷贝

```js
var arr = [1,2,3]
var arr2 = [...arr]
arr2.push(4)
//[1,2,3,4]
```

连接数组

```js
var arr1 = [0, 1, 2];
var arr2 = [3, 4, 5];
// 将 arr2 中所有元素附加到 arr1 后面并返回
var arr3 = arr1.concat(arr2);

//展开语法
var arr1 = [0, 1, 2];
var arr2 = [3, 4, 5];
var arr3 = [...arr1, ...arr2];
```

## 构造字面量对象时使用展开语法

```js
var obj1 = {foo: 'bar', x: 42}
var obj2 = {foo: 'baz', y:13}

var cloneObj = {...obj1}
var mergedObj = {...obj1, ...obj2}
```

## 只能用于可迭代对象

```
var obj = {'key1': 'value1'};
var array = [...obj]; // TypeError: obj is not iterable
```



# 剩余参数

允许我们将一个不定数量的参数表示为一个数组

## 语法

```js
function (a,b, ...theArgs){
    // ...
}
```

如果函数最后一个命名参数以`...`为前缀，它将成为一个由剩余参数组成的真数组。

### 剩余参数和arguments对象的区别

- 剩余参数只包含那些没有对应形参的实参，而 `arguments` 对象包含了传给函数的所有实参。
- `arguments`对象不是一个真正的数组，而剩余参数是真正的 `Array`实例，也就是说你能够在它上面直接使用所有的数组方法，比如 `sort`，`map`，`forEach`或`pop`。
- `arguments`对象还有一些附加的属性 （如`callee`属性）。

### 解构剩余参数

```js
function f(...[a, b, c]) {
  return a + b + c;
}

f(1)          // NaN (b and c are undefined)
f(1, 2, 3)    // 6
f(1, 2, 3, 4) // 6 (the fourth parameter is not destructured)
```



## 示例

`theArgs` 是数组，使用`lenght`属性得到它的个数

```js
function fun1(...theArgs){
    console.log(theArgs.lenght)
}
fun1()
fun1(2)
fun1(1,3,4)
```

剩余参数包含了从第二个到最后的所有参数

```js
function multiply(multiplier, ...theArgs){
    return thsArgs.map(function(element){
        return multiplier * element
    })
}
var arr = multiply(2,1,2,4)
console.log(arr)//[2,4,6]
```

在剩余参数上使用任意的数组方法，arguments对象不可以

```js
function sortRestArgs(...theArgs) {
  var sortedArgs = theArgs.sort();
  return sortedArgs;
}
(sortRestArgs(5,3,7,1)); // 弹出 1,3,5,7
//arguments对象上使用Array方法，它必须首先转换为一个真正的数组
function sortArguments() {
  //var args = Array.prototype.slice.call(arguments);//转换数组
  var sortedArgs = arguments.sort();
  return sortedArgs; // 不会执行到这里
}

alert(sortArguments(5,3,7,1)); // 抛出TypeError异常:arguments.sort is not a function

```



