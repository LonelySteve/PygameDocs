# pygame.mixer | Pygame中文文档

## pygame.mixer

> 用于加载和播放声音的pygame模块

## 函数

* pygame.mixer.init  —  初始化混音器模块
* pygame.mixer.pre_init  —  预设混音器初始化参数
* pygame.mixer.quit  —  未初始化混音器
* pygame.mixer.get_init  —  测试混音器是否初始化
* pygame.mixer.stop  —  停止播放所有声道
* pygame.mixer.pause  —  暂时停止播放所有声道
* pygame.mixer.unpause  —  恢复暂停播放声道
* pygame.mixer.fadeout  —  停止前淡出所有声音的音量
* pygame.mixer.set_num_channels  —  设置播放频道的总数
* pygame.mixer.get_num_channels  —  获取播放频道的总数
* pygame.mixer.set_reserved  —  预留频道自动使用
* pygame.mixer.find_channel  —  找到一个未使用的频道
* pygame.mixer.get_busy  —  测试是否混合了任何声音
* pygame.mixer.Sound  —  从文件或缓冲区对象创建新的Sound对象
* pygame.mixer.Channel  —  创建一个Channel对象来控制播放

此模块包含用于加载Sound对象和控制回放的类。混音器模块是可选的，取决于SDL_mixer。您的程序应该测试pygame.mixerpygame模块在加载和播放声音之前是否可用并在使用之前初始化。

调音台模块具有有限数量的声道播放声道。通常程序会告诉pygame开始播放音频，它会自动选择一个可用的频道。默认为8个并发通道，但复杂的程序可以更精确地控制通道数量及其使用。

所有声音播放都混合在后台线程中。当您开始播放Sound对象时，它会在声音继续播放时立即返回。单个Sound对象也可以多次主动播放。

调音台还有一个特殊的流媒体通道。这是用于音乐播放，可通过pygame.mixer.musicpygame模块访问，以控制流式音频模块。

混音器模块必须像其他pygame模块一样初始化，但它有一些额外的条件。该pygame.mixer.init()函数采用几个可选参数来控制播放速率和样本大小。Pygame将默认为合理的值，但pygame无法执行声音重采样，因此应初始化混音器以匹配音频资源的值。

注意：不要减少迟钝的声音，使用较小的缓冲区大小。默认设置为减少某些计算机上发出沙哑声音的可能性。您可以通过调用更改默认缓冲pygame.mixer.pre_init()预设混频器初始化参数之前 pygame.mixer.init()初始化混频器模块或pygame.init()初始化所有进口pygame的模块被调用。例如： 在pygame 1.8中，默认大小从1024更改为3072。pygame.mixer.pre_init(44100,-16,2, 1024)

## 函数详解

`pygame.mixer.init()`

初始化混音器模块

init(frequency=22050, size=-16, channels=2, buffer=4096) -> None

初始化混音器模块以进行声音加载和播放。可以覆盖默认参数以提供特定的音频混合。关键字参数被接受。对于参数设置为零的向后兼容性，使用默认值（可能由pre_init调用更改）。

size参数表示每个音频样本使用的位数。如果值为负，则将使用带符号的样本值。正值表示将使用未签名的音频样本。无效值会引发异常。

pygame 2中的新功能（使用SDL2编译时） - 大小可以是32（32位浮点数）。

channels参数用于指定是使用单声道还是立体声。1表示单声道，2表示立体声。不支持其他值（负值被视为1，大于2的值被视为2）。

buffer参数控制混音器中使用的内部采样数。默认值应适用于大多数情况。可以降低它以减少延迟，但可能会发生声音丢失。它可以被提升到更大的值，以确保播放永远不会跳过，但它会对声音播放施加延迟。缓冲区大小必须是2的幂（如果不是，则向上舍入到下一个最接近的2的幂）。

某些平台需要pygame.mixerpygame模块来加载和播放声音模块，以便在显示模块初始化后进行初始化。顶级pygame.init() 自动处理此问题，但无法将任何参数传递给混合器init。为了解决这个问题，混频器具有pygame.mixer.pre_init()在使用顶层初始化之前设置正确默认值的功能。

不止一次调用它是安全的，但是在初始化混音器后，如果没有先调用 pygame.mixer.quit()，则无法更改播放参数 。

