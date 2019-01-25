# gfxdraw | Pygame中文文档

## pygame.gfxdraw

>Pygame 中绘制图形的模块。

## 函数

* pygame.gfxdraw.pixel()  ——  绘制一个像素点
* pygame.gfxdraw.hline() ——  绘制一条水平线
* pygame.gfxdraw.vline()  ——  绘制一条垂直线
* pygame.gfxdraw.rectangle()  ——  绘制一个矩形边框
* pygame.gfxdraw.box()  ——  绘制一个填充的矩形
* pygame.gfxdraw.line()  ——  绘制一条直线
* pygame.gfxdraw.circle()  ——  绘制一个圆形边框
* pygame.gfxdraw.arc()  ——  绘制一条弧线
* pygame.gfxdraw.aacircle()  ——  绘制一个平滑（抗锯齿）的圆形
* pygame.gfxdraw.filled_circle()  ——  绘制一个填充的圆形
* pygame.gfxdraw.ellipse()  ——  绘制一个椭圆形边框
* pygame.gfxdraw.aaellipse()  ——  绘制一个平滑（抗锯齿）的椭圆形
* pygame.gfxdraw.filled_ellipse()  ——  绘制一个填充的椭圆形
* pygame.gfxdraw.pie()  ——  绘制一个扇形边框
* pygame.gfxdraw.trigon()  ——  绘制一个三角形边框
* pygame.gfxdraw.aatrigon()  ——  绘制一个平滑（抗锯齿）的三角形
* pygame.gfxdraw.filled_trigon()  ——  绘制一个填充的三角形
* pygame.gfxdraw.polygon()  ——  绘制一个多边形边框
* pygame.gfxdraw.aapolygon()   ——  绘制一个平滑（抗锯齿）的多边形
* pygame.gfxdraw.filled_polygon()  ——  绘制一个填充的多边形
* pygame.gfxdraw.textured_polygon()  ——  绘制一个纹理填充的多边形
* pygame.gfxdraw.bezier()  ——  绘制一条贝塞尔曲线

注意：当前版本 API 函数可能会在下一个版本发生改变或者取消。如果你要使用这个实验性的模块，你的代码将可能会与之后的 Pygame 版本不兼容。

在一个 Surface 上绘制出几种图形。

大多数函数中有一个表示 RGB 色彩的三元组参数，有时也接收一个表示 RGBA 色彩的四元组参数，色彩参数也可以是已经映射到 Surface 对象内的像素格式下的一个整数值。

所有函数的参数都使用固定坐标，坐标和圆的半径仅支持整数描述。

对于类似绘制矩形函数，尽管传入一个 pygame.Rect 对象才是首选，但也可以接收一个用于描述 rect 的参数，像 (x, y, w, h) 序列。注意，对于一个 pygame.Rect 对象来说，矩形将不包含右边和底边。因此，对于 Rect 的 right 和 bottom 属性的值其实是不再矩形上的。

绘制平滑和填充的图形，首先使用抗锯齿版本的函数（"aa" 开头的那些），然后使用填充版本的函数。

例如：

col = (255, 0, 0)
surf.fill((255, 255, 255))
pygame.gfxdraw.aacircle(surf, x, y, 30, col)
pygame.gfxdraw.filled_circle(surf, x, y, 30, col)
复制代码

注意：pygame 不会自动导入 pygame.gfxdraw 模块（因为目前来说，这还是一个实验性的模块），所以你需要在使用之前自己导入。

线程提示：在调用 C 语言函数部分，都会释放 GIL（Global Interpreter Lock，全局解释器锁）。

pygame.gfxdraw 模块不同于 draw 模块的 API 函数使用，并且绘制的图形也不一样。因为它打包了 SDL_gfx 库的原函数，而非使用修订后的版本。

### 函数详解

`pygame.gfxdraw.pixel()`

绘制一个像素点。

pixel(surface, x, y, color) -> None

在 Surface 对象上绘制一个像素点。

`pygame.gfxdraw.hline()`

绘制一条水平线。

hline(surface, x1, x2, y, color) -> None

在 Surface 对象上的 y 坐标处，绘制一条从 x1 到 x2 的直线。

`pygame.gfxdraw.vline()`

绘制一条垂直线。

vline(surface, x, y1, y2, color) -> None

在 Surface 对象上的 x 坐标处，绘制一条从 y1 到 y2 的直线。

`pygame.gfxdraw.rectangle()`

绘制一个矩形边框。

