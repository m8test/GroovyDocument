功能:

+ 获取通知最大音量.

定义:

+ int notificationMaxVolume()

参数:

+ 无

返回值:

+ int - 通知最大音量

示例代码:

+ 通过 [Audio.notificationMaxVolume()](/API/Device/Audio/README.md?id=notificationMaxVolume) 获取通知最大音量

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Device.audio() 用于获取Audio对象
def audio = $device.audio()
// Audio.notificationMaxVolume() 用于获取通知最大音量
def notificationMaxVolume = audio.notificationMaxVolume()
$console.log(notificationMaxVolume)
```