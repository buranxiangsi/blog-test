# JS函数

##### 函数定义

函数是对象。

1. 具名函数

   ```
   function 函数名(形式参数1, 形式参数2){
   	语句
   	return 返回值
   }
   ```

2. 匿名函数

   ```
   上面的居民函数去掉函数名就是匿名函数
   // 1
   function (形式参数1, 形式参数2){
   	语句
   	return 返回值
   }
   // 2
   let a = function(x,y){return}
   ```

3. 箭头函数

   ```js
   let f1 = x => x*x
   let f2 = (x,y) => {return x+y} //圆括号不能省
   let f2 = (x,y) => ({name:x,age:y})//直接返回对象会出错，需要加个圆括号
   ```

4. 构造函数

   ```js
   let f = new Function('x','y', 'return x+y')
   //基本没人用，但是能让你知道函数是谁构造的
   //所有函数都是Function构造出来的，包括Object，Array，Function
   ```

   

##### 函数自身VS函数调用=fn VS fn()

1. 函数自身

   ```js
   let fn = () => console.log('hi')
   //不会有任何记过，因为fn没执行
   ```

   

2. 函数调用

   ```js
   let fn = () => console.log('hi')
   
   fn()//打印hi，有圆括号才是调用
   ```

   

## 函数的要素

1. 调用时机

   ```js
   //1
   let a = 1
   function fn(){
       console.log(a)
   }
   
   //打印多少？不知，因为没有调用代码
   
   //2
   let a = 1
   function fn(){
       console.log(a)
   }
   fn()
   
   //打印多少？1
   
   //3
   let a = 1
   function fn(){
       console.log(a)
   }
   a=2
   fn()//2
   
   //4
   let a = 1
   function fn(){
       console.log(a)
   }
   fn()
   a=2
   //fn()1
   
   //5
   let a = 1
   function fn(){
       setTimeout(()=>{
   		console.log(a)
        },0)
   }
   fn()
   a=2
   
   //fn() 2
   
   // 6
   let i = 0
    for(i = 0; i<6; i++){
    	setTimeout(()=>{
   		console.log(i)
     },0)
   }
   // 打印6个6
   // setTimeout()是推迟打印，当for循环完再执行setTimeout函数。
   //setTimeout执行时，for已经循环了6次，此时i=6，所以重复打印出6个6
   
   
   
   //7 
   for(let i = 0; i<6; i++){
       setTimeout(()=>{
       	console.log(i)
       },0)
   }
   // 0，1，2，3，4，5
   // 因为js在for和let一起使用事会多复制i
   
   let i
   for(i = 0; i<6; i++){
       const x = i
       setTimeout(()=>{i
         console.log(x)
       })
   }
   //0 1 2 3 4 5
   ```

   

2. 作用域

   1. 每一个函数都会默认创建一个作用域
   2. 一个{  } 是一个作用域
   3. 顶级作用域声明的是全局变量
   4. window属性是全局变量
   5. 其它都是局部变量
   6. 作用域也可以嵌套
   7. 如果作用域有多个同名变量a
   8. 那么查找a的声明时，就向上取最近的作用域——最近原则
   9. 查找a的过程与函数执行无关，但a的值与函数执行有关。

   ```js
   function f1(){
   	let a = 1
   	function f2(){
           /*
           let a = 2
   		function f3(){
   			console.log(a)
   		}
   		闭包---a，与f3
           */
   		let a = 2
   		function f3(){
   			console.log(a)
   		}
   		a = 22
   		f3()
   	}
   	console.log(a)
   	a = 100
   	f2()
   }
   f1()
   ```

   

3. 闭包

   1. 一个函数用到了外部的变量，那么这个函数加这个变量就叫做闭包。

4. 形式参数

   1. 非实际参数，只是给参数取名字。
   2. 形参可以认为是变量声明

5. 返回值

   1. 每个函数都有返回值 
   2. 函数执行完了才会返回
   3. 只有函数有返回值
   4. 返回值不是打印值

6. 调用栈

   1. js引擎在调用一个函数前，需要把函数所在的环境push到一个数组里，这个数组叫调用栈
   2. 数组执行完了，把幻境弹出来，然后return到之前的环境，继续执行后续代码

7. 函数提升

8. arguments  (除了箭头函数)

9. this (除了箭头函数)

   1. person.sayHi.call(person) 手动把person传到函数里，作为this ，默认使用这种方法
   2. person.sayHi() 自动把person传到函数里，作为this

##### 立即执行函数

原理

1. ES5为了得到局部变量，必须引入一个函数
2. 函数必须是匿名函数，声明一个匿名函数，立即加()执行它
3. 但是这种语法不合法。
4. 所以需要在匿名函数前面加运算符，有些运算符会往上走，所以最好用！