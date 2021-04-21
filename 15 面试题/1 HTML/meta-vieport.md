# meta viewport 

###### 是做什么用的，怎么写？

meta是文档级元数据元素,可用于提供 名称-值 对形式的文档元数据。`charset ` 声明文档的字符编码，`name` 属性提供名称，`content` 属性提供值，

viewport 视口，当前可见部分叫做可视视口。用于移动设备，当用户缩小浏览器缩放比例时，布局视口不变，而可视视口会变小。

meta viewport 用来禁止用户在移动端缩放网页。

```html
<meta name="viewport" content="width=device-width,initial-scale=1,minimum-scale=1,maximum-scale=1,user-scalable=no,viewport-fit=cover">
```

- width 定义viewport 宽度，值 为正整数(则单位为像素)| device-width(纵向屏幕)
- height 定义viewport 高度， 值为device-height 横向屏幕
- initial-scale 定义设备宽度与viewport大小之间的缩放比例，值0.0-10.0
- maximum-scale 定义缩放的最大值,值0.0=10.0
- minimum-scale 定义缩放的最小值,值0.0=10.0
- user-scalable 默认yes，设置为no，用户无法缩放当前页面
- viewport-fit 值 auto|contain|cover 控制文档填充屏幕
  - auto 不影响初始布局视图端口，并且整个页面都可以查看
  - contain 视图端口按比列缩放
  - 视图端口被缩放以填充设备显示

