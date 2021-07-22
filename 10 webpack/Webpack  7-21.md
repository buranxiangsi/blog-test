# Webpack  7-21

- 前端框架

- webpack的作用

- 转移代码

- 构建build

- 代码压缩

- 代码分析

- 本地预览 `$webpack-dev-server`

- webpack  转译  js

- `$npx webpack`

- 初始化 **webpack.config.js**

- [文件名](https://webpack.js.org/configuration/output/#outputfilename)中的hash的用途

- ```js
  output:{
      filename: 'main.[contenthash].js'
  },
      //webpack.config.js
  ```

- HTTP 缓存

- `Cache-Control`

-  [自动生成html文件](https://webpack.js.org/plugins/html-webpack-plugin/)

- ```js
  var HtmlWebpackPlugin = require('html-webpack-plugin')
  plugins:[new HtmlWebpackPlugin()]
  ```

- [webpack 引入  css](https://webpack.js.org/loaders/css-loader/)

- 使用 `webpack-dev-server` [链接](https://webpack.js.org/configuration/dev-server/)

- 不需要重新build，不依赖dist，直接在内存更改

- [使用插件提取css文件](https://webpack.js.org/plugins/mini-css-extract-plugin/)

- 使用js生成style

- 把css抽成文件

- [使用两个webpack config 文件](https://github.com/survivejs/webpack-merge)

- 

