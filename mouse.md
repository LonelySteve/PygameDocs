# mouse | Pygame中文文档

## pygame.mouse

>Pygame 中与鼠标工作相关的模块。

## 函数

* pygame.mouse.get_pressed()  ——  获取鼠标按键的情况（是否被按下）
* pygame.mouse.get_pos()  ——  获取鼠标光标的位置
* pygame.mouse.get_rel()  ——  获取鼠标一系列的活动
* pygame.mouse.set_pos()  ——  设置鼠标光标的位置
* pygame.mouse.set_visible()  ——  隐藏或显示鼠标光标
* pygame.mouse.get_focused()  ——  检查程序界面是否获得鼠标焦点
* pygame.mouse.set_cursor()  ——  设置鼠标光标在程序内的显示图像
* pygame.mouse.get_cursor()  ——  获取鼠标光标在程序内的显示图像

这些函数可以用于获取目前鼠标设备的情况，也可以改变鼠标在程序内的显示光标。

当设置显示模式之后，事件队列将开始接收鼠标事件。当鼠标按键被按下时会产生 pygame.MOUSEBUTTONDOWN 事件，当鼠标按键被松开时会产生 pygame.MOUSEBUTTONUP 事件。这些事件包含了一个按键属性，用于表示具体由哪个按键所触发。

当鼠标滑轮被滚动时也会产生 pygame.MOUSEBUTTONDOWN 和 pygame.MOUSEBUTTONUP 事件。当鼠标滑轮往上滚动时，按键将会被设置成4；当鼠标滑轮向下滚动时，按键会被设置成 5。

任何时候鼠标移动都会产生一个 pygame.MOUSEMOTION 事件。鼠标的活动被拆分成小而精确的事件。当鼠标运动时，大量的运动事件会被放入相应的队列中等待处理。没有及时清除掉一些运动事件是队列被塞满的主要原因。

如果鼠标光标被隐藏并且输入被当前显示器占用，鼠标会进入虚拟输入模式，在此模式内，鼠标的相关活动不会因为屏幕的边界限制而停止。调用 pygame.mouse.set_visible() 方法和 pygame.event.set_grab() 方法进行设置。

## 函数详解

`pygame.mouse.get_pressed()`

获取鼠标按键的情况（是否被按下）。

get_pressed() -> (button1, button2, button3)

返回一个由布尔值组成的列表，代表所有鼠标按键被按下的情况。True 意味着在调用此方法时该鼠标按键正被按下。

注意1：获取所有的鼠标事件最好是使用 pygame.event.wait() 方法或者 pygame.event.get() 方法，然后检查确认所有事件是 MOUSEBUTTONDOWN、MOUSEBUTTONUP 或者 MOUSEMOTION。

注意2：在 X11 上一些 XServers 使用中间按键仿真机制。当你同时点击按键 1 和 3 时会发出一个按键 2 被按下的事件。

注意3：在使用此方法前记住要先调用 pygame.event.get() 方法，否则此方法将不会工作。

`pygame.mouse.get_pos()`

获取鼠标光标的位置。

get_pos() -> (x, y)

返回鼠标光标的坐标 (x, y)。这个坐标以窗口左上角为基准点。光标位置可以被定位于窗口之外，但是通常被强制性限制在屏幕内。

`pygame.mouse.get_rel()`

获取鼠标一系列的活动。

get_rel() -> (x, y)

返回在调用此方法之前的一系列活动坐标 (x, y)。鼠标光标的相关活动被限制在屏幕范围内，但是通过虚拟输入模式可以突破这个限制。此页面的顶部有虚拟输入模式的描述。

`pygame.mouse.set_pos()`

设置鼠标光标的位置。

set_pos([x, y]) -> None

通过提供相应的参数来设置当前鼠标的位置。如果鼠标光标是可视的，则光标将会跳到新的坐标上。移动鼠标将会产生一个新的 pygame.MOUSEMOTION 事件。

`pygame.mouse.set_visible()`

隐藏或显示鼠标光标。

set_visible(bool) -> bool

如果返回的布尔值为 True，鼠标光标将会是可视的。返回光标在调用该方法之前的可视化情况。

`pygame.mouse.get_focused()`

检查程序界面是否获得鼠标焦点。

get_focused() -> bool

当 pygame 正在接受鼠标输入事件（或者用专业术语说，鼠标正在处于“active”或“focus”状态）返回值为 True。

一般情况下此方法用于窗口模式。在全屏模式下，该方法总会返回 True。

注意：在 MS Windows 系统中，一个窗口可以同时对鼠标和键盘事件保持监听。但是在 X-Windows 系统中，需要用一个窗口监听鼠标事件而另一个窗口监听键盘事件。pygame.mouse.get_focused() 可以表示 pygame 窗口是否在接收鼠标事件。

`pygame.mouse.set_cursor()`

设置鼠标光标在程序内的显示图像。

set_cursor(size, hotspot, xormasks, andmasks) -> None

当鼠标光标是可视的时，它将通过我们提供的位掩码数组显示为一个黑白色的位图。size 指定光标的宽度和高度。hotspot 指定光标的热点位置。xormasks 指定一组字节，用于进行按位异或掩码的计算。andmasks 指定一组字节，用于进行按位与掩码的计算。

光标的宽度必须是 8 的倍数，并且提供的位掩码数组必须与宽度、高度匹配。否则将抛出异常。

关于如何创建一个系统光标，请查看 pygame.cursor 模块。

`pygame.mouse.get_cursor()`

获取鼠标光标在程序内的显示图像。

get_cursor() -> (size, hotspot, xormasks, andmasks)

获取关于系统光标的信息。返回值是与 pygame.mouse.set_cursor() 的传递参数相同的数据。