`pygame.mixer.pre_init()`

预设混音器初始化参数

pre_init(frequency=22050, size=-16, channels=2, buffersize=4096) -> None

调用pre_init可以更改调用real时使用的默认值 pygame.mixer.init()。关键字参数被接受。设置自定义混音器播放值的最佳方法是 pygame.mixer.pre_init()在调用顶级之前调用pygame.init()。对于向后兼容性参数，零值将替换为启动默认值。

`pygame.mixer.quit()`

退出混音器

quit() -> None

这将pygame.mixer取消初始化pygame模块以加载和播放声音。如果稍后重新初始化，则所有播放将停止并且任何加载的Sound对象可能与调音台不兼容。

`pygame.mixer.get_init()`

测试混音器是否初始化

get_init() -> (frequency, format, channels)

如果混合器已初始化，则返回正在使用的回放参数。如果混音器尚未初始化，则返回None

`pygame.mixer.stop()`

停止播放所有声道

stop() -> None

这将停止所有有效混音器通道的所有播放。

`pygame.mixer.pause()`

暂时停止播放所有声道

pause() -> None

这将暂时停止有效混音器通道上的所有播放。稍后可以恢复播放pygame.mixer.unpause()

`pygame.mixer.unpause()`

恢复暂停播放声道

unpause() -> None

这将在暂停后恢复所有活动声道。

`pygame.mixer.fadeout()`

停止前淡出所有声音的音量

fadeout(time) -> None

这将在时间参数上淡出所有活动通道上的音量，以毫秒为单位。声音静音后，播放将停止。

`pygame.mixer.set_num_channels()`

设置播放频道的总数

set_num_channels(count) -> None

设置调音台的可用频道数。默认值为8.可以增加或减少该值。如果该值减小，则截断的通道上播放的声音将停止。

`pygame.mixer.get_num_channels()`

获取播放频道的总数

get_num_channels() -> count

返回当前活动的播放通道数。

`pygame.mixer.set_reserved()`

预留频道自动使用

set_reserved(count) -> None

调音台可以保留任意数量的通道，这些通道不会被声音自动选择播放。如果声音当前正在预留频道播放，则不会停止。

这允许应用程序为重要声音保留特定数量的声道，这些声音不得被丢弃或具有可保证的频道。

`pygame.mixer.find_channel()`

找到一个未使用的频道

find_channel(force=False) -> Channel

这将找到并返回一个非活动的Channel对象。如果没有非活动通道，则此功能将返回None。如果没有非活动通道且force参数为True，则会找到运行时间最长的声道并返回它。

如果调音台有保留频道，pygame.mixer.set_reserved()则此处不会返回这些频道。

`pygame.mixer.get_busy()`

测试mixer 是否正忙

get_busy() -> bool

如果混音器正忙，则返回True。如果混音器处于空闲状态，则返回False。

## pygame.mixer.Sound

> 从文件或缓冲区对象创建新的Sound对象

Sound(filename) -> Sound
Sound(file=filename) -> Sound
Sound(buffer) -> Sound
Sound(buffer=buffer) -> Sound
Sound(object) -> Sound
Sound(file=object) -> Sound
Sound(array=object) -> Sound

* pygame.mixer.Sound.play  —  开始播放声音
* pygame.mixer.Sound.stop  —  停止声音播放
* pygame.mixer.Sound.fadeout  —  淡出后停止声音播放
* pygame.mixer.Sound.set_volume  —  设置此声音的播放音量
* pygame.mixer.Sound.get_volume  —  获取播放音量
* pygame.mixer.Sound.get_num_channels  —  计算此声音播放的次数
* pygame.mixer.Sound.get_length  —  得到声音的长度
* pygame.mixer.Sound.get_raw  —  返回Sound样本的bytestring副本。

从文件名，python文件对象或可读缓冲区对象加载新的声音缓冲区。将执行有限的重新采样以帮助样本匹配混音器的初始化参数。Unicode字符串只能是文件路径名。Python 2.x字符串或Python 3.x字节对象可以是路径名或缓冲区对象。使用'file'或'buffer'关键字来避免歧义; 否则声音可能会猜错。如果使用了array关键字，则该对象应该导出版本3，C级别数组接口，或者对于Python 2.6或更高版本，导出新的缓冲区接口（首先检查该对象的缓冲区接口。）

