# Overlay | Pygame中文文档

## 类

- class pygame.Overlay

Pygame 中用于视频叠加图形的 pygame 对象。

    Overlay(format, (width, height)) -> Overlay

## 方法

- pygame.Overlay.display  —  设置覆盖像素数据
- pygame.Overlay.set_location  —  控制显示的地方
- pygame.Overlay.get_hardware  —  测试是否支持硬件加速

Overlay 对象对使用硬件视频覆盖提供支持。视频覆盖不使用标准 RGB 像素格式，并且可以使用多个分辨率的数据来创建一个图像。

Overlay 对象使用硬件级别的“低级”访问，所以使用这个对象你必须理解视频覆盖的技术细节。

覆盖的格式决定了使用的像素数据类型。并不是所有的硬件都支持所有类型的覆盖格式。以下是可用的格式类型列表：

    YV12_OVERLAY, IYUV_OVERLAY, YUV2_OVERLAY, UYVY_OVERLAY, YVYU_OVERLAY

宽度和高度参数控制覆盖图像的大小。覆盖的图像大小可任意调整，不仅是覆盖图像的原分辨率。覆盖对象总是可见的，并且总是显示在原图像上方显示。

## 方法详解

`display()`

设置覆盖像素。

`display((y, u, v)) -> None`

`display() -> None`

显示 SDL 的覆盖平面的 YUV 数据。，y、u 和 v 参数都是二进制字符串数据，需使用正确格式的数据以创建覆盖图像。

如果没有参数传入，覆盖的图像仅是当前数据的重新绘制。当覆盖不支持硬件加速，这可能是很有用的。

如果不是合法、可用的字符串数据，将导致崩溃。


`set_location()`

设置覆盖图像的显示位置。

`set_location(rect) -> None`

设置覆盖图图像的位置，覆盖的图像总是显示在原图像的上面，调用此方法并没有立即重绘图像，它将在下一次调用 display() 方法时重新绘制。


`get_hardware()`

测试覆盖是否支持硬件加速。

`get_hardware(rect) -> int`

如果支持硬件加速返回 true，若不支持则会使用软件渲染。
