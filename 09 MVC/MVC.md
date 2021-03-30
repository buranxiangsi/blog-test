# MVC

- MVC是一种架构设计模式
- 设计模式是对通用代码取名。
- 代码重复——重构，取函数名，调用函数名
- 页面重复——MVC



### 定义

- 每个模块负责三个对象

  #### 以app1.js 为例

  ```js
    
  import "./app1.css";
  import $ from "jquery";
  
  const $button1 = $("#add1");
  const $button2 = $("#minus1");
  const $button3 = $("#mul2");
  const $button4 = $("#divide2");
  const $number = $("#number");
  
  const n = localStorage.getItem("n");
  $number.text(n || 100);
  
  $button1.on("click", () => {
    let n = parseInt($number.text());
    n += 1;
    localStorage.setItem("n", n);
    $number.text(n);
  });
  $button2.on("click", () => {
    let n = parseInt($number.text());
    n -= 1;
    localStorage.setItem("n", n);
    $number.text(n);
  });
  $button3.on("click", () => {
    let n = parseInt($number.text());
    n *= 2;
    localStorage.setItem("n", n);
    $number.text(n);
  });
  $button4.on("click", () => {
    let n = parseInt($number.text());
    n /= 2;
    localStorage.setItem("n", n);
    $number.text(n);
  });
  ```

  ### 使用MVC框架

- model  模型，负责数据

  ```js
  const m = {
      //数据
  	data : {
          n: parseInt(localStroage.getItem('n'))
      },
      //增删改查方法
      create(){},
      delete(){},
      update(date){
          Object.assign(m.data, data)
          eventBus.trigger('m:updated')//EventBus.trigger
          localStorage.setItem('n', m.data.n)
      },
      get(){}
  }
  ```

  

- view    视图，负责UI

  ```js
  const v = {
      el: null
      html:``,//初始化视图
      init(container){
          v.el = $(container)
      },
      render(n){//发送
          if (v.el.children.length !== 0) v.el.empty()
          $(v.html.replace('{{n}}', n)).appendTo(v.el)
      }
  
  }
  ```

  

- controller 控制器，负责其它功能

  ```js
  
  const c = {
    init(container) {
      v.init(container)
      v.render(m.data.n) // view = render(data)
      c.autoBindEvents()
      eventBus.on('m:updated', () => {//EventBus.on
        console.log('here')
        v.render(m.data.n)
      })
    },
    events: {
      'click #add1': 'add',
      'click #minus1': 'minus',
      'click #mul2': 'mul',
      'click #divide2': 'div',
    },
    add() {
      m.update({n: m.data.n + 1})
    },
    minus() {
      m.update({n: m.data.n - 1})
    },
    mul() {
      m.update({n: m.data.n * 2})
    },
    div() {
      m.update({n: m.data.n / 2})
    },
    autoBindEvents() {
      for (let key in c.events) {
        const value = c[c.events[key]]
        const spaceIndex = key.indexOf(' ')
        const part1 = key.slice(0, spaceIndex)
        const part2 = key.slice(spaceIndex + 1)
        v.el.on(part1, part2, value)
      }
    }
  }
  
  ```

  

### EventBus 

`EventBus`又称事件总线，所有组件共用相同的事件中心，进行组件之间的通信。

API ：  发送事件，接收事件。

```js
eventBus.on()//监听
eventBus.trigger()//触发    
```



## 表驱动编程

表驱动法(Table-Driven Approach),简单讲是指用查表的方法获取值。

- 直接访问，使用下标访问
- 索引访问，将string转换成表下标访问
- 阶梯访问，通过确定数据所处的范围确定分类（下标）
- 它不是一个全新的编程模型，而是一种设计思路。

## 如何理解模块化

模块化(modular)编程是强调将计算机程序的功能分离成独立的，可互相改变的模块的软件设计技术，它事的每个模块都包含着执行预期功能的一个唯一方面所必须的所有东西。

模块接口表示这个模块所提供和要求的元素，可以被其他模块检测。