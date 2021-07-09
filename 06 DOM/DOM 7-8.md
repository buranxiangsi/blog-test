# DOM 7-8

1. js无法操作dom
2. 浏览器在window上加了一个document
3. js用document操作网页
4. API
5. document.querySelector('#id')
6. document.querySelectorAll('.red')[0]
7. 兼容IE用 getElement(s)ByXXX
8. 获取特定元素
9. document.documentElement——html
10. document.head——head
11. document.body——body
12. window——窗口（窗口不是元素）监听
13. document.all——所有元素，第六个falsy值
14. 获取的元素是对象，元素 有6层原型链
15. x.nodeType **记住13**
16. **1 元素 Element，标签  Tag**
17. **3 文本 Text**
18. 8 注释 Comment
19. 9 文档  Document
20. 11  文档片段 DocumentFragment
21. 增删改查
22. 增
23. document.createElement('div|style|script|li')——标签节点
24. document.createTextNode('text') ——文本节点
25. div.appendChild(text,node接口) ——标签插入文本` element接口  div.innerText='text' div.textContent='text'`
26. 1个元素不能出现在两个地方，除非复制一份 div.cloneNode()
27. 删
28. parentNode.removeChild(childNode) ——旧
29. childNode.remove()——新
30. 改属性
31. div.className= "newdiv"——改class
32. div.classList.add('newdiv')——改class
33. div.style=' color:blue;'——改style
34. div.style.width = '100px'——改style
35. diy.style.backgroundColor = 'white' 大小写
36. div.dataset.x = 'xx' 改data-* 属性
37. 读属性
38. div.classList / a.href
39. div.getAttribute('class') /a.getAttribute('href')
40. 改事件处理
41. div.onclick(默认null)——升级版——div.addEventListener
42. div.onclik调用方式 fn.call(div,event)
43. 改内容
44. div.innerText = 'xxx' ——文本内容
45. div.textContent = 'xxx'
46. div.innerHTML = 'xxx' ——html内容
47. div.innerHTML = '' ——改标签，先清空
48. div.appendChild(div) ——再加内容
49. 查
50. node.parentNode | node.parentElement——查父元素
51. node.parentNode.parentNode——查祖元素
52. node.childNodes | node.children——查子元素
53. node.parentNode.childNodes | node.parentNode.children——查兄弟元素
54. node.firstChild
55. node.lastChild
56. node.previousSibling
57. node.nextSibling
58. 遍历 
59. DOM操作跨线程
60. 跨线程通信
61. 自动同步  id  dataset：{x:test}
62. js——property——属性，div1的虽有属性，支持字符串，布尔等类型
63. 渲染引擎——attribute——属性，渲染引擎div对应标签的属性 ，只支持字符串

