## 1. 浏览器渲染原理
1. 根据HTML构建HTML树（DOM）。
2. 根据CSS构建CSS树（CSSDOM）。
3. DOM 树与 CSSOM 树合并后形成渲染树。
4. Layout 布局（计算大小位置）
5. Paint绘制
6. Compose 合成
   
## 2. CSS动画优化
1. js优化
   1. 使用 requestAnimationFrame。
2. css优化
   1. 使用 will-change 或 translateZ 提升移动的元素。

### [transform 变换 MDN](https://developer.mozilla.org/zh-CN/docs/Web/CSS/transform)
1. 位移 translate
   ```
    transform: translateX(120px);
    transform: translateY (50%);
    transform: translate(120px, 50%);
    transform: translateZ(30px);父元素perspective。
    transform: translate3d(x,y,z);

    translate(-50%,-50%):绝对定位居中。
   ```
2. 缩放 scale
   ```
    transform: scaleX(number);
    transform: scaleY (number);
    transform: slate(number, number);
   ```
3. 旋转 rotate
4. 倾斜 skew
5. 配合transition过度
6. inline不支持transform，需要先变成block

## 3. CSS 动画的两种做法（transition 和 animation）

### [transition 过渡 MDN](https://developer.mozilla.org/zh-CN/docs/Web/CSS/transition)
1. 作用 补充中间帧
2. 语法
   ```
   transition: 属性名 时长 过度方式 延迟;
   transition: left 200ms linear 1s;
   ```
3. all代表所有属性
4. 不能过渡
   1. display: none=>block不能过渡

5. 除了起始，还有中间点。
   1. 使用两次transform
   2. 使用animation
   
### [animation 动画 MDN](https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_Animations/Using_CSS_animations)
1. 声明关键帧
2. 添加动画
3. 语法
   ```
    animation:时长|过渡方式|延迟|次数|方向|填充方式|是否暂停|动画名;
    @keyframes 动画名{
        from{
            transform: ;
        }
        to{
            transform: ;

        }
    }
        @keyframes 动画名{
        0{
            transform: ;
        }
        100%{
            transform: ;

        }
    }

   ```


## 参考
1. [渲染原理](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/render-tree-construction)
2. [渲染性能](https://developers.google.com/web/fundamentals/performance/rendering/)
3. [transform实现动画](https://developers.google.com/web/fundamentals/performance/rendering/stick-to-compositor-only-properties-and-manage-layer-count)
4. [查看css属性](https://csstriggers.com/)
5. 善于利用MDN


