功能1:

+ 设置音乐音量.

定义1:

+ [Audio](/API/Device/Audio/README.md) musicVolume(int volume)

参数1:

+ int volume - 需要设置的音量值

返回值1:

+ [Audio](/API/Device/Audio/README.md) - 返回对象本身方便链式调用

功能2:

+ 获取当前音乐音量.

定义2:

+ int musicVolume()

参数2:

+ 无

返回值2:

+ int - 当前音乐音量

示例代码:

+ 通过 [Audio.musicVolume()](/API/Device/Audio/README.md?id=musicVolume) 设置/获取音乐音量

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Device.audio() 用于获取Audio对象
def audio = $device.audio()
// Audio.musicVolume(int) 用于设置音乐音量
audio.musicVolume(1)
// Audio.musicVolume() 用于获取音乐音量
$assert.assertTrue(audio.musicVolume() == 1, "音乐音量为1")
// Audio.musicMaxVolume() 用于获取音乐最大音量
def musicMaxVolume = audio.musicMaxVolume()
// Audio.musicVolume(int) 用于设置音乐音量
audio.musicVolume(musicMaxVolume)
// Audio.musicVolume() 用于获取音乐音量
$assert.assertTrue(audio.musicVolume() == musicMaxVolume, "最大音乐音量")
```