DOM 事件相关

1. 什么是事件委托？

   - 事件委托是指把一个元素响应事件的函数委托父层或祖先元素上。当事件响应到需要绑定的元素上时，会通过事件冒泡机制触发祖先元素上绑定的事件，然后在祖先元素上执行函数。
   - 节省监听数，省内存
   - 监听动态元素
   - 事件监听函数：<code>addEventListener()</code>

   

2. 怎么阻止默认动作？

   有一些在html元素默认的行为，

   - ```a```标签，点击跳转
   - ```form```的```submit```类型的`input `的默认提交跳转
   - `reset`类型的`input`重置表单行为

   - 函数：<code>preventDefult</code>可以阻止

     ```js
     $a.onclick = function(e){
     	alert("阻止跳转")
     	e.preventDefault
         //return false
     }
     ```

     

3. 怎么阻止事件冒泡？

   事件监听函数<code>addEventListener(‘click', fn, bool)</code>的bool值中，默认为空，false是冒泡事件，bool为true是捕获事件。

   - 捕获是从父元素传递到子元素，不可以取消

   - 冒泡是从子元素传递到父元素，可以用`e.stopPropagation()`中断冒泡事件。

     ```js
     function stopBubble(e){
       if(e&&e.stopPropagation){//非IE
        		e.stopPropagation();
       }else{//IE
        window.event.cancelBubble=true;
       }
      } 
     ```

     