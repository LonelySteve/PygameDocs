# movie | Pygame中文文档

## pygame.movie

>Pygame 中播放 MPEG 视频的模块。


## 类

* pygame.movie.Movie  ——  载入一个 MPEG 视频文件。

注意：在由 NT 衍生出的 Windows 版本（例如 XT）中，默认的 SDL directx 视频驱动存在一定问题。对用于播放 MPEG 视频的 pygame.movie pygame 模块，请使用 windib 驱动来替代。在导入 pygame 之前，需要将 SDL_VIDEODRIVER 环境变量设置成 'windib'，使得 windib 处于可用状态。（例子请参考 pygame.examples.movieplayer.main()）

Pygame 可以播放视频和基于MPEG-1编码的视频文件中的音频。视频播放在后台线程中进行，这样使得播放更易于控制。

视频中的音频必须完全控制声音系统。这意味着在视频中的声音播放之前用于载入和运行声音模块的 pygame.mixer 模块必须被还原。一般的处理方式是在视频开始之前调用 pygame.mixer.quit() 方法。在视频结束后，调音器可以被重新初始化。

视频叠加面被绘制在显示器窗口最顶部。在显示器窗口中绘制正常的视频图像，创建一个屏幕外的 Surface 对象并将其指向对应视频。则每一帧图像通过 Surface 绘制到屏幕上。

通过使用 [ffmpeg](http://ffmpeg.org/) 视频转换程序可以将视频转换成 .mpg 格式（MPEG-1 video, MPEG-1 Audio Layer III (MP3) sound)：

```PowerShell
ffmpeg -i <infile> -vcodec mpeg1video -acodec libmp3lame -intra <outfile.mpg>
```

### 类 class pygame.movie.Movie

载入一个 MPEG 视频文件。

Movie(filename) -> Movie
Movie(object) -> Movie

#### 方法

* pygame.movie.Movie.play()  ——  开始播放视频
* pygame.movie.Movie.stop()  ——  停止播放视频
* pygame.movie.Movie.pause()  ——  暂停/继续播放视频
* pygame.movie.Movie.skip()  ——  快进视频播放的位置
* pygame.movie.Movie.rewind()  ——  重新播放视频
* pygame.movie.Movie.render_frame()  ——  设置当前视频帧数
* pygame.movie.Movie.get_frame()  ——  获取当前视频帧数
* pygame.movie.Movie.get_time()  ——  获取当前视频的播放时间
* pygame.movie.Movie.get_busy()  ——  检查当前是否正在播放视频
* pygame.movie.Movie.get_length()  ——  获取视频的总时长（以秒为单位）
* pygame.movie.Movie.get_size()  ——  获取视频的分辨率
* pygame.movie.Movie.has_video()  ——  检查视频文件里是否包含影像
* pygame.movie.Movie.has_audio()  ——  检查视频文件里是否包含音频
* pygame.movie.Movie.set_volume()  ——  设置音量
* pygame.movie.Movie.set_display()  ——  设置视频的目标 Surface 对象

从一个文件或者一个 python 文件对象内载入一个新的 MPEG 视频流。视频对象的控制类似于 pygame.mixer 控制音频对象。

视频对象有一个对应的目标 Surface 对象，视频流通过后台线程被传输到该 Surface 对象中。如果对应的 Surface 对象是窗口 Surface 对象，将会尝试使用硬件加速功能。默认情况下，目标对象即窗口 Surface 对象。

#### 方法详解

`pygame.movie.Movie.play()`

开始播放视频。

play(loops=0) -> None

如果音频和影像均可用，则开始播放音频和影像。

loops 参数控制视频将会重播多少次，如果 loops=-1，则视频将会无限重播。

`pygame.movie.Movie.stop()`

停止播放视频。

stop() -> None

影像和音频的播放将会在他们当前的位置上结束。

`pygame.movie.Movie.pause()`

暂停/继续播放视频。

pause() -> None

暂停/继续视频播放。

`pygame.movie.Movie.skip()`

快进视频播放的位置。

skip(seconds) -> None

以秒为单位快进视频播放的时间点。在视频（设置了播放起始时间）播放之前，该方法可以被调用。该方法仅仅可以向前快进而不能向后倒退。

seconds 参数是一个单精度浮点数。

`pygame.movie.Movie.rewind()`

重新播放视频。

rewind() -> None

设置视频的起始播放位置。如果视频播放结束了，将会自动重新开始播放。

如果视频不能被重播，此方法会产生一个 ValueError 错误。如果重播失败，视频对象会被认为是无效的。

`pygame.movie.Movie.render_frame()`

设置当前视频帧数。

render_frame(frame_number) -> frame_number

此方法需要传递一个整型帧数作为参数。

此方法会尝试把提供的帧数从视频对象传递给对应的 Surface 对象。

此方法会返回设置完成后的实际帧数。

`pygame.movie.Movie.get_frame()`

获取当前视频帧数。

get_frame() -> frame_number

返回当前视频的整形帧数。

`pygame.movie.Movie.get_time()`

获取当前视频的播放时间。

get_time() -> seconds

返回当前的播放时间（以秒为单位的单精度浮点数）。

注意：这个方法目前是坏的，会一直返回 0.0 （这是作者说的）。

`pygame.movie.Movie.get_busy()`

检查当前是否正在播放视频。

get_busy() -> bool

返回一个布尔值表示视频是否正在被播放。

`pygame.movie.Movie.get_length()`

获取视频的总时长（以秒为单位）。

get_length() -> seconds

返回视频的总时长（以秒为单位的单精度浮点数）。

`pygame.movie.Movie.get_size()`

获取视频的分辨率。

get_size() -> (width, height)

视频可以适应任何 Surface 对象的规格，但是此方法返回的是视频的自然规格（即原规格，在视频制作时规定的规格）。

`pygame.movie.Movie.has_video()`

检查视频文件里是否包含影像。

has_video() -> bool

当视频文件里包含影像流时返回 True。

`pygame.movie.Movie.has_audio()`

检查视频文件里是否包含音频。

has_audio() -> bool

当视频文件里包含音频流时返回 True。

`pygame.movie.Movie.set_volume()`

设置音量。

set_volume(value) -> None

value 参数范围为 0.0~1.0。

如果音量设置为 0，则视频的音频将不会被解码。

`pygame.movie.Movie.set_display()`

设置视频的目标 Surface 对象。

set_display(Surface, rect=None) -> None

设置视频的 Surface 对象。

你也可以传递一个用于确定位置的矩形参数，则视频窗口将会移动并调整，直至可以覆盖整个矩形范围。

如果目标 Surface 对象传入 None，则禁止视频解码。