功能:

+ 获取通话最大音量.

定义:

+ int voiceCallMaxVolume()

参数:

+ 无

返回值:

+ int - 通话最大音量

示例代码:

+ 通过 [Audio.voiceCallMaxVolume()](/API/Device/Audio/README.md?id=voiceCallMaxVolume) 获取通话最大音量

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Device.audio() 用于获取Audio对象
def audio = $device.audio()
// Audio.voiceCallMaxVolume() 用于获取通话最大音量
def voiceCallMaxVolume = audio.voiceCallMaxVolume()
$console.log(voiceCallMaxVolume)
```