

# Canvas的基本原理与操作

## 定义和用法 

Canvas是HTML5新增的组件，它就像一块幕布，可以用JavaScript在上面绘制各种图表、动画等。

没有Canvas的年代，绘图只能借助Flash插件实现，页面不得不用JavaScript和Flash进行交互。有了Canvas，我们就再也不需要Flash了，直接使用JavaScript完成绘制。

<canvas> 标签定义图形，比如图表和其他图像。

<canvas> 标签只是图形容器，您必须使用脚本来绘制图形。

## 实例

一个Canvas定义了一个指定尺寸的矩形框，，在这个范围内我们可以随意绘制

```
<canvas id="test-canvas" width="300" height="200"></canvas>
```

由于浏览器对HTML5标准支持不一致，所以，通常在`<canvas>`内部添加一些说明性HTML代码，如果浏览器支持Canvas，它将忽略`<canvas>`内部的HTML，如果浏览器不支持Canvas，它将显示`<canvas>`内部的HTML：

```
<canvas id="test-stock" width="300" height="200">
    <p>Current Price: 25.51</p>
</canvas>
```

在使用Canvas前，用`canvas.getContext`来测试浏览器是否支持Canvas：

```
<!-- HTML代码 -->
<canvas id="test-canvas" width="200" heigth="100">
    <p>你的浏览器不支持Canvas</p>
</canvas>
```

### 1、绘制一条线

第一步 ：获取绘图环境对象 画笔  2d或3d(没有功能)

```
var ctx = canvas.getContext('2d');
```

第二步：开始路径

~~~var ctx = canvas.getContext('2d');
ctx.beginPath();
~~~

第三步：设置起点

~~~ctx.moveTo(100,100);
ctx.moveTo(100,100);
~~~

第四步：设置终点（可以设置多个）

```
ctx.lineTo(300,100);
```

设置线的颜色

```
ctx.strokeStyle = "black";
```

设置线宽

```
ctx.lineWidth = 30;
```

第五步：绘制

```
ctx.stroke();
```

![屏幕快照 2018-01-06 下午3.30.13](/Users/dllo/Desktop/屏幕快照 2018-01-06 下午3.30.13.png)

### 2、绘制文字

```
ctx.fillText("Hello World",100,100);
```

![屏幕快照 2018-01-06 下午3.31.51](/Users/dllo/Desktop/屏幕快照 2018-01-06 下午3.31.51.png)

### 3、画圆

arc(圆心x,圆心y,半径,起始弧度,结束弧度,boolean(true:逆时针 false:顺时针))

```
ctx.arc(250,250,100,0,Math.PI*2);
```

填充颜色

```
ctx.fillStyle = "brown";
ctx.fill();
```

![屏幕快照 2018-01-06 下午3.54.17](/Users/dllo/Desktop/屏幕快照 2018-01-06 下午3.54.17.png)

### 4、绘制图片

创建图片对象

```
var theImg = new Image();
theImg.src = "img/八哥犬.jpg"
theImg.onload = function (ev) {
        //drawImage(图片对象,起始位置(左上角坐标):X Y)
        // ctx.drawImage(this,10,0);

        //drawImage(图片对象,起始位置(左上角坐标):X Y,图片宽高：W H)
        // ctx.drawImage(this,100,100,300,300);

        //drawImage(图片对象,图片截取位置X Y，截取宽高W H,绘制到画布的起始位置(左上角坐标):X Y,绘制宽高：W H)
        ctx.drawImage(this,10,10,100,100,20,20,200,200);
    }
```

![屏幕快照 2018-01-06 下午3.56.49](/Users/dllo/Desktop/屏幕快照 2018-01-06 下午3.56.49.png)

Canvas除了能绘制基本的形状和文本，还可以实现动画、缩放、各种滤镜和像素转换等高级操作。如果要实现非常复杂的操作，考虑以下优化方案：

- 通过创建一个不可见的Canvas来绘图，然后将最终绘制结果复制到页面的可见Canvas中；
- 尽量使用整数坐标而不是浮点数；
- 可以创建多个重叠的Canvas绘制不同的层，而不是在一个Canvas中绘制非常复杂的图；
- 背景图片如果不变可以直接用`<img>`标签并放到最底层。

