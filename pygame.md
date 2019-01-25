# pygame | Pygame中文文档

## pygame

>Pygame 最顶层的包。

## 函数 & 属性

* pygame.init()  —  初始化所有导入的 pygame 模块
* pygame.quit()  —  卸载所有导入的 pygame 模块
* pygame.error()  —  标准 pygame 异常模块
* pygame.get_error()  —  获得当前错误信息
* pygame.set_error()  —  设置当前错误信息
* pygame.get_sdl_version()  —  获得 SDL 的版本号
* pygame.get_sdl_byteorder()  —  获得 SDL 的字节顺序
* pygame.register_quit()  —  注册一个函数，这个函数将在 pygame 退出时被调用
* pygame.encode_string()  —  对 unicode 或字节对象编码
* pygame.encode_file_path()  —  将 unicode 或字节对象编码为文件系统路径

pygame 包是可供使用的最顶层的包。Pygame 被分成许多子模块，但是并不会影响程序使用 Pygame。

为了方便，在 pygame 中绝大多数的顶级变量被放入名为“pygame.locals”的模块中。意思是说这些变量可通过以下方式导入：

```Python
import pygame
from pygame.locals import *
```

当你导入 pygame 后，所有可用的 pygame 子模块都将自动被导入。需要注意的是，一些 pygame 模块是“可选的”，并且可能无法使用。以防万一，Pygame 将提供了一个占位符对象替代原来的模块，这个对象可用来测试某些功能（变量）是否可用。

## 函数 & 属性详解

`pygame.init()`

初始化所有导入的 pygame 模块。

init() -> (numpass, numfail)

初始化所有导入的 pygame 模块，如果有模块导入失败也不会显示异常，但是将返回一个元组，第一个元素为成功导入的模块数，第二个元素为导入失败的个数。

也许你想分开初始化不同的模块，以提高你程序的运行速度，或者不加载暂时用不到的模块。

重复调用 init() 方法是没问题的，也不会有任何负面影响。即使你已经调用了 pygame.quit() 卸载所有模块也是可以的。

`pygame.quit()`

卸载所有导入的 pygame 模块。

quit() -> None

卸载所有之前被初始化的 pygame 模块。当 python 解释器关闭时，这个方法将被无条件地调用，所以你的程序并不需要调用这个方法，除非你想要终止 pygame 资源，并继续执行其他功能。多次执行这个方法也是没有问题的。

注意：调用这个方法 pygame.quit() 会结束所有模块，但不会结束你的程序。建议用正常结束 python 程序的方法来结束 pygame 程序。

### exception pygame.error

>标准的 pygame 异常。
'
```Python
raise pygame.error(message)
```

当 pygame 或 SDL 操作失败时，将会引发异常。你可以捕获任何可预见的问题并处理异常。报告异常时，会同时显示问题的描述信息。

它是 RuntimeError 异常的子类，用于捕获这些异常。

`pygame.get_error()`

得到当前错误信息。

get_error() -> errorstr

获取 SDL 维护的一个内部错误消息。当标准 pygame.error() 标准 pygame 异常引发时，这些信息将会提供给你。

其实你很少会使用到这个方法的啦。

`pygame.set_error()`

设置当前错误信息。

set_error(error_msg) -> None

设置 SDL 维护的一个内部错误消息。当标准 pygame.error() 标准 pygame 异常引发时，这些信息将会提供给你。

其实你很少会使用到这个方法的啦。

`pygame.get_sdl_version()`

获得 SDL 的版本号。

get_sdl_version() -> major, minor, patch

返回 SDL 库有关版本的 3 个数字。这个版本是在编译时生成的。这个方法可用来得知哪个元件是不能正常使用的。

Pygame 1.7.0 新添加的方法。

`pygame.get_sdl_byteorder()`

获得 SDL 的字节顺序。

get_sdl_byteorder() -> int

获得 SDL 库的字节顺序。返回 LIL_ENDIAN 表示小端字节顺序；返回 BIG_ENDIAN 表示大端字节顺序。

Pygame 1.8 新添加的方法。

`pygame.register_quit()`

注册一个函数，这个函数将在 pygame 退出时被调用。

register_quit(callable) -> None

当调用 pygame.quit() 结束所有模块时，所有通过 register_quit() 方法注册过的函数将被调用。这一切都是自动执行的。

一般的 pygame 用户用不到这个方法。

`pygame.encode_string()`

对 unicode 或字节对象进行编码。

encode_string([obj [, encoding [, errors [, etype]]]]) -> bytes or None

obj：

传入 unicode 类型 -> 编码
传入 bytes 类型 -> 不变
传入其他类型 -> 返回 None
没有传递 obj 参数 -> 引起 SyntaxError 异常

encoding (string)：如果存在则进行编码，默认是 unicode_escape。

errors (string)：指定如何处理无法编码的内容，默认使用反斜杠（\）代替。

etype (exception type)：指定编码错误引发的异常类型。默认为 UnicodeEncodeError，由 PyUnicode_AsEncodedString() 返回。对于默认的编码和错误值不应该有编码错误。

这个函数被用于编码文件路径的时候，支持使用关键字参数。

Pygame 1.9.2 新增加的方法（主要用于单元测试）。

`pygame.encode_file_path()`

将 unicode 或 bytes 对象编码为文件系统路径。

encode_file_path([obj [, etype]]) -> bytes or None

obj：

传入 unicode 类型 -> 编码
传入 bytes 类型 -> 不变
传入其他类型 -> 返回 None
没有传递 obj 参数 -> 引起 SyntaxError 异常

etype（异常类型）：若给出，则出现异常时报相应编码错误，默认为 UnicodeEncodeError，由 PyUnicode_AsEncodedString() 返回。

这个函数被用于编码文件路径的时候，结果由 sys.getfilesystemencoding() 返回，支持使用关键字参数。

Pygame 1.9.2 新增加的方法（主要用于单元测试）。