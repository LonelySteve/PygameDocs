# pygame.examples | Pygame中文文档

## pygame.examples

> 示例程序模块

## 示例模块

- pygame.examples.aliens.main ——游玩完整外星人示例
- pygame.examples.oldalien.main——游玩原版外星人示例
- pygame.examples.stars.main——运行简易星空示例
- pygame.examples.chimp.main——击打移动的黑猩猩
- pygame.examples.moveit.main——在屏幕上显示动画化对象
- pygame.examples.fonty.main——运行字体渲染示例
- pygame.examples.freetype_misc.main——运行一个FreeType类型字体渲染示例
- pygame.examples.vgrade.main——展示垂直渐变
- pygame.examples.eventlist.main——展示pygame事件
- pygame.examples.arraydemo.main——展示各种视觉效果
- pygame.examples.sound.main——加载并播放声音
- pygame.examples.sound_arrary_demos.main——播放各种音效
- pygame.examples.liquid.main——展示液体的动画效果
- pygame.examples.glcube.main——使用OpenGL显示一个旋转的3D立方体
- pygame.examples.scrap_clipboard.main——访问剪切板
- pygame.examples.mask.main——利用碰撞检测显示多个图像相互反弹的情况
- pygame.examples.testsprite.main——展示多个精灵四处移动
- pygame.examples.headless_no_windows_needed.mian——写入一张图像文件为所输入文件平滑后的副本
- pygame.examples.fastevents.main——对fasetevents模块的负载能力测试
- pygame.examples.overlay.main——使用overlays播放.pgm格式的视频
- pygame.examples.blend_fill.main——演示各种suface.fill方法的混合选项
- pygame.examples.cursors.main——展示两个不同的自定义鼠标
- pygame.examples.pixelarray.main——展示各种由pixelarray生成的效果
- pygame.examples.scaletest.main——使用smoothscale交互式地缩放图像
- pygame.examples.midi.main——运行一个midi示例
- pygame.examples.scroll.main——运行Surface.scroll示例展示一个放大的图像
- pygame.examples.camera.main——显示从一个附加的摄像机中拍摄的实时视频
- pygame.examples.playmus.main——播放一个音频文件

这些示例应该有助于你pygame的起步。以下是对你需要学习的东西的一些简要介绍。这些示例的源码是公开的。你可以在自己的项目中随意使用。

有几种方式可以运行这些示例。首先，它们能作为一个独立的程序运行。其次它们可以被导入且它们的main()方法也可以被调用（见下）。最后，最简单的方式就是使用python -m选项：

```shell
python -m pygame.examples.<示例名> <示例参数>
```

示例：

```shell
python -m pygame.examles.scaletest someimage.png
```

这些示例的图像、声音等资源被存放于 pygame/examples/data 的子文件夹中。

通过在python的交互模式下输入下面的命令你可以得知示例文件的存放路径。

```python
>>> import pygame.examples.scaletest
>>> pygame.examples.scaletest.__file__
'/usr/bin/python2.6/site-packages/pygame/examples/scaltest.py'
```

在不同的操作系统及Python版本中，存放的路径都会略有不同。例如，在Windows上，它可能存放于“C:/Python26/Lib/site-packages/pygame/examples/”路径下，而在Mac OS X上，它则可能存放于“/Library/Frameworks/Python.framework/Versions/2.6/lib/python2.6/site-packages/pygame/examples/”

你还能在python的交互模式下通过调用各个包下的main()函数来运行示例。

```python
>>> import pygame.examples.scaletest
>>> pygame.examples.scaletest.main()
```

我们一直在寻找更多的示例和/或示例请求。这样的代码可能是开始参与python游戏编程的最佳方式。
示例作为一个包是pygame 1.9.0的新特性。但多数示例都是在pygame早期就已经有了。
