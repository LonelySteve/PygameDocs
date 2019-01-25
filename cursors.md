# cursors | Pygame中文文档

## pygame.cursors

>Pygame 中使用光标资源的模块。

### 函数

* pygame.cursors.compile()  ——  由纯字符串创建二进制光标数据
* pygame.cursors.load_xbm()  ——  由一个xbm 文件载入光标数据

Pygame 提供对系统硬件光标的控制，并且只支持白色和黑色光标格式。你可以通过使用 pygame.mouse 内的方法控制光标。

cursors 模块包含载入和解码各种光标格式的方法。这些方法允许你简便地将你的光标存储成扩展文件，或者直接作为编码后的 python 字符串存在。

这个模块包含若干个标准光标。pygame.mouse.set_cursor() 方法能够接收若干个参数。所有的参数以单个元组的形式存储，你可以用如下方式调用此方法：

```Python
pygame.mouse.set_cursor(*pygame.cursors.arrow)
```

这个模块也包含了一些格式化字符串形式的光标。在你使用到这些光标之前，你需要把相应字符串传递给 pygame.cursors.compile() 方法。你可以参照如下示例来调用：

```Python
cursor = pygame.cursors.compile(pygame.cursors.textmarker_strings)
pygame.mouse.set_cursor(*cursor)
```

以下变量是可以被用作光标的位图：

* pygame.cursors.arrow
* pygame.cursors.diamond
* pygame.cursors.broken_x
* pygame.cursors.tri_left
* pygame.cursors.tri_right

以下字符串可以通过 pygame.cursors.compile() 函数转换成光标位图：

* pygame.cursors.thickarrow_strings
* pygame.cursors.sizer_x_strings
* pygame.cursors.sizer_y_strings
* pygame.cursors.sizer_xy_strings

### 函数详解

`pygame.cursors.compile()`

由纯字符串创建二进制光标数据。

compile(strings, black=’X’, white=’.’, xor=’o’) -> data, mask

一串连续的字符串可以被用于创建对应系统光标的二进制光标数据。返回值要和 pygame.mouse.set_cursor() 所需要的参数格式相同。

如果你正在创建自己的光标字符串，你可使用任何值来代表白色和黑色像素。一些系统允许你根据系统颜色自己设置一种特殊的切换色，也被称为 xor  色。如果系统不支持 xor 光标，则光标颜色将会变为纯黑色。

字符串的长度必须全部相等，而且可以被 8 整除。一个光标字符串设定示例，如下所示：

```Python
thickarrow_strings = (               #sized 24x24
  "XX                      ",
  "XXX                     ",
  "XXXX                    ",
  "XX.XX                   ",
  "XX..XX                  ",
  "XX...XX                 ",
  "XX....XX                ",
  "XX.....XX               ",
  "XX......XX              ",
  "XX.......XX             ",
  "XX........XX            ",
  "XX........XXX           ",
  "XX......XXXXX           ",
  "XX.XXX..XX              ",
  "XXXX XX..XX             ",
  "XX   XX..XX             ",
  "     XX..XX             ",
  "      XX..XX            ",
  "      XX..XX            ",
  "       XXXX             ",
  "       XX               ",
  "                        ",
  "                        ",
  "                        ")
```

`pygame.cursors.load_xbm()`

由一个xbm 文件载入光标数据。

load_xbm(cursorfile) -> cursor_args
load_xbm(cursorfile, maskfile) -> cursor_args

该方法将根据 XBM 文件的某一个简单子集载入光标。XBM 文件从传统上是被用于保存 UNIX 系统内光标，它们是被用于代表一些简单图像的 ASCII 码。

一些时候，白色和黑色值将会分开在两个独立的 XBM 文件中。你可以通过传递第二个 maskfile 参数将两个图像载入到同一个光标中。

Cursorfile 和 maskfile 参数可以是带有 readlines 方法的 filenames 或者 filelike 对象。

返回值 cursor_args 可以被直接传递给 pygame.mouse.set_cursor() 方法。
