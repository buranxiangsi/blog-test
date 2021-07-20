# MVC ——JS  7-20

- MVC是设计模式的一种

- 不要重复自己——设计模式的由来

- 代码3遍重构，页面10遍重构

- MVC分三个模块，每个模块都可以写成三个对象。

- MVC 万金油设计模式

- M——Model  数据模型，负责操作所有数据

- V——View 视图，负责所有UI界面

- C——Controller  控制器，其它

- 最新的引入方法

- ```
  $yarn init -y
  $yarn add jquery
  ```

- ```js
  import './xxx.css'
  import './yyy.css'
  import $ from 'jquery'
  ```

- MVC历史

- Back bone.js  框架

- Angular JS  门槛高——了解JAVA ，   Angular ——js+dart+typescript

- C#——为取代JAVA发明的

- MVVM  双向绑定

- Vue0.8 —— Angular 简化版——双向绑定，Vue2   单向绑定，Vue3——函数式

- React  单向绑定——函数式发展 Hook

- 最小知识原则——只需要引入js

- 模块化

- `view = render(data)`——React 诞生，render渲染比DOM操作浪费性能，虚拟DOM可以解决这个问题

- 表驱动编程——大批类似但不重复的代码，把重要数据做成哈希表

- 对象间通信

- 把对象看成点

