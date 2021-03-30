# Webpack

- 转译代码 （ES6转为ES5，SCSS 转为CSS）
- 构建build
- 代码压缩
- 代码分析

#### 安装：官网安装

```bash
//本地安装
npm install -g webpack@4 webpack-cli@3
或
yarn global add webpack@4 webpack-cli@3
// 视频中误打成 webpack-cli@4 了

//项目安装依赖
npm init -y 
yarn add webpack@4 webpack-cli@3 --dev
./node_modules/.bin/webpack --version //查看版本
npx webpack //运行
```

#### 初始化

[官方文档](https://webpack.js.org/concepts/configuration/#simple-configuration)

```bash
npx webpack
//报错。不管也可以
WARNING in configuration
The 'mode' option has not been set, webp
ronment.
You can also set it to 'none' to disable

新建文档
webpack.config.js
输入
var path = require('path');

module.exports = {
  mode: 'development',//开发模式
 //其他代码在下行
};
```

## webpack 配置entry/output 

```js
entry: './foo.js',//运行会报错，改成项目默认文档
    output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'main.js', //将ertry默认文档转译到main.js
    
    },
```

[官方文档](https://webpack.js.org/guides/caching/#output-filenames)

```js
filename: '[name].[contenthash].js',//将filename替换成这个，文件名改成哈希模式
```

##### http缓存  Cache-Control

- 文件更新，webpack自动打包新的哈希name文件，浏览器请求新的信息。

- ```js
  //pajson
  "scripts": {
      "build": "rm -rf dist && webpack ",
          //删除旧缓存文件。命令行运行 yarn build /npm run build
      "test": "echo \"Error: no test specified\" && exit 1"
    },
  ```

  

## 自动生成HTML文件

[官方文档](https://webpack.js.org/plugins/html-webpack-plugin/#installation)下面的的链接就是参考文档的内容。

[参考文档](https://github.com/jantimon/html-webpack-plugin)

##### 安装

`yarn add html-webpack-plugin@4 --dev`

```js
//js
const HtmlWebpackPlugin = require('html-webpack-plugin');
const path = require('path');

module.exports = {
  plugins: [new HtmlWebpackPlugin()],
};
```

- 自动更改文件名

  ```html
  <!-- index.html-->
  
  <title><%= htmlWebpackPlugin.options.title %></title>
  ```

  

## 引入CSS文件

[官方文档](https://webpack.js.org/loaders/css-loader/)

1. js生产style  

2. CSS文件

   ```bash
   //1
   yarn add css-loader --dev  
   yarn add style-loader --dev
   //2
   yarn add  mini-css-extract-plugin --dev  
   ```

   ```js
   //webpack.config.js
   const MiniCssExtractPlugin = require('mini-css-extract-plugin');
   plugins: [
     new MiniCssExtractPlugin({
       filename: '[name].[contenthash].css',
       chunkFilename: '[id].[contenthash].css',
     }),
       
   module: {
       rules: [
         {
             //把css文件读到loader再存到style中
           test: /\.css$/i,//
           //use: ["style-loader", "css-loader"], //1
           use: [  //2
             {
               loader: MiniCssExtractPlugin.loader,
               options: {
                 publicPath: '/public/path/to/',
               },
             },
             'css-loader',
           ],
         },
       ],
     },
   ```

   

### webpack dev server

```bash
yarn add webpack-dev-server --dev//代替http-server 之后使用yarn start命令
```

```json
//package.json
"scripts": {
    "start": "webpack serve --open",//官方文档这样写的，但是会报错
    "start": "webpack-dev-server --open",//改成这个，就不会了，不知道是不是版本的问题。
  },

```

```js
//webpack.config.js
devtool: 'inline-source-map',
  devServer: {
    contentBase: './dist',
  },
```

### 

#### 切换生产模式和开发模式

1. webpack.config.js 复制
2. 改文件名为webpack.config.prod.js 
3. 修改不同环境所需的代码，删除不需要的代码
4. 新建一个webpack.config.base.js文件
5. 把共有的属性抽取到base文件中



## 引入SCSS

```bash
yarn add sass-loader dart-sass --dev
```

```sh
yarn build &&
git checkout gh-pages &&
rm -rf *.html *.js *.css *.png &&
mv dist/* ./ &&
rm -rf dist;
git add . &&
git commit -m 'update' &&
git push
```

