# this 2

## this指向window

```js
function fn(){
    console.log(this)
}
fn()// window
```

## 如何传this

call传this和arguments(伪数组，没有数组共有函数的数组)

`call(this,arguments)`

```js
fn.call(1)
//number{1}

```

js特性：传的this不是对象，js会自动封装成对象。

禁止这项特性

```js
function fn(){
    'use strict'//严格模式，禁止自动封装
    console.log(this)
}
fn.call(1)//1
```



```js
function fn(){
    console.log('this' + this)
}
fn.call(1)
//this:1
```

引用：变量保存对象地址



# js在每个函数加了this

**用this获取对象**

**this 关键字** 



```js
let person = {
    name: 'frank',
    sayHi(){
        console.log('Hello' + this.name)
    }
}
person.syaHi()
//person.sayHi()隐式的把person作为this传给sayHi，方便syahi通过this引用person
```

## 问

对的：person.syaHi()

错的：person.syaHi(person)

如何解决以上矛盾

1. person.sayHi()//隐示传递
2. person.sayHi.call(person) //显示传递，手动把person传到函数里this，作为this
3. this就是参数。



# 箭头函数

箭头函数没有this，arguments

```js
console.log(this)//window
let a =()=> console.log(this)
a()//window
a.call(1)//window

let b = 1
let fn = ()=>console.log(b)
//b是外面的值1
//函数b等价于,
let fn2 = ()=> console.log(this)
//this就是外面的this

let fn3 =()=> console.log(arguments)
//error
```



## 立即执行函数

var 声明全局变量

function 里面才是局部变量

当需要用局部变量时，需要用到函数。

然后衍生了立即执行函数，获取局部变量。

```js
! function(){//!可以是+|-|1*
    var a= 2
    console.log(a)
}()
```

新版局部变量

```js
{
    let a = 2
    console.log(2)
}
```









