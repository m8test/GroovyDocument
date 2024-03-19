功能:

+ 获取[Audio](/API/Device/Audio/README.md)对象.

定义:

+ [Audio](/API/Device/Audio/README.md) audio()

参数:

+ 无

返回值:

+ [Audio](/API/Device/Audio/README.md) - [Audio](/API/Device/Audio/README.md)对象

示例代码:

+ 通过 [Device.audio()](/API/Device/Device/README.md?id=audio) 获取
  [Audio](/API/Device/Audio/README.md) 对象并获取闹钟最大音量.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Device.audio() 用于获取Audio对象
def audio = $device.audio()
// Audio.alarmMaxVolume() 用于获取闹钟最大音量
def alarmMaxVolume = audio.alarmMaxVolume()
$console.log(alarmMaxVolume)
```