Sound对象表示实际的声音样本数据。更改Sound对象状态的方法将是Sound播放的所有实例。Sound对象还导出数组接口，对于Python 2.6或更高版本，还会导出新的缓冲区接口。

可以从OGG音频文件或未压缩的文件加载声音 WAV。

注意：缓冲区将在内部复制，不会在它与Sound对象之间共享数据。

目前缓冲区和数组支持与sndarray.make_sound 数值数组一致，因为忽略了样本符号和字节顺序。这将通过正确处理符号和字节顺序或在不同时引发异常来改变。此外，截断源样本以适合音频样本大小。这不会改变。

pygame.mixer.Sound(buffer)pygame中pygame.mixer.Sound的新功能 1.8 从 pygame 1.9.2中的文件或缓冲区对象关键字参数和数组接口支持创建新的Sound对象

`play()`

开始播放声音

play(loops=0, maxtime=0, fade_ms=0) -> Channel

在可用频道上开始播放声音（即，在计算机的扬声器上）。这将强制选择一个频道，因此如有必要，播放可能会切断当前正在播放的声音。

loops参数控制第一次播放后样本重复的次数。值5表示声音将播放一次，然后重复播放五次，因此共播放六次。默认值（零）表示声音不重复，因此只播放一次。如果循环设置为-1，Sound将无限循环（尽管您仍然可以调用stop()它来停止它）。

maxtime参数可用于在给定的毫秒数后停止播放。

fade_ms参数将使声音以0音量开始播放，并在给定时间内逐渐淡出至全音量。样品可以在淡入完成之前结束。

这将返回所选通道的Channel对象。

`stop()`

停止声音播放

stop() -> None

这将停止在任何活动频道上播放此声音。

`fadeout()`

淡出后停止声音播放

fadeout(time) -> None

这将在以毫秒为单位在时间参数上淡出后停止播放声音。声音会在所有主动播放的频道上消失并停止。

`set_volume()`

设置此声音的播放音量

set_volume(value) -> None

这将设置此声音的播放音量（响度）。如果正在播放，这将立即影响声音。它也会影响此声音的任何未来播放。参数是从0.0到1.0的值。

`get_volume()`

获取播放音量

get_volume() -> value

返回0.0到1.0之间的值，表示此Sound的音量。

`get_num_channels()`

计算此声音播放的次数

get_num_channels() -> count

返回此声音正在播放的活动频道数。

`get_length()`

得到声音的长度

get_length() -> seconds

以秒为单位返回此声音的长度。

`get_raw()`

返回Sound样本的bytestring副本。

get_raw() -> bytes

将Sound对象缓冲区的副本作为字节（对于Python 3.x）或str（对于Python 2.x）对象返回。

## pygame 1.9.2中的新功能

### pygame.mixer.Channel

> 创建一个Channel对象来控制播放
Channel(id) -> Channel

* pygame.mixer.Channel.play  —  在特定频道播放声音
* pygame.mixer.Channel.stop  —  停止在频道上播放
* pygame.mixer.Channel.pause  —  暂时停止播放频道
* pygame.mixer.Channel.unpause  —  恢复暂停播放频道
* pygame.mixer.Channel.fadeout  —  淡出通道后停止播放
* pygame.mixer.Channel.set_volume  —  设置播放频道的音量
* pygame.mixer.Channel.get_volume  —  获得播放频道的音量
* pygame.mixer.Channel.get_busy  —  检查通道是否处于活动状态
* pygame.mixer.Channel.get_sound  —  得到当前播放的声音
* pygame.mixer.Channel.queue  —  排队Sound对象以跟随当前
* pygame.mixer.Channel.get_queue  —  返回排队的任何声音
* pygame.mixer.Channel.set_endevent  —  播放停止时让频道发送事件
* pygame.mixer.Channel.get_endevent  —  获取播放停止时频道发送的事件

返回其中一个当前通道的Channel对象。id必须是从0到值的值pygame.mixer.get_num_channels()。

Channel对象可用于精确控制Sounds的播放。一个频道只能播放一个声音。使用频道完全是可选的，因为pygame默认可以管理它们。

