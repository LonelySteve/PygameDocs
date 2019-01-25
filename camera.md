# camera | Pygame中文文档

## pygame.camera

>Pygame 中使用摄像头的模块。

## 函数

* pygame.camera.colorspace()  ——  转换 Surface 对象的色彩空间
* pygame.camera.list_cameras()  ——  返回一个可用摄像头列表

## 类

* pygame.camera.Camera  ——  用于加载摄像头的类

Pygame 目前仅支持 linux 系统和 cameras_Video4Linux2 驱动。

注意！：这些应用程序编程接口可能在之后发行的 Pygame 版本内被改变或者删除。如果你使用了这些应用程序编程接口，你的程序很有可能与之后发行的 Pygame 版本不兼容。

## 函数详解

`pygame.camera.colorspace()`

转换 Surface 对象的色彩空间。

colorspace(Surface, format, DestSurface = None) -> Surface

允许从 RGB 转换到 HSV 或者 YUV。源和目标表面必须是相同大小和像素深度。对于在处理能力有限的设备上的计算机视觉是十分有用。在做任何处理前，尽可能小的捕获图像，使用 transform.scale() 让其变得更小，然后将色彩空间转换为 YUV 或者 HSV。

`pygame.camera.list_cameras()`

返回一个可用摄像头列表。

list_cameras() -> [cameras]

确认电脑是否有可用摄像头并且返回一个可用摄像头名称列表，然后用 pygame.camera.Camera 对象来加载一个摄像头。

## 类 class pygame.camera.Camera

>加载一个摄像头。

Camera(device, (width, height), format) -> Camera

## 方法

* pygame.camera.Camera.start()  ——  打开摄像头、初始化然后开始捕捉画面
* pygame.camera.Camera.stop()  ——  结束摄像头工作，还原并关闭摄像头
* pygame.camera.Camera.get_controls()  ——  获得当前用户设定的值
* pygame.camera.Camera.set_controls()  ——  修改当前摄像头设置（如果摄像头支持的话）
* pygame.camera.Camera.get_size()  ——  返回被记录的图像的尺寸
* pygame.camera.Camera.query_image()  ——  确认一帧图像是否准备好
* pygame.camera.Camera.get_image()  ——  捕获一张图像并转换为一个 Surface 对象
* pygame.camera.Camera.get_raw()  ——  以字符串的形式返回一张未修改的图像

加载一个 V4L2 摄像头。此设备通常类似于 "/dev/video0"。默认宽度和高度是 640 × 480。格式是输出所需的色彩空间。对于计算机视觉效果来说这样做是有用的。默认格式为 RGB。

以下为支持的格式：

* RGB - Red, Green, Blue
* YUV - Luma, Blue Chrominance, Red Chrominance
* HSV - Hue, Saturation, Value

## 方法详解

`pygame.camera.Camera.start()`

打开摄像头、初始化然后开始捕捉画面。

start() -> None

打开摄像设备，尝试将其初始化，并且开始将图像记录到缓冲区。在以下任何功能可以被使用之前，摄像头必须开启。

`pygame.camera.Camera.stop()`

结束摄像头工作，还原并关闭摄像头。

stop() -> None

停止摄像头记录录像的工作，还原摄像头并且将其关闭。一旦摄像头被关闭，以下功能都不能被使用，直到摄像头再次开启。

`pygame.camera.Camera.get_controls()`

获得当前用户设定的值。

get_controls() -> (hflip = bool, vflip = bool, brightness)

如果摄像头支持此功能，get_controls 函数将会返回当前设定值（用布尔值表示的图像是否水平、垂直翻转，用整数值表示的图像亮度）。如果摄像头不支持此功能，将会返回默认值 (0, 0, 0)。

注意：此函数的返回值可能和由 set_controls() 得到的不同，但并不意味着这些返回值有问题。

`pygame.camera.Camera.set_controls()`

修改当前摄像头设置（如果摄像头支持的话）。

set_controls(hflip = bool, vflip = bool, brightness) -> (hflip = bool, vflip = bool, brightness)

如果摄像头支持，则允许你改变当前的摄像头设定。如果摄像头表示改变成功或者不成功但输入值之前就已经在使用了，则返回值等于输入值。每一个参数都是可选的，并且我们需求的某个参数可以通过提供关键字（例如 "hflip"）进行选择。

注意：相机实际所用的设定值可能和 set_controls() 的返回值不同。

`pygame.camera.Camera.get_size()`

返回被记录的图像的尺寸。

get_size() -> (width, height)

返回当前被记录图像的尺寸。如果摄像头不支持在初始化过程中指定的图像尺寸，该函数将会返回图像的真实尺寸。

`pygame.camera.Camera.query_image()`

query_image() -> bool

确认一帧图像是否准备好。

如果一个图像已经成功捕获到，该函数返回 true，否则返回 false。

注意：当调用一个阻塞函数（例如 get_image()）时，一些摄像头将一直返回 false 并且仅将一帧画面放入队列中。这种机制对于从一些没有使用多线程的摄像头中区分游戏帧数是很有用的。

`pygame.camera.Camera.get_image()`

get_image(Surface = None) -> Surface

从缓冲区中取出一张图像转换为一个 RGB 的 Surface 对象。该函数可        以选择性的重用现有的 Surface 对象以节省时间。Surface 对象的位深可以是 24bit 或者与其他可供选择的选项。

`pygame.camera.Camera.get_raw()`

get_raw() -> string

从摄像头获取一张图像，该图像被表示为此摄像头本地像素格式下的一串字符串。此机制有利于和其他库的结合。
