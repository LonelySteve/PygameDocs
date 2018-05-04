# locals | Pygame中文文档

## pygame.locals

> Pygame 定义的常量。

这个模块包含了 Pygame 定义的各种常量。它的内容会被自动放入到 Pygame 模块的名字空间中。你可以使用“from pygame.locals import *”将所有的 Pygame 常量导入。

各个常量的详细描述记录在 Pygame 各个模块的相关文档中。比如 pygame.display.set_mode() 方法用到的 HWSURFACE 常量，你就可以在 display 模块的文档中找到详细的说明；事件类型在 event 模块的文档中可以找到；当产生 KEYDOWN 或 KEYUP 事件时，key 属性描述具体哪个按键被按下，该值是以 K_ 开头的常量（MOD_ 开头的常量表示各种组合键被按下），在 key 模块的文档中可以找到；最后，TIME_RESOLUTION 被定义在 time 模块中。