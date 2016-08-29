# 基础篇

## 1.什么事canvas
canvas是HTML5提供的一个用于展示绘图效果的标签。canvas画布，在HTML页面用于展示页面效果，最早的canvas是苹果提出的一种方案，今天已经在大多数浏览器实现。

## 2.canvas的基本语法
`<canvas></canvas>`
    * 使用canvas标签，即可在页面中开辟一个区域。可以设置width和height，设置该区域的尺寸。
    * 默认canvas的宽高是300和150.
    * 不能够使用css样式进行设置width和height，要使用html属性进行设置。
    * 如果浏览器不支持canvas标签，就会将其解析为div元素。因此常常会在canvas中设置文本，以提示用户浏览器的解析能力。
    * canvas的兼容性很强，只要支持该标签的，基本功能都可以实现，不需要考虑兼容性。
    * canvas本身不能够绘图，需要使用JavaScript才可以绘图。canvas对象提供了各种绘图的API。


## 3.canvas的使用领域
   * 游戏
   * 可视化数据(重点)
   * banner广告
   * 多媒体
   * 未来
        * 模拟仿真
        * 远程操作
        * 图形编辑


# 2.基本的绘图

## 基本的绘图方法

### 2.1步骤
    * 1.获得canvas对象 `var cas = document.getElementById("cas")`
    * 2.获得画布    `平面：var ctx = cas.getContext("2d") 或者 立体：var ctx = cas.getContext("webgl")`
        * 2.1 该方法返回 `CanvasRenderingContext2D`类型的对象，该对象提供基本的绘图命令
        * 2.2 使用`CanvasRenderingContext2D`对象提供的方法进行绘图
    * 3.设置图形的起始点   `ctx.moveTo(x,y)`
    * 4.设置图形的结束点   `ctx.lineTo(x,y)`
    * 5.将起始点和结束点连接起来，描边绘制 `ctx.stroke()`
    * 6.填充绘制 `ctx.fill()`
    * 7.闭合路径 `ctx.closePath()`

### 2.2绘制基本线

```
    <script>
        //1.获得对象,需要绘图就需要有canvas标签，该标签用于展示图像，canvas的宽高不能使用css来设置，会有拉伸问题，应该直接使用HTML属性来设置。canvas只是展示图像的标签，她没有绘图的能力。需要使用canvas的上下文工具来实现绘图。
        var cas = document.getElementById("cas");
        //2.获得画布。使用canvas.getContext("2d")可以获得绘图工具，该工具是CanvasRenderingContext2d类型的对象。
        var ctx = cas.getContext("2d");
        //3.首先要设置绘图的起始位置。然后在起点的基础上在绘制其他点
        ctx.moveTo(0,0);
        //4.结束位置
        ctx.lineTo(800,600);
        //5.设置起始位置
        ctx.moveTo(800,0);
        //6.设置结束位置
        ctx.lineTo(0,600);
        //7.描边显示效果
        ctx.stroke();
    </script>
```
### 2.3计算机的直角坐标系

计算机中X往右边是正方向，Y轴往下边是正方向。

### 2.4 getContext方法

语法:`canvas.getContext()`

描述：
    1. 该方法用于绘制上下文的工具
    2. 如果是绘图，平面使用"2d"作为参数，绘制立体图形使用"webgl"
    3. 使用2d返回`CanvasRenderingContext2d`对象
    4. 使用`webg1` 返回 `WebGLRenderingContext`类型的对象

### 2.5 moveTo方法

语法：CanvasRenderingContext2D.moveTo(x,y);

描述：
    * 该方法用于绘制起始点
    * 参数x/y表示坐标系中的位置，分别是x坐标和y坐标


### 2.6 lineTo 方法

语法: CanvasRenderingContext2D.lineTo(x,y);

描述：
    * 1.该方法用于设置需要绘制直线的另一个点，最终描边后会连线当前点和方法参数描述的点
    * 2.参数x/y表示坐标系中的位置，分别是x坐标和y坐标


### 2.7 stroke 方法

语法: CanvasRenderingContext.stroke();

描述：
    * 该方法用于连线，将描述的所有点按照指定的顺序连接起来

## 结论
    * 绘图先要获得上下文
    * 绘图需要设置开始的坐标
    * 绘图是先描点，然后在一点一点进行连线
    * 依次绘图只能绘制单一样式

### 练习题：
    * 绘制直线计算坐标
    * 描边 CanvasRenderingContext2d.stroke();
    * 填充 CanvasRenderingContext2d.fill();

###  fill方法

    * 语法:`CanvasRenderingContext2d.fill()`
    * 描述:该方法按照描绘的点的路径来填充图形，默认是黑色

## 3.非零环绕原则
    * 在canvas中使用各个方法描点实际上是描述的是一个称为路径(path)的东西。
    * 在canvas绘图中，所有描述的东西都是路径，只有最后填充或者描边的时候才会显示除效果
    * 每一个路径都是一个状态

## 4.闭合路径

## 4.1 closePath

用法： `CanvasRenderingContext2d.closePath()`
描述：使用该方法可以将最后一个描点与最开始的描点自动连接起来。

```
    <script>
        var cas = document.getElementById("cas");
        var ctx = cas.getContext("2d");
        ctx.moveTo(100,100);
        ctx.lineTo(300,100);
        ctx.lineTo(100,300);
        ctx.lineTo(200,0);
        ctx.lineTo(300,300);
        ctx.closePath();
        ctx.stroke()
    </script>
```
## 5.路径的概念

### 5.1 路径就是一次画图
    * canvas中一个统一的状态，属性和方法。


## 6.线性相关的属性
    * `1.CanvasRenderingContext2d.lineWidth` 设置线宽(number)
    * `2.CanvasRenderingContext2d.lineCap` 设置线末端类型(round/squre/butt(默认))
    * `3.CanvasRenderingContext2d.lineJoin` 设置相交线的拐点(round(圆角连接)/bevel(平且连接)/miter(默认))
    * `4.CanvasRenderingContext2d.getLineDash()` 获取线段样式的数组
    * `5.CanvasRenderingContext2d.setLineDash()` 设置线段样式(用于设置开始绘制虚线的偏移量，数字的正负表示左右偏移)
    * `6.CanvasRenderingContext2d.lineDashOffset` 设置线段的偏移量(number)

##  6.1 设置线宽
    * 语法:`CanvasRenderingContext2d.lineWidth=number`
    * 描述：设置线宽


## 6.2 填充与描边样式
```
    CanvasRenderingContext2d.strokeStyle = value;//设置描边的颜色
    CanvasRenderingContext2d.fillStyle = value;//设置填充颜色
    //两个颜色组合可以设置渐变


```