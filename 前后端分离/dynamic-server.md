# 动态服务器

动态服务器和静态服务器的区别是是否请求了数据库。

```js
const fs = require("fs")

//读数据库
const usersString = fs.readFileSync("/user.json").toString()
const usersArray = JSON.parse(usersString)

//写数据库
const user3 = {id:3,name:'tom', password:'yyy'}
userArray.push(user3)
const string = JSON.stringify(userArray)
fs.writeFileSync('/user.json',string)
```