rectangle(surface, rect, color) -> None

在 Surface 对象上绘制一个矩形边框，rect 参数指定矩形的区域。

记住，Surface.fill() 方法也可以用于绘制填充矩形。事实上，Surface.fill() 可以在一些平台上可以使用硬件加速，无论是软件还是硬件显示模式。

`pygame.gfxdraw.box()`

绘制一个填充的矩形。

box(surface, rect, color) -> None

在 Surface 对象上绘制一个填充的矩形。

`pygame.gfxdraw.line()`

绘制一条直线。

line(surface, x1, y1, x2, y2, color) -> None

在 Surface 对象上绘制一条直线，没有 endcaps。

`pygame.gfxdraw.circle()`

绘制一个圆形。

circle(surface, x, y, r, color) -> None

在 Surface 对象上绘制一个圆形边框。坐标参数 (x,y) 决定圆心的位置，r 参数决定半径长度。没有用颜色进行填充。

`pygame.gfxdraw.arc()`

绘制一条弧线。

arc(surface, x, y, r, start, end, color) -> None

在 Surface 对象上绘制一条弧线。

`pygame.gfxdraw.aacircle()`

绘制一个平滑（抗锯齿）的圆形。

aacircle(surface, x, y, r, color) -> None

在 Surface 对象上绘制一个平滑（抗锯齿）的圆形。

`pygame.gfxdraw.filled_circle()`

绘制一个填充的圆形。

filled_circle(surface, x, y, r, color) -> None

在 Surface 对象上绘制一个填充的原型，填充的颜色由 color 参数指定。

`pygame.gfxdraw.ellipse()`

绘制一个椭圆形边框。

ellipse(surface, x, y, rx, ry, color) -> None

在 Surface 对象上绘制一个椭圆形边框。

`pygame.gfxdraw.aaellipse()`

绘制一个平滑（抗锯齿）的椭圆形。

aaellipse(surface, x, y, rx, ry, color) -> None

在 Surface 对象上绘制一个平滑（抗锯齿）的椭圆形。

`pygame.gfxdraw.filled_ellipse()`

绘制一个填充的椭圆形。

filled_ellipse(surface, x, y, rx, ry, color) -> None

在 Surface 对象上绘制一个填充的椭圆形，填充的颜色由 color 参数指定。

`pygame.gfxdraw.pie()`

绘制一个扇形边框。

pie(surface, x, y, r, start, end, color) -> None

在 Surface 对象上绘制一个扇形边框。

`pygame.gfxdraw.trigon()`

绘制一个三角形边框。

trigon(surface, x1, y1, x2, y2, x3, y3, color) -> None

在 Surface 对象上绘制一个三角形边框。

`pygame.gfxdraw.aatrigon()`

绘制一个平滑（抗锯齿）的三角形。

aatrigon(surface, x1, y1, x2, y2, x3, y3, color) -> None

在 Surface 对象上绘制一个平滑（抗锯齿）的三角形。

`pygame.gfxdraw.filled_trigon()`

绘制一个填充的三角形。

filled_trigon(surface, x1, y1, x2, y2, x3, y3, color) -> None

在 Surface 对象上绘制一个填充的三角形，填充的颜色由 color 参数指定。

`pygame.gfxdraw.polygon()`

绘制一个多边形边框。

polygon(surface, points, color) -> None

在 Surface 对象上绘制一个多边形边框。

`pygame.gfxdraw.aapolygon()`

绘制一个平滑（抗锯齿）的多边形。

aapolygon(surface, points, color) -> None

在 Surface 对象上绘制一个平滑（抗锯齿）的多边形

`pygame.gfxdraw.filled_polygon()`

绘制一个填充的多边形。

filled_polygon(surface, points, color) -> None

在 Surface 对象上绘制一个填充的多边形，填充的颜色由 color 参数指定。

`pygame.gfxdraw.textured_polygon()`

绘制一个纹理填充的多边形。

textured_polygon(surface, points, texture, tx, ty) -> None

在 Surface 对象上绘制一个纹理填充的多边形。

一个带 alpha 通道的纹理绘制到另一个带 alpha 通道的 Surface 对象上，将不同于使用 Surface.blit() 绘制。

带 alpha 通道的纹理不能被用于一个 8 位单像素的目标。

`pygame.gfxdraw.bezier()`

绘制一条贝塞尔曲线。

bezier(surface, points, steps, color) -> None

在 Surface 对象上绘制一条贝塞尔曲线。
