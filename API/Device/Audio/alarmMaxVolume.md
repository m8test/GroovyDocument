功能:

+ 获取闹钟最大音量.

定义:

+ int alarmMaxVolume()

参数:

+ 无

返回值:

+ int - 闹钟最大音量

示例代码:

+ 通过 [Audio.alarmMaxVolume()](/API/Device/Audio/README.md?id=alarmMaxVolume) 获取闹钟最大音量

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Device.audio() 用于获取Audio对象
def audio = $device.audio()
// Audio.alarmMaxVolume() 用于获取闹钟最大音量
def alarmMaxVolume = audio.alarmMaxVolume()
$console.log(alarmMaxVolume)
```