功能1:

+ 设置通知音量.

定义1:

+ [Audio](/API/Device/Audio/README.md) notificationVolume(int volume)

参数1:

+ int volume - 需要设置的音量值

返回值1:

+ [Audio](/API/Device/Audio/README.md) - 返回对象本身方便链式调用

功能2:

+ 获取当前通知音量.

定义2:

+ int notificationVolume()

参数2:

+ 无

返回值2:

+ int - 当前通知音量

示例代码:

+ 通过 [Audio.notificationVolume()](/API/Device/Audio/README.md?id=notificationVolume) 设置/获取通知音量

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Device.audio() 用于获取Audio对象
def audio = $device.audio()
// Audio.notificationVolume(int) 用于设置通知音量
audio.notificationVolume(1)
// Audio.notificationVolume() 用于获取通知音量
$assert.assertTrue(audio.notificationVolume() == 1, "通知音量为1")
// Audio.notificationMaxVolume() 用于获取通知最大音量
def notificationMaxVolume = audio.notificationMaxVolume()
// Audio.notificationVolume(int) 用于设置通知音量
audio.notificationVolume(notificationMaxVolume)
// Audio.notificationVolume() 用于获取通知音量
$assert.assertTrue(audio.notificationVolume() == notificationMaxVolume, "最大通知音量")
```