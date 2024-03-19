功能:

+ 获取音乐最大音量.

定义:

+ int musicMaxVolume()

参数:

+ 无

返回值:

+ int - 音乐最大音量

示例代码:

+ 通过 [Audio.musicMaxVolume()](/API/Device/Audio/README.md?id=musicMaxVolume) 获取音乐最大音量

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Device.audio() 用于获取Audio对象
def audio = $device.audio()
// Audio.musicMaxVolume() 用于获取音乐最大音量
def musicMaxVolume = audio.musicMaxVolume()
$console.log(musicMaxVolume)
```