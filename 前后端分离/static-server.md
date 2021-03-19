#### 静态服务器

server.js文件

```js
response.statusCode =200
response.setHeader('Content-Tyoe', 'text/html'; 'charset=utf-8')
const x = path
response.write(fs.readFileSync(`./public${x}`))
response.send()
```

优化

```js
response.statusCode =200
response.setHeader('Content-Tyoe', 'text/html'; 'charset=utf-8')
const filePath = path === '/' ? 'index.html' : path
const index = filePath.lastIndexOf('.')
//获取文件后缀suffix
const suffix = filePath.substring(index)
const fuleTypes = {
    '.html': 'text/html',
    '.css': 'text/css',
    '.js': 'text/javascript',
    '.png': 'image/png',
    '.jpg': 'image/jpeg',
}
response.setHeader('Content-Tyoe', 
                   `${fileTypes[suffix] || 'text/html'}`; 'charset=utf-8')
let content
try{
    content = fs.readFileSync(`./public${filepath}`)
}catch(error){
    content = '文件不存在'
    respose.statucCode=404
}
response.write(content)
response.send()
```

