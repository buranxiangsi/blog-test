##### 举例1

```js
function random(){
    setTimeout(()=>{
        return parseInt(Math.random()*6) +1)
    }, 1000)
    //return undefined
}

const n = random()
console.log(n)//undefined

//random()没有写return 就是return undefined
//箭头函数里有return,返回真正的结果
//这是一个异步函数/任务
```

##### 拿到异步结果——回调，写个函数，把函数地址给它

```js
//在random函数得到的结果后，把结果作为参数传给f1
function random(fn){
   setTimeout(()=>{
        fn(parseInt(Math.random()*6) +1)
    }, 1000)
}
//写个函数，把函数地址传给f1
function f1(x){console.log(x)}
random(f1)
```

##### 简化

```js
random(x=>{
    console.log(x)
})
```

##### 再简化

```js
random(console.log)
//参数个数不一致不能这样简化
```

