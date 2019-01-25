# Color | Pygame中文文档

## class pygame.Color

>Pygame 中用于描述颜色的对象。

Color(name) -> Color

Color(r, g, b, a) -> Color

Color(rgbvalue) -> Color

### 方法 & 属性

* pygame.Color.r  —  获取或设置 Color 对象的红色值
* pygame.Color.g  —  获取或设置 Color 对象的绿色值
* pygame.Color.b  —  获取或设置 Color 对象的蓝色值
* pygame.Color.a  —  获取或设置 Color 对象的 alpha 值
* pygame.Color.cmy  —  获取或设置 Color 对象表示的 CMY 值
* pygame.Color.hsva  —  获取或设置 Color 对象表示的 HSVA 值
* pygame.Color.hsla  —  获取或设置 Color 对象表示的 HSLA 值
* pygame.Color.i1i2i3  —  获取或设置 Color 对象表示的 I1I2I3 值
* pygame.Color.normalize()  —  返回 Color 对象的标准化 RGBA 值
* pygame.Color.correct_gamma()  —  应用一定的伽马值调整 Color 对象
* pygame.Color.set_length()  —  设置 Color 对象的长度（成员数量）

Pygame 使用 Color 类表示 RGBA 颜色值，每个颜色值的取值范围是 0 ~ 255。允许通过基本的算术运算创造新的颜色值，支持转换为其他颜色空间，例如 HSV 或 HSL，并让你调整单个颜色通道。当没有给出 alpha 的值是，默认是 255（不透明）。

“RGB值”可以是一个颜色名，一个 HTML 颜色格式的字符串，一个 16 进制数的字符串，或者一个整型像素值。HTML 格式是 "#rrggbbaa"，其中 "rr"，"gg"，"bb"，"aa" 都是 2 位的 16 进制数。代表 alpha 的 "aa" 是可选的。16 进制数的字符串组成形式为 "0xrrggbbaa"，当然，其中的 "aa" 也是可选的。

Pygame 1.9.0 之后，颜色对象支持与其他颜色对象进行等值比较（3 或 4 整型元祖）。

在 Pygame 1.8.1 中有一个 bug，就是 alpha 的默认值被设置为 0，而不是 255。

Color 对象采用 C 级别的接口输出。输出为只读的一维无符号字节数组，分配与 color 对象相同的长度。对于 CPython 2.6 以后的版本，新的缓冲区接口（与数组接口具有相同的特性）也会被输出。Pygame 1.9.2 新增加的。

Color 的新实现在 Pygame 1.8.1 中完成。

### 方法 & 属性详解

`r`

获取或设置 Color 对象的红色值。

r -> int

Color 对象的红色值。

`g`

获取或设置 Color 对象的绿色值。

g -> int

Color 对象的绿色值。

`b`

获取或设置 Color 对象的蓝色值。

b -> int

Color 对象的蓝色值。

`a`

获取或设置 Color 对象的 alpha 值。

a -> int

Color 对象的 alpha 值。

`cmy`

获取或设置 Color 对象表示的 CMY 值。

cmy -> tuple

Color 对象表示的 CMY 值。CMY 每个分量的范围是 C = [0, 1]，M = [0, 1]，Y = [0, 1]。

注意：由于 RGB 值应设为 0 ~ 255，而 CMY 值为 0 ~ 1，因此无法绝对准确地返回所有 RGB 值对应的 CMY 值，会有少许偏差。

注：CMY 是青（Cyan）、洋红或品红（Magenta）和黄（Yellow）三种颜色的简写，是相减混色模式，用这种方法产生的颜色之所以称为相减色，乃是因为它减少了为视觉系统识别颜色所需要的反射光。由于彩色墨水和颜料的化学特性，用三种基本色得到的黑色不是纯黑色，因此在印刷术中，常常加一种真正的黑色（black ink），这种模型称为 CMYK 模型，广泛应用于印刷术。每种颜色分量的取值范围为0~100；CMY常用于纸张彩色打印方面。

`hsva`

获取或设置 Color 对象表示的 HSVA 值。

hsva -> tuple

Color 对象表示的 HSVA 值。HSVA 每个分量的范围是 H = [0, 360]，S = [0, 100]，V = [0, 100]，A = [0, 100]。

注意：由于 RGB 值应设为 0 ~ 255，而 HSV 值为 0 ~ 100 和 0 ~ 360，因此无法绝对准确地返回所有 RGB 值对应的 HSV 值，会有少许偏差。

注：HSV 色彩模型中颜色的参数分别是：色调（H），饱和度（S），亮度（V）。RGB 和 CMY 颜色模型都是面向硬件的，而 HSV（Hue Saturation Value）颜色模型是面向用户的。HSV 模型的三维表示从 RGB 立方体演化而来。设想从 RGB 沿立方体对角线的白色顶点向黑色顶点观察，就可以看到立方体的六边形外形。六边形边界表示色彩，水平轴表示纯度，明度沿垂直轴测量。