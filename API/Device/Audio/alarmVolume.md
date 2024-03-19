功能1:

+ 设置闹钟音量.

定义1:

+ [Audio](/API/Device/Audio/README.md) alarmVolume(int volume)

参数1:

+ int volume - 需要设置的音量值

返回值1:

+ [Audio](/API/Device/Audio/README.md) - 返回对象本身方便链式调用

功能2:

+ 获取当前闹钟音量.

定义2:

+ int alarmVolume()

参数2:

+ 无

返回值2:

+ int - 当前闹钟音量

示例代码:

+ 通过 [Audio.alarmVolume()](/API/Device/Audio/README.md?id=alarmVolume) 设置/获取闹钟音量

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Device.audio() 用于获取Audio对象
def audio = $device.audio()
// Audio.alarmVolume(int) 用于设置闹钟音量
audio.alarmVolume(1)
// Audio.alarmVolume() 用于获取闹钟音量
$assert.assertTrue(audio.alarmVolume() == 1, "闹钟音量为1")
// Audio.alarmMaxVolume() 用于获取闹钟最大音量
def alarmMaxVolume = audio.alarmMaxVolume()
// Audio.alarmVolume(int) 用于设置闹钟音量
audio.alarmVolume(alarmMaxVolume)
// Audio.alarmVolume() 用于获取闹钟音量
$assert.assertTrue(audio.alarmVolume() == alarmMaxVolume, "最大闹钟音量")
```