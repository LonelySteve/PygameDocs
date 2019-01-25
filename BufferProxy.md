# BufferProxy | Pygame中文文档

## class pygame.BufferProxy

>BufferProxy 是 Surface 对象通过数组协议导出的一个缓冲对象。

BufferProxy(\<parent>) -> BufferProxy

## 属性 & 方法

* pygame.BufferProxy.parent   —  返回被打包输出的对象
* pygame.BufferProxy.length  —  输出缓冲区的尺寸，以字节为单位
* pygame.BufferProxy.raw  —  一个导出缓冲区的拷贝，存储在单一的字节块中
* pygame.BufferProxy.write()  —  Write raw bytes to object buffer.

BufferProxy 是 Pygame 支持的一种类型，用于作为 Surface.get_buffer() 和 Surface.get_view() 方法的返回值。对于所有版本的 Python，BufferProxy 对象输出一个 C 结构和 Python 级别的数组接口代表其父对象的缓冲区。

对于 CPython2.6 及以后版本，使用了一个新的缓冲区接口输出。在 Pgame 中，BufferProxy 是实现 surfarra 模块（用于通过数组接口访问 Surface 对象的像素数据）的关键。

BufferProxy 实例可以直接通过 Python 代码实现，但无论是作为父对象输出的接口，或者 Python 字典描述的缓冲区布局，该实例（所有的字典项目均基于 Python 级别的数组接口映射方式）均包含以下键：

|键|值（类型）|含义|
|:--:|:--:|:--|
|"shape"|元组|1. 元祖中每个元素表示数组每个维度的长度 </br> 2. 元祖的长度表示数组的维数|
|"typestr"|字符串|用 3 个字符的字符串来描述数组元素的类型：</br> -- 第 1 个字符表示字节顺序：'<' 表示小端；'>' 表示大端（有关大端和小端的起源：[请戳我！](https://fishc.com.cn/home.php?mod=space&uid=9&do=blog&id=1495)）；'\|' 表示不适用 </br> -- 第 2 个字符表示元素的类型：'i' 表示带符号整形；'u' 表示无符号整形；'f' 表示浮点型；'V' 表示字节块 </br> -- 第 3 个字符表示每个元素的字节数：1 ~ 9 个字节 </br> 例如："\<u4" 表示无符号 4 个字节的小端整数，通常是 32 位像素的电脑；而 "\|V3" 则表示 24 位像素（但没有对应的整数）|
|"data"|元组|用一个 2 元祖表示物理缓冲区的起始地址和只读标志：起始地址是整型值，而只读标志是布尔类型（False 表示可写入，True 表示只读）|
|"strides"（可选）|元组|描述步进的信息，需要非 C 的相邻数组，但该元祖的长度必须与 "shape" 相匹配|
|"parent"（可选）|对象|输出对象，用于保持当缓冲区可见时父对象存活|
|"before"（可选）|回调函数|1. 指定当 BufferProxy 实例输出缓冲区时的回调函数 </br> 2. 如果指定 "parent" 对象，该回调函数作为参数传递，否则参数为 None </br> 3. 该回调函数对设置父对象锁有用|
|"after"（可选）|回调函数|1. 指定当 BufferProxy 实例输出缓冲区被释放时的回调函数 </br> 2. 如果指定 "parent" 对象，该回调函数作为参数传递，否则参数为 None </br> 3. 该回调函数对释放父对象锁有用|

该 BufferProxy 类支持的子类，实例变量和弱引用。

## 属性 & 方法详解

`parent`

返回被打包输出的对象。

parent -> Surface
parent -> \<parent>

返回该 BufferProxy 的 Surface 对象，或者调用 BufferProxy 的对象。

`length`

输出缓冲区的尺寸，以字节为单位。

length -> int

导出数据的有效字节数。对于不连续（不在同一块内存中）数据来说，间隙中的字节并不在计算范围内。该属性等同于 C 的 Py_buffer 结构的 len 字段。

`raw`

一个导出缓冲区的拷贝，存储在单一的字节块中。

raw -> bytes

将缓冲区的数据拷贝为 str 或 bytes 对象，导出数据中的任何间隙将被删除。

`write()`

写入原始字节到缓冲区对象中。

write(buffer, offset=0)

覆盖写入父对象中的字节数据。数据必须是连续的 C 或 F，否则将抛出 ValueError 异常。

buffer 参数是 str 或 bytes 对象。

可选参数 offset 指定缓冲区内开始覆盖的起始偏移位置，以字节为单位。

如果偏移量为负数或大于等于缓冲区的尺寸，将抛出 IndexException 异常。

如果 len(buffer) > proxy.length + offset，将抛出 ValueError 异常。
