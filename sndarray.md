# sndarray | Pygame中文文档

## pygame.sndarray

>Pygame 中访问音频采样数据的模块。

## 函数

* pygame.sndarray.array  ——  将一个音频采样复制到一个数组内
* pygame.sndarray.samples  ——  将一个音频采样引用到一个数组内
* pygame.sndarray.make_sound  ——  将一个数组转变成一个音频对象
* pygame.sndarray.use_arraytype  ——  设置用于音频数组的数组系统
* pygame.sndarray.get_arraytype  ——  获取当前正在使用的数组类型
* pygame.sndarray.get_arraytypes  ——  获取当前正在工作的数组系统类型

以上函数用于在数字数组和音频对象之间进行相互转换。

本模块仅当 pygame 可以使用 numpy 或 Numeric 模块时是有效的（Numeric 相对过时了，请使用最新的 numpy）。

音频数据是由每秒数千个采样组成，而且每个采样都是特定时刻的音波的振幅。例如，在 22-kHz 格式里，音频数组的第 5 个元素是音波在 5/22000 秒后的振幅。

每个采样是一个 8 位或者 16 位的整数，这取决于数据格式。一个立体声文件里每个采样有两个值，而单声道文件里每个采样只有一个值。

支持的数组系统有：

* numpy
* Numeric（过时，将在 Pygame 1.9.3 中弃用）

如果安装了 numpy 模块，那么默认使用的是 numpy 数组。否则将会被设置成 Numeric（如果有安装），但会产生一个反对的警告（说这玩意儿快过时了，建议使用 numpy 代替）。

如果 numpy 和 Numeric 都没有安装，本模块会产生一个 ImportError 错误。

通过使用 use_arraytype() 函数，可以改变使用的数组类型（将字符串 "numpy" 或 "Numeric" 作为参数）。

注意：numpy 和 Numeric 并不是完全兼容。对于某一种数组类型来说的一个正确操作，可能在另外一种数组类型中会产生不同的效果，甚至导致彻底的崩溃。

此外，相比于 Numeric，numpy 可以使用无符号 16 位整数。如果音频采样类型需要，16 位的音频数据可以被当做无符号整数使用。而 Numeric 则总是使用有符号整数表示采样数据。这十分重要，请务必牢记。

在 Pygame 1.8 中加入对 numpy 的支持，并于 Pygame 1.9.2 开始反对使用 Numeric 。

## 函数详解

`pygame.sndarray.array()`

将一个音频采样复制到一个数组内。

array(Sound) -> array

创建一个新的数组用于保存音频数据，并将采样值复制到数组内。

这个数组将一直保持由 pygame.mixer.get_init() 所返回的格式。

`pygame.sndarray.samples()`

将一个音频采样引用到一个数组内。

samples(Sound) -> array

创建一个直接引用音频对象内的采样的新数组。修改这个数组将会改变音频。

这个数组将一直保持由 pygame.mixer.get_init() 所返回的格式。

`pygame.sndarray.make_sound()`

将一个数组转变成一个音频对象。

make_sound(array) -> Sound

根据一个音频数组，创建一个可播放的音频对象。

mixer 模块必须先初始化，且数组格式必须与 mixer 音频格式相似。

`pygame.sndarray.use_arraytype()`

设置用于音频数组的数组系统。

use_arraytype (arraytype) -> None

使用模块函数所要求的数组类型。目前支持的数组类型为：

* numpy
* Numeric（过时，将在 Pygame 1.9.3 中弃用）

如果要求的类型不被支持，会产生一个 ValueError 的错误。

`pygame.sndarray.get_arraytype()`

获取当前正在使用的数组类型。

get_arraytype () -> str

返回当前正在使用的数组的类型。

此函数返回的是 get_arraytypes() 的返回元组内的一个值，而且会表明哪种数组模块类型被用于创建该数组。

`pygame.sndarray.get_arraytypes()`

获取当前正在工作的数组系统类型

get_arraytypes () -> tuple

检查哪个数组系统是可使用的然后返回相应的字符串元组。

元组的值可以被直接用于 pygame.sndarray.use_arraytype() 函数。如果没有发现受支持的数组系统类型，返回 None。
