# 进程与线程
1. js是单线程
2. 跨线程通信——DOM操作慢
   
# JS引擎 默认V8引擎
1. 编译
2. 优化
3. 执行
   
  - 准备工作(js运行环境)：
     - window
     - document
     - setTimeout
  
  - 在内存OS运行
     - stack栈 heap堆
     - stack栈——连续存储数据——顺序存放
     - heap 堆——链接存储数据——随机存放
4. 垃圾回收
5. 数据分为两种，对象（存在stack）非对象（存在heap）。
   
# JS三座大山之原型（1、this 2、原型 3、AJAX）
## 挂在window上，方便使用
1. console
2. document
3. Object
4. Array 特殊对象
   ```js
   var a = [1,2,3];  等价于 var a = New Array(1,2,3);
   ```
5. function 特殊对象
   ```js
   function f(){}    等价于 var f = New function();
   ```

- 对象和变量是两个不同的东西。
- 变量是容器，存放对象地址。
- 对象是存放在heap里面的数据。
<br>

- 原型: xxx.prototype 存储了xxx 对象的共同属性
- 每个对象都有1个隐藏属性，指向原型(对象)
- 关注小写对象的隐藏属性__proto__

   