`play()`

在特定频道播放声音

play(Sound, loops=0, maxtime=0, fade_ms=0) -> None

这将开始播放特定频道上的声音。如果频道正在播放任何其他声音，它将被停止。

loops参数具有与以下相同的含义Sound.play()：它是第一次重复声音的次数。如果是3，声音将播放4次（第一次，然后是三次）。如果循环为-1，则播放将无限重复。

同样Sound.play()，maxtime参数可用于在给定的毫秒数后停止播放声音。

在中Sound.play()，fade_ms参数可用于淡入声音。

`stop()`

停止在频道上播放

stop() -> None

停止在频道上播放声音。播放停止后，频道可用于播放新的声音。

`pause()`

暂时停止播放频道

pause() -> None

暂时停止在频道上播放声音。它可以在以后恢复Channel.unpause()

`unpause()`

恢复暂停播放频道

unpause() -> None

在暂停的频道上恢复播放。

`fadeout()`

淡出通道后停止播放

fadeout(time) -> None

在给定时间参数上淡出声音后，以毫秒为单位停止播放通道。

`set_volume()`

设置播放频道的音量

set_volume(value) -> None

set_volume(left, right) -> None

设定播放声音的音量（响度）。当频道开始播放时，其音量值将被重置。这只会影响当前的声音。value参数介于0.0和1.0之间。

如果传递一个参数，则它将是两个发言者的音量。如果传递两个参数并且混音器处于立体声模式，则第一个参数将是左扬声器的音量，第二个参数将是右扬声器的音量。（如果第二个参数为None，则第一个参数将是两个扬声器的音量。）

如果频道正在播放set_volume()已调用的声音，则会同时考虑这两个呼叫。例如：

    sound = pygame.mixer.Sound("s.wav")
    channel = s.play()      # Sound plays at full volume by default
    sound.set_volume(0.9)   # Now plays at 90% of full volume.
    sound.set_volume(0.6)   # Now plays at 60% (previous value replaced).
    channel.set_volume(0.5) # Now plays at 30% (0.6 * 0.5).

`get_volume()`

获得播放频道的音量

get_volume() -> value

返回当前播放声音的通道音量。这没有考虑到使用的立体声分离 Channel.set_volume()。Sound对象也有自己的音量，与音频混合。

`get_busy()`

检查通道是否处于活动状态

get_busy() -> bool

如果通道正在主动混合声音，则返回true。如果通道空闲，则返回False。

`get_sound()`

得到当前播放的声音

get_sound() -> Sound

返回当前在此频道上播放的实际Sound对象。如果通道空闲，则返回None。

`queue()`

排队Sound对象以跟随当前

queue(Sound) -> None

当声音在频道上排队时，它将在当前声音结束后立即开始播放。每个通道一次只能排队一个声音。排队的声音仅在当前播放自动结束时播放。在对Channel.stop()或的任何其他呼叫中清除它 Channel.play()。

如果在频道上没有主动播放声音，则声音将立即开始播放。

`get_queue()`

返回排队的任何声音

get_queue() -> Sound

如果声音已在此频道上排队，则会返回该声音。一旦排队的声音开始播放，它将不再在队列中。

`set_endevent()`

播放停止时让频道发送事件

set_endevent() -> None

set_endevent(type) -> None

当为某个频道设置了一个尝试时，每当一个声音在该频道上播放时（不仅仅是第一次），它就会向一个游戏队列发送一个事件。使用pygame.event.get()一旦它发送到检索ENDEVENT。

请注意，如果您调用Sound.play(n)或Channel.play(sound,n)，结束事件仅发送一次：声音播放“n + 1”次后（请参阅Sound.play文档）。

如果在声音仍然播放时调用Channel.stop()或Channel.play()调用，则会立即发布事件。

type参数将是发送到队列的事件id。这可以是任何有效的事件类型，但一个好的选择是pygame.locals.USEREVENT和之间的值 pygame.locals.NUMEVENTS。如果没有给出类型参数，那么Channel将停止发送事件。

`get_endevent()`

获取播放停止时频道发送的事件

get_endevent() -> type

返回每次Channel完成声音播放时要发送的事件类型。如果没有功能返回该功能 pygame.NOEVENT。