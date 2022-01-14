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

- props  外部数据

- 类读取，this.props.xxx

- 函数读取 props.xxx

- state   内部数据  初始化，读，写

- 类读取：this.state   this.setState

- 函数读取：useState 返回数组，第一线读，第二项写

- 函数组件也通过setX更新UI，类组件也是

- 函数组件没有this，一律用参数和变量，类组件有this

- 事件绑定

- ```jsx
  // this参数
  class Son extends React.Component{//函数在对象上
      addN =()=> this.setState({n:this.state.n + 1})//等价于下面的写法
      consrtuctor(){
          this.addN = ()=> this.setState({n: this.state.n + 1})
      }
  }
  
  addN(){  //函数在原型上   等价于下面的写法
      this.setState({n: this.state.n + 1})
  }
  addN: function(){
      this.setState({n: this.state.n + 1})
  }
  ```

- 类组件

- class组件

- ```jsx
  class B extends React.Component{//extends  继承
      constructor(props){
          //constructor 构造函数  初始化class创建的对象的特殊方法，从父组件传入props
          super(props)
          //super  调用父类的构造方法，把props放到this上，this.props外部数据对象的地址
          this.state = {//初始化state 内部数据
              user:{name:'React', age: 18}
          }
      }
      render(){
          return (
          	<div>Hi</div>
          )
      }
  }
  //props读取，通过this.props.xxx读取
  //props写  ，不写props，外部数据由外部更改
  
  //state 读取  this.state.xxx.yyy.zzz
  //state 写    this.setState(newState,fn)  this.setState((state,props)=>newState,fn)
  ```

- props

- 接收外部数据

- 接收外部函数

- state

- 生命周期 `create`  `state`  `mount`  `update`  `unmount`

- `constructor()`  - 初始化state

- ```jsx
  //初始化props
  //初始化state ，但此时不能调用setState
  //用来写 bind this
  onClick=()=>{}
  constructor(){/*...*/}
  //可不写
  ```

- `shouldComponentUpdate()` - return false 阻止更新 

- return true  不阻止UI更新

- return false  阻止UI更新

- 作用：它允许我们手动判断是否进行组件更新，根据应用场景灵活设置返回值，避免不必要的更新

- React.PureComponent 自动判断数据是否更改，来阻止或更新UI

- `render()`  - 创建虚拟DOM

- 展示视图

- 只能由一个根元素

- 两个根元素需要用React.Fragment包起来，或者`<></>`

- `componentDidMount()` - 组件已出现在页面

- 在元素插入页面后执行代码

- 可以发起加载数据的AJAX请求

- 首次渲染执行此钩子

- `componentDidUpdate()`  - 组件已更新

- UI更新执行代码

- 发起AJAX请求，用于更新数据

- flase 不触发

- `componentWillUnmount()`  - 组件将死

- 移出页面然后被销毁时执行的代码

- 函数组件

- ```jsx
  const Hello = (props) =>{
      return <div>{props.message}</div>
  }
  ```
  
- 函数组件没有state，生命周期

- React v16.8.0  Hooks  API  

- Hooks API  useState  解决没有state的问题

- Hooks API  useEffect 解决没有生命周期的问题 Effect  副作用

- 模拟 componentDidMount

- ```js
  useEffect(()=>{console.log('第一次渲染')}, [])
  ```
  
- 模拟 componentDidUpdate

- ```js
  useEffect(()=>{console.log('任意属性变更')})
  useEffect(()=>{console.log('变了')})
  ```

- 模拟 componentWillUnmount

- ```jsx
  useEffect(()=>{
      console.log('第一次渲染')
      return ()=>{
          console.log('组件要死了')
      }      
  })
  ```

- 自定义Hooks

- Hooks 原理解析

- [useState](https://juejin.cn/post/6844903704437456909#heading-3)

- useState读取state最新值

- setN  把数据存入state

- useState不能使用if，多个useState执行顺序需一致

- useRef

- 引用div ， 引用任意数据

- 数据贯穿始终

- useContext  初始化上下文（上下文 => 变量）

- 不仅贯穿始终，还能贯穿不同组件

- **Hooks  详解**

- useState  状态

- ```jsx
  //使用状态
  const [n, setN] = React.useState(0)
  const [user, setUser] = React.useState({name:'f'})
  //不可以局部更新，属性不会自动合并，需手动合并
  //obj地址需变更，不然UI不会更新
  
  //useState | setN  接受函数--->减少多余的计算，优先使用函数。
  ```
  
- useEffect 副作用

- ```jsx
  //副作用：对环境的改变，每次在render之后执行
  //用途，可以代替以下三个生命周期
  componentDidMount    //[空数组是第一次执行，只执行一次]作第二个参数
  componentDidupdate   //可指定依赖
  componentWillUnmount // 通过return
  //多个useEffect 会按照出现次序执行
  ```
  
- useContext 上下文

- ```jsx
  // 全局变量是全局的上下文，上下文是局部的全局变量
  
  C = createCointext(initial) //1创建上下文
  <C.provider>                //2圈定作用域
  useContext(C)               //3在作用域使用上下文
  
  //注意：不是响应式的
  ```
  
- Redux | useReducer

- ```jsx
  // useReducer API  践行Flux|Redux思想
  创建初始值 initalState
  创建所有操作 reducer(state, action)
  传给useReducer 得到读和写API
  调用写({type:'操作类型'})
  
  //useReducer 是 useState 的复杂版
  
  
  //Redux (复杂) 状态管理工具 (它是一个架构)
  设计思想： 
  Web 应用是一个状态机，视图与状态一一对应。
  所有的状态，保存在一个对象里
  
  //useReducer 不能代替 Redux 需要
  数据集中在store对象                        store：储存数据的地方
  将所有操作集中在reducer                    reducer
  创建一个Context                           Context
  创建对数据的读写API                        useReducer
  第4步的内容放到第三步的Context              <Context.Provider value={ {value1,value2} }>
  用Context.Provider将Context提供给所有组件  <Context.Provider/>
  各个组件用useContext获取读写API             const {state, useState} = useContext(Context)
  ```
  
- useMemo  记忆

- useRef  引用

- Hook 自定义

  

