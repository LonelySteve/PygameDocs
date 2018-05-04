# joystick | Pygame中文文档

## pygame.joystick

>与游戏杆、游戏手柄、追踪球进行交互的 pygame 模块。

## 函数

* pygame.joystick.init()  —  初始化 joystick 模块
* pygame.joystick.quit()  —  卸载 joystick 模块
* pygame.joystick.get_init()  —  如果 joystick 模块已经初始化，返回 True
* pygame.joystick.get_count()  —  临时设置某些组合键为被按下状态

## 类

* pygame.joystick.Joystick  —  新建一个 Joystick 对象

joystick 模块用来管理电脑上游戏杆类的设备。游戏杆类的设备包括追踪球和游戏手柄。这个模块允许使用多个按钮和“帽键”。计算机可同时管理多个游戏杆类设备。

以 PS4 次世代游戏手柄为例，本文出现的名称含义如下:

![PS4 次世代游戏手柄](https://raw.githubusercontent.com/LonelySteve/PygameDocs/master/77_400_300.jpg)
