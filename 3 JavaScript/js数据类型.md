# 数字和字符串
1. <code>1</code> | <code>'1'</code>
2. 数字能加减，字符串不能
3. 字符串能代表手机号码，数字不能
4. 字符串存储方式utf-8,数字64位浮点数。
   
# 数据类型 4基2空1对象
1. number 数字
  - 64位浮点数
  - NAN 无法表示的数字
  - 正0 和 负0 是不一样的
2. string 字符串
  - UTF-8
  - 单/双/反引号写法
  - 转义 \
  - 属性，长度/下标
3. bool   布尔
  - 否定运算 !value
  - 相等运算 
  - 比较运算
  - 配合if使用
4. symbol 符号
5. undefined 空
    undefined是一个表示"此处无定义"的原始值，转为数值时为NaN。

   声明变量，非对象的空值，函数额return
6. null      空
   null是一个表示“空”的对象，转为数值时为0；
7. object    对象

# falsy
1. falsy 相当于false但又不是false的值，除了falsy其他都是真值。
2. falsy 包含：undefined，null，0，NaN，''
   
# 变量
1. var a=1 过时
2. let a = 1 
   - 循环块作用域，使用范围不能超出{}
   - 不能重复申明
   - 可以赋值，也可以不赋值
   - 必须先声明再使用，否则报错
   - 全局声明的let变量，不会变成window属性
   - for循环配合let有奇效
3. const
   - 跟let几乎一样
   - 不一样的是，声明就要赋值，赋值后不能更改
## 类型转换
1. number=>string
  ```js
      String(n)
      n + ''
  ```
2. string => number
  ```js

      Number(s)
      parseInt(s)/parseFloat(s)
      s - 0
  ```
3. x => bool
  ```js
    Boolean(x)
    !!x
  ```
4. x => String
   ```js
    String(x)
    x.toString()

   ```