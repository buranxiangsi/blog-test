# 配置

安装，两种css方案，使用css-in-js方案（12-13）

1. create-react-app 默认安装不支持typescript,如果使用typescript需要在官网上重新找安装命令。
2. 禁止重复打开浏览器，新建`.env` 文件，在文件写入 `BROWSER=none`
3. `.gitignore` 加上`/.idea`
4. 目录说明
   1. `.js` 
   2. `.jsx` - 支持标签的JS
   3. `.ts` - TypeScript
   4. `tsx` - 支持标签的TS
5. `React.StrictMode` 检查代码是否用错，暂无实际用途
6. `react-app-env.d.ts`  声明类型文件
7. `tsconfig.json` 配置文件
8. `index.css` 写入 `@import-normalize;` 保证页面在不同浏览器上默认样式相近
9. `scss` 官方支持`node-sass`，网速慢，编译慢，改用`dart-sass`，但官方不支持`dart-sass` ==技术问题==
   1. npm 6.9 支持一个新功能，叫做package alias
   2. `yarn add node-sass@npm:dart-sass`
   3. 安装成功
10. @import
    1. 引入src/xxx/yyy目录
    2. css `@import 'xxx/yyy'`
    3. [js](https://create-react-app.dev/docs/importing-a-component) `import 'xxx/yyy'`
11. helper.scss
    1. 新建 `src/helper.scss`
    2. 放置变量，函数等公用的东西
    3. 使用:在`index.scss`| `App.scss` 写`@import "helper"` 
12. CSS-in-JS方案：[styled-components](https://github.com/styled-components/styled-components)
    1. `yarn add styled-components `
    2. `yarn add --dev @types/styled-components ` 它不支持ts，需要再运行此命令。
13. style componets webstrom插件



# React Router

1. `yarn add react-router-dom`
2. `yarn add --dev @types/react-router-dom`安装依赖
3. 2种模式：history|hash
   1. history:需要后台R服务器
   2. hsah:不需要后台服务器
4. svg的使用方式
   1. 当图片用import

   2. SVG symbols

      自定义webpack，当前文件没有webpack-config，所以需要yarn eject一下

      1. svg-sprite-loader
      2. `yarn eject`：弹出webpack配置文件可自定义
      3. `yarn add --dev svg-sprite-loader`
      4. `yarn add --dev svgo-loader`

   3. ==TreeShaking 不适用require==（结论）

   4. 封装svg

   5. `yarn add --dev @types/webpack-env@1.15.1`

   6. readdirSync(path):该方法返回一个包含指定目录下所有文件名称的数组对象

   7. require.context()创建自己的上下文，允许传递要搜索的目录。

   8. `__WebpackModuleApi`







```bash
$ create-react-app filename --template typescript
$ yarn add --dev node-sass@npm:dart-sass@1.25.0
$ yarn add styled-components
$ yarn add styled-components@5.0.1
$ yarn add --dev styled-components@5.0.1
$ yarn add --dev @types/styled-components@5.0.1
$ yarn add react-router-dom@5.1.2
$ yarn add --dev @types/react-router-dom@5.1.2
$ yarn eject
$ yarn add --dev svg-sprite-loader@4.2.2
$ yarn add --dev svgo-loader@2.2.1
$ yarn add --dev @types/webpack-env@1.15.1
```







