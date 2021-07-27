# Promise

### Promise

Promise 对象用于表示一个异步操作的最终完成（或失败）及其结果值。

一个Promise 处于以下几种状态之一

- pending  初始状态
- fulfilled  操作成功
- rejected  操作失败

当Promise 对象成功或失败，promise的then方法排列起来的处理程序会被调用。

```js
const promise1 = new Promise((resolve, reject)=>{
    resolve('Success')
   // reject('错误')
})
promise1().then((value)=>{
    console.log(value)
})
```



### Promise.all()

返回一个新的Promise对象，promise对象读成功时才触发，一个失败则触发失败。

```js
const promise1 = 100
const promise2 = Promise.resolve(555)
Promise.all([promise1, peomise2])
    .then((value)=>{
    console.log(value)
})
```



### Promise.race()

一个peomise成功或失败后，就返回成功失败的详情，并返回promise对象。

```js
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



