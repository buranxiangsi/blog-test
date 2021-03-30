# JS 数组

数组对象：一种特殊的对象

1. 典型的数组
   - 元素的数据类型相同
   - 使用连续的内存存储
   - 通过数字下标获取元素
2. JS数组不是典型的数组
   - 元素的数据可以不同
   - 内存不一定是连续的
   - 不能通过数字下标，而是通过字符串下标

## 1 创建数组

```js
//新建
let arr = [1,2,3] //常用
let arr = new Array(1,2,3)
let arr = new Array(3) //(3) [empty × 3]

//转化
let arr = '1,2,3'.split(',')
let arr = '123'.split('')
Array.from('123')

//伪数组
let divList = document.querySrlrctorAll('div')
//伪数组的原型链中并没有数组的原型=没有数组的共用属性


//合并两个数组，得到新数组
arr.concat(arr2)

//截取一个数组的一部分
arr1.slice(1)//从第二个元素开始
arr1.slice(0)//全部截取
//js只提供浅拷贝
```



## 2 增删改查

删元素

```js
//跟对象一样，但是数组的长度不会改变
let arr = ['a', 'b', 'c']
delete arr['0']
arr // [empty, 'b', 'c']

//1 删头部的元素
arr.shift()//arr被修改，并返回被删元素
//2 删尾部的元素
arr.pop()  //arr被修改，并返回被删元素
//3 删中间的元素
arr.splice(index,1)//删除index的一个元素
arr.splice(index,1,'x')//并在删除位置添加'x'
arr.splice(index,1,'x','y')//并在删除位置添加'x','y'
```

查看元素

```js
//查看所有属性名
let arr = [1,2,3,4,5];arr.x= 'xxx'
Object.keys(arr)
for(let key in arr){console.log(`${key}:${arr[key]}`)}

//查看数字（字符串）属性名和值
for (let i=0; i<arr.length;i++){
    console.log(`${i}: ${b[i]}`)
}

arr.forEach(function(item, index){
    console.log(`${index}: ${item}`)
})

//查看单个属性

//1 跟对象一样
let arr = [111,222,333]
arr[0]
// 索性越界
arr[arr.length]===undefined
arr[-1]===undefined

for(let i = 0; i<= arr.length; i++){
console.log(arr[i].toString())
}
//报错 
// 查找某个元素是否在数组里
arr.indexOf(item)//存在返回索引，否则返回-1
//使用条件查找元素
arr.find(item => item%2===0)//找到第一个偶数
//使用条件查找元素的索引
arr.findIndex(item=>item%2 ===0)//找到第一个偶数的索引
```

增加元素

```js
//在尾部增加元素
arr.push(newItem)//修改arr,返回新长度
arr.push(item1,item2)//修改arr，返回新长度

//在头部增加元素
arr.unshift(newItem)//修改arr,返回新长度
arr.unshift(item1,item2)//修改arr,返回新长度

//在中间添加元素
arr.splice(index,0,'x')//在index处插入x
arr.splice(index,0,'x','y')
```

改

```js
//反转顺序
arr.reverse()//修改原数组

//自定义顺序
arr.sort((a,b)=>a-b)
```





## 3 数组变换

##### map (n-->n)

`map()` 方法创建一个新数组，其结果是该数组中的每个元素是调用一次提供的函数后的返回值

```js
var new_array = arr.map(function callback(currentValue[, index[, array]]) {
 // Return element for new_array 
}[, thisArg])

let arr = [1,2,3,4,5,6]
//平方
arr.map(item => item*item)
```



##### filter (n-->少)

```js
let arr = [1,2,3,4,5,6]
//返回偶数
arr.filter(item=> item%2===0)
```



##### reduce (n-->1)

```js
let arr = [1,2,3,4,5,6]

//和
let sum=0
for(let i=0; i<arr.length; i++){
    sum += arr[i]
}
console.log(sum)

arr.reduce((sum,item)=>{return sum+item} ,0)
```

# 训练

1. 请使用 <code>arr.map</code> 把 0 变成'周日'，把 1 变成'周一'，以此类推

```js
let arr = [0,1,2,2,3,3,3,4,4,4,4,6]
let arr2 = arr.map(补全代码)
console.log(arr2) // ['周日', '周一', '周二', '周二', '周三', '周三', '周三', '周四', '周四', '周四', '周四','周六']
```

2. 找出所有大于 60 分的成绩

```js
let scores = [95,91,59,55,42,82,72,85,67,66,55,91]
let scores2 = scores.filter(补全代码)
console.log(scores2) //  [95,91,82,72,85,67,66, 91]
```

3. 算出所有奇数之和

```js
let scores = [95,91,59,55,42,82,72,85,67,66,55,91]
let sum = scores.reduce((sum, n)=>{
  补全代码
},0)
console.log(sum) // 奇数之和：598 
```

