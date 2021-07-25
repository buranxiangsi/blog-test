# React

- 引入React

- CDN

- ```html
  https://.../react.x.min.js     //引入React
  https://.../react-dom.x.min.js  //引入ReactDom
  ```

- cjs  umd

- cjs  Common JS  Node.js  支持的模块规范

- umd  统一模块定义，兼容各种模块规范（含浏览器）

- 最新的模块规范 `import  \  export`

- webpack+babel.loader 引入 React  //  create-react-app

- ```js
  yarn add react react-dom
  import React from 'react'
  import ReactDom from 'react-dom'
  ```

- 最简便的方法：create-react-app

- **函数与延迟执行**

- ```js
  //函数执行的时机
  let a = console.log(1) 
  //值 1
  
  let b = ()=> console.log(2)
  b() //2
  
  
  app1 = React.createElemennt('div', null, n)  //元素
  app2 = ()=> React.createElement('div', null, n)  //函数组件，延迟执行代码，被调用时执行
  ```

- `React 元素`

- createElement  的返回值 element，不是真正的DOM对象  ， element 为虚拟DOM对象

- `()=> React元素`

- 返回element 的函数，也可以代表一个div，可多次执行，每次得到最新的div，React对比虚拟div，找出不同(DOM DIff 算法)，局部更新视图，

- JSX  JS扩展版

- Vue有 vue-loader  

- .vue 文件写`template  script  style` 通过vue-loader 编程要给构造选项

- React  有 JSX

- JS 写法   `<button onClick="add">+1</button>`  

- JSX写法  `React.createElement('button', {onClick:...}, '+1')`

- 注意

- ```jsx
  <div className="red">n </div>
  div被jsx转译成下面的函数。
  React.createElement('div', {className:'red'}, 'n')
  //标签里面所有的js要用{}包起来
  //变量n要用{}把n包起来
  // 对象也是，{ {name: myName} }
  //return 加 () => return()
  ```

- 元素  vs  组件

- Element  VS  Component

- 返回React元素的函数就是组件，在Vue里，一个构造选项就可以表示一个组件

- React 两种组件

- 函数组件

- ```jsx
  function Welcome(props){
      return <h1>Hello, {props.name}</h1>
  
  }
  <Welecome name="myName" />
  ```

- 类组件

- ```jsx
  class Welcome extends React.Component{
      render(){
          return <h1>Hello, {this.props.name}</h1>
      }
  }
  <Welecome name="myName" />
  ```

- 在React里，HTML **标签会被翻译成React.createElement** [babel](https://babeljs.io/repl#?browsers=defaults%2C%20not%20ie%2011%2C%20not%20ie_mob%2011&build=&builtIns=false&corejs=3.6&spec=false&loose=false&code_lz=Q&debug=false&forceAllTransforms=false&shippedProposals=false&circleciRepo=&evaluate=false&fileSize=false&timeTravel=false&sourceType=module&lineWrap=true&presets=env%2Creact%2Cstage-2&prettier=false&targets=&version=7.14.8&externalPlugins=)

- `React.createElement`  参数

- 传入字符串'div'，创建div

- 传入函数，调用函数，获取返回值

- 传入类，在类前加new（执行constructor），获取一个组件对象，调用对象的render方法，获取返回值

- 

