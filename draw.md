# draw | Pygame中文文档

## pygame.draw

>Pygame 中绘制图形的模块。

### 函数

* pygame.draw.rect()  —  绘制矩形
* pygame.draw.polygon()  —  绘制多边形
* pygame.draw.circle()  —  根据圆心和半径绘制圆形
* pygame.draw.ellipse()  —  根据限定矩形绘制一个椭圆形
* pygame.draw.arc()  —  绘制弧线
* pygame.draw.line()  —  绘制线段
* pygame.draw.lines()  —  绘制多条连续的线段
* pygame.draw.aaline()  —  绘制抗锯齿的线段
* pygame.draw.aalines()  —  绘制多条连续的线段（抗锯齿）

该模块用于在 Surface 对象上绘制一些简单的形状。这些函数将渲染到任何格式的 Surface 对象上。硬件渲染会比普通的软件渲染更耗时。

大部分函数用 width 参数指定图形边框的大小，如果 width = 0 则表示填充整个图形。

所有的绘图函数仅能在 Surface 对象的剪切区域生效。这些函数返回一个 Rect，表示包含实际绘制图形的矩形区域。

大部分函数都有一个 color 参数，传入一个表示 RGB 颜色值的三元组，当然也支持 RGBA 四元组。其中的 A 是 Alpha 的意思，用于控制透明度。不过该模块的函数并不会绘制透明度，而是直接传入到对应 Surface 对象的 pixel alphas 中。color 参数也可以是已经映射到 Surface 对象的像素格式中的整型像素值。

当这些函数在绘制时，必须暂时锁定 Surface 对象。许多连续绘制的函数可以通过一次性锁定直到画完再解锁来提高效率。

### 函数详解

`pygame.draw.rect()`

绘制矩形。

rect(Surface, color, Rect, width=0) -> Rect

在 Surface 对象上绘制一个矩形。Rect 参数指定矩形的位置和尺寸。width 参数指定边框的宽度，如果设置为 0 则表示填充该矩形。

`pygame.draw.polygon()`

绘制多边形。

polygon(Surface, color, pointlist, width=0) -> Rect

在 Surface 对象上绘制一个多边形。pointlist 参数指定多边形的各个顶点。width 参数指定边框的宽度，如果设置为 0 则表示填充该矩形。

绘制一个抗锯齿的多边形，只需要将 aalines() 的 closed 参数设置为 True 即可。

`pygame.draw.circle()`

根据圆心和半径绘制圆形。

circle(Surface, color, pos, radius, width=0) -> Rect

在 Surface 对象上绘制一个圆形。pos 参数指定圆心的位置，radius 参数指定圆的半径。width 参数指定边框的宽度，如果设置为 0 则表示填充该矩形。

`pygame.draw.ellipse()`

根据限定矩形绘制一个椭圆形。

ellipse(Surface, color, Rect, width=0) -> Rect

在 Surface 对象上绘制一个椭圆形。Rect 参数指定椭圆外围的限定矩形。width 参数指定边框的宽度，如果设置为 0 则表示填充该矩形。

`pygame.draw.arc()`

绘制弧线。

arc(Surface, color, Rect, start_angle, stop_angle, width=1) -> Rect

在 Surface 对象上绘制一条弧线。Rect 参数指定弧线所在的椭圆外围的限定矩形。两个 angle 参数指定弧线的开始和结束位置。width 参数指定边框的宽度。

`pygame.draw.line()`

绘制线段。

line(Surface, color, start_pos, end_pos, width=1) -> Rect

在 Surface 对象上绘制一条线段。两端以方形结束。

`pygame.draw.lines()`

绘制多条连续的线段。

lines(Surface, color, closed, pointlist, width=1) -> Rect

在 Surface 对象上绘制一系列连续的线段。pointlist 参数是一系列短点。如果 closed 参数设置为 True，则绘制首尾相连。

`pygame.draw.aaline()`

绘制抗锯齿的线段。

aaline(Surface, color, startpos, endpos, blend=1) -> Rect

在 Surface 对象上绘制一条抗锯齿的线段。blend 参数指定是否通过绘制混合背景的阴影来实现抗锯齿功能。该函数的结束位置允许使用浮点数。

`pygame.draw.aalines()`

绘制多条连续的线段（抗锯齿）。

aalines(Surface, color, closed, pointlist, blend=1) -> Rect

在 Surface 对象上绘制一系列连续的线段（抗锯齿）。如果 closed 参数为 True，则首尾相连。blend 参数指定是否通过绘制混合背景的阴影来实现抗锯齿功能。该函数的结束位置允许使用浮点数。
