# Canvas

## 用法

```html
<canvas id="canvas" ></canvas>                                 "
```

```js
var canvas = document.getElementById('canvas')//获取DOM
var ctx = canvas.getContext('2d')//获取渲染上下文和绘画功能
```

canvas只支持矩形和路径(由点连成的线段)的图形绘制。

## 绘制矩形

- `fillRect(x,y,width,height)` 绘制填充矩形

- `strokeRect(x,y,width,height)` 绘制矩形边框

- `clearRect(x,y,width,height)` 清除指定矩形区域，让清除部分完全透明

  x/y指定左上角坐标，width/height尺寸

  ```js
    var canvas = document.getElementById('canvas')
      var ctx = canvas.getContext('2d')
      ctx.fillStyle = 'green';
      ctx.fillRect(0,0,canvas.width,canvas.height)
      ctx.strokeRect(10,10,400,400)
  ```

  

## 绘制路径

创建路径起始点

画出路径

封闭路径

路径生成，渲染图形

- `beginPath()` 新建路径
- `closePath()` 闭合路径
- `stroke()`  描边
- `fill()`  填充

```js
 var canvas = document.getElementById('canvas');
  if (canvas.getContext) {
    var ctx = canvas.getContext('2d');

    ctx.beginPath();
    ctx.moveTo(75, 50);
    ctx.lineTo(100, 75);
    ctx.lineTo(100, 25);
    ctx.fill();
  }
```

### 移动笔触

- `moveTo(x,y)` 将笔移动到指定的坐标(x,y)

```js
 var canvas = document.getElementById('canvas');
  if (canvas.getContext){
    var ctx = canvas.getContext('2d');

    ctx.beginPath();
    ctx.arc(75, 75, 50, 0, Math.PI * 2, true); // 绘制
    ctx.moveTo(110, 75);
    ctx.arc(75, 75, 35, 0, Math.PI, false);   // 口(顺时针)
    ctx.moveTo(65, 65);
    ctx.arc(60, 65, 5, 0, Math.PI * 2, true);  // 左眼
    ctx.moveTo(95, 65);
    ctx.arc(90, 65, 5, 0, Math.PI * 2, true);  // 右眼
    ctx.stroke();
  }
```

### 线

- `lineTo(x,y)` 绘制直线

```js
 var canvas = document.getElementById('canvas');
  if (canvas.getContext){
  var ctx = canvas.getContext('2d');

  // 填充三角形
  ctx.beginPath();
  ctx.moveTo(25, 25);
  ctx.lineTo(105, 25);
  ctx.lineTo(25, 105);
  ctx.fill();

  // 描边三角形
  ctx.beginPath();
  ctx.moveTo(125, 125);
  ctx.lineTo(125, 45);
  ctx.lineTo(45, 125);
  ctx.closePath();
  ctx.stroke();
  }
```

### 圆弧 | 圆

- `arc(x,y,radius,startAngle,endAngle,anticlokwise)`
  - (x,y)圆心坐标
  - radius 半径
  - startAngle 开始
  - endAngle 结束
  - anticlokwise 方向 默认顺时针

```js
 var canvas = document.getElementById('canvas');
  if (canvas.getContext){
  var ctx = canvas.getContext('2d');
  ctx.beginPath();
  ctx.arc(50,50,50,0, ath.PI*2,false);
  ctx.stroke();
  }
```

### 矩形

- `rect(x,y,width,height)` 

  moveTo 方法自动设置坐标参数为(0,0)

## Path2D 对象

简化代码和提高性能，用来缓存或记录绘画命令。

- `Path2D(path|d)`  返回一个新初始化的Path2D对象,d:调用svg path 数据构成的字符串，创建新路径

  ```js
  var canvas = document.getElementById('canvas');
    if (canvas.getContext){
      var ctx = canvas.getContext('2d');
  
      var rectangle = new Path2D();
      rectangle.rect(10, 10, 50, 50);
  
      var circle = new Path2D();
      circle.moveTo(125, 35);
      circle.arc(100, 35, 25, 0, 2 * Math.PI);
  
      ctx.stroke(rectangle);
      ctx.fill(circle);
    }
  
  //svg路径
  var canvas = document.getElementById("canvas");
  var ctx = canvas.getContext("2d");
  
  var p = new Path2D("M10 10 h 80 v 80 h -80 Z");
  ctx.fill(p);
  ```

  

