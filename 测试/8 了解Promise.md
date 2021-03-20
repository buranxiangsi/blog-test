# Promise

### 用途

**`Promise`**对象用于表示一个异步操作的最终完成或失败。在函数上绑定回调函数。

### 如何创建

```js
return new Promise((resolve,reject)=>{})
```

### 如何使用 Promise.prototype.then

**`.then()`**Promise的链式调用（chaining），它会返回一个和原来不同的新的Promise

```js
const promise = doSomething();
const promise2 = promise.then(successCallback, failureCallback);
//或者
const promise2 = doSomething().then(successCallback, failureCallback);
//或者 把回调绑在到返回的Promise上
doSomething()
    .then(function(result) {
  		return doSomethingElse(result);
	})
    .then(function(newResult) {
 		 return doThirdThing(newResult);
	})
    .then(function(finalResult) {
  		console.log('Got the final result: ' + finalResult);
	})
    .catch(failureCallback);
//或者 then的参数可选，改为箭头函数
doSomething()
.then(result => doSomethingElse(result))
.then(newResult => doThirdThing(newResult))
.then(finalResult => {
  console.log(`Got the final result: ${finalResult}`);
})
.catch(failureCallback);//回调后失败继续使用链式操作
```



### 如何使用 Promise.all() 

语法

```js
Promise.all(iterble)//iterble 可迭代对象，Array，string
```

示例

```js
const promise1 = Promise.resolve(3)
const promise2 = 42
const promise3 = new Promise((resolve, reject) => {
    setTimeout(resolve, 100, 'foo')
})

Promise.all([promise1,promise2, promise3])
    .then((values)=>{
    console.log(values)
})
//Array[3, 43, 'foo']
//用于集合多个Promise的返回结果，

//fulfillment 完成结果在任何情况下都是数组，
//Rejection失败，它会异地的将失败状态传给回调函数，不管其它Promise是否完成。

var p = Promise.all([1,2,3]);                        //Promise {<fulfilled>: Array(3)}
var p2 = Promise.all([1,2,3, Promise.resolve(444)]); //Promise {<fulfilled>: Array(4)}
var p3 = Promise.all([1,2,3, Promise.reject(555)]);  // Promise {<rejected>: 555}

//promise.all()当且仅当传入的可迭代对象为空时为同步
var p = Promise.all([]);
var p2 = Promise.all([1337, "hi"]);
console.log(p);
console.log(p2)
setTimeout(function(){
    console.log('the stack is now empty');
    console.log(p2);
});

// Promise { <state>: "fulfilled", <value>: Array[0] }
// Promise { <state>: "pending" }
// the stack is now empty
// Promise { <state>: "fulfilled", <value>: Array[2] }
```



### 如何使用 Promise.race()

语法

```js
Promise.race(iterable); // 参数可迭代对象，

```

示例

```js
// 返回值：Promise解决或拒绝，就采用第一个Promise的值作为它的值，从而异步地解析或拒绝
// 如果迭代为空，则返回的promise将永远的等待。
const promise1 = new Promise((resolve, reject) => {
  setTimeout(resolve, 500, 'one');
});

const promise2 = new Promise((resolve, reject) => {
  setTimeout(resolve, 100, 'two');
});

Promise.race([promise1, promise2]).then((value) => {
  console.log(value);
 
});
// "two"
```

