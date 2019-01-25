# version | Pygame中文文档

## pygame.version

>包含 Pygame 版本信息的小模块。

* pygame.version.ver  —  string 类型的版本号
* pygame.version.vernum  —  用元组来表示版本
* pygame.version.rev  —  库版本构建号

这个模块将被自动导入到 pygame 包并且提供了一些变量来检查 pygame 的版本导入。

## 属性详解

`pygame.version.ver`

string 类型的版本号。

ver = '1.2'

这是用 string 类型表示的版本号。它也可以包含更详细的版本号，例如：'1.5.2'

`pygame.version.vernum`

用元组来表示版本。

vernum = (1, 5, 3)

这种类型的版本号可以很容易的和其他相同类型的版本号相比较。

下面是一个检查 Pygame 版本号的例子：

```Python
if pygame.version.vernum < (1, 5):
    print 'Warning, older version of Pygame (%s)' %  pygame.version.ver
    disable_advanced_features = True
```

`pygame.version.rev`

库版本构建号。

rev = 'a6f89747b551+'

检出这个包被构建时仓库的 Mercurial 结点标识符。如果标识符以 '+' 结尾，则这个包包含未提交的更改。请在错误报告中包含这个修订号，特别是对于 Pygame 中未发布工程的构建。