## 色彩

- `fillStyle = color` 填充颜色
- `strokeStyle = color`  描边颜色
- `globalAlpha = transparencyValue ` 影响所有属性的透明度，0-1
- 或者直接设置`ctx.strokeStyle|fillStyle = "rgba(255,0,0,0.5)";`

### 调色板

```js
//fillStyle
var ctx = document.getElementById('canvas').getContext('2d');
  for (var i=0;i<6;i++){
    for (var j=0;j<6;j++){
      ctx.fillStyle = 'rgb(' + Math.floor(255-42.5*i) + ',' +
                       Math.floor(255-42.5*j) + ',0)';
      ctx.fillRect(j*25,i*25,25,25);
    }
  }

//strokeStyle
 var ctx = document.getElementById('canvas').getContext('2d');
    for (var i=0;i<6;i++){
      for (var j=0;j<6;j++){
        ctx.strokeStyle = 'rgb(0,' + Math.floor(255-42.5*i) + ',' +
                         Math.floor(255-42.5*j) + ')';
        ctx.beginPath();
        ctx.arc(12.5+j*25,12.5+i*25,10,0,Math.PI*2,true);
        ctx.stroke();
      }
    }
```

## 线型 

- `lineWidth = value` 线宽
- `lineCap = type`  线条末端样式
- `lineJoin = type` 线条与线条间接合处的样式
- `miterLimit = value` 限制当两条线相交时交接处最大长度
- `getLineDash()` 返回包含当前虚线样式，长度为非负偶数的数组。
- `setLineDash(segments)` 虚线样式
- `LineDashOffset = value` 设置虚线样式的起始偏移量。



## 渐变 Gradients

- createLinearGradient(x1,y1,x2,y2) 画线
- createRadialGradient(x1,y1,r1,x2,y2,r2) 画圆
- gradient.addColorStop(position,color) 上色



## 图案样式 Patterns

- `createPattern(image,type)` 
  - image:`image|canvas`
  - type:` repeat|repeat-x|repeat-y|no-repeat`



## 阴影 Shadows

- `shadowOffsetX = float` 阴影在x轴延申距离
- `shadowOffsetY = float`  阴影在y轴延申距离
- `shadowBlur = float`  阴影模糊程度
- `shadowColor = color` 阴影颜色

## 文本

- `fillText(text,x,y[,maxEidth])`
- `strokeText(text,x,y[,maxEidth])`

## 图像

获取需要绘制的图片

- HTMLImageElement 
- HTMLVideoElement
- HTMLCanvasElement
- ImageBitmap

获取在canvas上使用的图片

相同页面的图片引用

- document.images
- document.getElementsByTagName()

其它域名下的图片

- HTMLImageElement 上使用crossOrigin属性

其它canvas元素

- document.getElementsByTagName()
- document.getElementById()

缩放

- drawImage(image,x,y,width,height)

切片

- drawImage(image, sx, sy, sWidth, sHeight, dx, dy, dWidth, dHeight)

## 变形

- save()保存画布所有状态
- restore() 恢复画布所有状态
- translate(x,y) 移动canvas和它的原点到不同的位置
- ratate(angle) 以原点为中心旋转canvas，angle：旋转角度。
- scale(x,y) 缩放画布的水平和垂直单位
- transform(a,b,c,d,e,f)
  - a(m11) 水平方向缩放
  - b(m12) 竖直方向偏移
  - c(m21) 水平方向倾斜偏移
  - d(m22) 竖直方向缩放
  - e(dx) 水平方向移动
  - f(dy) 竖直方向移动
- setTransform(a,b,c,d,e,f)
- resetTransform()